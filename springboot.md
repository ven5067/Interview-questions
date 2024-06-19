

**Spring Boot:**

**What is Spring Boot?**

Spring Boot is an opinionated framework built on top of the Spring framework, designed to simplify the development of production-ready applications with minimal configuration. It provides out-of-the-box solutions for dependency management, configuration, and monitoring, allowing developers to focus more on business logic.

**What are the key features of Spring Boot?**


- **Autoconfiguration:** Automatically configures application based on dependencies and properties.
- **Starter dependencies:** Pre-configured dependencies to simplify the setup of new projects.
- **Embedded server:** Includes an embedded servlet container (Tomcat, Jetty, or Undertow) for running applications.
- **Production-ready features:** Built-in metrics, health checks, and externalized configuration.
- **Opinionated defaults:** Encourages best practices and convention over configuration.

**Explain the difference between Spring and Spring Boot.**


- **Spring:** The core Spring framework provides fundamental features such as Dependency Injection (DI), Aspect-Oriented Programming (AOP), and transaction management. It requires explicit configuration and setup using XML or Java annotations.
- **Spring Boot:** Builds on top of the Spring framework and aims to simplify Spring application development by providing defaults for configuration and eliminating the need for boilerplate code. It includes an embedded server and allows standalone execution of applications with minimal setup.

**What is a Spring Boot starter? Give examples.**

Spring Boot starters are a set of convenient dependency descriptors that you can include in your application. You get a one-stop-shop for all the dependencies needed for a specific purpose. Examples include:


- **spring-boot-starter-web:** Starter for building web, including RESTful, applications using Spring MVC.
- **spring-boot-starter-data-jpa:** Starter for using Spring Data JPA with Hibernate.
- **spring-boot-starter-security:** Starter for securing Spring applications using Spring Security.
- **spring-boot-starter-test:** Starter for testing Spring Boot applications with libraries including JUnit, Hamcrest, and Mockito.

**How does Spring Boot support externalized configuration?**

Spring Boot allows externalized configuration using property files (`application.properties` or `application.yml`), environment variables, command-line arguments, and profiles. It provides default property values and allows overriding these values based on different environments or configurations.

Example (`application.yml`):

```yaml<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
server:
  port: 8080

```
**What are Spring Boot Actuator endpoints?**

Spring Boot Actuator endpoints are built-in features that provide insight into the application’s runtime behavior, such as health, metrics, info, and environment details. They allow you to monitor and manage your application using HTTP endpoints or JMX beans.

Example enabling Actuator endpoints in `application.properties`:

```properties<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
management.endpoints.web.exposure.include=health,info,metrics

```
**Explain the stereotype annotations used in Spring Boot.**

Stereotype annotations in Spring Boot are used to indicate the roles of Java classes and methods. They include:


- **@Component:** Indicates that a class is a Spring component.
- **@Controller:** Indicates that a class is a Spring MVC controller.
- **@Service:** Indicates that a class is a service layer component.
- **@Repository:** Indicates that a class is a data access component.
These annotations help Spring manage and instantiate components based on auto-scanning or explicit configuration.

**What is Spring Boot autoconfiguration?**

Spring Boot autoconfiguration automatically configures the Spring application based on the classpath dependencies and defined beans. It analyzes the environment and automatically configures the Spring application with sensible defaults, reducing the need for explicit configuration.

Example `Application.java`:

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}

```
**How does Spring Boot support dependency injection?**

Spring Boot uses the core Spring framework's Dependency Injection (DI) mechanism to manage dependencies and promote loose coupling between components. It supports constructor injection, setter injection, and field injection using `@Autowired` annotation or `@Inject` (for JSR-330 compatibility) to inject dependencies.

**What are the advantages of using Spring Boot for microservices development?**


- **Simplified setup:** Minimizes boilerplate code and configuration, making it easy to start new projects.
- **Opinionated defaults:** Encourages best practices and conventions, reducing development time.
- **Embedded server:** Provides an embedded servlet container for standalone execution of microservices.
- **Production-ready:** Includes features like health checks, metrics, and externalized configuration out-of-the-box.
- **Ecosystem:** Integrates seamlessly with other Spring projects and third-party libraries, enhancing flexibility and scalability.

**Explain the difference between @RequestBody and @RequestParam in Spring REST controllers.**


- **@RequestBody:** Used to bind the HTTP request body to a Java object. It is typically used with POST or PUT requests where the client sends data in the request body.

Example:

```java
Copy code
@PostMapping("/users")
public ResponseEntity
createUser(@RequestBody User user) {
    // Process user creation
}

```
- **@RequestParam:** Used to extract query parameters from the request URL. It binds a single query parameter to a method parameter in the controller method.

Example:

```java
Copy code
@GetMapping("/users")
public ResponseEntity
getUserById(@RequestParam Long userId) {
    // Process getting user by ID
}

```

**How does Spring handle content negotiation in RESTful services?**

Spring uses content negotiation to select the representation of the resource based on the client's Accept header in the HTTP request. It supports various formats such as JSON, XML, and others based on the configured HttpMessageConverters.

Example:

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
@GetMapping(value = "/user", produces = MediaType.APPLICATION_JSON_VALUE)
public ResponseEntity<User> getUser() {
    // Return user object as JSON
}

```
**What are @RestControllerAdvice and @ExceptionHandler used for in Spring REST?**


- **@RestControllerAdvice:** Annotated class that combines `@ControllerAdvice` and `@ResponseBody`, allowing you to handle exceptions across multiple REST controllers. It is used to centralize exception handling and apply it uniformly across all REST endpoints.

Example:

```java
Copy code
@RestControllerAdvice
public class GlobalExceptionHandler {
    @ExceptionHandler(ResourceNotFoundException.class)
    public ResponseEntity
handleResourceNotFoundException(ResourceNotFoundException ex) {
        // Return custom error response
    }
}

```
- **@ExceptionHandler:** Annotates methods in controllers or `@ControllerAdvice` classes to handle specific exceptions thrown during the execution of REST endpoints. It provides a way to customize error responses for different types of exceptions.

**Explain the usage of @PathVariable and @RequestParam together in a Spring REST controller method.**


- **@PathVariable:** Extracts values from the URI path template. It is used to capture dynamic parts of the URI.
- **@RequestParam:** Extracts query parameters from the request URL. In combination with `@PathVariable`, it can be used to provide additional parameters for the method.

Example:

```java
Copy code
@GetMapping("/users/{userId}/accounts")
public ResponseEntity
> getUserAccounts(@PathVariable Long userId, @RequestParam String type) {
    // Process retrieving accounts for a specific user based on type
}

```

**How does Spring handle CORS (Cross-Origin Resource Sharing) in RESTful services?**

Spring provides CORS support through configuration or annotations. You can configure CORS globally or per controller method using `@CrossOrigin` annotation to specify allowed origins, methods, and headers.

Example:

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
@CrossOrigin(origins = "http://localhost:4200")
@RestController
@RequestMapping("/api")
public class UserController {
    // Controller methods
}

```
**Explain the use of @RequestBody with Map<String, Object> in Spring REST controllers.**


- **@RequestBody Map
:** Allows flexible binding of JSON or form data sent in the request body to a Map object. It can handle dynamic keys and values but requires careful validation and parsing.

Example:

```java
Copy code
@PostMapping("/users")
public ResponseEntity
createUser(@RequestBody Map
userData) {
    // Extract and validate user data from the map
}

```

**What are the different ways to handle versioning in Spring RESTful services?**


- **URL-based versioning:** Include the version in the URI path.

Example:

```java
Copy code
@GetMapping("/api/v1/users")
public ResponseEntity
> getAllUsersV1() {
    // Version 1 of the API
}

```
- **Header-based versioning:** Specify the version in a custom header.
- **Media type-based versioning:** Use different media types (e.g., `application/vnd.company.v1+json`) to distinguish API versions.

_____________________________________________________________________________________________

_____________________________________________________________________________________________
**Spring REST:**


- **What are some common security vulnerabilities in RESTful APIs?**
   - **Answer:** Common vulnerabilities include:
      - Injection attacks: SQL injection, LDAP injection, etc.
      - Broken authentication: Weak passwords, session hijacking, etc.
      - Sensitive data exposure: Insecure transmission, inadequate encryption, etc.
      - XML/JSON attacks: Malicious input manipulation, schema poisoning, etc.
      - Improper error handling: Revealing stack traces, sensitive information, etc.
   - **How can you secure REST endpoints in a Spring Boot application?**
   - **Answer:**
      - Use HTTPS: Ensure secure transmission of data.
      - Implement authentication: Use mechanisms like Basic Auth, JWT, OAuth 2.0.
      - Apply authorization: Restrict access based on roles and permissions using annotations (@PreAuthorize, @Secured).
      - Input validation: Validate and sanitize input data to prevent injection attacks.
      - Error handling: Properly handle errors to avoid exposing sensitive information.
   - **Explain the concept of Basic Authentication and how it is implemented in Spring Boot.**
   - **Answer:**
      - Basic Authentication: A simple authentication scheme where the client sends the username and password encoded in Base64 in the HTTP Authorization header.
      - Implementation in Spring Boot: Configure `spring-boot-starter-security` and define security rules in `SecurityConfig`.
```java
@Configuration
@EnableWebSecurity
public class SecurityConfig extends WebSecurityConfigurerAdapter {
    @Override
    protected void configure(HttpSecurity http) throws Exception {
        http.authorizeRequests()
            .anyRequest().authenticated()
            .and()
            .httpBasic();
    }
}
```
- **What is JWT (JSON Web Token) and how can it be used to secure RESTful APIs?**
   - **Answer:**
      - JWT: A compact, URL-safe token format used for securely transmitting information between parties as a JSON object.
      - Usage in RESTful APIs:
         - Issued by an authentication server upon successful login.
         - Sent by the client in subsequent requests to authenticate and authorize access.
         - Verifiable and stateless, eliminating the need for server-side session management.
      - Example implementation with Spring Security and JWT libraries (jjwt):
```java
// JWT generation and validation
String token = Jwts.builder()
    .setSubject(username)
    .setExpiration(new Date(System.currentTimeMillis() + EXPIRATION_TIME))
    .signWith(SignatureAlgorithm.HS512, SECRET_KEY)
    .compact();
```
- **How can you restrict access to specific REST endpoints based on user roles in Spring Boot?**
   - **Answer:** Use annotations (@PreAuthorize, @Secured) to restrict access based on user roles defined in the application.
      - Example using @PreAuthorize:
```java
@GetMapping("/admin/users")
@PreAuthorize("hasRole('ADMIN')")
public ResponseEntity
   > getAllUsers() {
    // Retrieve and return list of users
}
```
- **What are CSRF attacks, and how can you prevent them in a Spring Boot REST application?**
   - **Answer:**
      - CSRF (Cross-Site Request Forgery): An attack where a malicious website tricks a user's browser into executing unauthorized actions on another site where the user is authenticated.
      - Prevention in Spring Boot:
         - Use CSRF protection enabled by default in Spring Security (`csrf()` method).
         - Include a CSRF token in requests (`_csrf` parameter in forms or headers) and validate it on the server side.
      - **Explain the concept of OAuth 2.0 and its role in securing RESTful APIs.**
   - **Answer:**
      - OAuth 2.0: An authorization framework that enables third-party applications to obtain limited access to a user's resources without exposing credentials.
      - Role in RESTful APIs:
         - Allows secure authorization between applications and users without sharing passwords.
         - Defines roles such as Resource Owner, Client, Authorization Server, and Resource Server.
         - Provides access tokens that can be used to access protected resources on behalf of the user.
      - Example implementation using Spring Security OAuth 2.0 (`spring-security-oauth2`).
   - **How can you handle secure file uploads in a Spring Boot REST application?**
   - **Answer:**
      - Use HTTPS to secure file transmission.
      - Validate file types and sizes to prevent malicious uploads.
      - Store files in a secure location with restricted access.
      - Implement authentication and authorization checks before accepting file uploads.
   - **What are the best practices for logging and auditing security-related events in Spring Boot REST applications?**
   - **Answer:**
      - Log security events and exceptions with detailed information.
      - Use logging frameworks like SLF4J and Logback to manage and store logs securely.
      - Implement audit trails to track access to sensitive resources and operations.
      - Regularly review and analyze logs for suspicious activities or anomalies.
   - **Explain the role of CORS (Cross-Origin Resource Sharing) in securing RESTful APIs.**
   - **Answer:**
      - **CORS:** A security feature implemented by web browsers to prevent unauthorized cross-origin requests.
      - **Role in security:**
         - Restricts which domains can access resources on the server.
         - Use `@CrossOrigin` annotation or configure CORS globally in Spring Security (`CorsConfiguration`).
         - Prevents unauthorized JavaScript from making requests to APIs with sensitive data.

_____________________________________________________________________________________________
**Spring Data JPA**


- **What is Spring Data JPA?**
   - **Answer:** Spring Data JPA is a part of the larger Spring Data family that makes it easier to implement JPA-based repositories. It simplifies the implementation of data access layers by automatically generating queries from method names and providing additional features like pagination and auditing.
- **Explain the difference between Hibernate and Spring Data JPA.**
   - **Answer:**
      - **Hibernate:** It is an implementation of the Java Persistence API (JPA) specification and provides ORM (Object-Relational Mapping) capabilities to map Java objects to database tables and vice versa.
      - **Spring Data JPA:** It is a higher-level abstraction over JPA and provides repository support, eliminating the need for boilerplate code in data access layers. Spring Data JPA uses Hibernate (or other JPA providers) under the hood for ORM operations.
   - **What are the key advantages of using Spring Data JPA?**
   - **Answer:**
      - Reduces boilerplate code: Automatically generates repository implementations for CRUD operations.
      - Simplifies query creation: Supports query methods derived from method names.
      - Supports pagination and auditing out-of-the-box.
      - Integrates easily with other Spring projects and frameworks.
   - **How do you define a Spring Data JPA repository interface?**
   - **Answer:**
```java 
import org.springframework.data.jpa.repository.JpaRepository;

public interface UserRepository extends JpaRepository
   {
    // Custom query methods if needed
}
```
`UserRepository` extends `JpaRepository` and is parameterized with entity type (`User`) and primary key type (`Long`). Spring Data JPA provides implementations for basic CRUD operations and allows custom query methods to be defined.

- **What is the purpose of @Entity annotation in Spring Data JPA?**
   - **Answer:** `@Entity` annotates a Java class to be mapped to a table in the database. It denotes that instances of the class will be stored in the database and specifies the table name, columns, and relationships between entities.
  
- **How does Spring Data JPA generate queries from method names?**
   - **Answer:** Spring Data JPA derives query methods based on the method names defined in the repository interfaces. For example:
 ```java
// Derived query method
List findByFirstName(String firstName);
```
In this case, Spring Data JPA automatically generates a query to find all users with a specific `firstName` attribute.

**Explain the use of @Query annotation in Spring Data JPA.**
   - **Answer:** `@Query` allows defining custom JPQL (Java Persistence Query Language) or native SQL queries directly within repository methods.
```java
@Query("SELECT u FROM User u WHERE u.age > :age")
List findByAgeGreaterThan(@Param("age") int age);
```
This annotation provides flexibility to execute complex queries not covered by the derived method names.

**What is lazy loading in the context of Spring Data JPA?**
   - **Answer:** Lazy loading delays the fetching of associated entities until they are explicitly accessed. It helps optimize performance by fetching only the necessary data when needed, reducing memory consumption and improving response times. Lazy loading is the default behavior for `@ManyToOne` and `@OneToOne` associations in JPA entities.

**How do you enable auditing (createdBy, createdDate, etc.) in Spring Data JPA repositories?**
   - **Answer:**
      - Use `@EnableJpaAuditing` annotation in a configuration class or directly on the main Spring Boot application class.
      - Annotate entities with `@EntityListeners(AuditingEntityListener.class)` and use `@CreatedBy`, `@CreatedDate`, `@LastModifiedBy`, and `@LastModifiedDate` annotations in entity classes to capture audit information.
 
 **What are the different inheritance strategies supported by JPA, and how do you specify them in Spring Data JPA?**
   - **Answer:**
      - JPA supports inheritance strategies such as `SINGLE_TABLE`, `TABLE_PER_CLASS`, and `JOINED`.
      - Specify inheritance strategy using `@Inheritance` and `@DiscriminatorColumn` annotations in entity classes:
```java
@Entity
@Inheritance(strategy = InheritanceType.SINGLE_TABLE)
@DiscriminatorColumn(name = "user_type", discriminatorType = DiscriminatorType.STRING)
public abstract class User {
    // Common attributes and methods
}
```
      - `SINGLE_TABLE`: Uses a single table to store data for all subclasses, with a discriminator column (`user_type` in this example) to differentiate between subclasses.
