# java
java repositorie


import java.io.IOException;
import java.nio.file.*;
import java.util.*;
import java.util.regex.*;

public class AnnotationCounter {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto
        Map<String, Integer> annotationCount = new HashMap<>();

        try {
            // Recorremos todos los archivos del proyecto
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .filter(file -> file.toString().endsWith(".java"))
                .forEach(file -> processFile(file, annotationCount));

            // Mostramos el resultado
            System.out.println("Conteo de anotaciones:");
            annotationCount.forEach((annotation, count) -> 
                System.out.println(annotation + ": " + count));

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void processFile(Path file, Map<String, Integer> annotationCount) {
        try {
            List<String> lines = Files.readAllLines(file);
            Pattern annotationPattern = Pattern.compile("@\\w+");

            for (String line : lines) {
                Matcher matcher = annotationPattern.matcher(line);
                while (matcher.find()) {
                    String annotation = matcher.group();
                    annotationCount.put(annotation, annotationC
                    
                    ount.getOrDefault(annotation, 0) + 1);
                }import java.io.IOException;
import java.nio.file.*;
import java.util.*;
import java.util.regex.*;

public class AnnotationCounter {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto
        Map<String, Integer> annotationCount = new HashMap<>();

        try {
            // Recorremos todos los archivos del proyecto
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .filter(file -> file.toString().endsWith(".java"))
                .forEach(file -> processFile(file, annotationCount));

            // Mostramos el resultado
            System.out.println("Conteo de anotaciones:");
            annotationCount.forEach((annotation, count) -> 
                System.out.println(annotation + ": " + count));

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void processFile(Path file, Map<String, Integer> annotationCount) {
        try {
            List<String> lines = Files.readAllLines(file);
            Pattern annotationPattern = Pattern.compile("@\\w+");

            for (String line : lines) {
                Matcher matcher = annotationPattern.matcher(line);
                while (matcher.find()) {
                    String annotation = matcher.group();
                    annotationCount.put(annotation, annotationCount.getOrDefault(annotation, 0) + 1);
                }
            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}





import java.io.IOException;
import java.nio.file.*;
import java.util.*;

public class ProjectAnalyzer {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto
        Map<String, Integer> projectCount = new HashMap<>();

        try {
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .forEach(file -> classifyFile(file, projectCount));

            // Mostramos el conteo de subproyectos detectados
            System.out.println("Subproyectos detectados:");
            projectCount.forEach((projectType, count) -> 
                System.out.println(projectType + ": " + count));

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void classifyFile(Path file, Map<String, Integer> projectCount) {
        String fileName = file.getFileName().toString();

        if (fileName.equals("pom.xml")) {
            projectCount.put("Maven", projectCount.getOrDefault("Maven", 0) + 1);
        } else if (fileName.equals("build.gradle") || fileName.equals("settings.gradle")) {
            projectCount.put("Gradle", projectCount.getOrDefault("Gradle", 0) + 1);
        } else if (fileName.equals("ivy.xml")) {
            projectCount.put("Ivy", projectCount.getOrDefault("Ivy", 0) + 1);
        }
    }
}






import java.io.IOException;
import java.nio.file.*;
import java.util.*;

public class ProjectAnalyzer {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto
        Map<String, Integer> projectCount = new HashMap<>();

        try {
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .forEach(file -> classifyFile(file, projectCount));

            // Mostramos el conteo de subproyectos detectados
            System.out.println("Subproyectos detectados:");
            projectCount.forEach((projectType, count) -> 
                System.out.println(projectType + ": " + count));

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void classifyFile(Path file, Map<String, Integer> projectCount) {
        String fileName = file.getFileName().toString();

        if (fileName.equals("pom.xml")) {
            projectCount.put("Maven", projectCount.getOrDefault("Maven", 0) + 1);
        } else if (fileName.equals("build.gradle") || fileName.equals("settings.gradle")) {
            projectCount.put("Gradle", projectCount.getOrDefault("Gradle", 0) + 1);
        } else if (fileName.equals("ivy.xml")) {
            projectCount.put("Ivy", projectCount.getOrDefault("Ivy", 0) + 1);
        }
    }
}
import java.io.IOException;
import java.nio.file.*;
import java.util.*;

public class ProjectAnalyzer {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto
        Map<String, Integer> projectCount = new HashMap<>();

        try {
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .forEach(file -> classifyFile(file, projectCount));

            // Mostramos el conteo de subproyectos detectados
            System.out.println("Subproyectos detectados:");
            projectCount.forEach((projectType, count) -> 
                System.out.println(projectType + ": " + count));

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void classifyFile(Path file, Map<String, Integer> projectCount) {
        String fileName = file.getFileName().toString();

        if (fileName.equals("pom.xml")) {
            projectCount.put("Maven", projectCount.getOrDefault("Maven", 0) + 1);
        } else if (fileName.equals("build.gradle") || fileName.equals("settings.gradle")) {
            projectCount.put("Gradle", projectCount.getOrDefault("Gradle", 0) + 1);
        } else if (fileName.equals("ivy.xml")) {
            projectCount.put("Ivy", projectCount.getOrDefault("Ivy", 0) + 1);
        }
    }
}





import java.io.IOException;
import java.nio.file.*;
import java.util.*;

public class ProjectRestructurer {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto base
        Map<String, List<String>> suggestedStructure = new HashMap<>();

        try {
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .forEach(file -> analyzeFile(file, suggestedStructure));

            // Mostrar la sugerencia de reestructuración
            System.out.println("Sugerencia de reestructuración del proyecto:");
            suggestedStructure.forEach((projectType, files) -> {
                System.out.println("Proyecto de tipo " + projectTyp              
                e + ":");
                files.forEach(file -> System.out.println("  - " + file));
            });

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void analyzeFile(Path file, Map<String, List<String>> suggestedStructure) {
        String fileName = file.getFileName().toString();
        String parentDir = file.getParent().toString(); //







            }
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}




reorganizaimport java.io.IOException;
import java.nio.file.*;
import java.util.*;

public class ProjectRestructurer {
    public static void main(String[] args) {
        String projectPath = "ruta/a/tu/proyecto"; // Cambia a la ruta de tu proyecto base
        Map<String, List<String>> suggestedStructure = new HashMap<>();

        try {
            Files.walk(Paths.get(projectPath))
                .filter(Files::isRegularFile)
                .forEach(file -> analyzeFile(file, suggestedStructure));

            // Mostrar la sugerencia de reestructuración
            System.out.println("Sugerencia de reestructuración del proyecto:");
            suggestedStructure.forEach((projectType, files) -> {
                System.out.println("Proyecto de tipo " + projectType + ":");
                files.forEach(file -> System.out.println("  - " + file));
            });

        } catch (IOException e) {
            e.printStackTrace();
        }
    }

    private static void analyzeFile(Path file, Map<String, List<String>> suggestedStructure) {
        String fileName = file.getFileName().toString();
        String parentDir = file.getParent().toString(); // Obtener el directorio del archivo

        if (fileName.equals("pom.xml")) {
            addToStructure(suggestedStructure, "Maven", parentDir);
        } else if (fileName.equals("build.gradle") || fileName.equals("settings.gradle")) {
            addToStructure(suggestedStructure, "Gradle", parentDir);
        } else if (fileName.equals("ivy.xml")) {
            addToStructure(suggestedStructure, "Ivy", parentDir);
        }
    }

    private static void addToStructure(Map<String, List<String>> structure, String projectType, String directory) {
        // Agrega el directorio al tipo de proyecto correspondiente
        structure.putIfAbsent(projectType, new ArrayList<>());
        if (!structure.get(projectType).contains(directory)) {
            structure.get(projectType).add(directory);
        }
    }
}




import java.io.File;
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Path;
import java.nio.file.Paths;
import java.util.ArrayList;
import java.util.List;
import java.util.regex.Matcher;
import java.util.regex.Pattern;

public class CodeAnalyzer {

    private static final String PROJECT_PATH = "ruta/del/proyecto"; // Cambia esto a la ruta de tu proyecto
    
    // Expresiones regulares para detectar referencias a EJB y anotaciones de Spring Boot
    private static final Pattern EJB_PATTERN = Pattern.compile("\\b(EJB|@EJB|@Stateless|@Stateful)\\b");
    private static final Pattern SPRING_ANNOTATIONS_PATTERN = Pattern.compile(
        "\\b(@Controller|@Service|@Component|@Repository)\\b"
    );

    public static void main(String[] args) {
        List<String> ejbClasses = new ArrayList<>();
        List<String> springClasses = new ArrayList<>();
        
        // Analiza los archivos Java en el proyecto
        analyzeProject(new File(PROJECT_PATH), ejbClasses, springClasses);
        
        // Imprime los resultados
        System.out.println("Clases con referencias a EJB:");
        ejbClasses.forEach(System.out::println);

        System.out.println("\nClases con anotaciones de Spring Boot:");
        springClasses.forEach(System.out::println);
    }

    private static void analyzeProject(File folder, List<String> ejbClasses, List<String> springClasses) {
        for (File file : folder.listFiles()) {
            if (file.isDirectory()) {
                // Analiza recursivamente si es una carpeta
                analyzeProject(file, ejbClasses, springClasses);
            } else if (file.getName().endsWith(".java")) {
                // Analiza el archivo Java
                analyzeFile(file.toPath(), ejbClasses, springClasses);
            }
        }
    }

    private static void analyzeFile(Path filePath, List<String> ejbClasses, List<String> springClasses) {
        try {
            List<String> lines = Files.readAllLines(filePath);
            String content = String.join(" ", lines);
            
            // Busca referencias a EJB
            Matcher ejbMatcher = EJB_PATTERN.matcher(content);
            if (ejbMatcher.find()) {
                ejbClasses.add(filePath.toString());
            }
            
            // Busca anotaciones de Spring Boot
            Matcher springMatcher = SPRING_ANNOTATIONS_PATTERN.matcher(content);
            if (springMatcher.find()) {
                springClasses.add(filePath.toString());
            }
        } catch (IOException e) {
            System.err.println("Error leyendo el archivo: " + filePath + " - " + e.getMessage());
        }
    }
}




import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        String cadena = "1234"; // Cambia esta cadena de prueba según necesites

        // Validamos si la cadena es numérica y tiene menos de 10 caracteres, si es así, la rellenamos
        cadena = validarYRellenarConCeros(cadena);

        System.out.println("Cadena final: " + cadena);
    }

    // Método que valida si es numérica y rellena con ceros si cumple con la longitud
    public static String validarYRellenarConCeros(String cadena) {
        if (cadena.length() < 10 && esNumerica(cadena)) {
            return String.format("%-10s", cadena).replace(' ', '0'); // Rellenamos con ceros hasta alcanzar 10 caracteres
        }
        return cadena;
    }

    // Método que verifica si la cadena es numérica (sin expresiones regulares)
    public static boolean esNumerica(String cadena) {
        for (char c : cadena.toCharArray()) {
            if (!Character.isDigit(c)) {
                return false; // Si algún carácter no es un dígito, retorna false
            }
        }
        return true; // Si todos son dígitos, retorna true
    }
}

