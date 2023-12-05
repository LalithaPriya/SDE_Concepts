###SpringBoot Framework:

- Easy to use -> In spring, need to add congiguration changes in XML file but  in springboot Simply add a annotation in the main application class @SpringBootApplication, to start a web application 

- Rapid development -->By including this 'spring-boot-starter-data-jpa' in xml, it direclty configures a datasource and JPA

- Scalable 
- Production ready --> Spring Boot Actuator provides a set of production-ready features exposed as endpoints like '/actuator/health' , /metrics, /info, /env

* By using Spring boot we can create web applications, Microservices and console applications etc...

In Configurations:
**Web**
-Spring Web -->  Builds web, including RESTful, applications using Spring MVC, uses Apache Tomcat 
-Rest repositories
-Spring session

**SQL**
- JDBC API
- Spring Data JPA
- Spring Data JDBC

**Security**
- Oauth2 client
- Spring Security

-----

- Pom.xml --> project metadata and dependencies
- application.properties - all the properties to configure as well as evirment properties

- controller class will have all of the resources for our API.

- use service for method/ business logic implementation 

### Dependency Injection 
by avoiding new class() , we use dependency injection 
- this can be done by using @Autowired  --> it is intantiated, then we add @component to service class that needs to be intantiated to say that is a bean.
- both @Component and @Service are used for component scanning and bean creation in a Spring application. @Component is a general-purpose stereotype annotation, while @Service is a specialization of @Component specifically used for service layer components.
    - types:
        - Constructor injection
        - setter injection 
        - field injection

### properties file / db connection:
-  to connec the db we need ,
    spring.datasource.url
    spring.datasource.username
    spring.datasource.password 
    spring.jpa. ....

- add the jpa dependency in pom.xml, start/reload the project 
 
###  JPA & @entity:

- @Entity --> is for hibernate
- @Table

 Repository class (studentreposotory.class), anything that access database. Generally its an interface and it extends JPARepository<T,Id>

### 1. What is a Bean?

- In the Spring Framework, a **bean** is an object managed by the Spring IoC container.
- These objects, forming the backbone of the application, are instantiated, assembled, and managed by the container.
- The term "bean" encompasses objects that play a central role in Spring's dependency injection mechanism.
- ApplicationContext is responsible for managing beans and their dependencies.

### 2. What is Inversion of Control (IoC)?

- **IoC** is a design principle where an object **defines its dependencies without creating them**.
- Illustrate IoC with classes like `Company` and `Address`, showcasing a departure from traditional direct object creation.

**Advantages of IoC:**
- **Simplifies Dependency Management:** Objects no longer manage their dependencies directly.
- **Improves Code Organization:** Delegating dependency creation enhances code modularity and maintainability.

### 3. Uses of IoC and Beans:

**Bean Configuration:**
- Annotate classes with `@Component` to designate them as Spring beans.
- Use `@Configuration` along with `@Bean` annotations to provide metadata to the IoC container.

**IoC in Action:**
- Instantiate an IoC container (`AnnotationConfigApplicationContext`) to manage and assemble beans.
- Verify bean properties through tests, ensuring correct instantiation and initialization.

**Bean Wiring**:
- used to manage dependencies between beans. Allows spring to inject collaborating beans into each other.
- 2 types:
    - Autowiring
    - Manual wiring


-----------
## Annotations 
- @SpringBootApplication - main annotaion, used to run the main class, added for main class
- @RestController --> used to define RESTful service controller, @Controller + @ResponseBody
- @RequestMapping --> maps requests to at either base url for class level or specific url for method level
- @Autowired --> automatically inject dependencies into spring bean. Applied to fields, constructor params or setter methods
- @SequenceGenerator 
- @Id 
- @Transient -- no need to be in database
- @Repository --> used to indicate a class represents a data repository or DAO. which is used to interact with db or orther storage.


### SpringBoot Actuator:

It a component that gives your applications production ready operational monitoring and management capapbilities. dependency to add, "spring-boot-starter-actuator"

### Spring Profile:
u can configure and manage various sets of beans definitions and configurations. By spring.profiles.active. typically used in applications.properties file or application.yml file.

### Spring MVC:
A web framework within Spring, focused on building web applications and handling HTTP requests using the Model-View-Controller (MVC) pattern.

**Model:** Manages application data. \
**View:** Displays data to the user.\
**Controller:** Handles user requests, interacts with the model and view.\

- We can change port of Tomcat server in spring boot by server.port\
i.e server.port = 8081 in application.properties file


| **Points** | **@SpringBootApplication** | **@EnableAutoConfiguration** |
|------------|---------------------------|-------------------------------|
| **When to use** | When you want to use auto-configuration | When you want to customize auto-configuration |
| **Entry point** | Typically used on the main class of a Spring Boot application, serving as the entry point. | Can be used on any configuration class or in conjunction with @SpringBootApplication. |
| **Component Scanning** | Includes @ComponentScan annotation to enable component scanning. | Does not perform component scanning by itself. |
----------------------------------
 **Example**:\
 @SpringBootApplication \
public class MyApplication { \
    public static void main(String[] args) { \
        SpringApplication.run(MyApplication.class, args); \
    } \
} \
@Configuration \
@EnableAutoConfiguration \
public class MyConfiguration { 
}  

### Reasons Spring Data REST may not be Recommended:
- Performance Concerns:
Dynamic endpoint generation may lead to suboptimal performance, especially in very large-scale applications.

- Versioning Challenges:
Versioning REST APIs exposed by Spring Data REST can be challenging, posing issues for maintaining backward compatibility.

- Complex Relationship Handling:
Managing relationships between entities can be challenging and may require additional effort with Spring Data REST.

- Limited Filtering Options:
The options for filtering results returned by endpoints are limited, restricting flexibility in data retrieval. 

----------
- Hibernate is choosen as default implementation for JPA. when u add spring-boot-starter-data-jpa.
- u can override this by providing own JPA prop or hibernate properties in application.properties file.
