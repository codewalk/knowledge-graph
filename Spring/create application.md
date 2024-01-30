### Spring Boot Basics:

#### Creating a Spring Boot Project:

1. **Using Spring Maven Project:**
   - Use Maven archetype for Spring Boot:
     ```bash
     mvn archetype:generate -DgroupId=com.example -DartifactId=myproject -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
     ```

2. **Using Spring Starter Project Wizard:**
   - Open Spring Tool Suite (STS) or IntelliJ IDEA.
   - Choose "File" -> "New" -> "Spring Starter Project" and follow the wizard.

3. **Using Spring Initializr:**
   - Visit [Spring Initializr](https://start.spring.io/).
   - Select project metadata and dependencies, then click "Generate."

4. **Using Spring Boot CLI:**
   - Install Spring Boot CLI.
   - Open a terminal and run:
     ```bash
     spring init --dependencies=web myproject
     ```

#### Creating a Simple Spring Boot Application:

```java
@SpringBootApplication
public class MyApplication {

    public static void main(String[] args) {
        SpringApplication.run(MyApplication.class, args);
    }
}
```

#### Spring Boot Annotations:

1. **@SpringBootApplication:**
   - Marks the main class of a Spring Boot application.
   - Enables auto-configuration and component scanning.

2. **@Controller:**
   - Indicates that a class serves as a Spring MVC controller.
   - Handles HTTP requests and returns responses.

3. **@RequestMapping:**
   - Maps HTTP requests to handler methods.

4. **@RestController:**
   - A specialized version of `@Controller` for RESTful web services.
   - Combines `@Controller` and `@ResponseBody`.

#### Spring Boot Starters:

- **Spring Boot Starters:** Pre-configured templates with common dependencies for specific functionalities.
  - **Example Dependency in `pom.xml`:**
    ```xml
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    ```

### Demonstration:

#### Project Creation:

1. **Using Spring Initializr:**
   - Go to [Spring Initializr](https://start.spring.io/).
   - Set "Group" to "com.example" and "Artifact" to "demo."
   - Add "Spring Web" and "Spring Data JPA" as dependencies.
   - Click "Generate" to download the project.

2. **Using Spring Boot CLI:**
   - Open a terminal and run:
     ```bash
     spring init --dependencies=web,data-jpa demo-cli
     ```

#### Simple Spring Boot Application:

- Create a file `DemoApplication.java`:

```java
import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}
```

#### Controller with Request Mapping:

- Create a file `DemoController.java`:

```java
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@RequestMapping("/demo")
public class DemoController {

    @GetMapping("/hello")
    public String hello() {
        return "Hello, Spring Boot!";
    }
}
```

#### Run the Application:

- Build and run the application using Maven or your IDE.
- Access [http://localhost:8080/demo/hello](http://localhost:8080/demo/hello) in a web browser.

This demonstration covers creating a Spring Boot project, using annotations, adding starters, and implementing a simple web service. Each step includes practical examples to reinforce the understanding of Spring Boot concepts.
