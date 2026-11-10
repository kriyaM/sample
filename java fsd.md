Java Full Stack Developer – Senior Interview Preparation Guide

7 years experienceAll topicsInterview Q&A

This guide is based on your uploaded Java FSD Questions.pdf. It covers the original questions, with answers, practical examples, and likely follow-up questions.

The answers are framed for a senior developer interview, particularly around explaining implementation decisions, trade-offs, troubleshooting and real project scenarios.

Guide structure

* Core Java and OOP
* Java 8, 17 and Stream API
* Collections and HashMap
* Multithreading and concurrency
* Spring Boot and Spring Framework
* Spring Data JPA and Hibernate
* Microservices architecture
* REST APIs and WebClient
* Kafka and RabbitMQ
* Application security
* Angular and TypeScript
* JavaScript, HTML and CSS
* SQL, PostgreSQL and MongoDB
* Design patterns
* Coding exercises and SQL problems
* Project architecture and scenario-based questions

Part 1 – Core Java and OOP

1. Why Java?

Interview question: Why do you use Java? What makes it suitable for enterprise applications?

Answer:

Java is a platform-independent, object-oriented programming language widely used for building scalable enterprise applications.

Key advantages:

* Platform independent through JVM.
* Strong object-oriented programming support.
* Automatic garbage collection.
* Multithreading and concurrency support.
* Rich ecosystem of frameworks such as Spring Boot and Hibernate.
* Strong security features.
* Good performance through JIT compilation.
* Large community and ecosystem.

Example from a project:

For a healthcare application, Java Spring Boot can be used to develop REST APIs for member management, rating and commission processing. Its mature ecosystem makes it suitable for transaction management, database integration and microservices.

Follow-up questions:

* Is Java completely platform independent?
* What is the difference between JDK, JRE and JVM?
* How does JVM execute Java code?
* Why is Java not considered purely object-oriented?
* What is JIT compilation?

2. Explain OOP concepts

Answer:

There are four major OOP principles.

1. Encapsulation

Wrapping data and methods into a single unit and controlling access through access modifiers.

public class Employee {
    private String name;
    private double salary;
    public String getName() {
        return name;
    }
    public void setName(String name) {
        this.name = name;
    }
}

The private fields cannot be accessed directly from outside the class.

2. Inheritance

One class acquires properties and behaviours from another class.

class Animal {
    void eat() {
        System.out.println("Eating");
    }
}
class Dog extends Animal {
    void bark() {
        System.out.println("Barking");
    }
}

3. Polymorphism

One interface or method can represent multiple implementations.

* Compile-time: method overloading.
* Runtime: method overriding.

4. Abstraction

Hiding implementation details and exposing only essential functionality.

interface Payment {
    void pay(double amount);
}
class CardPayment implements Payment {
    public void pay(double amount) {
        System.out.println("Card payment");
    }
}

Follow-up questions:

* Difference between abstraction and encapsulation?
* Can Java support multiple inheritance?
* Why do we prefer interfaces for loose coupling?
* Can constructors be overridden?
* Can static methods be overridden?

3. Abstract class vs Interface

Abstract class	Interface
Uses abstract class	Uses interface
Can have constructors	Cannot have constructors
Can have instance variables	Fields are implicitly public static final
Supports abstract and concrete methods	Supports abstract, default, static and private methods
A class can extend only one class	A class can implement multiple interfaces

Example:

interface Notification {
    void send();
}
abstract class BaseNotification {
    void log() {
        System.out.println("Logging notification");
    }
}
class EmailNotification extends BaseNotification
        implements Notification {
    public void send() {
        System.out.println("Sending email");
    }
}

Senior-level answer: I generally prefer interfaces when defining contracts between components. Abstract classes are useful when related classes need to share common state or implementation.

Follow-up questions:

* Can an interface have a default method?
* What happens if two interfaces have the same default method?
* Why were default methods introduced in Java 8?

4. Compile-time vs Runtime Polymorphism

Answer:

Compile-time polymorphism is achieved through method overloading. The compiler determines which method to call.

Runtime polymorphism is achieved through method overriding. The JVM determines the implementation based on the actual object.

class Calculator {
    int add(int a, int b) {
        return a + b;
    }
    int add(int a, int b, int c) {
        return a + b + c;
    }
}

Runtime example:

class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}
class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Bark");
    }
}
Animal animal = new Dog();
animal.sound(); // Bark

Follow-up questions:

* What is dynamic method dispatch?
* Can private methods be overridden?
* Can static methods be overridden?
* What is method hiding?

5. What is Dynamic Method Dispatch?

Dynamic method dispatch is the mechanism through which an overridden method is resolved at runtime based on the actual object.

class Payment {
    void process() {
        System.out.println("Generic payment");
    }
}
class UpiPayment extends Payment {
    @Override
    void process() {
        System.out.println("UPI payment");
    }
}
class CardPayment extends Payment {
    @Override
    void process() {
        System.out.println("Card payment");
    }
}
Payment payment = new UpiPayment();
payment.process();

Output:

UPI payment

Real-time example: A payment service can accept a common Payment interface while different implementations process card, UPI or bank payments.

Follow-up: How does runtime polymorphism support extensibility and loose coupling?

6. Why is String immutable in Java?

Answer:

String is immutable, meaning once a String object is created, its value cannot be modified.

Reasons:

* Security – useful for file paths, URLs and credentials.
* String pool optimization – multiple references can share the same object.
* Thread safety – immutable objects can be safely shared.
* HashCode caching – useful when String is used as a HashMap key.
* Predictable behaviour.

Example:

String str = "Java";
str.concat(" Developer");
System.out.println(str);

Output:

Java

The original object remains unchanged.

str = str.concat(" Developer");
System.out.println(str);

Output:

Java Developer

A new String object is created and the reference is reassigned.

Follow-up questions:

* String vs StringBuilder vs StringBuffer?
* What is the String constant pool?
* Why is String commonly used as a HashMap key?
* Can we make a custom immutable class?

7. What are Generics in Java?

Generics allow classes, interfaces and methods to work with different data types while maintaining compile-time type safety.

List<String> names = new ArrayList<>();
names.add("John");
names.add("Alice");
// names.add(100); // Compilation error

Without generics, we may need explicit type casting and can encounter runtime ClassCastException.

Why use a specific generic list instead of a normal list?

Because List<String> guarantees that only String values can be added.

Follow-up questions:

* What are bounded type parameters?
* What is ? extends T?
* What is ? super T?
* What is type erasure?

8. Why use List instead of Array?

Array	List
Fixed size	Dynamic size
Can store primitives and objects	Stores objects; primitives use wrappers
Limited built-in operations	Provides collection methods
Supports direct indexing	Supports indexing through List implementations

List<String> names = new ArrayList<>();
names.add("John");
names.add("Alice");
names.remove("John");

Follow-up: When would you prefer an array over an ArrayList?

When the size is fixed, primitive storage is important, or low-level performance and memory control are required.

9. What are Static and Default methods?

Static method:

Belongs to the class rather than an object.

class Employee {
    static String company() {
        return "ABC";
    }
}
System.out.println(Employee.company());

Default method:

A method with an implementation inside an interface.

interface Vehicle {
    default void start() {
        System.out.println("Vehicle started");
    }
}

Default methods were introduced in Java 8 to allow interfaces to evolve without forcing all existing implementations to implement new methods.

Follow-up questions:

* Can static methods be overridden?
* Can interfaces contain static methods?
* Can an implementing class override a default method?

10. What is Closure?

Your PDF lists Closure under the initial JavaScript-related questions.

A closure is a JavaScript function that remembers variables from its outer lexical scope even after the outer function has completed execution.

function counter() {
    let count = 0;
    return function() {
        count++;
        return count;
    };
}
const increment = counter();
console.log(increment()); // 1
console.log(increment()); // 2

Follow-up: What are practical uses of closures?

Data privacy, function factories, callbacks and maintaining state.

Part 2 – Java 8, Java 17 and Stream API

11. What are the important Java 8 features?

Answer:

The major Java 8 features are:

* Lambda expressions.
* Functional interfaces.
* Stream API.
* Default and static interface methods.
* Optional class.
* Method references.
* New Date and Time API.
* CompletableFuture improvements.

Example – Lambda:

List<String> names = Arrays.asList("John", "Alice");
names.forEach(name -> System.out.println(name));

Without lambda, we would traditionally use an anonymous inner class.

Follow-up questions:

* What is a functional interface?
* What is a method reference?
* Difference between map and flatMap?
* What is lazy evaluation in Streams?
* Can we reuse a Stream?

12. What are the new features in Java 17?

Java 17 is an LTS release.

Important features:

Feature	Description
Records	Simplifies immutable data carrier classes
Sealed classes	Controls which classes can extend a class
Pattern matching for instanceof	Avoids explicit casting
Text blocks	Supports multiline strings
Switch expressions	Returns values from switch
Helpful NullPointerExceptions	Better NPE diagnostics
Strong encapsulation	Improves JDK internal API security

Example – Record:

public record Employee(
    Long id,
    String name,
    double salary
) {}

Java automatically provides constructor, accessors, equals, hashCode and toString.

Example – Pattern matching:

Object obj = "Java";
if (obj instanceof String str) {
    System.out.println(str.toUpperCase());
}

Follow-up questions:

* Record vs normal POJO?
* Can a record extend another class?
* What is a sealed class?
* Difference between Java 8 and Java 17?
* Which Java 17 features have you used in your project?

13. What is a Functional Interface?

An interface containing exactly one abstract method is called a functional interface.

It can have multiple default and static methods.

@FunctionalInterface
interface Calculator {
    int add(int a, int b);
}

Implementation:

Calculator calculator = (a, b) -> a + b;
System.out.println(calculator.add(10, 20));

Output: 30

Common built-in functional interfaces:

Interface	Method	Purpose
Predicate	test()	Returns boolean
Function	apply()	Transforms input
Consumer	accept()	Consumes input
Supplier	get()	Supplies a value
BiFunction	apply()	Accepts two inputs

Follow-up: Difference between Predicate and Function?

14. What is Stream API?

Stream API processes collections in a declarative way.

It supports filtering, mapping, sorting, grouping and aggregation.

Example:

List<Integer> numbers =
    Arrays.asList(1, 2, 3, 4, 5, 6);
List<Integer> result = numbers.stream()
    .filter(n -> n % 2 == 0)
    .map(n -> n * n)
    .toList();
System.out.println(result);

Output:

[4, 16, 36]

Follow-up questions:

* Intermediate vs terminal operations?
* What is lazy evaluation?
* Can a Stream be reused?
* What is the difference between findFirst() and findAny()?
* When should parallel streams be avoided?

15. Difference between Stream and Parallel Stream

Stream	Parallel Stream
Sequential execution	Processes elements in parallel
Usually one processing thread	Uses ForkJoinPool common pool by default
Predictable execution order	Processing order may differ
Suitable for most workloads	Useful for suitable CPU-intensive workloads

Example:

numbers.stream()
    .filter(n -> n > 10)
    .forEach(System.out::println);

Parallel:

numbers.parallelStream()
    .filter(n -> n > 10)
    .forEach(System.out::println);

Senior-level answer: I would not automatically replace sequential streams with parallel streams. I would consider dataset size, task complexity, shared mutable state, thread safety and benchmarking results.

16. What are Collectors in Java?

Collectors are used to accumulate Stream elements into collections or aggregated results.

Example – Group employees by department:

Map<String, List<Employee>> result =
    employees.stream()
        .collect(Collectors.groupingBy(
            Employee::getDepartment
        ));

Example – Count employees by department:

Map<String, Long> result =
    employees.stream()
        .collect(Collectors.groupingBy(
            Employee::getDepartment,
            Collectors.counting()
        ));

Other commonly used collectors:

* toList()
* toSet()
* joining()
* counting()
* groupingBy()
* partitioningBy()
* mapping()
* summarizingDouble()
* maxBy()
* averagingDouble()

Follow-up: Difference between groupingBy() and partitioningBy()?

17. What is Optional in Java 8?

Optional is a container object that may or may not contain a non-null value. It helps express potentially missing results and reduce accidental null handling.

Optional<Employee> employee =
    employeeRepository.findById(101L);
employee.ifPresent(e ->
    System.out.println(e.getName())
);

Common methods:

* of()
* ofNullable()
* empty()
* orElse()
* orElseGet()
* orElseThrow()
* map()
* flatMap()

Follow-up: Difference between orElse() and orElseGet()?

orElse() evaluates its argument eagerly, whereas orElseGet() evaluates the supplier only when the Optional is empty.

18. Difference between map() and flatMap()

map() transforms a value into another value.

flatMap() transforms and flattens nested structures.

Optional<String> name =
    Optional.of("John");
Optional<Integer> length =
    name.map(String::length);

With flatMap:

Optional<String> result =
    name.flatMap(n -> Optional.of(n.toUpperCase()));

For Streams:

List<List<String>> names = List.of(
    List.of("John", "Alice"),
    List.of("Bob", "Jane")
);
List<String> result = names.stream()
    .flatMap(List::stream)
    .toList();

Follow-up: When would you use flatMap in a Spring Boot service?

When transforming nested Optional or collection results, or when a method already returns a Stream or Optional.

Part 3 – Collections and HashMap

19. What is a Collection?

Collection is the root interface of the Java Collections Framework. It represents a group of objects.

Major interfaces:

* List
* Set
* Queue

Map is part of the Collections Framework but does not extend Collection.

20. What is a Map?

A Map stores key-value pairs. Keys are unique, while values can be duplicated.

Map<Integer, String> employees =
    new HashMap<>();
employees.put(101, "John");
employees.put(102, "Alice");
employees.put(103, "John");

Follow-up questions:

* Can Map contain null keys?
* How does HashMap handle duplicate keys?
* Difference between HashMap and TreeMap?
* Difference between HashMap and ConcurrentHashMap?

21. How does HashMap work internally?

This is one of the most important senior Java interview questions.

Answer:

HashMap uses an array of buckets. Each bucket can contain a node, and collisions are handled using a linked list or, under certain conditions, a balanced tree.

When inserting a key-value pair:

* Calls hashCode() on the key.
* Spreads the hash.
* Calculates the bucket index.
* Checks whether the bucket is empty.
* If occupied, checks key equality using equals().
* Updates the value if the key already exists.
* Otherwise adds a new entry.

Java 8 introduced treeification for heavily populated buckets, subject to capacity and threshold conditions.

Important default values:

* Initial capacity: 16.
* Load factor: 0.75.
* Resize threshold: capacity × load factor.

Follow-up questions:

* What happens when two objects have the same hash code?
* Why must equals() and hashCode() be overridden together?
* What is a collision?
* What is the time complexity of get() and put()?
* Can we use a mutable object as a key?

22. HashMap vs ConcurrentHashMap

HashMap	ConcurrentHashMap
Not thread-safe	Thread-safe
Allows one null key	Does not allow null keys
Multiple threads can cause unsafe concurrent modification	Designed for concurrent access
No concurrency guarantees	Supports concurrent reads and updates

Example:

Map<String, Integer> map =
    new ConcurrentHashMap<>();
map.put("Java", 10);
map.put("Spring", 20);

Follow-up: How does ConcurrentHashMap achieve thread safety?

In modern Java, it uses CAS operations and fine-grained synchronization for updates rather than locking the entire map for every operation.

23. ArrayList vs LinkedList

ArrayList	LinkedList
Dynamic array	Doubly linked list
Fast random access	Slow random access
Insertions in middle require shifting	Insertion after locating node is inexpensive
Better cache locality	More memory overhead
Usually preferred for general-purpose lists	Useful for specific deque operations

Senior-level answer: I generally prefer ArrayList unless there is a specific requirement for LinkedList or Deque behaviour. LinkedList is not automatically faster for insertions because locating the insertion position can itself take O(n).

24. HashSet vs LinkedHashSet

HashSet	LinkedHashSet
No guaranteed iteration order	Maintains insertion order
Hash table implementation	Hash table with linked ordering
Generally lower memory overhead	Additional ordering overhead

Set<String> names = new LinkedHashSet<>();
names.add("John");
names.add("Alice");
names.add("Bob");

Iteration preserves the insertion order.

Follow-up: How does HashSet ensure uniqueness?

It uses hashCode() to locate a bucket and equals() to check whether an equivalent element exists.

Part 4 – Multithreading and Concurrency

25. What is Multithreading?

Multithreading allows multiple threads to execute concurrently within a process.

Advantages:

* Better resource utilization.
* Improved responsiveness.
* Parallel execution for suitable workloads.
* Efficient handling of concurrent tasks.

Example:

Thread thread = new Thread(() ->
    System.out.println("Running thread")
);
thread.start();

Follow-up: Difference between start() and run()?

start() creates a new thread of execution. Calling run() directly executes the method on the current thread.

26. What is ExecutorService?

ExecutorService manages thread execution through a thread pool.

Instead of creating a new thread for every task, we submit tasks to an executor.

ExecutorService executor =
    Executors.newFixedThreadPool(5);
executor.submit(() ->
    System.out.println("Task executed")
);
executor.shutdown();

Follow-up questions:

* What is a thread pool?
* Difference between submit() and execute()?
* What happens if the thread pool is exhausted?
* How do you configure a production thread pool?

Senior-level answer: For production workloads, I would prefer a configured ThreadPoolExecutor with a bounded queue, appropriate rejection policy and monitoring rather than blindly using an unbounded executor.

27. What is CompletableFuture?

CompletableFuture supports asynchronous and non-blocking composition of tasks.

CompletableFuture<String> future =
    CompletableFuture.supplyAsync(() -> "Java");
future.thenApply(String::toUpperCase)
      .thenAccept(System.out::println);

Output:

JAVA

Important methods:

Method	Purpose
supplyAsync()	Runs a task returning a value
runAsync()	Runs a task without a return value
thenApply()	Transforms result
thenAccept()	Consumes result
thenCompose()	Chains dependent asynchronous tasks
thenCombine()	Combines independent results
exceptionally()	Handles failure
handle()	Handles success or failure

Follow-up: Difference between thenApply and thenCompose?

thenApply() transforms a result, while thenCompose() chains another asynchronous operation and avoids nested CompletableFuture objects.

28. What is synchronized?

synchronized ensures mutual exclusion and memory visibility for code protected by the same monitor lock.

class Counter {
    private int count;
    public synchronized void increment() {
        count++;
    }
}

Only one thread at a time can execute a synchronized instance method on the same object monitor.

Follow-up: Difference between synchronized method and synchronized block?

A synchronized block allows locking only the critical section, giving more control over lock scope.

29. What is volatile?

volatile ensures visibility of updates to a variable across threads and establishes ordering guarantees around volatile reads and writes.

class Worker {
    private volatile boolean running = true;
    void stop() {
        running = false;
    }
}

A thread checking running can observe the updated value.

Important: Volatile does not make compound operations such as count++ atomic.

Follow-up: Volatile vs synchronized vs AtomicInteger?

30. What is wait()?

wait() is an Object class method used for inter-thread communication.

It releases the object’s monitor and waits until notified or interrupted.

synchronized (lock) {
    while (!condition) {
        lock.wait();
    }
    // Continue after condition is met
}

notify() wakes one waiting thread, while notifyAll() wakes all threads waiting on that object’s monitor.

Follow-up: Why should wait() be called inside a synchronized block?

Because the thread must own the object’s monitor before calling wait().

31. What is Thread.yield()?

yield() is a static method that hints to the thread scheduler that the current thread is willing to allow another thread to execute.

It is only a hint, not a guarantee.

Follow-up: Difference between yield(), sleep() and wait()?

* yield() – scheduling hint.
* sleep() – pauses execution for a specified time without releasing the monitor.
* wait() – waits for notification and releases the monitor.

32. How do you resolve Deadlock?

Deadlock occurs when two or more threads wait indefinitely for locks held by each other.

Example:

* Thread 1 holds Lock A and waits for Lock B.
* Thread 2 holds Lock B and waits for Lock A.

Prevention:

* Maintain consistent lock ordering.
* Avoid nested locks where possible.
* Use tryLock() with timeouts.
* Keep synchronized blocks small.
* Avoid unnecessary shared mutable state.

Follow-up: How do you identify a deadlock in production?

Capture a thread dump using jstack, inspect blocked threads and identify the lock ownership cycle.

Part 5 – Spring Boot and Spring Framework

33. What is Spring Boot? What dependencies do you commonly use?

Spring Boot simplifies Spring application development through auto-configuration, starter dependencies and embedded servers.

Common dependencies:

Dependency	Purpose
spring-boot-starter-web	REST APIs and Spring MVC
spring-boot-starter-data-jpa	Database persistence
spring-boot-starter-validation	Request validation
spring-boot-starter-security	Authentication and authorization
spring-boot-starter-actuator	Monitoring
spring-boot-starter-test	Unit and integration testing
spring-kafka	Kafka integration
PostgreSQL driver	PostgreSQL connectivity

Follow-up questions:

* What is auto-configuration?
* What is the difference between Spring and Spring Boot?
* How does an embedded Tomcat server work?
* How does Spring Boot determine which beans to create?

34. What annotations execute when Spring Boot starts?

The main application class generally contains:

@SpringBootApplication
public class Application {
    public static void main(String[] args) {
        SpringApplication.run(Application.class, args);
    }
}

@SpringBootApplication combines:

* @SpringBootConfiguration
* @EnableAutoConfiguration
* @ComponentScan

During startup, Spring Boot:

* Creates the application context.
* Performs component scanning.
* Processes configuration classes.
* Applies auto-configuration.
* Creates and initializes beans.
* Starts the embedded web server for a web application.

Follow-up: How can you execute logic after application startup?

Use ApplicationRunner, CommandLineRunner or an application-ready event listener.

35. Explain Spring MVC and how you implement it in your project.

Spring MVC follows the Model-View-Controller pattern.

For REST applications, the typical flow is:

Angular / REST Client

DispatcherServlet

Controller

Service layer – Business logic

Repository / JPA

Database

Example:

@RestController
@RequestMapping("/employees")
public class EmployeeController {
    private final EmployeeService service;
    public EmployeeController(EmployeeService service) {
        this.service = service;
    }
    @GetMapping("/{id}")
    public Employee getEmployee(@PathVariable Long id) {
        return service.getEmployee(id);
    }
}

Service:

@Service
public class EmployeeService {
    private final EmployeeRepository repository;
    public EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }
    public Employee getEmployee(Long id) {
        return repository.findById(id)
            .orElseThrow(() ->
                new RuntimeException("Employee not found"));
    }
}

Senior-level answer: In my project, I keep controllers responsible for request and response handling, services for business logic and repositories for persistence. This improves maintainability, testability and separation of concerns.

Follow-up questions:

* What is DispatcherServlet?
* What is the difference between @Controller and @RestController?
* How does request mapping work?
* How do you handle exceptions globally?

36. What is Model-View-Controller?

MVC separates application responsibilities:

* Model – data and business state.
* View – presentation.
* Controller – handles requests and coordinates processing.

In a REST-based Spring Boot application, JSON responses are often returned instead of server-rendered views.

37. What is IoC and Dependency Injection?

Inversion of Control (IoC) means the Spring container manages object creation and dependencies rather than application classes creating all their dependencies themselves.

Dependency Injection (DI) is the mechanism used to provide those dependencies.

Example:

@Service
class PaymentService {
    private final PaymentRepository repository;
    PaymentService(PaymentRepository repository) {
        this.repository = repository;
    }
}

Spring injects the repository into the service.

Why constructor injection?

* Makes dependencies explicit.
* Supports immutability.
* Simplifies unit testing.
* Avoids partially initialized objects.
* Helps identify circular dependencies.

Follow-up: Difference between @Autowired, @Qualifier and @Resource?

38. Explain @Autowired, @Qualifier and @Resource.

@Autowired: Injects a dependency by type by default.

@Qualifier: Selects a specific bean when multiple beans of the same type exist.

@Resource: Uses name-based resolution by default, with fallback resolution rules.

Example:

public interface NotificationService {
    void send();
}
@Service("emailService")
class EmailService implements NotificationService {
    public void send() {}
}
@Service("smsService")
class SmsService implements NotificationService {
    public void send() {}
}

Injection:

@Service
class NotificationManager {
    private final NotificationService service;
    NotificationManager(
        @Qualifier("emailService")
        NotificationService service) {
        this.service = service;
    }
}

Follow-up: What happens if two beans of the same type are available without a qualifier?

39. Explain Singleton and Prototype bean scopes.

Singleton: One bean instance per Spring IoC container for that bean definition.

Prototype: A new instance is created whenever the container is asked for that bean.

Example:

@Component
@Scope("singleton")
class EmployeeService {
}
@Component
@Scope("prototype")
class EmployeeRequest {
}

Real-time examples:

* Singleton: Stateless service or repository.
* Prototype: Stateful object requiring a separate instance for each lookup.

Important senior-level point: A prototype bean injected directly into a singleton bean is resolved only during singleton creation. It does not automatically produce a new instance on every method call.

Follow-up: How would you obtain a fresh prototype instance each time?

Use ObjectProvider, a provider abstraction or an appropriate scoped proxy.

40. Explain @PostConstruct and @PreDestroy.

@PostConstruct executes after dependency injection and bean initialization.

@PreDestroy executes before the bean is destroyed.

@Component
class ApplicationCache {
    @PostConstruct
    public void initialize() {
        System.out.println("Loading initial data");
    }
    @PreDestroy
    public void cleanup() {
        System.out.println("Releasing resources");
    }
}

Follow-up: Does @PreDestroy work with prototype-scoped beans?

Spring does not manage the complete destruction lifecycle of prototype instances after handing them to the client.

41. What is @Configuration?

@Configuration identifies a class that declares bean definitions.

@Configuration
public class AppConfig {
    @Bean
    public RestTemplate restTemplate() {
        return new RestTemplate();
    }
}

@Bean registers the returned object in the Spring application context.

Follow-up: Difference between @Component and @Bean?

@Component marks a class for component scanning, while @Bean explicitly declares a bean through a configuration method.

42. Explain @EnableAutoConfiguration.

It enables Spring Boot’s auto-configuration mechanism.

Spring Boot examines:

* Classpath dependencies.
* Existing beans.
* Configuration properties.
* Conditional annotations.

It configures appropriate beans when the conditions are satisfied.

For example, adding Spring Web dependencies can trigger web application auto-configuration.

Follow-up: What is @ConditionalOnClass? What is @ConditionalOnMissingBean?

43. How do you improve Spring Boot startup performance?

Answer:

I would first measure startup time and identify which phases consume time.

Potential improvements:

* Remove unnecessary dependencies.
* Reduce unnecessary component scanning.
* Avoid unnecessary bean initialization.
* Use lazy initialization where appropriate.
* Optimize database connection initialization.
* Avoid expensive operations in constructors and @PostConstruct.
* Review auto-configuration.
* Use startup metrics and application startup logging.

Spring Boot supports ApplicationStartup instrumentation and startup endpoint/diagnostic approaches.

Follow-up: What are the disadvantages of lazy initialization?

The first request that triggers a lazy bean can experience additional latency, and configuration errors may surface later.

44. How do you pick up the latest configuration changes?

Common approaches:

* Restart the application after configuration changes.
* Use Spring Cloud Config Server.
* Use Actuator refresh mechanisms with supported Spring Cloud components.
* Use configuration refresh events and refresh-scoped beans where appropriate.

Example:

@RefreshScope
@RestController
class ConfigController {
    @Value("${message}")
    private String message;
    @GetMapping("/message")
    public String getMessage() {
        return message;
    }
}

Follow-up: Does changing application.properties automatically update existing beans?

Not necessarily. Configuration binding and bean refresh depend on the configuration mechanism.

45. How do you handle CORS and CSRF attacks in Spring Boot?

CORS controls which browser origins are allowed to access resources.

Example:

@Configuration
public class CorsConfig {
    @Bean
    WebMvcConfigurer corsConfigurer() {
        return new WebMvcConfigurer() {
            @Override
            public void addCorsMappings(
                CorsRegistry registry) {
                registry.addMapping("/api/**")
                    .allowedOrigins("https://example.com")
                    .allowedMethods("GET", "POST", "PUT");
            }
        };
    }
}

CSRF protects against unauthorized requests made using a victim’s authenticated browser session.

Protection options:

* CSRF tokens.
* SameSite cookie settings.
* Secure session management.
* Appropriate Spring Security configuration.

For stateless bearer-token APIs that do not use automatically attached browser credentials, the CSRF risk profile differs. Do not disable CSRF without evaluating the authentication mechanism.

Follow-up questions:

* CORS vs CSRF?
* What is a preflight request?
* Why should wildcard origins be avoided with credentials?
* When is CSRF protection required?

46. What is Spring Boot Actuator?

Actuator provides application monitoring and management endpoints.

Common endpoints:

Endpoint	Purpose
/actuator/health	Application health
/actuator/info	Application information
/actuator/metrics	Application metrics
/actuator/env	Environment properties
/actuator/beans	Registered beans
/actuator/mappings	Request mappings

Senior-level answer: I would expose only necessary endpoints, secure sensitive endpoints and integrate health and metrics with monitoring systems.

Part 6 – Spring Data JPA and Hibernate

47. What is JPA?

JPA (Jakarta Persistence API) is a specification for object-relational mapping in Java.

Hibernate is a popular JPA implementation.

It allows us to map Java entities to database tables and perform persistence operations without writing every SQL statement manually.

48. Explain Entity, Repository and Service layers.

Entity:

@Entity
@Table(name = "employee")
public class Employee {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private Long id;
    private String name;
    private double salary;
}

Repository:

public interface EmployeeRepository
        extends JpaRepository<Employee, Long> {
}

Service:

@Service
public class EmployeeService {
    private final EmployeeRepository repository;
    public EmployeeService(EmployeeRepository repository) {
        this.repository = repository;
    }
    public Employee getById(Long id) {
        return repository.findById(id)
            .orElseThrow(() ->
                new EntityNotFoundException("Employee not found"));
    }
}

Follow-up: How does Spring Data JPA generate the repository implementation?

Spring Data creates a runtime proxy for the repository interface and provides implementations for inherited CRUD operations and derived query methods.

49. How does findById() work internally?

When we call:

repository.findById(101L);

The flow is:

* The repository proxy receives the call.
* Spring Data delegates to its repository implementation.
* The JPA EntityManager performs the lookup.
* Hibernate checks the persistence context (first-level cache).
* If the entity is not found there, it queries the database.
* Hibernate maps the result to an entity object.
* The result is returned as an Optional.

Follow-up questions:

* What is first-level cache?
* What is second-level cache?
* What is persistence context?
* Difference between find() and getReferenceById()?
* What is dirty checking?

50. Explain JPA relationships.

Relationship	Annotation	Example
One-to-One	@OneToOne	Employee and employee profile
One-to-Many	@OneToMany	Department and employees
Many-to-One	@ManyToOne	Employees belonging to a department
Many-to-Many	@ManyToMany	Students and courses

Example:

@Entity
class Department {
    @Id
    private Long id;
    @OneToMany(mappedBy = "department")
    private List<Employee> employees;
}
@Entity
class Employee {
    @Id
    private Long id;
    @ManyToOne
    @JoinColumn(name = "department_id")
    private Department department;
}

Follow-up questions:

* What is owning side and inverse side?
* What is mappedBy?
* Lazy vs eager fetching?
* Cascade types?
* What is orphanRemoval?
* How do you avoid infinite JSON recursion?

51. What is the N+1 query problem?

It occurs when one query fetches parent records and additional queries are executed for each parent to retrieve associated records.

For example:

* One query retrieves 100 departments.
* 100 additional queries retrieve employees for each department.

Possible solutions:

* JOIN FETCH.
* Entity graphs.
* DTO projections.
* Batch fetching.
* Appropriate fetch strategy.

Follow-up: Why not always use EAGER fetching?

It can cause unnecessary data retrieval, larger joins and performance problems.

52. How do you handle large database results?

Avoid loading the entire dataset into memory.

Options:

* Pagination.
* Batch processing.
* Projection queries.
* Streaming where supported and correctly managed.
* Keyset pagination for large, sequential datasets.

Example:

Pageable pageable =
    PageRequest.of(0, 100);
Page<Employee> employees =
    repository.findAll(pageable);

Follow-up: Offset pagination vs keyset pagination?

Keyset pagination is often more efficient for deep pagination because it uses the last-seen sort key rather than scanning large offsets.

53. What is @Transactional?

@Transactional defines a transaction boundary.

@Transactional
public void transferMoney(
        Long fromId,
        Long toId,
        BigDecimal amount) {
    debit(fromId, amount);
    credit(toId, amount);
}

If an applicable unchecked exception occurs, Spring normally rolls back the transaction.

By default, checked exceptions do not trigger rollback.

For checked exceptions:

@Transactional(rollbackFor = Exception.class)
public void process() throws Exception {
    // business operation
}

Follow-up questions:

* What is transaction propagation?
* What is isolation level?
* What is rollbackFor?
* What happens when an exception is caught inside a transactional method?
* Why does self-invocation affect @Transactional?
* What is the difference between REQUIRED and REQUIRES_NEW?

Part 7 – Microservices Architecture

54. What is Microservices Architecture?

Microservices architecture divides an application into smaller, independently deployable services.

Each service owns a specific business capability.

Example for a banking application:

* Customer Service.
* Account Service.
* Transaction Service.
* Payment Service.
* Notification Service.

Each service can be developed, deployed and scaled independently, subject to its dependencies.

Follow-up questions:

* Monolith vs microservices?
* Advantages and disadvantages?
* How do you decide service boundaries?
* What is bounded context?
* What is database per service?

55. How do you convert a monolithic application into microservices?

Answer:

I would use an incremental migration approach rather than rewriting the entire application at once.

Steps:

* Understand existing business functionality.
* Identify domain boundaries.
* Identify tightly coupled modules.
* Define independent service responsibilities.
* Extract one business capability at a time.
* Define API and messaging contracts.
* Separate data ownership.
* Introduce API Gateway and service discovery if needed.
* Add monitoring, security and resilience.
* Gradually route traffic to the new services.

This approach is commonly associated with the Strangler Fig pattern.

Follow-up: How would you handle transactions across services?

Use patterns such as Saga, transactional outbox and compensating transactions rather than relying on a single local database transaction.

56. How do you set up a microservice project from scratch?

A typical approach:

* Identify business domains.
* Create separate Spring Boot services.
* Configure independent databases or schemas with clear ownership.
* Implement REST APIs.
* Configure API Gateway.
* Configure service discovery if needed.
* Implement security using OAuth2/OIDC.
* Add messaging using Kafka or RabbitMQ.
* Implement centralized logging and monitoring.
* Set up CI/CD and container deployment.

Follow-up: Which components are mandatory and which are optional?

Not every microservices architecture needs a service registry, separate message broker or centralized configuration server. These depend on the deployment environment and requirements.

57. What is API Gateway?

API Gateway provides a single entry point for clients accessing multiple backend services.

Responsibilities:

* Routing.
* Authentication and authorization integration.
* Rate limiting.
* Request filtering.
* Logging and tracing.
* Cross-cutting policies.

Example:

Angular
   |
API Gateway
   |
   |---- Customer Service
   |
   |---- Account Service
   |
   |---- Transaction Service

Follow-up: API Gateway vs Service Registry?

API Gateway handles incoming requests and routing policies. A service registry maintains information about service instances and their locations.

58. How do microservices communicate?

Two main approaches:

Synchronous communication:

* REST APIs.
* WebClient.
* gRPC.

Asynchronous communication:

* Kafka.
* RabbitMQ.
* Event-driven messaging.

Example:

Order Service
      |
      | Publish OrderCreated
      v
    Kafka
      |
      +---- Inventory Service
      |
      +---- Notification Service

Follow-up: When would you choose asynchronous communication?

When services should be loosely coupled, processing can happen later, or the system needs buffering and independent consumer processing.

59. How do you handle errors when communicating with multiple microservices?

Use:

* Connection and response timeouts.
* Retry with exponential backoff.
* Circuit breaker.
* Fallback where business-appropriate.
* Bulkhead isolation.
* Idempotency.
* Distributed tracing.
* Dead-letter queues for failed messages.

Example:

Suppose Payment Service calls Customer Service.

If Customer Service is unavailable:

* Apply a timeout.
* Retry transient failures within a controlled limit.
* Open the circuit if failures continue.
* Return a meaningful response or apply a valid fallback.
* Log correlation IDs and trace the failure.

Follow-up: What is the difference between retry and circuit breaker?

Retry attempts an operation again. Circuit breaker temporarily prevents calls to a failing dependency to avoid cascading failures.

60. How do you improve application performance?

A senior developer should discuss multiple layers.

Layer	Optimizations
Java	Reduce unnecessary object creation, optimize algorithms
Database	Indexing, query optimization, pagination
Spring Boot	Efficient bean lifecycle and connection pool configuration
API	Pagination, compression, smaller payloads
Caching	Redis or local caching where appropriate
Microservices	Reduce unnecessary synchronous calls
Infrastructure	Horizontal scaling and resource tuning
Monitoring	Profiling, metrics and distributed tracing

Follow-up: How would you identify the bottleneck before optimizing?

Use logs, metrics, traces, JVM profiling and database query analysis rather than guessing.

61. What are different caching techniques? Why do we need caching?

Caching stores frequently accessed data for faster retrieval.

Types:

* Local in-memory caching.
* Distributed caching – Redis.
* Database caching.
* HTTP caching.
* CDN caching.

Use cases:

* Frequently accessed reference data.
* Product or customer metadata.
* Expensive calculations.
* Read-heavy workloads.

Avoid or carefully manage caching for:

* Highly volatile data.
* Sensitive data without appropriate controls.
* Data requiring strong freshness guarantees.
* Low-reuse data where cache overhead exceeds the benefit.

Follow-up questions:

* Cache-aside vs write-through?
* What is cache invalidation?
* What is cache stampede?
* How do you maintain consistency?
* What is TTL?

Part 8 – REST API and HTTP

62. What is REST?

REST is an architectural style for designing network-based applications around resources.

Example:

GET    /employees
GET    /employees/101
POST   /employees
PUT    /employees/101
PATCH  /employees/101
DELETE /employees/101

63. Explain GET, POST, PUT, DELETE and PATCH.

Method	Purpose	Idempotent?
GET	Retrieve resource	Yes
POST	Create/process resource	Not generally
PUT	Replace resource	Yes
PATCH	Partially update resource	Depends on operation
DELETE	Delete resource	Yes, by HTTP semantics

Follow-up: Difference between PUT and PATCH?

PUT generally replaces the complete resource representation, whereas PATCH applies partial changes.

64. What are idempotent methods?

An operation is idempotent when making the same request multiple times has the same intended effect on the server state as making it once.

Examples:

* GET.
* PUT.
* DELETE.
* HEAD.
* OPTIONS.

POST is not inherently idempotent, but an API can implement idempotency using an idempotency key.

Follow-up: Why is idempotency important in payment processing?

It prevents duplicate transactions when clients retry requests after network failures.

65. Can DELETE be performed using GET mapping?

No. GET should be a safe retrieval operation and should not perform destructive actions.

Use:

@DeleteMapping("/{id}")
public void deleteEmployee(@PathVariable Long id) {
    service.deleteEmployee(id);
}

66. Can @RequestBody be used in GET mapping?

HTTP does not universally prohibit GET request bodies, but their semantics are undefined and many clients, proxies and servers do not handle them consistently.

For conventional Spring REST APIs, use query parameters and path variables for GET requests.

@GetMapping
public List<Employee> getEmployees(
    @RequestParam String department) {
    return service.findByDepartment(department);
}

For complex search criteria, consider POST with a search request body when appropriate.

67. WebClient vs RestTemplate

RestTemplate	WebClient
Synchronous, blocking	Supports non-blocking reactive calls
Traditional Spring HTTP client	Modern Spring HTTP client
Suitable for existing blocking applications	Useful for asynchronous and reactive workflows
Maintenance mode in modern Spring	Recommended for new reactive use cases

Example:

WebClient client = WebClient.create();
Mono<String> response = client.get()
    .uri("http://employee-service/employees/101")
    .retrieve()
    .bodyToMono(String.class);

Follow-up: Is WebClient always non-blocking?

Only if you maintain a non-blocking flow. Calling .block() makes the calling thread wait.

68. How do you implement API calls?

A typical Spring Boot API implementation involves:

* Define an endpoint in the controller.
* Validate the request.
* Delegate business logic to service.
* Access the database through the repository.
* Return a suitable response.
* Handle exceptions centrally.

@PostMapping
public ResponseEntity<Employee> create(
        @Valid @RequestBody Employee employee) {
    Employee saved = service.save(employee);
    return ResponseEntity
        .status(HttpStatus.CREATED)
        .body(saved);
}

Follow-up: How do you handle API versioning, validation and error responses?

Part 9 – Kafka and RabbitMQ

69. What is Apache Kafka?

Kafka is a distributed event-streaming platform used to publish, store and consume events.

Core components:

* Producer.
* Consumer.
* Topic.
* Partition.
* Broker.
* Consumer group.
* Offset.
* Replication.

Example:

Order Service
     |
  Producer
     |
  Kafka Topic
     |
  Consumer Group
     |
Inventory Service

Follow-up questions:

* What is a Kafka partition?
* What is an offset?
* What is a consumer group?
* What is a broker?
* How does Kafka achieve fault tolerance?

70. What is idempotency in Kafka?

Idempotency ensures that processing the same logical event more than once does not create duplicate business effects.

Kafka producer idempotence helps prevent duplicate writes caused by producer retries within its supported scope.

For business-level idempotency, consumers should also track processed event IDs or use idempotent database updates.

Follow-up: Does Kafka guarantee exactly-once processing in every external database operation?

No. Kafka’s exactly-once capabilities have specific boundaries. External database side effects need their own transactional or idempotency strategy.

71. What is ZooKeeper in Kafka?

ZooKeeper was traditionally used by Kafka for cluster coordination, broker metadata and controller election.

Modern Kafka supports KRaft mode, which uses Kafka’s own metadata quorum and removes the ZooKeeper dependency.

Follow-up: What is the difference between ZooKeeper mode and KRaft?

72. What is RabbitMQ?

RabbitMQ is a message broker that supports messaging using exchanges, queues and bindings.

Main components:

* Producer.
* Exchange.
* Queue.
* Binding.
* Consumer.
* Routing key.

Types of exchanges:

* Direct.
* Fanout.
* Topic.
* Headers.

Follow-up questions:

* What is acknowledgement?
* What is dead-letter exchange?
* What is message durability?
* What is prefetch count?
* Kafka vs RabbitMQ?

73. Kafka vs RabbitMQ

Kafka	RabbitMQ
Distributed event streaming	Message broker
Events retained based on retention policy	Messages generally removed after acknowledgement
Partition-based parallelism	Queue and consumer-based distribution
Suitable for event streams and replay	Suitable for task queues and routing
Consumer tracks offsets	Consumer acknowledges messages

Interview example: Kafka is useful for transaction event streams that need replay and multiple independent consumers. RabbitMQ is useful for task distribution and flexible routing.

Part 10 – Application Security

74. How do you secure frontend-to-backend communication?

A good answer should cover:

* HTTPS/TLS.
* OAuth 2.0 / OpenID Connect.
* JWT validation.
* Role-based authorization.
* Input validation.
* CORS restrictions.
* Secure token storage and cookie settings.
* Rate limiting.
* API Gateway security.
* Logging without exposing sensitive information.

Follow-up: Authentication vs authorization?

Authentication verifies who the user is. Authorization determines what the authenticated user is allowed to do.

75. How do you secure microservice-to-microservice communication?

Approaches include:

* OAuth2 client credentials flow.
* Mutual TLS.
* Service identity.
* Short-lived tokens.
* Network segmentation.
* Secrets management.
* Authorization at each service.

Follow-up: Is JWT alone sufficient to secure a microservice architecture?

No. You also need token validation, authorization, transport security, service identity and appropriate key management.

Part 11 – Angular and TypeScript

76. What is JavaScript vs TypeScript?

JavaScript	TypeScript
Dynamically typed	Statically typed development experience
Browser-native language	Compiles/transpiles to JavaScript
Runtime type errors are possible	Many type errors can be caught during development
No built-in compile-time type system	Supports interfaces, generics and type annotations

Example:

JavaScript:

let age = 25;
age = "Twenty five";

TypeScript:

let age: number = 25;
// Compilation error
// age = "Twenty five";

Follow-up: Why doesn’t the browser execute TypeScript directly?

Browsers execute JavaScript. TypeScript is transpiled to JavaScript.

77. Why do we use TypeScript?

* Type safety.
* Better IDE support.
* Interfaces and generics.
* Improved maintainability.
* Easier refactoring.
* Better support for large applications.

Follow-up: Does TypeScript prevent all runtime errors?

No. TypeScript checks many errors during development but cannot eliminate runtime issues.

78. What is @Input and @Output?

@Input() passes data from parent to child.

@Output() sends events from child to parent.

Parent:

<app-child
  [employeeName]="name"
  (employeeChanged)="updateEmployee($event)">
</app-child>

Child:

@Input() employeeName!: string;
@Output() employeeChanged =
    new EventEmitter<string>();
changeName() {
    this.employeeChanged.emit("John");
}

Follow-up: How do you communicate between unrelated components?

Options include shared services, RxJS subjects, signals or a state management solution.

79. What is one-way and two-way binding?

One-way binding: Data flows in one direction.

<p>{{ employeeName }}</p>

Two-way binding: Data flows from component to view and view to component.

<input [(ngModel)]="employeeName">

It combines property binding and event binding.

Follow-up: Difference between property binding and interpolation?

80. What are Directives in Angular?

Directives change the behaviour or structure of DOM elements.

Types:

* Component directives.
* Structural directives.
* Attribute directives.

Examples:

<p *ngIf="isVisible">Welcome</p>
<li *ngFor="let item of items">
    {{ item }}
</li>
<p [ngClass]="{'active': isActive}">
    Employee
</p>

Modern Angular also supports built-in control flow such as @if and @for.

Follow-up: Structural vs attribute directives?

Structural directives change DOM structure; attribute directives modify the appearance or behaviour of an element.

81. What are Angular lifecycle hooks?

Hook	Purpose
ngOnChanges	Responds to input changes
ngOnInit	Initializes component
ngDoCheck	Custom change detection
ngAfterContentInit	Content projection initialized
ngAfterContentChecked	Projected content checked
ngAfterViewInit	Component view initialized
ngAfterViewChecked	Component view checked
ngOnDestroy	Cleanup before destruction

Example:

export class EmployeeComponent
    implements OnInit, OnDestroy {
    ngOnInit() {
        console.log("Component initialized");
    }
    ngOnDestroy() {
        console.log("Component destroyed");
    }
}

Follow-up: Where do you unsubscribe from Observables?

Typically in ngOnDestroy, or using takeUntilDestroyed() in supported Angular versions.

82. What is Angular Routing?

Angular Router enables navigation between different views without full-page reloads.

const routes: Routes = [
    {
        path: 'employees',
        component: EmployeeComponent
    },
    {
        path: 'departments',
        component: DepartmentComponent
    }
];

HTML:

<a routerLink="/employees">Employees</a>
<router-outlet></router-outlet>

Follow-up questions:

* What are route guards?
* What is lazy loading?
* What is child routing?
* How do you pass parameters between routes?

83. What is routerLink?

routerLink is an Angular directive used for navigating to routes.

<a [routerLink]="['/employee', employee.id]">
    View Employee
</a>

It integrates with Angular Router rather than performing a normal browser navigation.

84. What is an Observable and Observer?

Observable: Represents a stream of values over time.

Observer: Contains methods to handle notifications emitted by an Observable.

const observable = new Observable(observer => {
    observer.next("Java");
    observer.next("Angular");
    observer.complete();
});
observable.subscribe({
    next: value => console.log(value),
    error: err => console.error(err),
    complete: () => console.log("Completed")
});

Follow-up: Difference between Observable and Promise?

Promise	Observable
Usually one eventual result	Zero, one or multiple values
Eager once created	Generally lazy until subscribed
Not cancellable through standard Promise API	Subscription can be cancelled
Native chaining	Rich RxJS operators

85. What is a Promise?

A Promise represents the eventual success or failure of an asynchronous operation.

const promise = new Promise((resolve, reject) => {
    resolve("Success");
});
promise.then(result => console.log(result));

States:

* Pending.
* Fulfilled.
* Rejected.

Follow-up: What is async/await? How do you handle Promise errors?

86. What is an Angular Interceptor?

An HTTP interceptor intercepts outgoing HTTP requests and incoming responses.

Common uses:

* Add authentication tokens.
* Handle 401/403 responses.
* Add correlation IDs.
* Centralize error handling.
* Log HTTP requests.

Example:

export const authInterceptor: HttpInterceptorFn =
    (req, next) => {
        const token = localStorage.getItem('token');
        const cloned = req.clone({
            setHeaders: {
                Authorization: `Bearer ${token}`
            }
        });
        return next(cloned);
    };

For production authentication, consider safer token storage and appropriate browser security protections rather than automatically placing long-lived tokens in localStorage.

Follow-up: How do you implement token refresh using an interceptor?

87. What is an Angular Pipe?

A pipe transforms data for display in templates.

Examples:

<p>{{ employee.name | uppercase }}</p>
<p>{{ employee.salary | currency:'INR' }}</p>
<p>{{ employee.joiningDate | date:'dd-MM-yyyy' }}</p>

Types:

* Built-in pipes.
* Custom pipes.

Follow-up: Pure vs impure pipes?

88. How do you use a dropdown in PrimeNG?

Example:

<p-dropdown
    [options]="departments"
    [(ngModel)]="selectedDepartment"
    optionLabel="name"
    placeholder="Select Department">
</p-dropdown>

For newer PrimeNG versions, the component is commonly p-select; the exact component depends on the version.

Follow-up: How do you implement server-side dropdown filtering?

89. AG Grid vs PrimeNG Table

AG Grid	PrimeNG Table
Advanced data-grid solution	General-purpose Angular UI table
Rich enterprise grid features	Integrated PrimeNG UI ecosystem
Advanced filtering, grouping and virtualization	Sorting, filtering and pagination
Strong option for complex data grids	Suitable for common application tables

Follow-up: Which would you choose for a table with millions of records?

Use server-side pagination, filtering and sorting. Neither grid should be expected to load millions of rows into browser memory.

90. How do you create a responsive UI?

Approaches:

* CSS Flexbox.
* CSS Grid.
* Media queries.
* Responsive units.
* Angular layout components.
* Responsive tables and grid systems.

Example:

.container {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 16px;
}
@media (max-width: 768px) {
    .container {
        grid-template-columns: 1fr;
    }
}

Follow-up: How do you test responsive layouts?

Use browser device emulation and real-device testing.

Part 12 – JavaScript, HTML5 and CSS

91. What are the features of HTML5?

Important features:

* Semantic tags: header, footer, section, article, nav.
* Audio and video support.
* Canvas and SVG.
* Local storage and session storage.
* Form validation attributes.
* Geolocation API.
* Web Workers.
* New input types such as email, date and number.

Follow-up: Difference between localStorage, sessionStorage and cookies?

92. Script tag in head vs body

Inside head:

The browser encounters the script while parsing the document. Without defer or async, it blocks HTML parsing while downloading and executing the script.

Inside body:

Placing the script near the end of body allows most HTML content to be parsed first.

Recommended modern approach:

<head>
    <script src="app.js" defer></script>
</head>

defer downloads the script without blocking HTML parsing and executes it after document parsing, in document order.

Follow-up: Difference between async and defer?

93. What is hoisting in JavaScript?

Hoisting refers to how JavaScript processes declarations before executing code.

console.log(a);
var a = 10;

Output:

undefined

With let:

console.log(b);
let b = 20;

This throws a ReferenceError because b is in the temporal dead zone until initialization.

Follow-up: Is let hoisted?

Yes, but it cannot be accessed before initialization.

94. Difference between var, let and const

Feature	var	let	const
Scope	Function	Block	Block
Redeclaration in same scope	Allowed	Not allowed	Not allowed
Reassignment	Allowed	Allowed	Not allowed
Hoisting	Yes	Yes, TDZ	Yes, TDZ

Example:

var a = 10;
var a = 20; // Allowed
let b = 10;
// let b = 20; // Error
const c = 10;
// c = 20; // Error

Important: A const object can still have its properties modified.

const employee = { name: "John" };
employee.name = "Alice"; // Allowed

Follow-up: Explain block scope with an example.

95. Difference between display:none and visibility:hidden

display:none	visibility:hidden
Element is removed from layout flow	Element occupies its layout space
No space reserved	Space is reserved
Not visually displayed	Not visually displayed

.hidden1 {
    display: none;
}
.hidden2 {
    visibility: hidden;
}

Follow-up: What is opacity: 0 and how is it different?

96. Write CSS for a paragraph and change its parent div background to yellow.

<div class="container">
    <p>This is an employee paragraph.</p>
</div>
.container {
    background-color: yellow;
    padding: 20px;
}
.container p {
    color: black;
    font-size: 16px;
    font-weight: bold;
}

Follow-up: Difference between class selector, ID selector and element selector?

97. What is a Closure?

This question appears in the initial JavaScript list as well as the language-specific preparation.

A closure allows a function to retain access to variables from its outer scope.

Example:

function createCounter() {
    let count = 0;
    return function() {
        return ++count;
    };
}
const counter = createCounter();
console.log(counter()); // 1
console.log(counter()); // 2

Follow-up: Can closures cause memory leaks?

They can retain references longer than intended, so unnecessary references should be released.

Part 13 – SQL, PostgreSQL and MongoDB

98. PostgreSQL vs MongoDB

PostgreSQL	MongoDB
Relational database	Document database
Table-based	Document-based
Structured schema	Flexible document schema
SQL queries	MongoDB query language
Supports joins and relational constraints	Supports embedded documents and references
Strong relational capabilities	Useful for document-oriented data

When would you choose PostgreSQL?

For banking transactions, financial data and relational information with complex queries and integrity requirements.

When would you choose MongoDB?

For document-oriented data with flexible structures and use cases where document access patterns are suitable.

Follow-up questions:

* SQL vs NoSQL?
* What is normalization?
* What are indexes?
* How does MongoDB indexing work?
* What is ACID?

99. Write a SQL query to find the Nth highest salary.

Using DENSE_RANK:

SELECT salary
FROM (
    SELECT salary,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employee
) e
WHERE rnk = 3;

This finds the third-highest distinct salary.

To retrieve employee details:

SELECT *
FROM (
    SELECT e.*,
           DENSE_RANK() OVER (
               ORDER BY salary DESC
           ) AS rnk
    FROM employee e
) result
WHERE rnk = 3;

Follow-up: Difference between ROW_NUMBER, RANK and DENSE_RANK?

Function	Behaviour with ties
ROW_NUMBER	Unique sequential numbers
RANK	Same rank, leaves gaps
DENSE_RANK	Same rank, no gaps

100. Write a self join to retrieve currency description using currency code.

The original question does not specify the exact table structure. Assume a currency table containing currency_code and currency_description, and a transaction table containing currency_code.

SELECT
    t.transaction_id,
    t.currency_code,
    c.currency_description
FROM transactions t
JOIN currency c
    ON t.currency_code = c.currency_code;

Strictly speaking, this is a regular join, not a self join.

If the question specifically requires a self join, an example would be matching currency records to a parent/reference currency record within the same table:

SELECT
    child.currency_code,
    parent.currency_description
FROM currency child
JOIN currency parent
    ON child.parent_currency_code =
       parent.currency_code;

Follow-up: Difference between inner join, left join and self join?

101. SQL query to retrieve subjects and counts from Student table.

Assuming the table contains a major_subject column:

SELECT
    major_subject,
    COUNT(*) AS student_count
FROM student
GROUP BY major_subject;

To retrieve only subjects having more than two students:

SELECT major_subject
FROM student
GROUP BY major_subject
HAVING COUNT(*) > 2;

Follow-up: Difference between WHERE and HAVING?

WHERE filters rows before grouping. HAVING filters groups after aggregation.

102. Sort employees by salary.

SELECT *
FROM employee
ORDER BY salary DESC;

For department-wise highest-paid employees:

SELECT *
FROM (
    SELECT e.*,
           ROW_NUMBER() OVER (
               PARTITION BY department
               ORDER BY salary DESC
           ) AS rn
    FROM employee e
) result
WHERE rn = 1;

Follow-up: How would you return all employees tied for the highest salary in each department?

Use DENSE_RANK() instead of ROW_NUMBER().

103. Explain database relationships.

The four common relationships:

* One-to-One.
* One-to-Many.
* Many-to-One.
* Many-to-Many.

Example:

A department has many employees. Each employee belongs to one department.

Follow-up: How would you model a many-to-many relationship in a relational database?

Use a junction table with foreign keys to both entities.

Part 14 – Design Patterns

104. Explain Singleton Design Pattern.

Singleton ensures that a class has only one instance and provides a global access point to it.

Example:

public class Singleton {
    private static final Singleton INSTANCE =
        new Singleton();
    private Singleton() {
    }
    public static Singleton getInstance() {
        return INSTANCE;
    }
}

This is eager initialization.

Follow-up questions:

* How do you implement lazy Singleton?
* How do you make Singleton thread-safe?
* How can reflection or serialization affect Singleton?
* Why is an enum Singleton often preferred?

105. Explain Factory Method Pattern.

Factory Method delegates object creation to a factory method rather than directly instantiating concrete classes throughout the application.

Example:

interface Notification {
    void send();
}
class EmailNotification implements Notification {
    public void send() {
        System.out.println("Email sent");
    }
}
class SmsNotification implements Notification {
    public void send() {
        System.out.println("SMS sent");
    }
}

Factory:

class NotificationFactory {
    public Notification create(String type) {
        if ("EMAIL".equalsIgnoreCase(type)) {
            return new EmailNotification();
        }
        if ("SMS".equalsIgnoreCase(type)) {
            return new SmsNotification();
        }
        throw new IllegalArgumentException(
            "Unsupported notification type");
    }
}

Follow-up: How would you avoid large if-else blocks in a factory?

Use a Map of type to supplier or strategy implementations.

106. How do you load a HashMap of subclass instances in a Factory Pattern?

This is specifically listed in your uploaded PDF.

interface Payment {
    void pay();
}
@Component("UPI")
class UpiPayment implements Payment {
    public void pay() {
        System.out.println("UPI payment");
    }
}
@Component("CARD")
class CardPayment implements Payment {
    public void pay() {
        System.out.println("Card payment");
    }
}

Factory:

@Component
class PaymentFactory {
    private final Map<String, Payment> payments;
    PaymentFactory(Map<String, Payment> payments) {
        this.payments = payments;
    }
    public Payment getPayment(String type) {
        Payment payment = payments.get(type);
        if (payment == null) {
            throw new IllegalArgumentException(
                "Unsupported payment type");
        }
        return payment;
    }
}

Spring can inject the discovered beans into the Map using their bean names as keys.

Follow-up questions:

* How does Spring populate the Map?
* How can you use @Qualifier?
* How would you register new payment implementations without changing the factory?
* How does this relate to the Strategy pattern?

Part 15 – Coding Interview Exercises

These are the coding questions from your PDF, with Java 17 solutions.

107. Filter numbers greater than 2 and calculate their sum.

List<Integer> numbers =
    Arrays.asList(1, 2, 3, 4, 5, 6);
int sum = numbers.stream()
    .filter(n -> n > 2)
    .mapToInt(Integer::intValue)
    .sum();
System.out.println(sum);

Output: 18

Follow-up: How would you find the average of the filtered values?

108. Arrange all 1s at the beginning and 0s at the end.

Input:

[0, 1, 0, 1, 1, 0]

Output:

[1, 1, 1, 0, 0, 0]

Using two pointers:

int[] arr = {0, 1, 0, 1, 1, 0};
int left = 0;
int right = arr.length - 1;
while (left < right) {
    while (left < right && arr[left] == 1) {
        left++;
    }
    while (left < right && arr[right] == 0) {
        right--;
    }
    if (left < right) {
        int temp = arr[left];
        arr[left] = arr[right];
        arr[right] = temp;
    }
}

Time complexity: O(n).

Space complexity: O(1).

Follow-up: How would you maintain the original relative order of the elements?

109. Move all zeros to the beginning.

Input:

[1, 2, 0, 4, 0, -3, 5]

Output:

[0, 0, 1, 2, 4, -3, 5]

Two-pointer approach:

int[] arr = {1, 2, 0, 4, 0, -3, 5};
int index = arr.length - 1;
for (int i = arr.length - 1; i >= 0; i--) {
    if (arr[i] != 0) {
        arr[index--] = arr[i];
    }
}
while (index >= 0) {
    arr[index--] = 0;
}

Time complexity: O(n).

Space complexity: O(1).

This implementation preserves the relative order of non-zero elements.

Follow-up: How would you move zeros to the end instead?

110. Sort employees by first name ascending, last name descending and salary greater than 50,000.

List<Employee> result = employees.stream()
    .filter(e -> e.getSalary() > 50000)
    .sorted(
        Comparator.comparing(Employee::getFirstName)
            .thenComparing(
                Employee::getLastName,
                Comparator.reverseOrder()
            )
    )
    .toList();

Follow-up questions:

* How does thenComparing work?
* Difference between reversed() and reverseOrder()?
* How would you handle null names?
* How would you implement the same using SQL?

SQL:

SELECT *
FROM employee
WHERE salary > 50000
ORDER BY first_name ASC,
         last_name DESC;

111. Find employees by date of joining and sort them.

List<Employee> result = employees.stream()
    .filter(e ->
        e.getDateOfJoining() != null)
    .sorted(
        Comparator.comparing(
            Employee::getDateOfJoining
        )
    )
    .toList();

Follow-up: How would you sort by date descending?

.sorted(
    Comparator.comparing(
        Employee::getDateOfJoining
    ).reversed()
)

112. Store two addresses separately when an employee is used as a HashMap key.

The original question is ambiguous about whether addresses belong to an employee or whether they should be independent entries.

A clean design is to represent employee ID as the key and addresses as a list.

Map<Long, List<String>> employeeAddresses =
    new HashMap<>();
employeeAddresses.put(
    101L,
    new ArrayList<>(
        List.of("Chennai", "Coimbatore")
    )
);
employeeAddresses.get(101L).add("Namakkal");

Follow-up: Why should mutable Employee objects be avoided as HashMap keys?

If fields used by hashCode() change after insertion, the object may become difficult to retrieve from the map.

113. Find the number closest to 5.

Input:

int[] arr = {1, 4, 7, 8, 9};
int target = 5;

Solution:

int closest = Arrays.stream(arr)
    .boxed()
    .min(Comparator.comparingInt(
        n -> Math.abs(n - target)
    ))
    .orElseThrow();
System.out.println(closest);

Output:

4

Follow-up: What if two numbers are equally close? How would you select the smaller number?

int closest = Arrays.stream(arr)
    .boxed()
    .min(
        Comparator.comparingInt(
            (Integer n) -> Math.abs(n - target)
        ).thenComparingInt(n -> n)
    )
    .orElseThrow();

114. Group strings by their length and count occurrences.

Input:

List<String> names = Arrays.asList(
    "John", "Alice", "Bob", "Jane"
);

Solution:

Map<Integer, Long> result = names.stream()
    .collect(Collectors.groupingBy(
        String::length,
        Collectors.counting()
    ));
System.out.println(result);

Output:

{3=1, 4=2, 5=1}

Follow-up: How would you return the actual names grouped by length instead of counts?

Map<Integer, List<String>> grouped =
    names.stream()
        .collect(Collectors.groupingBy(
            String::length
        ));

115. Find common elements between two lists.

List<Integer> list1 =
    List.of(1, 2, 3, 4, 5);
List<Integer> list2 =
    List.of(3, 4, 5, 6, 7);
List<Integer> common = list1.stream()
    .filter(list2::contains)
    .distinct()
    .toList();

Output:

[3, 4, 5]

For better performance with large lists, create a HashSet of the second list.

Follow-up: What is the time complexity of each approach?

116. Find duplicate elements using Stream API.

List<Integer> numbers =
    List.of(1, 2, 3, 2, 4, 3, 5);
Set<Integer> seen = new HashSet<>();
Set<Integer> duplicates = numbers.stream()
    .filter(n -> !seen.add(n))
    .collect(Collectors.toSet());

Output:

[2, 3]

Follow-up: Is this approach suitable for parallel streams?

No. The shared mutable HashSet is not thread-safe. Use a frequency map or an appropriate concurrent approach.

117. Find employees by age and salary using Streams.

List<Employee> result = employees.stream()
    .filter(e -> e.getAge() > 25)
    .filter(e -> e.getSalary() > 50000)
    .toList();

Follow-up: How would you group the result by department?

118. Sort employees by age using Stream API.

List<Employee> result = employees.stream()
    .sorted(Comparator.comparingInt(
        Employee::getAge
    ))
    .toList();

Descending:

.sorted(
    Comparator.comparingInt(
        Employee::getAge
    ).reversed()
)

119. Give employee bonus based on rating using Streams.

Assume:

* Rating 5: 20% bonus.
* Rating 4: 15% bonus.
* Rating 3: 10% bonus.
* Other ratings: No bonus.

Map<Integer, Double> bonusMap = Map.of(
    5, 0.20,
    4, 0.15,
    3, 0.10
);
Map<String, Double> bonuses =
    employees.stream()
        .collect(Collectors.toMap(
            Employee::getName,
            e -> e.getSalary() *
                bonusMap.getOrDefault(
                    e.getRating(), 0.0
                )
        ));

Follow-up: How would you calculate the final salary including the bonus?

120. Implement Singleton Design Pattern using code.

A thread-safe lazy initialization approach:

public class Singleton {
    private Singleton() {}
    private static class Holder {
        private static final Singleton INSTANCE =
            new Singleton();
    }
    public static Singleton getInstance() {
        return Holder.INSTANCE;
    }
}

This uses the initialization-on-demand holder idiom.

Follow-up: Why is this thread-safe without using synchronized?

Because class initialization is guaranteed to be thread-safe by the JVM.

121. Implement an LRU Cache.

LRU means Least Recently Used. When the cache reaches capacity, the least recently accessed entry is removed.

Java implementation using LinkedHashMap:

class LRUCache<K, V> extends LinkedHashMap<K, V> {
    private final int capacity;
    public LRUCache(int capacity) {
        super(capacity, 0.75f, true);
        this.capacity = capacity;
    }
    @Override
    protected boolean removeEldestEntry(
            Map.Entry<K, V> eldest) {
        return size() > capacity;
    }
}

Usage:

LRUCache<Integer, String> cache =
    new LRUCache<>(2);
cache.put(1, "Java");
cache.put(2, "Spring");
cache.get(1);
cache.put(3, "Angular");

Entry 2 is removed because entry 1 was recently accessed.

Follow-up questions:

* Why is LinkedHashMap suitable?
* What does the accessOrder parameter do?
* What is the time complexity?
* How would you make this cache thread-safe?

122. Write SQL to retrieve employee details sorted by salary descending.

SELECT *
FROM employee
ORDER BY salary DESC;

To sort within a department:

SELECT *
FROM employee
ORDER BY department ASC,
         salary DESC;

Follow-up: How would you find the highest-paid employee in each department?

Use ROW_NUMBER() or DENSE_RANK() with PARTITION BY department.

Part 16 – Project Explanation and Senior-Level Scenarios

These questions are particularly important because interviewers expect a seven-year developer to explain actual implementation decisions, not just definitions.

123. Explain your project.

A suggested interview answer based on the project experience you have described:

Answer:

“I have been working as a Java Backend Developer on a US healthcare application, primarily in member management, rating and commissions.

My responsibilities include understanding business requirements, developing backend functionality using Java and Spring Boot, designing and maintaining REST APIs, and integrating with databases, primarily IBM DB2.

I work closely with business analysts, QA engineers and cross-functional teams to understand requirements, resolve issues and deliver features within sprint timelines.

I also work on enhancing existing applications, database procedures, integration activities, code reviews and maintaining clean and reusable code. We follow Agile development practices and use CI/CD processes for application delivery.”

Likely follow-up questions:

* Explain your project architecture.
* What are the microservices in your application?
* How does your Angular application communicate with Spring Boot?
* How do you handle authentication?
* How do you handle exceptions?
* How do you connect to DB2?
* Have you used stored procedures?
* How do you handle database performance?
* How do you troubleshoot production issues?
* Explain one challenging technical issue you resolved.

124. How is Angular implemented in your project?

Answer:

“Angular is used for the presentation layer. We organize the application into feature-based components and services.

Components handle the UI and user interactions. Angular services manage reusable business logic and API communication using HttpClient.

We use routing for navigation, interceptors for common HTTP concerns, and RxJS for asynchronous operations.”

Follow-up questions:

* How do you pass data between components?
* How do you implement lazy loading?
* How do you manage subscriptions?
* How do you handle API errors?
* How do you implement route guards?

125. How do you handle errors in a distributed application?

Answer:

“I would categorize errors into business errors, validation errors, technical failures and dependency failures.

For synchronous communication, I would configure timeouts, controlled retries and circuit breakers.

For asynchronous communication, I would use acknowledgements, retries, idempotent consumers and dead-letter queues.

I would also use correlation IDs and distributed tracing to identify the flow of a request across services.”

Follow-up: How do you avoid duplicate processing when a message is retried?

126. How would you download a large report through Angular and Spring Boot?

This is a useful senior-level scenario.

For a report containing one year of transaction records, I would avoid loading the entire report into application memory.

Possible design:

Angular – Request report

Spring Boot – Create report job

Background processing

Paginated DB retrieval / streaming

Object storage – Generated report

Angular – Download link

Implementation considerations:

* Asynchronous report generation.
* Database pagination or cursor-based retrieval.
* Streaming file generation.
* Temporary storage or object storage.
* Job status API.
* Download authorization.
* Expiry of generated reports.
* Error handling and cleanup.

Follow-up: Why not directly return a huge Excel file from the REST API?

It can cause high memory consumption, long-running requests, timeouts and poor user experience.

127. How do you improve database performance?

Answer:

* Analyze slow SQL queries.
* Add appropriate indexes.
* Avoid unnecessary columns.
* Use pagination.
* Avoid N+1 queries.
* Optimize joins.
* Review execution plans.
* Use connection pooling.
* Use caching where suitable.
* Monitor database performance.

Follow-up: What is the difference between an index scan and a table scan?

128. How do you handle a production OutOfMemoryError?

Answer:

* Capture heap dumps.
* Analyze using Eclipse MAT or similar tools.
* Identify memory leaks or excessive object creation.
* Check large collections and caches.
* Review thread and connection usage.
* Optimize batch processing.
* Fix the underlying issue before increasing heap size.

Follow-up: Difference between heap and stack memory?

129. How do you write unit tests for a Spring Boot service?

Example:

@ExtendWith(MockitoExtension.class)
class EmployeeServiceTest {
    @Mock
    private EmployeeRepository repository;
    @InjectMocks
    private EmployeeService service;
    @Test
    void shouldReturnEmployee() {
        Employee employee = new Employee();
        employee.setId(1L);
        when(repository.findById(1L))
            .thenReturn(Optional.of(employee));
        Employee result = service.getById(1L);
        assertEquals(1L, result.getId());
        verify(repository).findById(1L);
    }
}

Follow-up questions:

* @Mock vs @MockBean?
* @InjectMocks?
* When to use @SpringBootTest?
* Mockito when() vs doReturn()?
* How do you test exceptions?
* Unit testing vs integration testing?

130. How do you communicate with different microservices securely?

Answer:

“I would use service-to-service authentication, such as OAuth2 client credentials, or mutual TLS depending on the infrastructure.

Each service should validate the identity and authorization of the caller. Secrets and credentials should be managed securely. Sensitive information should not be exposed in logs.”

Follow-up: How do you propagate a user identity when Service A calls Service B?

Use a carefully designed token propagation or token exchange approach, depending on the authorization architecture.

Part 17 – Additional Interview Questions and Coverage Checklist

The following are important questions from the original PDF that should also be included in your revision.

131. JavaScript vs TypeScript in web applications

Why not use TypeScript directly in the browser?

Browsers execute JavaScript, not TypeScript. TypeScript is compiled into JavaScript during the build process.

Follow-up: What is the role of Angular CLI and the TypeScript compiler?

132. How do you implement API calls in Angular?

@Injectable({
  providedIn: 'root'
})
export class EmployeeService {
  constructor(private http: HttpClient) {}
  getEmployees(): Observable<Employee[]> {
    return this.http.get<Employee[]>('/api/employees');
  }
}

Component:

employees: Employee[] = [];
ngOnInit() {
    this.employeeService.getEmployees()
        .subscribe({
            next: data => this.employees = data,
            error: error => console.error(error)
        });
}

Follow-up: How do you handle loading indicators, errors and subscription cleanup?

133. What is a database self join?

A self join joins a table with itself. For example, finding employee-manager relationships:

SELECT
    e.employee_name,
    m.employee_name AS manager_name
FROM employee e
LEFT JOIN employee m
    ON e.manager_id = m.employee_id;

Follow-up: How would you retrieve employees who earn more than their managers?

134. What is the difference between SQL and NoSQL?

Explain relational data, flexible schemas, consistency, scalability and transaction requirements. Give PostgreSQL and MongoDB examples from question 98.

135. How do you implement messaging?

For RabbitMQ, explain producer, exchange, routing key, queue, consumer and acknowledgement.

For Kafka, explain producer, topic, partition, consumer group and offset.

Follow-up: How would you handle message failures and duplicate messages?

Final revision checklist

Use this to track your preparation.

Your preparation progress

0/72

0% completed

Core Java and OOP

0/8

OOP concepts

Abstract class vs interface

Polymorphism and dynamic dispatch

String immutability

Generics

Static and default methods

Java 8 features

Java 17 features

Collections and Concurrency

0/8

ArrayList vs LinkedList

HashMap internals

HashSet vs LinkedHashSet

ConcurrentHashMap

ExecutorService and thread pools

CompletableFuture

volatile vs synchronized

Deadlock, wait and yield

Spring Boot and JPA

0/10

Spring Boot annotations and startup

Spring MVC

IoC and DI

Bean lifecycle and scopes

Configuration and Actuator

CORS and CSRF

JPA entities and repositories

findById internals

Relationships and N+1

Transactions

Microservices and APIs

0/9

Monolith to microservices

API Gateway

Service communication

Resilience and error handling

Caching

REST HTTP methods

Idempotency

WebClient vs RestTemplate

Security

Kafka and RabbitMQ

0/7

Kafka architecture

Producer and consumer

Partitions and consumer groups

Idempotency

ZooKeeper and KRaft

RabbitMQ exchanges and queues

Kafka vs RabbitMQ

Angular and Frontend

0/11

JavaScript vs TypeScript

Input and Output

Data binding

Directives

Lifecycle hooks

Routing and routerLink

Observable, Observer and Promise

Interceptors and pipes

AG Grid vs PrimeNG

Responsive UI

HTML5, CSS and JavaScript

SQL and Coding

0/11

N-th highest salary

Self join

Group by and Having

Employee sorting

Stream API problems

Move zeros

Find duplicates

Group strings by length

Closest number

Singleton and Factory

LRU Cache

Project and Scenarios

0/8

Project architecture explanation

Angular and Spring Boot integration

Large report download

Production troubleshooting

Performance optimization

OutOfMemoryError

Unit testing with Mockito

Microservice security

Reset progress

Important source note: Your original PDF contains repeated questions and a few questions with incomplete table structures or unspecified business rules. I’ve retained the distinct questions, consolidated repeated concepts, and explicitly stated assumptions where necessary.

My interview recommendation: For seven years of experience, don’t just memorize definitions. For every major topic, prepare:

* Concept and internal working.
* Practical Java/Spring Boot code.
* Real project implementation.
* Performance and failure scenarios.
* Two likely follow-up questions.

This is what will help you handle senior-level technical rounds confidently.