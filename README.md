import com.github.javaparser.JavaParser;
import com.github.javaparser.ast.CompilationUnit;
import com.github.javaparser.ast.body.ClassOrInterfaceDeclaration;
import com.github.javaparser.ast.body.MethodDeclaration;
import com.github.javaparser.ast.body.Parameter;
import com.github.javaparser.ast.visitor.VoidVisitorAdapter;
import org.slf4j.Logger;
import org.slf4j.LoggerFactory;

import java.io.File;
import java.io.FileInputStream;
import java.io.FileWriter;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.stream.Collectors;

public class LoggerInjector {
    private static final Logger log = LoggerFactory.getLogger(LoggerInjector.class);

    public void processProject(String projectPath) {
        try {
            // Encontrar todos los archivos .java recursivamente
            List<Path> javaFiles = Files.walk(Paths.get(projectPath))
                .filter(path -> path.toString().endsWith(".java"))
                .collect(Collectors.toList());

            for (Path javaFile : javaFiles) {
                processJavaFile(javaFile.toFile());
            }
        } catch (Exception e) {
            log.error("Error procesando el proyecto", e);
        }
    }

    private void processJavaFile(File file) {
        try {
            // Parsear el archivo Java
            CompilationUnit cu = new JavaParser().parse(new FileInputStream(file)).getResult().get();
            
            // Visitor para modificar el código
            new LoggerVisitor().visit(cu, null);
            
            // Guardar cambios
            try (FileWriter writer = new FileWriter(file)) {
                writer.write(cu.toString());
            }
        } catch (Exception e) {
            log.error("Error procesando archivo: " + file.getName(), e);
        }
    }

    private static class LoggerVisitor extends VoidVisitorAdapter<Void> {
        @Override
        public void visit(ClassOrInterfaceDeclaration n, Void arg) {
            // Agregar campo logger si no existe
            if (!hasLogger(n)) {
                n.addField("Logger", "log",
                    "private static final")
                    .getVariables().get(0)
                    .setInitializer("LoggerFactory.getLogger(" + n.getNameAsString() + ".class)");
            }

            // Agregar import para SLF4J si no existe
            n.findCompilationUnit().ifPresent(cu -> {
                cu.addImport("org.slf4j.Logger");
                cu.addImport("org.slf4j.LoggerFactory");
            });

            super.visit(n, arg);
        }

        @Override
        public void visit(MethodDeclaration n, Void arg) {
            // Ignorar métodos getter/setter
            if (isGetterOrSetter(n)) {
                return;
            }

            // Crear log de entrada
            StringBuilder entryLog = new StringBuilder("log.debug(\"Entering " + n.getNameAsString() + "(");
            List<Parameter> params = n.getParameters();
            List<String> paramLogs = new ArrayList<>();
            
            for (Parameter param : params) {
                paramLogs.add(param.getNameAsString() + ": {}");
            }
            entryLog.append(String.join(", ", paramLogs)).append(")\", ");
            
            if (!params.isEmpty()) {
                List<String> paramNames = params.stream()
                    .map(Parameter::getNameAsString)
                    .collect(Collectors.toList());
                entryLog.append(String.join(", ", paramNames));
            }
            entryLog.append(");");

            // Agregar log de entrada al inicio del método
            n.getBody().ifPresent(body -> {
                body.addStatement(0, entryLog.toString());
                
                // Agregar log de salida antes de cada return
                body.findAll(ReturnStmt.class).forEach(returnStmt -> {
                    String returnLog = "log.debug(\"Exiting " + n.getNameAsString() + " with return: {}\", " +
                        returnStmt.getExpression().map(Object::toString).orElse("null") + ");";
                    returnStmt.setExpression(returnStmt.getExpression().get());
                    body.addStatement(body.getStatements().indexOf(returnStmt),
                        returnLog);
                });
            });

            super.visit(n, arg);
        }

        private boolean hasLogger(ClassOrInterfaceDeclaration n) {
            return n.getFields().stream()
                .anyMatch(field -> field.getVariable(0).getNameAsString().equals("log"));
        }

        private boolean isGetterOrSetter(MethodDeclaration method) {
            String name = method.getNameAsString();
            return name.startsWith("get") || name.startsWith("set")
                || name.startsWith("is");
        }
    }

    public static void main(String[] args) {
        if (args.length != 1) {
            System.out.println("Uso: java LoggerInjector <ruta-del-proyecto>");
            return;
        }
        new LoggerInjector().processProject(args[0]);
    }
}
