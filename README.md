# springBootBasics

## Spring Framework in 10 Steps

### Introduction

Spring Framework  is a widely used open-source application framework for building  enterprise Java  applications. It provides a comprehensive programming and  configuration model  for modern Java-based enterprise applications, making it popular in the industry due to its modular architecture, robustness, and flexibility.

### Spring Framework Levels

Spring Framework comprises three levels:

-   **Level 1**: Core Container - provides the fundamental functionality of the framework, including IoC (Inversion of Control) and DI (Dependency Injection).
-   **Level 2**: Data Access/Integration - provides support for  JDBC,  ORM  (Object-Relational Mapping), and other data access technologies.
-   **Level 3**: Web - provides support for building  web applications  using  Spring MVC  (Model-View-Controller) framework.

### Github Folder

The  Github folder  for this tutorial series contains all the necessary code examples for each step. You can access the  Github  folder by clicking  [here](https://github.com/in28minutes/spring-master-class/tree/master/01-spring-in-10-steps).

### Step 1 - Setting up a  Java Spring Project  using  [http://start.spring.io](http://start.spring.io/)

In Step 1, we will set up a new  Spring Boot project  using  [http://start.spring.io](http://start.spring.io/).  Spring Boot  is a popular project within the  Spring  ecosystem that provides an easier and faster way to set up a Spring-based application.

For example, let's say we want to build a simple  Spring Boot application  that exposes a  REST endpoint  to retrieve a list of students. We can follow these steps:

1.  Go to  [http://start.spring.io](http://start.spring.io/).
2.  Select the project type (Maven  or  Gradle), language (Java,  Kotlin, or  Groovy), and Spring Boot version.
3.  Choose any additional dependencies required for our project, such as Spring Web.
4.  Click on the Generate button to download the  project zip file.

### Step 2 - Understanding Tight Coupling using the  Binary Search Algorithm  Example

In Step 2, we will understand the concept of  tight coupling  using the  Binary Search Algorithm example. Tight coupling occurs when two or more components are dependent on each other, and any changes made to one component will affect the other.

For example, let's say we have two classes:  `BinarySearch`  and  `BubbleSort`. The  `BinarySearch`  class has a method  `search`  that performs a  binary search  on an array of integers. The  `BubbleSort`  class has a method  `sort`  that sorts an array of integers using the  bubble sort algorithm.

If we want to use the  `BinarySearch`  class to search a sorted array of integers, we need to first sort the array using the  `BubbleSort`  class. This creates a tight coupling between the two classes, as any changes made to the  `BubbleSort`  class will affect the  `BinarySearch`  class.

```
public class BinarySearch {
    public int search(int[] numbers, int numberToSearchFor) {
        BubbleSort bubbleSort = new BubbleSort();
        int[] sortedNumbers = bubbleSort.sort(numbers);
        // Binary search algorithm implementation
        return 0;
    }
}

public class BubbleSort {
    public int[] sort(int[] numbers) {
        // Bubble sort algorithm implementation
        return numbers;
    }
}

```

### Step 3 - Making the Binary  Search Algorithm  Example Loosely Coupled

In Step 3, we will make the Binary Search Algorithm example loosely coupled by introducing an interface. An interface defines a set of methods that a class must implement. By using an interface, we can decouple the  `BinarySearch`  and  `BubbleSort`  classes.

For example, we can create an interface called  `SortAlgorithm`  that defines a single method  `sort`  that takes an array of integers as input and returns a sorted array of integers. The  `BubbleSort`  class will implement the  `SortAlgorithm`  interface, and the  `BinarySearch`  class will depend on the  `SortAlgorithm`  interface instead of the  `BubbleSort`  class.

This decouples the  `BinarySearch`  and  `BubbleSort`  classes, making them easier to maintain and modify.
```
public interface SortAlgorithm {
    int[] sort(int[] numbers);
}

public class BubbleSort implements SortAlgorithm {
    public int[] sort(int[] numbers) {
        // Bubble sort algorithm implementation
        return numbers;
    }
}

public class BinarySearch {
    private SortAlgorithm sortAlgorithm;

    public BinarySearch(SortAlgorithm sortAlgorithm) {
        this.sortAlgorithm = sortAlgorithm;
    }

    public int search(int[] numbers, int numberToSearchFor) {
        int[] sortedNumbers = sortAlgorithm.sort(numbers);
        // Binary search algorithm implementation
        return 0;
    }
}

```

To use the updated code, we can create instances of the  `BubbleSort`  and  `BinarySearch`  classes as follows:
```
SortAlgorithm sortAlgorithm = new BubbleSort();
BinarySearch binarySearch = new BinarySearch(sortAlgorithm);
int[] numbers = {1, 2, 3, 4, 5};
int numberToSearchFor = 3;
int index = binarySearch.search(numbers, numberToSearchFor);
System.out.println("Number found at index: " + index);
```

### Step 4 - Using Spring Framework to Manage Dependencies - @Component, @Autowired

In Step 4, we will use the Spring Framework to manage dependencies using the  `@Component`  and  `@Autowired`  annotations. Spring Framework provides a powerful and flexible way to manage dependencies in a Java application.

For example, let's say we have a  `BinarySearchImpl`  class that implements the  `BinarySearch`  interface. The  `BinarySearchImpl`  class will depend on the  `SortAlgorithm`  interface, which will be injected into the class using the  `@Autowired`  annotation.

We can also annotate the  `BubbleSort`  class with the  `@Component`  annotation, which tells Spring Framework to create an instance of the  `BubbleSort`  class and manage its lifecycle.

By using the  `@Component`  and  `@Autowired`  annotations, we can easily manage the dependencies between the  `BinarySearchImpl`  and  `BubbleSort`  classes, making the application more modular and flexible.

## Conclusion

In this tutorial, we learned about the Spring Framework and its levels. We also covered the steps to set up a new Spring Boot project, understand tight coupling, make an example loosely coupled, and use Spring Framework to manage dependencies. Spring Framework is a powerful and popular  application framework  that provides a comprehensive programming and configuration model for modern Java-based enterprise applications.
## Step 4 - Using  Spring Framework  to Manage Dependencies -  `@Component`,  `@Autowired`

In Step 4, we use Spring Framework to manage dependencies between components in our Java application. Spring provides a number of annotations that we can use to define and inject dependencies between components, such as  `@Component`  and  `@Autowired`.

`@Component`  is an annotation that marks a  Java class  as a Spring-managed component. Spring will automatically create an instance of the component and manage its lifecycle. We can use the  `@Component`  annotation to define a component that implements the  `SortAlgorithm`  interface:

```
@Component
public class BubbleSort implements SortAlgorithm {
    public int[] sort(int[] numbers) {
        // Bubble sort algorithm implementation
        return numbers;
    }
}

```

`@Autowired`  is an annotation that tells Spring to inject a dependency into a Spring-managed component. We can use the  `@Autowired`  annotation to inject the  `SortAlgorithm`  implementation into the  `BinarySearch`  class:

```
@Component
public class BinarySearch {
    @Autowired
    private SortAlgorithm sortAlgorithm;

    public int search(int[] numbers, int numberToSearchFor) {
        int[] sortedNumbers = sortAlgorithm.sort(numbers);
        // Binary search algorithm implementation
        return 0;
    }
}

```

By using  `@Component`  and  `@Autowired`, we can easily manage dependencies between components in our  Java  application and make our code more modular and maintainable.

## Step 5 - What is happening in the background?

In Step 5, we look at what is happening in the background when we use annotations like  `@Component`  and  `@Autowired`  in our Spring application.

When we use  `@Component`  to mark a class as a Spring-managed component, Spring will automatically create an instance of the component and manage its lifecycle. Spring maintains a context of all the components in our application, which allows it to manage dependencies between components and resolve  circular dependencies.

When we use  `@Autowired`  to inject dependencies into a component, Spring will look for a matching component in its context and inject it into the component. Spring uses a number of strategies to resolve dependencies, such as by type, by name, or by using  `@Qualifier`.

By understanding what is happening in the background when we use  Spring annotations, we can better manage dependencies in our application and troubleshoot issues that may arise.

## Example 
here's a simple example that shows how  `@Component`  and  `@Autowired`  annotations make  dependency injection  much simpler:
```
@Component
public class MyService {
  public void doSomething() {
    System.out.println("Doing something...");
  }
}

@Component
public class MyController {
  @Autowired
  private MyService myService;

  public void doSomethingInController() {
    myService.doSomething();
  }
}

```

In this example, we have a  `MyService`  class that does some work, and a  `MyController`  class that depends on  `MyService`. We mark both classes with  `@Component`  to indicate that they are Spring-managed beans.

We also use  `@Autowired`  annotation to inject an instance of  `MyService`  into  `myService`  field in  `MyController`.

Now, here's the same code without using  `@Component`  and  `@Autowired`  annotations:

```
public class MyService {
  public void doSomething() {
    System.out.println("Doing something...");
  }
}

public class MyController {
  private MyService myService;

  public MyController() {
    this.myService = new MyService();
  }

  public void doSomethingInController() {
    myService.doSomething();
  }
}

```

In this example, we manually create an instance of  `MyService`  in the constructor of  `MyController`  and assign it to  `myService`  field.

The problem with this approach is that it tightly couples  `MyController`  to  `MyService`. If we decide to change the implementation of  `MyService`  in the future, we would have to modify the constructor of  `MyController`  to use the new implementation.

Moreover, if we had multiple implementations of  `MyService`, we would have to manually instantiate the correct implementation in the constructor of  `MyController`. This can quickly become tedious and error-prone.

Using  `@Component`  and  `@Autowired`  annotations allows  Spring  to handle the instantiation and injection of dependencies automatically. This makes the code more flexible, maintainable, and easier to manage.
# Dynamic Auto Wiring and Troubleshooting - @Primary

In Spring Framework, we can use  `@Primary`  annotation to indicate that a particular bean should be given preference when multiple beans of the same type are candidates to be autowired by other components.

For example, let's say we have two implementations of a  service interface  `MyService`:
```
@Service
public class MyServiceImplOne implements MyService {
  // implementation
}

@Service
public class MyServiceImplTwo implements MyService {
  // implementation
}

```

Now, if we try to autowire  `MyService`  in another component, we'll get an exception because  Spring  doesn't know which implementation to use:
```
@Component
public class MyComponent {
  @Autowired
  private MyService myService; // throws NoUniqueBeanDefinitionException
}

```

To solve this problem, we can use  `@Primary`  annotation to indicate that one of the beans should be given preference:
```
@Service
@Primary
public class MyServiceImplOne implements MyService {
  // implementation
}

@Service
public class MyServiceImplTwo implements MyService {
  // implementation
}

```

Now, if we try to autowire  `MyService`  in another component, Spring will use  `MyServiceImplOne`  by default:
```
@Component
public class MyComponent {
  @Autowired
  private MyService myService; // uses MyServiceImplOne
}

```

# Fastest Approach to Solve All Your Exceptions

Exception handling  is an important part of any software application. Here are some tips to quickly solve exceptions:

1.  Read the Exception message: The first step in solving an  exception  is to read the exception message. The message will often give you a clue as to what went wrong.
    
2.  Check the Stack Trace: The  stack trace  will tell you where the exception occurred in your code. Look at the top of the stack trace to see the method that threw the exception.
    
3.  Google the Exception: Copy the exception message and search it on Google. You'll often find discussions on forums or  Stack Overflow  that can help you solve the problem.
    
4.  Check the Code: Look at the code that threw the exception and see if there are any obvious errors. Check for  null values,  incorrect variable types, and other common mistakes.
    
5.  Use a Debugger: If you still can't solve the problem, use a  debugger  to step through your code and see where the exception is occurring. This can help you pinpoint the problem.
    

By following these steps, you can quickly solve most exceptions and keep your application running smoothly.
## Step 7 - Spring Injection using Java Constructor and Setter Methods

Spring Framework  provides two main ways to inject dependencies into an object:  constructor injection  and  setter injection.

### Constructor Injection

Constructor injection involves passing the dependencies as arguments to the constructor of the object. Here's an example:

```
public class MyService {
    private final MyDependency myDependency;
    
    public MyService(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
    
    // ...
}

```

In this example, the  `MyService`  class has a dependency on  `MyDependency`, which is passed as an argument to the constructor. The  `final`  keyword is used to ensure that the  `myDependency`  field is set only once and cannot be changed.

### Setter Injection

Setter injection, on the other hand, involves calling  setter methods  on the object to set the dependencies. Here's an example:

```
public class MyService {
    private MyDependency myDependency;
    
    public void setMyDependency(MyDependency myDependency) {
        this.myDependency = myDependency;
    }
    
    // ...
}

```

In this example, the  `MyService`  class has a  setter method  `setMyDependency`  that sets the  `myDependency`  field.

### Choosing between Constructor and Setter Injection

Both constructor and setter injection have their pros and cons. Constructor injection ensures that the dependencies are set at the time of  object creation  and cannot be changed later. Setter injection, on the other hand, allows for more flexibility and can be used to set  optional dependencies.

In general, it's recommended to use constructor injection for  mandatory dependencies  and setter injection for optional dependencies.

## Step 8 - Spring Framework Modules

Spring Framework is a  modular framework, which means that it is composed of several modules, each of which provides a different set of features and functionality. Here are some of the core modules of Spring:

### Spring Core

The  Spring Core module  provides the basic components of the Spring Framework, including the  IoC container  and DI functionality. This module is the foundation of the Spring Framework and is required by all other modules.

### Spring MVC

The  Spring MVC module  provides a web framework for building  web applications  using Spring. It includes features such as  request mapping,  data binding, and  view resolution.

### Spring Data

The Spring Data module provides a  unified API  for accessing various types of  data sources, including relational databases, NoSQL databases, and more. It includes modules such as  Spring Data JPA,  Spring Data MongoDB, and  Spring Data Redis.

### Spring Security

The  Spring Security module  provides security features for Spring applications, including authentication and authorization. It includes features such as  user authentication, access control, and  secure communication.

### Spring Boot

Spring Boot is a framework for building standalone Spring applications that are easy to deploy and run. It includes features such as auto-configuration, embedded servers, and production-ready metrics.

### Spring Cloud

Spring Cloud  is a collection of tools and frameworks for building distributed systems and microservices using Spring. It includes modules such as  Spring Cloud Config,  Spring Cloud Netflix, and  Spring Cloud Stream.

### Spring Integration

Spring Integration  is a framework for building message-driven applications using Spring. It includes features such as  channel adapters,  message routers, and  message transformers.

## Conclusion

Spring Framework is a powerful and popular framework for building Java applications. In this tutorial, we learned about constructor and setter injection in Spring, as well as the  core modules  of the Spring Framework. By understanding these concepts, you'll be well on your way to building robust and maintainable Spring applications.

## Step 10 - Why is Spring Framework Popular in the Java World?

Spring Framework is one of the most popular frameworks for building Java applications. Here are some of the reasons why:

### Dependency Injection

Spring Framework provides a powerful and flexible  dependency injection mechanism  that makes it easy to manage dependencies and decouple components in a Java application. With Spring's IoC container, you can easily wire together your application's components and manage their lifecycle.

### Modularity

Spring Framework is designed to be modular, which means that you can use only the components and features that you need in your application. This makes it easy to build applications that are lightweight and optimized for performance.

### Integration

Spring Framework provides integration with a wide variety of other technologies and frameworks, including  Hibernate,  JPA, and many others. This makes it easy to build applications that work seamlessly with existing systems and technologies.

### Testability

Spring Framework's modularity and  dependency injection  mechanism make it easy to write  unit tests  for your Java applications. With Spring, you can easily mock dependencies and test each component of your application in isolation.

### Community

Spring Framework has a large and active community of developers and users who contribute to the project and provide support to others. This makes it easy to find help and resources when you need them, and ensures that the framework is constantly evolving and improving.

## Step 17 - DO NOT SKIP: New to Maven and Eclipse

If you're new to Maven and Eclipse, here's a quick overview of how to get started:

1.  Install Eclipse: Download and install Eclipse from the official website.
    
2.  Install Maven: Download and install Maven from the official website.
    
3.  Create a new  Maven project: In Eclipse, go to File > New > Maven Project. Follow the prompts to create a new Maven project.
    
4.  Add dependencies: To add dependencies to your project, add them to the "pom.xml" file in your project. Maven will automatically download and manage the dependencies for you.
    
5.  Build and run your project: To build and run your project, use the  Maven commands  "mvn clean install" and "mvn exec:java" respectively.
    

Here's an example of a simple Maven project:
```
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0
                             http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.example</groupId>
    <artifactId>my-app</artifactId>
    <version>1.0-SNAPSHOT</version>

    <dependencies>
        <dependency>
            <groupId>junit</groupId>
            <artifactId>junit</artifactId>
            <version>4.12</version>
            <scope>test</scope>
        </dependency>
    </dependencies>
</project>

```

In this example, we've defined a Maven project with a single dependency on  JUnit  4.12. When we buildand run the project using Maven, it will automatically download and include the  JUnit library  in our project.

To summarize, Maven is a powerful  build tool  that makes it easy to manage dependencies and build Java projects. Eclipse is a popular  IDE  that provides an  integrated environment  for developing Java applications. By using Maven and Eclipse together, you can streamline your development process and build high-quality, maintainable Java applications.

## 19. Step 11 - Dependency Injection - A few more examples

Dependency injection is a core concept in the Spring framework and allows for a more modular and flexible design of applications. In this step, we will go through a few more examples of how to use dependency injection in Spring.

### Constructor Injection

Constructor injection is a type of dependency injection where dependencies are injected through a constructor. For example, let's say we have a class  `Foo`  that depends on an interface  `Bar`. We can inject the dependency through the constructor as follows:

```
public class Foo {
    private Bar bar;

    public Foo(Bar bar) {
        this.bar = bar;
    }
}

```

### Setter Injection

Setter injection is a type of dependency injection where dependencies are injected through setter methods. For example, let's say we have a class  `Foo`  that depends on an interface  `Bar`. We can inject the dependency through a  setter method  as follows:

```
public class Foo {
    private Bar bar;

    public void setBar(Bar bar) {
        this.bar = bar;
    }
}

```

## 20. Step 12 - Autowiring in Depth - by Name and @Primary

Autowiring is a feature in Spring that allows the framework to automatically inject dependencies into a bean without the need for explicit configuration. In this step, we will go through autowiring in more depth and cover how to use it by name and with the  `@Primary`  annotation.

### Autowiring by Name

Autowiring by name is a way of  autowiring dependencies  in Spring by matching the  bean name  with the name of the dependency. For example, let's say we have a class  `Foo`  that depends on a bean with the name  `bar`. We can autowire the dependency by name as follows:

```
public class Foo {
    @Autowired
    private Bar bar;
}

```

### @Primary Annotation

The  `@Primary`  annotation is used to indicate that a bean should be considered the  primary bean  when multiple beans of the same type are present. For example, let's say we have two beans of type  `Bar`:

```
@Component
public class BarOne implements Bar {}

@Component
@Primary
public class BarTwo implements Bar {}

```

In this case, if we autowire a  `Bar`  dependency, Spring will inject an instance of  `BarTwo`  because it is marked as the primary bean.

## 21. Step 13 - Autowiring in Depth - @Qualifier annotation

The  `@Qualifier`  annotation is used in Spring to specify which bean to autowire when there are multiple beans of the same type. For example, let's say we have two beans of type  `Bar`:

```
@Component
@Qualifier("one")
public class BarOne implements Bar {}

@Component
@Qualifier("two")
public class BarTwo implements Bar {}

```

In this case, if we want to autowire a  `Bar`  dependency with the  `one`  qualifier, we can use the  `@Qualifier`  annotation as follows:

```
public class Foo {
    @Autowired
    @Qualifier("one")
    private Bar bar;
}

```

This tells Spring to inject an instance of  `BarOne`  because it is the bean with the  `one`  qualifier.
## 22. Step 14 - Scope of a Bean - Prototype and Singleton

In Spring, the scope of a bean defines the lifecycle and visibility of the bean instance. The two most common scopes in Spring are prototype and singleton.

### Singleton Scope

The default scope in Spring is singleton, which means that only one instance of the bean is created and shared for all requests for that bean. For example, let's say we have a class  `Foo`:

```
@Component
public class Foo {}

```

By default, Spring will create a single instance of  `Foo`  and share it across all requests for  `Foo`.

### Prototype Scope

Prototype scope in Spring means that a new instance of the bean is created for each request for that bean. For example, let's say we have a class  `Bar`:

```
@Component
@Scope("prototype")
public class Bar {}

```

In this case, each time we request a  `Bar`  instance from Spring, a new instance of  `Bar`  will be created.

## 23. Step 15 - Complex Scope Scenarios of a Spring Bean - Mix Prototype and Singleton

In more complex scenarios, we may want to mix prototype and  singleton scopes  for different beans. For example, let's say we have a class  `Foo`  that depends on a prototype-scoped bean  `Bar`:

```
@Component
public class Foo {
    @Autowired
    private Bar bar;
}

@Component
@Scope("prototype")
public class Bar {}

```

In this case, each time we request a  `Foo`  instance from Spring, a new instance of  `Bar`  will be created and injected into  `Foo`.

## 24. Step 15B - Difference Between Spring Singleton and GOF Singleton

It is important to note that the  Spring singleton scope  is different from the  singleton pattern  in the  Gang of Four  (GOF) design patterns. In the GOF singleton pattern, there is only one instance of a class globally, whereas in  Spring singleton  scope, there is only one instance of a bean per Spring container.

For example, let's say we have a class  `SingletonClass`  implemented as a GOF singleton:

```
public class SingletonClass {
    private static SingletonClass instance = new SingletonClass();
    private SingletonClass() {}
    public static SingletonClass getInstance() {
        return instance;
    }
}

```

In this case, there is only one instance of  `SingletonClass`  globally.

On the other hand, if we have a  Spring bean  with  singleton scope:

```
@Component
public class SingletonBean {}

```

In this case, there is only one instance of  `SingletonBean`  per Spring container.
Let's consider an example to illustrate this difference. Suppose we have a simple bean called  `Counter`  that increments an  internal counter  each time it is called:

```
@Component
@Scope("prototype")
public class Counter {
    private int count = 0;

    public int increment() {
        return ++count;
    }
}

```

If we inject this bean into another bean as a prototype, a new instance of  `Counter`  will be created each time it is requested:

```
@Component
public class PrototypeBean {
    @Autowired
    private Counter counter;

    public int incrementCounter() {
        return counter.increment();
    }
}

```

On the other hand, if we inject this bean into another bean as a singleton, only one instance of  `Counter`  will be created and shared among all requests:

```
@Component
@Scope("singleton")
public class SingletonBean {
    @Autowired
    private Counter counter;

    public int incrementCounter() {
        return counter.increment();
    }
}

```

Now, let's test these two scenarios by creating a new instance of each bean and invoking the  `incrementCounter()`  method on each:

```
@Component
public class Test {
    @Autowired
    private PrototypeBean prototypeBean;

    @Autowired
    private SingletonBean singletonBean;

    public void runTest() {
        // Prototype scope
        System.out.println("Prototype scope:");
        System.out.println(prototypeBean.incrementCounter()); // 1
        System.out.println(prototypeBean.incrementCounter()); // 1

        // Singleton scope
        System.out.println("Singleton scope:");
        System.out.println(singletonBean.incrementCounter()); // 1
        System.out.println(singletonBean.incrementCounter()); // 2
    }
}

```

In the prototype scope, a new instance of  `Counter`  is created each time  `incrementCounter()`  is called, so the counter is always reset to zero. In the  singleton scope, only one instance of  `Counter`  is created, so the counter is incremented each time  `incrementCounter()`  is called. Therefore, the output of this test would be:

```
Prototype scope:
1
1
Singleton scope:
1
2

```

As we can see, the behavior of the two scenarios is different due to the difference in scope. The  prototype scope  creates a new instance of the bean each time it is requested, while the singleton scope creates only one instance of the bean that is shared among all requests.

# Step 16 - Using Component Scan to scan for beans

In Spring  Framework, we can use component scan to scan for beans in our application. Component scan is a way to automatically detect and register beans in the  Spring container  based on certain criteria such as  class annotations.

## Enabling Component Scan

We can enable component scan in our  Spring application  by adding the  `@ComponentScan`  annotation to a configuration class. For example:

```
@Configuration
@ComponentScan("com.example.demo")
public class AppConfig {
    // configuration code here
}

```

In the above example, we have enabled component scan for the package  `com.example.demo`. This means that  Spring  will scan this package and its sub-packages for classes with certain annotations (such as  `@Component`,  `@Service`,  `@Repository`, etc.) and register them as beans in the Spring container.

## Defining Component Scan Filters

We can also define filters for component scan to include or exclude certain classes from being registered as beans. There are several types of filters we can use, such as  `@ComponentScan.Filter`,  `RegexPatternTypeFilter`,  `AspectJTypeFilter`, etc.

For example, if we want to include only classes annotated with  `@Controller`  in our component scan, we can do:

java

Copy

```
@Configuration
@ComponentScan(basePackages = "com.example.demo", includeFilters = @ComponentScan.Filter(type = FilterType.ANNOTATION, value = Controller.class))
public class AppConfig {
    // configuration code here
}

```

In the above example, we have used  `@ComponentScan.Filter`  to define an  annotation filter  that includes only classes annotated with  `@Controller`.

# Step 17 - Lifecycle of a Bean - @PostConstruct and @PreDestroy

In Spring Framework, the lifecycle of a bean refers to the various stages in the life of a bean, from its creation to its destruction. During the lifecycle of a bean, we can perform certain actions, such as initializing the bean, cleaning up resources, etc. We can use the  `@PostConstruct`  and  `@PreDestroy`  annotations to define methods that should be executed after the bean has been created and before the bean is destroyed, respectively.

## @PostConstruct Annotation

The  `@PostConstruct`  annotation is used to specify a method that should be called immediately after the bean has been created, and after all dependencies have been injected. The method annotated with  `@PostConstruct`  can be used to perform any  initialization logic  for the bean.

For example:

```
@Component
public class MyBean {
 
    @PostConstruct
    public void init() {
        // initialization logic here
    }
}

```

In the above example, the  `init()`  method will be called immediately after the  `MyBean`  has been created, and after all dependencies have been injected.

## @PreDestroy Annotation

The  `@PreDestroy`  annotation is used to specify a method that should be called just before the bean is destroyed. The method annotated with  `@PreDestroy`  can be used to perform any  cleanup logic  for the bean.

For example:

```
@Component
public class MyBean {
 
    @PreDestroy
    public void cleanup() {
        // cleanup logic here
    }
}

```

In the above example, the  `cleanup()`  method will be called just before the  `MyBean`  is destroyed. This method can be used to release any resources held by the bean, such as closing a database connection or releasing a file handle.

It is important to note that the  `@PostConstruct`  and  `@PreDestroy`  annotations only work with singleton scoped beans. If a bean is defined with a different scope, such as  prototype scope, these annotations will not be effective.
## Step 19 - Removing Spring Boot in Basic Application

In this step, we remove the  Spring Boot  framework from our basic application and replace it with the Spring Framework. Here are the steps we need to follow:

1.  Remove the  `spring-boot-starter-web`  dependency from the  `pom.xml`  file.
2.  Add the  `spring-webmvc`  and  `spring-context`  dependencies to the  `pom.xml`  file.
3.  Create a  `WebAppInitializer`  class that extends the  `AbstractAnnotationConfigDispatcherServletInitializer`  class.
4.  In the  `WebAppInitializer`  class, implement the  `getRootConfigClasses()`  and  `getServletConfigClasses()`  methods to define the  root configuration  and the  servlet configuration.
5.  Create a  `WebConfig`  class that extends the  `WebMvcConfigurerAdapter`  class and annotate it with the  `@Configuration`  annotation.
6.  In the  `WebConfig`  class, override the  `configureDefaultServletHandling()`  method and call the  `enable()`  method on the  `DefaultServletHandlerConfigurer`  object.
7.  In the  `WebConfig`  class, create a  `ViewResolver`  bean to configure the view resolver.
8.  Create a controller class that handles requests and returns a view.

## Step 20 - Fixing minor stuff - Add Logback and Close Application Context

In this final step, we add the  Logback logging framework  to our application and make sure that the application context is closed properly when the application shuts down.

1.  Add the  Logback dependencies  to the  `pom.xml`  file:

```
<dependencies>
    <!-- ... -->
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-classic</artifactId>
        <version>1.2.3</version>
    </dependency>
    <dependency>
        <groupId>ch.qos.logback</groupId>
        <artifactId>logback-core</artifactId>
        <version>1.2.3</version>
    </dependency>
</dependencies>

```

2.  Create a  `logback.xml`  file in the  `src/main/resources`  directory to configure Logback. Here's an example configuration:

```
<configuration>
    <appender name="CONSOLE" class="ch.qos.logback.core.ConsoleAppender">
        <encoder>
            <pattern>%d{HH:mm:ss.SSS} [%thread] %-5level %logger{36} - %msg%n</pattern>
        </encoder>
    </appender>
    <root level="DEBUG">
        <appender-ref ref="CONSOLE" />
    </root>
</configuration>

```

Note: The above  Logback configuration  will log messages to the console in a specific format.

3.  In the  `WebConfig`  class, add the following method to configure Logback:


```
@Bean
public LoggerContext loggerContext() {
    return (LoggerContext) LoggerFactory.getILoggerFactory();
}

```

4.  In the  `Main`  class, add the following code to close the application context when the application shuts down:


```
public static void main(String[] args) {
    try (AnnotationConfigApplicationContext context = new AnnotationConfigApplicationContext(AppConfig.class)) {
        // Run the application
    } catch (Exception e) {
        LOGGER.error("Error while running the application", e);
    }
}

```

Note: The  `AnnotationConfigApplicationContext`  class implements the  `AutoCloseable`  interface, which means that we can use it in a try-with-resources statement to automatically close the  application context  when the application exits.

## Step 21 - Defining Spring Application Context using XML - Part 1

In this step, we will be defining the  Spring application context  using XML.

### What is  Spring Application  Context?

The Spring  application context is a container that holds all the beans (objects) required by the application. It creates, manages, and wires the beans together. The  Spring framework  provides various implementations of the application context, such as XML-based, annotation-based, and Java-based.

### How to Define Spring Application Context using XML?

To define the Spring application context using XML, we need to create a  configuration file  named  `applicationContext.xml`  in the  `src/main/resources`  directory. This file will contain the bean definitions.

Here's an example of  `applicationContext.xml`  file:

```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <bean id="greetingService" class="com.example.service.GreetingServiceImpl">
        <property name="greeting" value="Hello, World!"/>
    </bean>

    <bean id="greetingController" class="com.example.controller.GreetingController">
        <property name="greetingService" ref="greetingService"/>
    </bean>

</beans>

```

In this example, we have defined two beans -  `greetingService`  and  `greetingController`. The  `greetingService`  bean is of type  `GreetingServiceImpl`, which is a service that provides a greeting message. The  `greetingController`  bean is of type  `GreetingController`, which is a controller that uses the  `greetingService`  to get the  greeting message  and returns it to the client.

### How to Use Spring Application Context in Code?

To use the Spring application context in code, we need to create an instance of  `ClassPathXmlApplicationContext`  by passing the  configuration file path  as a parameter. Here's an example:

```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
GreetingController greetingController = context.getBean(GreetingController.class);
String result = greetingController.greet();
System.out.println(result);

```

In this example, we have created an instance of  `ClassPathXmlApplicationContext`  by passing the  `applicationContext.xml`  file path as a parameter. We have then retrieved the  `GreetingController`  bean from the context and called its  `greet()`  method, which returns the greeting message. The message is then printed to the console.

## Step 22 - Defining Spring Application Context using XML - Part 2

In the previous step, we learned how to define the Spring application context using XML. In this step, we will cover some advanced features of  Spring XML configuration.

### Property Placeholder

Spring provides a way to externalize the configuration using property files. We can define placeholders in the  XML configuration file  and use property files to replace those placeholders at runtime.

Here's an example of how to define a  property placeholder  in the XML configuration file:

```
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

```

In this example, we have defined a bean of type  `BasicDataSource`  and used property placeholders for the  driver class name,  URL, username, and password. We can replace these placeholders with actual values at runtime by defining them in a property file.

Here's an example of a  property file  named  `application.properties`:


```
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/mydb
jdbc.username=root
jdbc.password=password

```

We can load this property file at runtime using  `PropertyPlaceholderConfigurer`.

```
<context:property-placeholder location="classpath:application.properties"/>

```

### Bean Scopes

Spring provides several scopes for beans, such as singleton, prototype, request, session, and global session. The default scope is singleton, which means Spring creates only one instance of the bean and returns the same instance every time it is requested.

Here's an example of how to define a  prototype scope  for a bean:

xml

Copy

```
<bean id="myBean" class="com.example.MyBean" scope="prototype"/>

```

In this example, we have defined a bean of type  `MyBean`  with a prototype scope. This means Spring creates a new instance of the bean every time it is requested.

### Bean Inheritance

Spring provides a way to inherit  bean definitions. We can define a  parent bean  and then create  child beans  that inherit the properties of the parent bean.

Here's an example of a parentbean:

```
<bean id="parentBean" class="com.example.Parent">
    <property name="name" value="Parent"/>
</bean>

```

And here's an example of a  child bean  that inherits from the parent bean:

```
<bean id="childBean" class="com.example.Child" parent="parentBean">
    <property name="age" value="10"/>
</bean>

```

In this example, we have defined a parent bean of type  `Parent`  with a name property. We have then defined a child bean of type  `Child`  that inherits from the parent bean and adds an age property.

### Aliases

Spring provides a way to define  aliases  for beans. We can define multiple aliases for a single bean.

Here's an example of how to define aliases for a bean:

```
<bean id="myBean" class="com.example.MyBean"/>
<alias name="myBean" alias="myAlias"/>
<alias name="myBean" alias="myOtherAlias"/>

```

In this example, we have defined a bean of type  `MyBean`  with an id of  `myBean`. We have then defined two aliases for the bean -  `myAlias`  and  `myOtherAlias`.

## Step 23 - Mixing XML Context with Component Scan for Beans defined with Annotations

In the previous steps, we have learned how to define the Spring application context using XML. We have also learned how to use  component scanning  to automatically detect and register beans defined with annotations. In this step, we will learn how to mix XML context with component scan.

### Why Mix XML Context with Component Scan?

Although component scanning is a powerful feature of Spring, there may be cases where we need to define beans using XML configuration. For example, we may need to define beans with  complex initialization logic  or we may need to use property placeholders. In such cases, we can mix  XML context  with component scan.

### How to Mix XML Context with Component Scan?

To mix XML context with component scan, we can define the XML configuration file and enable component scanning in the same application context.

Here's an example of how to define the XML configuration file:

```
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
                        http://www.springframework.org/schema/beans/spring-beans.xsd">

    <context:property-placeholder location="classpath:application.properties"/>

    <bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
        <property name="driverClassName" value="${jdbc.driverClassName}"/>
        <property name="url" value="${jdbc.url}"/>
        <property name="username" value="${jdbc.username}"/>
        <property name="password" value="${jdbc.password}"/>
    </bean>

    <bean id="myBean" class="com.example.MyBean"/>

</beans>

```

In this example, we have defined two beans using  XML configuration  -  `dataSource`  and  `myBean`. We have also loaded property placeholders from the  `application.properties`  file.

To enable component scanning, we can add the following line to the XML configuration file:

```
<context:component-scan base-package="com.example"/>

```

This tells Spring to scan the  `com.example`  package for beans defined with annotations.

We can then use the beans defined in the XML configuration file and the beans detected by component scanning in the same application context.

```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
MyBean myBean = context.getBean(MyBean.class);
myBean.doSomething();

```

In this example, we have created an instance of  `ClassPathXmlApplicationContext`  by passing the  `applicationContext.xml`  file path  as a parameter. We have then retrieved the  `MyBean`  bean from the context and called its  `doSomething()`  method. The  `MyBean`  bean is defined using XML configuration.

A property placeholder is a placeholder used in the  Spring XML configuration file  to specify a value that can be resolved at runtime from a property file or environment variables. It allows us to externalize the configuration and change values at runtime without modifying the code.

Here's an example of how to define a  property placeholder  in the Spring XML configuration file:


```
<bean id="dataSource" class="org.apache.commons.dbcp2.BasicDataSource" destroy-method="close">
    <property name="driverClassName" value="${jdbc.driverClassName}"/>
    <property name="url" value="${jdbc.url}"/>
    <property name="username" value="${jdbc.username}"/>
    <property name="password" value="${jdbc.password}"/>
</bean>

```

In this example, we have defined a bean of type  `BasicDataSource`  and used property placeholders for the  driver class name,  URL, username, and password.

We can replace these placeholders with actual values at runtime by defining them in a  property file. Here's an example of a property file named  `application.properties`:

```
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql://localhost:3306/mydb
jdbc.username=root
jdbc.password=password

```

We can then load this property file at runtime using  `PropertyPlaceholderConfigurer`:

```
<context:property-placeholder location="classpath:application.properties"/>

```

This will replace the placeholders in the Spring  XML configuration file  with the values from the  `application.properties`  file at runtime.

In Spring, an alias is an alternative name or identifier for a bean. It allows us to refer to a bean by multiple names. We can define one or more aliases for a single bean.

Here's an example of how to define aliases for a bean in the  Spring XML configuration file:

```
<bean id="myBean" class="com.example.MyBean"/>
<alias name="myBean" alias="myAlias"/>
<alias name="myBean" alias="myOtherAlias"/>

```

In this example, we have defined a bean of type  `MyBean`  with an id of  `myBean`. We have then defined two aliases for the bean -  `myAlias`  and  `myOtherAlias`.

We can then use any of these names to retrieve the bean from the  Spring application context:

```
ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
MyBean myBean = context.getBean("myBean", MyBean.class);
MyBean myAlias = context.getBean("myAlias", MyBean.class);
MyBean myOtherAlias = context.getBean("myOtherAlias", MyBean.class);

```

In this example, we have retrieved the bean using the original name  `myBean`, as well as the aliases  `myAlias`  and  `myOtherAlias`. All three calls will return the same instance of the  `MyBean`  bean.
## IOC Container  vs Application Context vs  Bean Factory

In Spring, an Inversion of Control (IOC) container is responsible for managing the lifecycle of beans. It creates and manages instances of beans, and injects dependencies into them. There are two types of  IOC containers  in Spring:  BeanFactory  and ApplicationContext.

BeanFactory is the basic IOC container that provides the fundamental features of the IOC container. It reads  bean definitions  and creates  bean instances  lazily, i.e., only when they are requested. It is suitable for small to medium-sized applications where the performance is not a significant concern.

ApplicationContext is a sub-interface of BeanFactory that provides additional features like  AOP,  message resource handling,  event publication, and internationalization support. It reads bean definitions and creates bean instances eagerly, i.e., at the time of application startup. It is suitable for large, enterprise-level applications where the performance is a significant concern.

Here's an example that demonstrates the use of  ApplicationContext:

```
public class MyApp {
    public static void main(String[] args) {
        ApplicationContext context = new ClassPathXmlApplicationContext("applicationContext.xml");
        MyBean myBean = context.getBean("myBean", MyBean.class);
        myBean.doSomething();
    }
}

```

In this example, we have created an instance of the ApplicationContext by providing the path to the  XML configuration  file. We have then retrieved an instance of the  MyBean class  from the context and called its  `doSomething()`  method.

## @Component vs @Service vs @Repository vs @Controller

In Spring, we use annotations to mark classes as beans and to specify their roles. There are four annotations that are commonly used to mark classes as beans:  `@Component`,  `@Service`,  `@Repository`, and  `@Controller`.

`@Component`  is the most basic annotation that marks a class as a Spring bean. It is used to indicate that a class is a general-purpose component that does not fall into any specific category.

`@Service`  is an annotation that marks a class as a business service. It is used to indicate that a class performs some  business logic  and is usually used in the service layer of the application.

`@Repository`  is an annotation that marks a class as a data access object (DAO). It is used to indicate that a class performs database operations and is usually used in the  persistence layer  of the application.

`@Controller`  is an annotation that marks a class as a controller. It is used to indicate that a class handles  HTTP requests  and is usually used in the  presentation layer  of the application.

Here's an example that demonstrates the use of  `@Service`:

```
@Service
public class MyService {
    public void doSomething() {
        // business logic here
    }
}

```

In this example, we have marked the  MyService  class with  `@Service`  to indicate that it is a business service. We can then inject an instance of this class into other beans using  `@Autowired`.

## Read values from external properties file

In Spring, we can  externalize configuration  by storing values in an  external properties file. We can then read these values into our  Spring beans  using  `@Value`  annotations.

Here's an example of how to define properties in an external properties file:

```
my.property=value

```

We can then read this property into a  Spring bean  using  `@Value`:

```
@Service
public class MyService {
    @Value("${my.property}")
    private String myProperty;

    public void doSomething() {
        System.out.println("my.property = " + myProperty);
    }
}

```

In this example, we have injected the value of the  `my.property`  key into the  `myProperty`  field of the  MyService bean  using  `@Value`. We can then use this value in our business logic. We can also use  `@PropertySource`  to specify the location of the properties file.

```
@Service
@PropertySource("classpath:my.properties")
public class MyService {
    @Value("${my.property}")
    private String myProperty;

    public void doSomething() {
        System.out.println("my.property = " + myProperty);
    }
}

```

In this example, we have used  `@PropertySource`  to specify the location of the  properties file. We can then inject the value of the  `my.property`  key into the  `myProperty`  field of the MyService bean using  `@Value`.

## Understanding the World Before Spring Boot

Before Spring Boot, building a Spring-based application required a lot of manual configuration. It involved setting up a project with the required dependencies, configuring the web server, setting up the  database connection, and configuring the  Spring framework  itself.

Developers had to spend a significant amount of time and effort in configuring the application, which often led to configuration errors and inconsistencies.  Spring Boot  aims to simplify this process by providing a set of  opinionated defaults  and auto-configuration features.

## Setting up  New Spring  Boot Project with Spring Initializr

Spring Initializr is a web-based tool that allows developers to quickly generate a new  Spring Boot project  with the required dependencies and configurations. It provides a simple user interface to configure the project, select the required dependencies, and download the project as a zip file.

Here's an example of how to create a new Spring Boot project using  Spring Initializr:

1.  Go to  [https://start.spring.io/](https://start.spring.io/)
2.  Select the required  project metadata  such as Group, Artifact and dependencies
3.  Click "Generate" button and download the  project zip file
4.  Extract the  zip file  to a new directory in your local machine

## Build a Hello World API with Spring Boot

Now that we have set up a new Spring Boot project, let's build a simple  Hello World API  using Spring Boot.

Here's an example of how to build a simple Hello World API with Spring Boot:

1.  Create a new Spring Boot project using Spring Initializr
2.  Open  `src/main/java/com/example/demo/DemoApplication.java`
3.  Add a  `@RestController`  annotation to the class to indicate that it is a REST controller
4.  Add a  `@GetMapping`  annotation to a method in the class to handle  GET requests
5.  Return a simple string from the method
6.  Run the application using  `./mvnw spring-boot:run`  command
7.  Open a  web browser  and navigate to  `http://localhost:8080`

```
@RestController
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }

    @GetMapping("/")
    public String hello() {
        return "Hello, World!";
    }
}

```

In this example, we have annotated the  `DemoApplication`  class with  `@RestController`  and  `@SpringBootApplication`. We have also added a  `@GetMapping`  annotation to the  `hello()`  method to handle GET requests.

When we run the application using  `./mvnw spring-boot:run`  command, Spring Boot starts an  embedded Tomcat server  and deploys our application to it. We can then open a web browser and navigate to  `http://localhost:8080`  to see the "Hello, World!" message returned by the API.

## Step 08 - Build Faster with Spring Boot DevTools

Spring Boot  DevTools is a set of tools that can help you develop Spring Boot applications more efficiently. It includes several features that can help you speed up your development process, such as  automatic restarts,  live reload, and improved  error reporting.

### Automatic restarts

One of the most useful features of  Spring Boot DevTools  is automatic restarts. This feature will automatically restart your application whenever you make changes to your code. This can save you a lot of time since you don't have to manually restart your application every time you make changes.

To use automatic restarts, you need to include the  `spring-boot-devtools`  dependency in your project:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>

```

Once you have included the dependency, you can start your application using the  `spring-boot:run`  command. Spring Boot DevTools will automatically detect changes to your code and restart your application.

### Live reload

In addition to automatic restarts, Spring Boot DevTools also includes a live reload feature. This feature will automatically reload your changes in the browser whenever you make changes to your code. This can save you even more time since you don't have to manually refresh your browser every time you make changes.

To use live reload, you need to include the  `spring-boot-devtools`  dependency and a  JavaScript library  in your project:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>

<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>webjars-locator</artifactId>
</dependency>

<dependency>
    <groupId>org.webjars</groupId>
    <artifactId>jquery</artifactId>
    <version>3.6.0</version>
</dependency>

```

Once you have included the dependencies, you can add the  JavaScript  library to your  HTML file:

```
<script src="/webjars/jquery/3.6.0/jquery.min.js"></script>
<script src="/webjars/spring-boot-devtools/2.6.0/devtools.js"></script>

```

With the JavaScript library in place, Spring Boot DevTools will automatically reload your changes in the browser whenever you make changes to your code.

### Improved error reporting

Finally, Spring Boot DevTools includes improved error reporting. When an error occurs in your application, Spring Boot DevTools will display a more detailed error page that includes information about the error, the  stack trace, and other useful information.

To use improved error reporting, you need to include the  `spring-boot-devtools`  dependency in your project:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-devtools</artifactId>
    <scope>runtime</scope>
</dependency>

```

Once you have included the dependency, Spring Boot DevTools will automatically display the improved error page whenever an error occurs in your application.

## Conclusion

Spring Boot DevTools can help you develop  Spring Boot applications  more efficiently by providing features such as automatic restarts, live reload, and improved error reporting. By including the  `spring-boot-devtools`  dependency in your project, you can take advantage of these features and speed up your development process.

# Step 09 - Get Production Ready with  Spring Boot  - 1 - Profiles

## What are Spring Profiles?

-   Spring Profiles  allow us to have different configurations for our application based on active profiles.
-   We can enable multiple profiles at once.
-   Profiles are enabled using:
    -   JVM system properties:  `-Dspring.profiles.active=dev`
    -   Environment variable:  `SPRING_PROFILES_ACTIVE=dev`
    -   As an IDE run configuration

## Applying Profiles

We can apply profiles in different ways:

### Annotating Components

```
@Component
@Profile("dev")
public class DevDatasourceConfig {
  
}

@Component
@Profile("prod") 
public class ProdDatasourceConfig {
  
}

```

### Annotating Configuration Classes

```
@Configuration
@Profile("dev")
public class DevConfig {
  
}

```

### Application Property Files

`application-dev.properties`  
`application-prod.properties`

Spring will load the correct property file based on the active profile.

### Bean Definition Profiles
```
<bean profile="dev">
 ... 
</bean>

```

## Using Profiles in our Application

We can define a  `DataSource`  bean for each profile:
```
@Configuration
public class DataSourceConfig {
  
  @Bean
  @Profile("dev")
  public DataSource devDataSource() {
    return new HikariDataSource(...);  
  }
  
  @Bean
  @Profile("prod")
  public DataSource prodDataSource() {
    return new BasicDataSource(...);    
  }
}

```

Then we activate the relevant profile when running our application.
# ConfigurationProperties in Java

In Java, the  `ConfigurationProperties`  annotation is used to map and bind external properties to fields in a class. This feature is commonly used in  Spring Boot  applications to externalize  configuration properties  and simplify the code.

The  `ConfigurationProperties`  annotation is used on a class to indicate that the properties defined in an  external configuration file  should be bound to the fields of the class. The fields in the class should have the same name as the properties defined in the  configuration file.

Here is an example of a class that uses  `ConfigurationProperties`  annotation to bind external properties:

```
@ConfigurationProperties(prefix = "example")
public class ExampleProperties {
    private String name;
    private int age;
    private List<String> hobbies;

    // getters and setters
}

```

In this example, the  `prefix`  attribute of the  `ConfigurationProperties`  annotation specifies the prefix of the properties that should be bound to the fields of the class. In this case, the prefix is "example".

Assuming the following properties are defined in the external configuration file:

```
example.name=John
example.age=30
example.hobbies=reading,traveling

```

The properties will be bound to the corresponding fields in the  `ExampleProperties`  class.

Here's another example that shows how you can use the  `@ConfigurationProperties`  annotation to bind properties to a nested class:

```
@ConfigurationProperties(prefix = "database")
public class DatabaseProperties {
    private String url;
    private String username;
    private String password;
    private Pool pool;

    // getters and setters

    public static class Pool {
        private int maxActive;
        private int maxIdle;

        // getters and setters
    }
}

```

If the following properties are defined in the external configuration file:

```
database.url=jdbc:mysql://localhost:3306/mydb
database.username=root
database.password=secret
database.pool.maxActive=10
database.pool.maxIdle=5

```

The properties will be bound to the corresponding fields in the  `DatabaseProperties`  class, including the  `Pool`  nested class.

Here's another example that shows how you can use the  `@ConfigurationProperties`  annotation with a list of objects:

```
@ConfigurationProperties(prefix = "employees")
public class EmployeeProperties {
    private List<Employee> employees;

    // getters and setters

    public static class Employee {
        private String name;
        private int age;

        // getters and setters
    }
}

```

If the following properties are defined in the external configuration file:

```
employees.employees[0].name=John
employees.employees[0].age=30
employees.employees[1].name=Jane
employees.employees[1].age=25

```

The properties will be bound to the corresponding fields in the  `EmployeeProperties`  class, including the list of  `Employee`  objects.

In summary, the  `ConfigurationProperties`  annotation is a powerful feature in Java that allows you to externalize configuration properties and bind them to fields in a class. This provides a simple and efficient way to manage configuration properties in an application.
# Step 11 - Get Production Ready with  Spring Boot  - 3 - Embedded Servers

In this step, we will look at embedded servers in Spring Boot and how they can be used to deploy our application.

## What is an Embedded Server?

An embedded server is a web server that is packaged with your application. Unlike traditional web servers, where applications are deployed onto the server, an embedded server deploys the application within itself. This makes it easier to deploy and manage your application, as you don't need to install and configure a separate web server.

Spring Boot comes with a number of embedded servers out of the box, including  Tomcat,  Jetty, and Undertow. These servers can be used to deploy your application, and can be configured programmatically or via configuration files.

## Configuring an Embedded Server

To configure an embedded server, you need to add the relevant dependency to your  `pom.xml`  file. For example, to use Tomcat, you would add the following dependency:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-tomcat</artifactId>
</dependency>

```

Similarly, to use Jetty, you would add the following dependency:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jetty</artifactId>
</dependency>

```

And to use  Undertow, you would add the following dependency:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-undertow</artifactId>
</dependency>

```

Once you have added the relevant dependency, you can configure the embedded server by setting properties in your  `application.properties`  file. For example, to configure Tomcat to listen on port 8080, you would add the following property:

```
server.port=8080

```

Similarly, to configure Jetty to use  HTTPS, you would add the following properties:

```
server.ssl.enabled=true
server.ssl.key-store-type=PKCS12
server.ssl.key-store=classpath:keystore.p12
server.ssl.key-store-password=password

```

## Running an Embedded Server

To run an embedded server, you simply need to run your Spring Boot application. If you have configured multiple embedded servers, Spring Boot will automatically choose the appropriate server based on the dependencies you have added.

For example, if you have added the  Tomcat dependency  to your  `pom.xml`  file and have configured the  `server.port`  property in your  `application.properties`  file, you can run your application using the following command:

```
mvn spring-boot:run

```

This will start your application using Tomcat, listening on the configured port.

## Conclusion

In this step, we looked at embedded servers in Spring Boot and how they can be used to deploy our application. We also saw how to configure and run an embedded server. By using an embedded server, we can simplify the deployment and management of our application, making it easier to get our application up and running quickly.

# Step 12 - Get Production Ready with  Spring Boot  - 4 - Actuator

In this step, we will look at  Spring Boot Actuator, a set of tools for monitoring and managing your Spring Boot application.

## What is Spring Boot Actuator?

Spring Boot Actuator is a set of tools for monitoring and managing your Spring Boot application. It provides a number of endpoints that can be used to gather information about your application, such as health, metrics, and environment information. Actuator also provides a number of tools for managing your application, such as shutting down the application and reloading the configuration.

Actuator is included in all  Spring Boot projects  by default, and can be easily configured using properties or  Java configuration.

## Enabling Actuator

To enable Actuator in your  Spring Boot application, you simply need to add the  `spring-boot-starter-actuator`  dependency to your  `pom.xml`  file:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>

```

Once you have added the dependency, Actuator will be enabled by default and will expose a number of endpoints.

## Actuator Endpoints

Actuator provides a number of endpoints that can be used to gather information about your application. Some of the most commonly used endpoints are listed below:

-   `/actuator/health`: Returns application  health information.
-   `/actuator/info`: Returns application information, such as the version number.
-   `/actuator/metrics`: Returns application metrics, such as  memory usage  and CPU usage.
-   `/actuator/env`: Returns environment information, such as system properties and environment variables.
-   `/actuator/loggers`: Returns and manages the logging configuration.
-   `/actuator/shutdown`: Shuts down the application.

These endpoints can be accessed using HTTP requests. For example, to access the  health endpoint, you can use the following URL:


```
http://localhost:8080/actuator/health

```

## Customizing Actuator

Actuator can be customized using properties or  Java  configuration. For example, to change the port that Actuator listens on, you can add the following property to your  `application.properties`  file:

```
management.server.port=8081

```

Similarly, to customize the health endpoint, you can create a new  `HealthIndicator`  and register it with Spring Boot. For example, the following code creates a new  `HealthIndicator`  that checks the status of a database:

```
@Component
public class DatabaseHealthIndicator implements HealthIndicator {

    @Override
    public Health health() {
        // Check the status of the database
        if (databaseIsUp()) {
            return Health.up().build();
        } else {
            return Health.down().build();
        }
    }
}

```

The  `DatabaseHealthIndicator`  can then be registered with Spring Boot using the  `@Component`  annotation.

## Conclusion

In this step, we looked at Spring Boot Actuator, a set of tools for monitoring and managing your Spring Boot application. We saw how to enable Actuator, how to use its endpoints to gather information about your application, and how to customize Actuator using properties or Java configuration. By using Actuator, we can more easily monitor and manage our application, making it easier to keep our application up and running smoothly.

# Step 13 - Understanding Spring Boot vs Spring vs Spring MVC

In this step, we will look at the differences between Spring Boot, Spring, and Spring MVC.

## Spring

Spring is a popular  Java framework  for building enterprise applications. It provides a wide range of features, including  dependency injection, aspect-oriented programming, and transaction management. Spring is modular, allowing you to use only the components you need in your application.

Spring is a powerful framework, but it can be complex to configure and manage. You need to configure a lot of different components to get your application up and running, which can be time-consuming and error-prone.

## Spring MVC

Spring MVC is a  web framework  built on top of Spring. It provides a model-view-controller architecture for building web applications.  Spring MVC  is highly configurable, allowing you to customize your application's behavior and appearance.

To use Spring MVC, you need to configure a number of components, such as controllers, views, and handlers. This can be time-consuming and complex, especially if you are new to the framework.

## Spring Boot

Spring Boot is a framework built on top of Spring that makes it easier to build and run Spring applications.  Spring Boot  provides a number of features that simplify the development process, including auto-configuration, embedded servers, and  starter dependencies.

Auto-configuration allows Spring Boot to automatically configure the components you need in your application, based on the dependencies you have added to your  `pom.xml`  file. This makes it much easier to get your application up and running quickly.

Embedded servers allow you to run your application without needing to install and configure a separate web server. Spring Boot supports a number of embedded servers out of the box, including  Tomcat,  Jetty, and  Undertow.

Starter dependencies provide a set of pre-configured dependencies that you can use in your application. For example, if you want to use  Spring Data JPA  in your application, you can simply add the  `spring-boot-starter-data-jpa`  dependency to your  `pom.xml`  file and Spring Boot will automatically configure the necessary components.

## Spring Boot vs Spring vs Spring MVC

Spring Boot, Spring, and Spring MVC are all related frameworks, but they serve different purposes.

Spring is a powerful framework for building  enterprise applications, but it can be complex to configure and manage. Spring MVC is a web framework built on top of Spring that provides a model-view-controller architecture for building web applications. Spring MVC is highly configurable, but can be time-consuming and complex to set up.

Spring Boot is a framework built on top of Spring that makes it easier to build and run Spring applications. It provides a number of features that simplify the development process, including auto-configuration, embedded servers, and starter dependencies. Spring Boot is ideal for developers who want to quickly build and run Spring applications without needing to spend a lot of time configuring and managing components.

## Conclusion

In this step, we looked at the differences between Spring Boot, Spring, and Spring MVC. We saw that Spring is a powerful framework for building enterprise applications, Spring MVC is a web framework built on top of Spring that provides a model-view-controller architecture for building  web applications, and Spring Boot is a framework built on top of Spring that makes it easier to build and run Spring applications. By understanding the differences between these frameworks, you can choose the one that best suits your needs and build better applications.

# 80. Step 01 - Setting up a project with JDBC, JPA, H2 and Web Dependencies

In this step, we will set up a new  Spring Boot project  with the necessary dependencies for working with JDBC, JPA, H2, and web applications.

## Dependencies

To work with JDBC and JPA, we will need to add the following dependencies to our  `pom.xml`  file:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-jdbc</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-data-jpa</artifactId>
</dependency>

```

We will also add the  H2 database dependency, which we will use for testing our application:

```
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>test</scope>
</dependency>

```

Finally, we will add the  web dependency, which we will use to expose our data through a  RESTful API:

```
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
</dependency>

```

## Configuration

We will configure our  data source  in our  `application.properties`  file:


```
spring.datasource.url=jdbc:h2:mem:testdb
spring.datasource.driver-class-name=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

```

We will also enable  JPA auditing  by adding the following property:

```
spring.jpa.hibernate.ddl-auto=create-drop

```

This will create our  database schema  automatically and drop it when the application is shut down.

## Testing

We will create a simple  `Employee`  entity to test our  database configuration:
```
@Entity
public class Employee {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String name;

    private String department;

    // getters and setters
}

```

We will then create a  `JpaRepository`  for accessing our  `Employee`  entity:

```
@Repository
public interface EmployeeRepository extends JpaRepository<Employee, Long> {
}

```

Finally, we will create a  RESTful controller  to expose our data:

```
@RestController
@RequestMapping("/employees")
public class EmployeeController {

    @Autowired
    private EmployeeRepository employeeRepository;

    @GetMapping
    public List<Employee> getEmployees() {
        return employeeRepository.findAll();
    }

}

```

## Conclusion

In this step, we set up a new Spring Boot project with the necessary dependencies for working with JDBC, JPA, H2, and  web applications. We also configured our data source and enabled JPA auditing, and created a simple RESTful controller to expose our data. In the next steps, we will look at working with JDBC and JPA in more detail.



# 82. Step 02 - Launching up H2 Console

In this step, we will launch the  H2 console  to interact with our database.

To launch the H2 console, we will first need to add the H2 console dependency to our  `pom.xml`  file:

```
<dependency>
    <groupId>com.h2database</groupId>
    <artifactId>h2</artifactId>
    <scope>runtime</scope>
</dependency>

```

We will then need to configure the H2 console in our  `application.properties`  file:

```
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console

```

Finally, we can launch the H2 console by navigating to  `http://localhost:8080/h2-console`  in a web browser.

# 83. Updates to Step 03 and Step 04

In Step 03, we will need to update the  H2 database URL  to  `jdbc:h2:mem:testdb;DB_CLOSE_DELAY=-1`.

In Step 04, we will need to update the  `Person`  entity to use  `@GeneratedValue(strategy = GenerationType.IDENTITY)`  instead of  `@GeneratedValue(strategy = GenerationType.AUTO)`.

# 84. Step 03 - Creating a  Database Table  in H2

In this step, we will create a database table in H2.

We will first create a  `Person`  entity:

```
@Entity
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String firstName;

    private String lastName;

    // getters and setters
}

```

We will then create a  `PersonRepository`:

```
@Repository
public interface PersonRepository extends JpaRepository<Person, Long> {
}

```

Finally, we will create a  SQL script  to create the  `person`  table:

```
CREATE TABLE person (
  id BIGINT AUTO_INCREMENT PRIMARY KEY,
  first_name VARCHAR(255) NOT NULL,
  last_name VARCHAR(255) NOT NULL
);

```

# 85. Step 04 - Populate data into Person Table

In this step, we will populate data into the  `person`  table.

We will first create a  `DataLoader`  component that will populate some data into the  `person`  table:

java

Copy

```
@Component
public class DataLoader implements CommandLineRunner {

    @Autowired
    private PersonRepository personRepository;

    @Override
    public void run(String... args) throws Exception {
        personRepository.save(new Person("John", "Doe"));
        personRepository.save(new Person("Jane", "Doe"));
    }
}

```

We will also update the  `Person`  entity to include a constructor:

```
@Entity
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String firstName;

    private String lastName;

    public Person() {}

    public Person(String firstName, String lastName) {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    // getters and setters
}

```

Finally, we can test our application by launching the H2 console and running a query to retrieve the data from the  `person`  table:

```
SELECT * FROM person;

```

## Conclusion

In this step, we created a database table in H2 and populated it with some data. We also updated the  `Person`  entity to include a constructor, and created a  `DataLoader`  component to populate the data. In the next steps, we will look at working with  JDBC  and  JPA  in more detail.

## Step 05: Implementing findAll Persons  Spring JDBC  Query Method

In this step, we will learn how to implement a Spring JDBC query method to retrieve all persons from the database.

We will first create a  `PersonRowMapper`  class to map the result set to a  `Person`  object:

```
public class PersonRowMapper implements RowMapper<Person> {

    @Override
    public Person mapRow(ResultSet rs, int rowNum) throws SQLException {
        Person person = new Person();
        person.setId(rs.getLong("id"));
        person.setFirstName(rs.getString("first_name"));
        person.setLastName(rs.getString("last_name"));
        return person;
    }
}

```

Next, we will create a  `PersonJdbcRepository`  class to implement the  query method:

```
@Repository
public class PersonJdbcRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public List<Person> findAll() {
        return jdbcTemplate.query("SELECT * FROM person", new PersonRowMapper());
    }
}

```

Finally, we can test the query method by injecting the  `PersonJdbcRepository`  into a service or controller and calling the  `findAll`  method:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonJdbcRepository personJdbcRepository;

    @GetMapping
    public List<Person> getAllPersons() {
        return personJdbcRepository.findAll();
    }
}

```

## Step 06: Executing the findAll Method Using CommandLineRunner

In this step, we will learn how to execute the  `findAll`  method using the  `CommandLineRunner`  interface.

We will first create a  `CommandLineAppStartupRunner`  class:

```
@Component
public class CommandLineAppStartupRunner implements CommandLineRunner {

    @Autowired
    private PersonJdbcRepository personJdbcRepository;

    @Override
    public void run(String... args) throws Exception {
        List<Person> persons = personJdbcRepository.findAll();
        for (Person person : persons) {
            System.out.println(person.getFirstName() + " " + person.getLastName());
        }
    }
}

```

We can then run the application and check the console output to ensure that the  `findAll`  method is properly executed.

```
@SpringBootApplication
public class DemoApplication {

    public static void main(String[] args) {
        SpringApplication.run(DemoApplication.class, args);
    }
}

```

## Conclusion

In this tutorial, we learned how to work with databases in  Spring Boot  using JDBC and JPA. We created a  database table  in H2 and populated it with some data, and we implemented a  Spring JDBC query method  to retrieve all persons from the database. We also learned how to execute the query method using the  `CommandLineRunner`  interface.

## Step 07: A Quick Review - JDBC vs Spring JDBC

In this step, we will do a quick review of JDBC and  Spring JDBC.

JDBC (Java Database Connectivity) is a Java  API  that provides a standard way to interact with relational databases. With JDBC, we can create  database connections, execute  SQL statements, and retrieve results from the database.

Spring JDBC is a part of the  Spring Framework  that provides a higher-level abstraction over JDBC. Spring JDBC provides a set of classes and methods to simplify database access, such as the  `JdbcTemplate`  class, which provides a convenient way to execute SQL statements and map the results to  Java objects.

One of the key benefits of Spring JDBC is its ability to handle exceptions and  boilerplate code, which can make database access much easier and more efficient.

## Step 08: Understanding Spring Boot Autoconfiguration

In this step, we will learn about  Spring Boot  Autoconfiguration.

Spring Boot Autoconfiguration is a feature of Spring Boot that automatically configures beans based on the dependencies present in the classpath.  Spring Boot Autoconfiguration  can help reduce boilerplate code and simplify configuration by automatically configuring common components and providing sensible defaults.

For example, if we include the  H2 database dependency  in our project, Spring Boot will automatically create an  H2 database connection  and configure it for us. We can also customize the configuration by providing our own properties in the  `application.properties`  file.

## Step 09: Implementing findById Spring JDBC Query Method

In this step, we will learn how to implement a  Spring JDBC query method  to retrieve a person by ID.

We will first update the  `PersonJdbcRepository`  class to include the  `findById`  method:

```
@Repository
public class PersonJdbcRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public List<Person> findAll() {
        return jdbcTemplate.query("SELECT * FROM person", new PersonRowMapper());
    }

    public Person findById(Long id) {
        return jdbcTemplate.queryForObject("SELECT * FROM person WHERE id=?", new Object[]{id}, new PersonRowMapper());
    }
}

```

Next, we can test the  `findById`  method by calling it from a service or controller:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonJdbcRepository personJdbcRepository;

    @GetMapping("/{id}")
    public Person getPersonById(@PathVariable Long id) {
        return personJdbcRepository.findById(id);
    }
}

```

## Step 10: Implementing deleteById Spring JDBC Update Method

In this step, we will learn how to implement a Spring JDBC update method to delete a person by ID.

We will update the  `PersonJdbcRepository`  class to include the  `deleteById`  method:

```
@Repository
public class PersonJdbcRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public void deleteById(Long id) {
        jdbcTemplate.update("DELETE FROM person WHERE id=?", id);
    }
}

```

We can then test the  `deleteById`  method by calling it from a service or controller:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonJdbcRepository personJdbcRepository;

    @DeleteMapping("/{id}")
    public void deletePersonById(@PathVariable Long id) {
        personJdbcRepository.deleteById(id);
    }
}

```

## Step 11: Implementing insert and update Spring JDBC Update Methods

In this step, we will learn how to implement Spring JDBC update methods to insert and update persons in the database.

We will update the  `PersonJdbcRepository`  class to include the  `save`  method:

```
@Repository
public class PersonJdbcRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public void save(Person person) {
        if (person.getId() == null) {
            // Insert
            jdbcTemplate.update("INSERT INTO person (first_name, last_name) VALUES (?, ?)",
                    person.getFirstName(), person.getLastName());
        } else {
            // Update
            jdbcTemplate.update("UPDATE person SET first_name=?, last_name=? WHERE id=?",
                    person.getFirstName(), person.getLastName(), person.getId());
        }
    }
}

```

We can then test the  `save`  method by calling it from a service or controller:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonJdbcRepository personJdbcRepository;

    @PostMapping
    public void addPerson(@RequestBody Person person) {
        personJdbcRepository.save(person);
    }

    @PutMapping("/{id}")
    public void updatePerson(@PathVariable Long id, @RequestBody Person person) {
        person.setId(id);
        personJdbcRepository.save(person);
    }
}

```

## Conclusion

In this tutorial, we learned how to work with databases in Spring Boot using JDBC and JPA. We reviewed the differences between JDBC and Spring JDBC, and we learned about Spring Boot Autoconfiguration. We also implemented  Spring JDBC query  and update methods to retrieve, delete, insert, and update persons in the database. By following these steps, we can create a robust and efficient database-driven application using Spring Boot.

## Step 12: Creating a Custom Spring  JDBC RowMapper

In this step, we will learn how to create a custom  `RowMapper`  in Spring JDBC.

A  `RowMapper`  is used to map the result set of a  SQL query  to a Java object. We can create a custom  `RowMapper`  to map the result set to a more complex object.

We will create a  `PersonWithAddressRowMapper`  class that extends the  `PersonRowMapper`  class and maps the result set to a  `PersonWithAddress`  object:

java

Copy

```
public class PersonWithAddressRowMapper extends PersonRowMapper {

    @Override
    public Person mapRow(ResultSet rs, int rowNum) throws SQLException {
        Person person = super.mapRow(rs, rowNum);
        Address address = new Address();
        address.setStreet(rs.getString("street"));
        address.setCity(rs.getString("city"));
        address.setState(rs.getString("state"));
        address.setZip(rs.getString("zip"));
        person.setAddress(address);
        return person;
    }
}

```

We can then update the  `PersonJdbcRepository`  class to use the  `PersonWithAddressRowMapper`:

java

Copy

```
@Repository
public class PersonJdbcRepository {

    @Autowired
    private JdbcTemplate jdbcTemplate;

    public List<Person> findAll() {
        return jdbcTemplate.query("SELECT * FROM person", new PersonRowMapper());
    }

    public Person findById(Long id) {
        return jdbcTemplate.queryForObject("SELECT * FROM person WHERE id=?", new Object[]{id}, new PersonRowMapper());
    }

    public void save(Person person) {
        // ...
    }

    public void deleteById(Long id) {
        // ...
    }

    public List<Person> findAllWithAddress() {
        return jdbcTemplate.query("SELECT p.*, a.street, a.city, a.state, a.zip FROM person p LEFT JOIN address a ON p.id = a.person_id", new PersonWithAddressRowMapper());
    }
}

```

We can then test the  `findAllWithAddress`  method by calling it from a service or controller.

## Step 13: Quick Introduction to JPA

In this step, we will learn about JPA (Java Persistence API), which is a  Java specification  for object-relational mapping (ORM).

JPA provides a set of interfaces and annotations that allow us to map Java objects to database entities. JPA is implemented by various  ORM frameworks, such as  Hibernate,  EclipseLink, and  OpenJPA.

JPA provides a higher-level abstraction over JDBC and allows us to work with objects instead of raw SQL statements.

## Step 14: Defining Person Entity

In this step, we will define a  `Person`  entity class  that will be mapped to a  database table  using JPA.

We will annotate the  `Person`  class with the  `@Entity`  annotation to indicate that it is a JPA entity. We will also annotate the  `id`  field with the  `@Id`  annotation to indicate that it is the primary key:

```
@Entity
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    private String firstName;

    private String lastName;

    // getters and setters
}

```

We can also annotate the  `firstName`  and  `lastName`  fields with the  `@Column`  annotation to specify the column names:

```
@Entity
public class Person {

    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;

    @Column(name = "first_name")
    private String firstName;

    @Column(name = "last_name")
    private String lastName;

    // getters and setters
}

```

## Step 15: Implementing findById  JPA Repository  Method

In this step, we will implement a  JPA repository method  to retrieve a person by ID.

We will create a  `PersonRepository`  interface that extends the  `JpaRepository`  interface provided by  Spring Data  JPA. We will then define a  `findById`  method in the  `PersonRepository`  interface:

```
@Repository
public interface PersonRepository extends JpaRepository<Person, Long> {

    Optional<Person> findById(Long id);
}

```

We can then inject the  `PersonRepository`  into a service or controller and call the  `findById`  method:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonRepository personRepository;

    @GetMapping("/{id}")
    public Person getPersonById(@PathVariable Long id) {
        return personRepository.findById(id).orElse(null);
    }
}

```

## Step 16: Implementing insert and update JPA Repository Methods

In this step, we will implement JPA repository methods to insert and update persons in the database.

We will update the  `PersonRepository`  interface to include the  `save`  method:

```
@Repository
public interface PersonRepository extends JpaRepository<Person, Long> {

    Optional<Person> findById(Long id);

    Person save(Person person);
}

```

We can then test the  `save`  method by calling it from a service or controller:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonRepository personRepository;

    @PostMapping
    public void addPerson(@RequestBody Person person) {
        personRepository.save(person);
    }

    @PutMapping("/{id}")
    public void updatePerson(@PathVariable Long id, @RequestBody Person person) {
        person.setId(id);
        personRepository.save(person);
    }
}

```

## Step 17: Implementing deleteById JPA Repository Method

In this step, we will implement a JPA repository method to delete a person by ID.

We will update the  `PersonRepository`  interface to include the  `deleteById`  method:

```
@Repository
public interface PersonRepository extends JpaRepository<Person, Long> {

    Optional<Person> findById(Long id);

    Person save(Person person);

    void deleteById(Long id);
}

```

We can then test the  `deleteById`  method by calling it from a service or controller:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonRepository personRepository;

    @DeleteMapping("/{id}")
    public void deletePersonById(@PathVariable Long id) {
        personRepository.deleteById(id);
    }
}

```

## Step 18: Implementing findAll using JPQL Named Query

In this step, we will implement a JPA repository method to retrieve all persons from the database using a JPQL (Java Persistence Query Language) named query.

We will create a named query in the  `Person`  entity class using the  `@NamedQuery`  annotation:

```
@Entity
@NamedQuery(name = "Person.findAll", query = "SELECT p FROM Person p")
public class Person {

    // ...
}

```

We will then update the  `PersonRepository`  interface to include the  `findAll`  method:

```
@Repository
public interface PersonRepository extends JpaRepository<Person, Long> {

    Optional<Person> findById(Long id);

    Person save(Person person);

    void deleteById(Long id);

    List<Person> findAll();
}

```

We can then test the  `findAll`  method by calling it from a service or controller:

```
@RestController
@RequestMapping("/persons")
public class PersonController {

    @Autowired
    private PersonRepository personRepository;

    @GetMapping
    public List<Person> getAllPersons() {
        return personRepository.findAll();
    }
}

```

## Step 19: Introduction to Spring Data JPA

In this step, we will introduce  Spring Data JPA, which is a higher-level abstraction over JPA.

Spring Data JPA provides a set of interfaces and classes that simplify JPA repository creation and provide additional features, such as  query methods  and pagination.

To use Spring Data JPA, we simply need to create an interface that extends one of the Spring Data JPA repository interfaces, such as  `JpaRepository`  or  `CrudRepository`.

## Step 20: Connecting to Other Databases

In this step, we will learn how to connect to other databases using Spring Boot.

Spring Boot  provides autoconfiguration for several popular databases, such as  MySQL,  PostgreSQL, and Oracle. We can simply include the  database driver dependency  and configure the connection properties in the  `application.properties`  file.

For example, to connect to a  MySQL database, we can add the following properties to the  `application.properties`  file:


```
spring.datasource.url=jdbc:mysql://localhost:3306/mydatabase
spring.datasource.username=root
spring.datasource.password=password
spring.datasource.driver-class-name=com.mysql.cj.jdbc.Driver

```

We can also configure multiple  data sources  by creating multiple  `DataSource`  beans and annotating them with  `@ConfigurationProperties`  and  `@Primary`  annotations.
