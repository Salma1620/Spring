# Spring

## Spring IoC
In the traditional approach without using Spring and IoC

the interface MessageService :
```java
public interface MessageService {
    String getMessage();
}
```
the first implementation of the interface :
```java
public class EmailService implements MessageService {
    @Override
    public String getMessage() {
        return "Email Message";
    }
}
```
the second implementation of the interface :
```java
public class NumberService implements MessageService {
    @Override
    public String getMessage() {
        return "Number Message";
    }
}
```
the Main class :
```java
public class Main {
    public static void main(String[] args) {
        // Create EmailService instance
        EmailService emailservice = new EmailService();
        // use the instance
        emailservice.getMessage();
    }
}
```
`Problem` :
if we want to instanciate an object of the second implementation we need to change the code source (the ain class ) witch we should not touch.
In a regular program, you usually control the flow of your code. <br/>
You create objects, call methods, and manage their interactions. <br/>
`Solution` :
With IoC, you “invert” this control. 
Instead of you managing everything, a framework like Spring takes charge of creating objects and making sure they work together in a spring container.
So you don’t need to make changes in the code source.

## Spring Container

The spring container creates objects, wire them together, configures them and manages their complete lifecycle from birth to death. Spring comes with several implementations of containers which can be categorized into two different types.

`Bean factories` : These are the simplest type of container, providing basic support for DI.<br/>
`ApplicationContext` : These are built on the notion of bean factories. It adds some extra functionality as compared to its parent class.

> [!NOTE]
> we will focus on the ApplicationContext.

### the Application Context

The Spring Application Context is an extension of the BeanFactory, offering advanced integration capabilities, event propagation, and application-layer specific contexts. 
It’s responsible for instantiating, configuring, and assembling beans, and it facilitates the creation of fully-configured application systems.

### Configuring the Spring Application Context

Spring supports several methods to configure the Application Context, including `XML configuration` ,`Annotation-based configuration`, and `Java-based configuration`. 
For modern Spring applications, **Annotation-based** and **Java-based** configurations are preferred due to their simplicity and clarity.

1. **XML-based Configuration:** <br/>
XML-based configuration involves defining Spring beans and their dependencies in XML configuration files. These files typically have a .xml extension and contain bean definitions using XML tags. <br/>
we use for this method the `ClassPathXmlApplicationContext`
 > simple XML configuration file defining a UserService bean:
```java
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd"><bean id="userService" class="com.example.UserService">
        <constructor-arg ref="userRepository" />
    </bean>
    // create an instance userRepository of the UserRepositoryImpl class
<bean id="userRepository" class="com.example.UserRepositoryImpl" />
</beans>
```
> the Main Class :
```java
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        // Retrieve beans from the Application Context
        MyService myService = context.getBean(userRepository.class);

        // Use the beans
        myApplication.runApp();
    }
}
```

2. **Annotation-based Configuration:** <br/>
Annotation-based configuration leverages annotations to configure Spring beans and their dependencies. Annotations like `@Component`, `@Service`, `@Repository`, and `@Autowired` are commonly used for this approach. <br/>
we use for this method the `AnnotationConfigApplicationContext`
### example with Annotation-based Configuration



3. **Java-based Configuration:** <br/>
Java-based configuration allows you to define Spring beans and their dependencies using Java code. This approach uses annotations like `@Configuration` and `@Bean` to specify configurations.

### example with Java-based configuration

1- Create a Service Bean:<br/>
```java
public class HelloService(){
    public String Hello(String name){
        return "hello"+name ;
    }
}
```
2- Configure the Bean with Java Config:<br/>
```java
@configuration
public class AppConfig{
    @Bean
    public HelloService HelloService(){
        return new HelloService();
    }
}
3- Use the Application Context in Your Application:
```java
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Retrieve beans from the Application Context
        MyService myService = context.getBean(HelloService.class);

        // Use the beans
        myService.HelloService();
        
        // Close the Application Context (optional)
        context.close();
    }
}
```
## Dependency Injection
Dependency Injection (DI), is a core feature of Spring that allows for `loose coupling` between components, 
making your applications more modular, easier to test, and maintain.<br/>
It's a design pattern where the dependencies of a class (the services it needs to perform its function) are supplied externally rather than hard-coded within the class.<br/> 
Spring Framework supports DI through its IoC container, which manages the creation and injection of dependencies.
>**Let's take an example:** <br/>
**Class Me :**

```java
public Class Me{
    String Name;
    int HomeNo;
    Family F;
    Job J;
    ArrayList <Integer> impNos;
}
```
> [!NOTE]
> This class depends on :<br/>
>**Dependencies in form of literals**   : Name and HomeNo.<br/>
>**Dependencies in form of objective**  : Family and Job.<br/>
>**Dependencies in form of collection** : impNos.<br/>




### Types of Dependency Injection in Spring
`Constructor Injection`: Dependencies are provided through class constructors.
`Setter Injection`     : Dependencies are set through setter methods.
`Field Injection`      : Dependencies are injected directly into the class fields.

**Setter Injection** <br/>
```java
// Bean class
public class MyBean {
    private String name;
    private int age;

    // Setter methods
    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
```java
//Main Class
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Retrieve the bean from the Application Context
        MyBean myBean = context.getBean(MyBean.class);

        // Use the bean
        System.out.println("Name: " + myBean.getName());
        System.out.println("Age: " + myBean.getAge());

        // Close the Application Context (optional)
        context.close();
    }
}
```
# Spring

## Spring IoC
In the traditional approach without using Spring and IoC

the interface MessageService :
```java
public interface MessageService {
    String getMessage();
}
```
the first implementation of the interface :
```java
public class EmailService implements MessageService {
    @Override
    public String getMessage() {
        return "Email Message";
    }
}
```
the second implementation of the interface :
```java
public class NumberService implements MessageService {
    @Override
    public String getMessage() {
        return "Number Message";
    }
}
```
the Main class :
```java
public class Main {
    public static void main(String[] args) {
        // Create EmailService instance
        EmailService emailservice = new EmailService();
        // use the instance
        emailservice.getMessage();
    }
}
```
`Problem` :
if we want to instanciate an object of the second implementation we need to change the code source (the ain class ) witch we should not touch.
In a regular program, you usually control the flow of your code. <br/>
You create objects, call methods, and manage their interactions. <br/>
`Solution` :
With IoC, you “invert” this control. 
Instead of you managing everything, a framework like Spring takes charge of creating objects and making sure they work together in a spring container.
So you don’t need to make changes in the code source.

## Spring Container

The spring container creates objects, wire them together, configures them and manages their complete lifecycle from birth to death. Spring comes with several implementations of containers which can be categorized into two different types.

`Bean factories` : These are the simplest type of container, providing basic support for DI.<br/>
`ApplicationContext` : These are built on the notion of bean factories. It adds some extra functionality as compared to its parent class.

> [!NOTE]
> we will focus on the ApplicationContext.

### the Application Context

The Spring Application Context is an extension of the BeanFactory, offering advanced integration capabilities, event propagation, and application-layer specific contexts. 
It’s responsible for instantiating, configuring, and assembling beans, and it facilitates the creation of fully-configured application systems.

### Configuring the Spring Application Context

Spring supports several methods to configure the Application Context, including `XML configuration` ,`Annotation-based configuration`, and `Java-based configuration`. 
For modern Spring applications, **Annotation-based** and **Java-based** configurations are preferred due to their simplicity and clarity.

1. **XML-based Configuration:** <br/>
XML-based configuration involves defining Spring beans and their dependencies in XML configuration files. These files typically have a .xml extension and contain bean definitions using XML tags. <br/>
we use for this method the `ClassPathXmlApplicationContext`
 > simple XML configuration file defining a UserService bean:
```java
<beans xmlns="http://www.springframework.org/schema/beans"
       xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
       xsi:schemaLocation="http://www.springframework.org/schema/beans
                           http://www.springframework.org/schema/beans/spring-beans.xsd"><bean id="userService" class="com.example.UserService">
        <constructor-arg ref="userRepository" />
    </bean>
    // create an instance userRepository of the UserRepositoryImpl class
<bean id="userRepository" class="com.example.UserRepositoryImpl" />
</beans>
```
> the Main Class :
```java
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");

        // Retrieve beans from the Application Context
        MyService myService = context.getBean(userRepository.class);

        // Use the beans
        myApplication.runApp();
    }
}
```

2. **Annotation-based Configuration:** <br/>
Annotation-based configuration leverages annotations to configure Spring beans and their dependencies. Annotations like `@Component`, `@Service`, `@Repository`, and `@Autowired` are commonly used for this approach. <br/>
we use for this method the `AnnotationConfigApplicationContext`
> Example with Annotation-based Configuration



3. **Java-based Configuration:** <br/>
Java-based configuration allows you to define Spring beans and their dependencies using Java code. This approach uses annotations like `@Configuration` and `@Bean` to specify configurations.

> Example with Java-based configuration

1- Create a Service Bean:<br/>
```java
public class HelloService(){
    public String Hello(String name){
        return "hello"+name ;
    }
}
```
2- Configure the Bean with Java Config:<br/>
```java
@configuration
public class AppConfig{
    @Bean
    public HelloService HelloService(){
        return new HelloService();
    }
}
```
3- Use the Application Context in Your Application:
```java
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Retrieve beans from the Application Context
        MyService myService = context.getBean(HelloService.class);

        // Use the beans
        myService.HelloService();
        
        // Close the Application Context (optional)
        context.close();
    }
}
```
## Dependency Injection
Dependency Injection (DI), is a core feature of Spring that allows for `loose coupling` between components, 
making your applications more modular, easier to test, and maintain.<br/>
It's a design pattern where the dependencies of a class (the services it needs to perform its function) are supplied externally rather than hard-coded within the class.<br/> 
Spring Framework supports DI through its IoC container, which manages the creation and injection of dependencies.<br/>
**Let's take an example:** <br/>
>**Class Me :**

```java
public Class Me{
    String Name;
    int HomeNo;
    Family F;
    Job J;
    ArrayList <Integer> impNos;
}
```
> [!NOTE]
> This class depends on :<br/>
>**Dependencies in form of literals**   : Name and HomeNo.<br/>
>**Dependencies in form of objective**  : Family and Job.<br/>
>**Dependencies in form of collection** : impNos.<br/>




### Types of Dependency Injection in Spring
`Constructor Injection`: Dependencies are provided through class constructors.<br/>
`Setter Injection`     : Dependencies are set through setter methods.<br/>
`Field Injection`      : Dependencies are injected directly into the class fields.<br/>
**Constructor Injection** <br/>
```java
// Bean class
public class Person {
    private String name;
    private int age;

    // constructor
    public Person (String name,int age){
        this.name=name;
        this.age=age;
    }
}
```

```java
// Configuration class
@Configuration
public class AppConfig {

    @Bean
    public Person Person() {
        return new Person("Salma",20);
    }
}
```
or with xml configuration
```java
<bean id="Person" class="com.example.Person">
<constructor-arg value="Salma"/>
<constructor-arg value="20"/>
</bean>
```
```java
//Main Class
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Retrieve the bean from the Application Context
        Person Person = context.getBean(Person.class);

        // Use the bean
        System.out.println("Name: " + Person.getName());
        System.out.println("Age: " + Person.getAge());

        // Close the Application Context (optional)
        context.close();
    }
}
```
**Setter Injection** <br/>
```java
// Bean class
public class MyBean {
    private String name;
    private int age;

    // Setter methods
    public void setName(String name) {
        this.name = name;
    }

    public void setAge(int age) {
        this.age = age;
    }
}
```
```java
//Main Class
public class Main {
    public static void main(String[] args) {
        // Create the Application Context
        AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class);

        // Retrieve the bean from the Application Context
        MyBean myBean = context.getBean(MyBean.class);

        // Use the bean
        System.out.println("Name: " + myBean.getName());
        System.out.println("Age: " + myBean.getAge());

        // Close the Application Context (optional)
        context.close();
    }
}
```

## Spring Architecture

<img src="https://github.com/Salma1620/Spring/assets/127985387/5a6b0d30-ffc5-44a3-8ad8-c720b85c8671"/>

### Core Spring container
This module of the Spring Framework uses lot of the design pattern such as the Factory method design pattern, DI pattern, Abstract Factory Design pattern, Singleton Design pattern, Prototype Design pattern, and so on.<br/>
`All other Spring modules are dependent on this module`. You'll implicitly use these classes when you configure your application. It is also called the `IoC container` and is central to Spring's support for dependency injection, which manages how the beans in a Spring application are created, configured, and managed.<br/> 
You can create Spring container either by using the implementations of BeanFactory or the implementations of the ApplicationContext. This module contains the Spring bean factory, which is the portion of Spring that provides the DI.<br/>
<br/>
`Spring Core` :
Spring Core is the foundational module of the Spring framework, providing fundamental features that include Dependency Injection (DI) and Inversion of Control (IoC). <br/>
Through IoC, Spring Core takes charge of managing and creating instances of JavaBeans, promoting a more flexible and loosely coupled application architecture.<br/>
<br/>
`Spring Bean` :
In a Spring framework, a Bean is identified as any Java class that is registered with Spring. <br/>
The Spring Bean module is responsible for managing the lifecycle of these bean classes. <br/>
This module provides a BeanFactory which creates bean instances, resolves bean-to-bean dependencies, and auto-wires the beans based on the name, or type.<br/>
<br/>
`Spring Context` :
All beans in the Spring framework are listed in a space called “Context” which holds everything in our Spring Application whether it is a simple configuration detail or a user-defined class like ‘Student’. <br/>
Imagine the Context as a hub that holds information about these beans, such as their setup details (like constructor or factory methods), and any other beans they rely on (dependencies). <br/>
We can access these beans (also called components) by interacting with the context. <br/>
When we start the Spring Application, the context is also brought to life, often referred to as “Application Context”. It’s like the Control Center that keeps track of all the important details to make our Spring Application work properly.

### Spring Web
Spring Web, a crucial module in the Spring framework, facilitates the development of powerful and scalable web applications in Java. <br/>
It provides a comprehensive set of tools and features, empowering developers to create dynamic and responsive web solutions efficiently.
<br/>
`Spring MVC` :<br/>
As the name says it is a way of implementing web applications using MVC (model view controller) design pattern. <br/>
It provides a structured approach to building web applications by separating different aspects of the implementation into 3 main components.
<br/>
>- **Model**: Represents the application’s data and business logic.<br/>
>- **View**: Renders the model data and generates the final output to be presented to the user.<br/>
>- **Controller**: Handles user requests, processes input, and interacts with the model to update the data.
