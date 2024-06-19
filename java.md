
## Threads:

### What is the difference between Runnable and Callable in Java?

**Answer:**

- **Runnable:** Represents a task that can be executed by a thread. It does not return a result and cannot throw checked exceptions.

```java
public class MyRunnable implements Runnable {
    @Override
    public void run() {
        System.out.println("Runnable running");
    }
}
```

- **Callable:** Represents a task that can be executed by a thread and returns a result. It can throw checked exceptions.
```java
public class MyCallable implements Callable<String> {
    @Override
    public String call() throws Exception {
        return "Callable result";
    }
}
```

### What is the difference between synchronized method and synchronized block in Java?

**Answer:**

- **synchronized method:** Locks the entire method, preventing multiple threads from executing it simultaneously on the same object.

```java
public synchronized void synchronizedMethod() {
    // critical section
}
```

- **synchronized block:** Allows more granular control over the synchronization by locking only the specific block of code, reducing the scope of the lock.
```java
public void method() {
    synchronized(this) {
        // critical section
    }
}
```

### What is a deadlock and how can it be prevented?

**Answer:**

A deadlock occurs when two or more threads are blocked forever, each waiting for a resource that the other thread holds. This situation leads to a deadlock where neither thread can proceed. Deadlocks are typically caused by the improper synchronization of threads and resources.

**Prevention Strategies:**

1. **Avoiding nested locks:** Do not acquire a lock when already holding another lock. This can be achieved by carefully designing your locking strategy and ensuring that locks are acquired in a consistent order.

2. **Lock ordering:** Ensure that all threads acquire locks in a consistent and predictable order across the application. By enforcing a global ordering of locks, you can prevent cyclic dependencies that lead to deadlocks.

3. **Using tryLock:** The `tryLock()` method from `ReentrantLock` class in Java allows a thread to acquire a lock only if it is available. This method returns immediately whether the lock is acquired or not, rather than waiting indefinitely. It's useful for avoiding deadlock situations where threads might wait indefinitely for resources.

```java
import java.util.concurrent.locks.ReentrantLock;

ReentrantLock lock1 = new ReentrantLock();
ReentrantLock lock2 = new ReentrantLock();

public void method() {
    if (lock1.tryLock()) {
        try {
            if (lock2.tryLock()) {
                try {
                    // critical section
                } finally {
                    lock2.unlock();
                }
            }
        } finally {
            lock1.unlock();
        }
    }
}
```

### Differences between Thread class and ExecutorService in Java

**Thread class:**
- Represents a single thread of execution.
- Requires manual management of threads, including creation, starting, scheduling, and termination.
- Suitable for scenarios where you need direct control over individual threads.
- Can be error-prone and inefficient when handling multiple threads or complex thread interactions.

Example:
```java
Thread thread = new Thread(new MyRunnable());
thread.start(); // Starts the thread
```

**ExecutorService:** Provides a higher-level API for managing a pool of threads. It simplifies thread management by handling thread creation, scheduling, and termination.

Example:
```java
ExecutorService executor = Executors.newFixedThreadPool(10);
executor.submit(new MyRunnable());
executor.shutdown();
```

### Explanation of ThreadLocal in Java

**ThreadLocal** in Java provides a way to maintain thread-local variables. These variables are unique to each thread that accesses them. Each thread sees its own independently initialized copy of the variable, which is isolated from changes made by other threads.

**Usage Scenario:**
ThreadLocal is particularly useful in situations where you need to maintain state information that is specific to a thread, such as user sessions in web applications or transaction contexts in database operations. It allows you to store and retrieve data on a per-thread basis without explicitly passing the data through method parameters or using global variables, which can lead to synchronization issues in concurrent environments.

**Example:**

```java
import java.util.concurrent.ThreadLocalRandom;

public class ThreadLocalExample {
    private static ThreadLocal<Integer> threadLocal = ThreadLocal.withInitial(() -> ThreadLocalRandom.current().nextInt(100));

    public static void main(String[] args) {
        // Create multiple threads to access the thread-local variable
        Thread thread1 = new Thread(() -> {
            // Each thread will have its own initialized value
            System.out.println("Thread 1 Initial Value: " + threadLocal.get());
            threadLocal.set(10); // Set thread-local value to 10
            System.out.println("Thread 1 Updated Value: " + threadLocal.get());
        });

        Thread thread2 = new Thread(() -> {
            // Each thread will have its own initialized value
            System.out.println("Thread 2 Initial Value: " + threadLocal.get());
            threadLocal.set(20); // Set thread-local value to 20
            System.out.println("Thread 2 Updated Value: " + threadLocal.get());
        });

        thread1.start();
        thread2.start();
    }
}
```

_____________________________________________________________________________________________
## Collections:

**What are the differences between ArrayList and LinkedList in Java?**

**Answer:**


- **ArrayList:**
   - Backed by an array.
   - Provides constant-time access with index.
   - Slower insertions and deletions compared to LinkedList as elements need to be shifted.
   - Better for random access.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
List<String> arrayList = new ArrayList<>();
arrayList.add("A");
arrayList.get(0); // O(1)

```
**LinkedList:**


- Backed by a doubly linked list.
- Provides constant-time insertions and deletions.
- Slower access times compared to ArrayList as it requires traversal.
- Better for frequent insertions and deletions.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
List<String> linkedList = new LinkedList<>();
linkedList.add("A");
linkedList.get(0); // O(n)

```
**What is the difference between HashMap and Hashtable?**

**Answer:**


- **HashMap:**
   - Not synchronized, making it faster but not thread-safe.
   - Allows one null key and multiple null values.
   - Generally preferred for non-threaded applications.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
Map<String, String> hashMap = new HashMap<>();
hashMap.put(null, "value");

```
**Hashtable:**


- Synchronized, making it thread-safe but slower.
- Does not allow null keys or values.
- Considered legacy and generally replaced by ConcurrentHashMap in concurrent applications.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
Map<String, String> hashtable = new Hashtable<>();
hashtable.put(null, "value"); // Throws NullPointerException

```
**Explain the ConcurrentHashMap and how it works.**

**Answer:**

- ConcurrentHashMap is a thread-safe variant of HashMap designed for concurrent access without using synchronized blocks. It divides the map into segments, allowing multiple threads to read and write without contention. It achieves concurrency by using a finer-grained locking mechanism, typically with a lock for each segment.
```java
Map concurrentMap = new ConcurrentHashMap<>();
concurrentMap.put("key", "value");
```

**What is the difference between Set and List in Java?**

**Answer:**


**Set:**
   - Does not allow duplicate elements.
   - Implementations include HashSet, LinkedHashSet, TreeSet.
   - HashSet provides constant-time performance for basic operations.
   - TreeSet maintains elements in a sorted order.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
Set<String> set = new HashSet<>();
set.add("A");
set.add("A"); // No duplicate allowed

```
**List:**


- Allows duplicate elements.
- Maintains the order of insertion.
- Implementations include ArrayList, LinkedList.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
List<String> list = new ArrayList<>();
list.add("A");
list.add("A"); // Duplicates allowed

```
**How do you sort a List of objects in Java?**

**Answer:** You can sort a List of objects using Collections.sort() or List.sort() with a Comparator or by implementing the Comparable interface.


**Using Comparable:**

```java
public class Person implements Comparable
{
    private String name;
    private int age;

    // Constructors, getters, and setters

    @Override
    public int compareTo(Person other) {
        return Integer.compare(this.age, other.age);
    }
}

List
people = new ArrayList<>();
Collections.sort(people); // Sorts based on age

```
**Using Comparator:**

```java
Copy code
List
people = new ArrayList<>();
people.sort(Comparator.comparing(Person::getName)); // Sorts based on name

```

_____________________________________________________________________________________________
**Java 8 Features:**

**What are the main features introduced in Java 8?**

**Answer:** The main features introduced in Java 8 include:


- Lambda Expressions
- Functional Interfaces
- Streams API
- Default and Static Methods in Interfaces
- Optional Class
- New Date and Time API (java.time package)
- Nashorn JavaScript Engine
- Method References
- Collectors Class

**Explain lambda expressions and provide an example.**

**Answer:** Lambda expressions are a new syntax introduced in Java 8 that allows you to write anonymous functions (functions without names). They provide a clear and concise way to represent one method interface using an expression.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
// Syntax: (parameters) -> expression or (parameters) -> { statements; }

// Example with single parameter
List<String> list = Arrays.asList("a", "b", "c");
list.forEach(s -> System.out.println(s));

// Example with multiple parameters
Comparator<String> comparator = (s1, s2) -> s1.compareTo(s2);

```
**What is a functional interface? Can you give an example?**

**Answer:** A functional interface is an interface that contains exactly one abstract method. It can contain any number of default or static methods. The @FunctionalInterface annotation can be used to ensure that the interface is functional.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
@FunctionalInterface
interface MyFunctionalInterface {
    void execute();
}

// Example usage with lambda expression
MyFunctionalInterface func = () -> System.out.println("Executing...");
func.execute();

```
**Explain the Streams API and provide an example of how it can be used.**

**Answer:** The Streams API provides a functional approach to processing sequences of elements, allowing operations such as filtering, mapping, and reducing. Streams are designed to work with collections and support both sequential and parallel execution.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Example: Filter and collect names starting with 'A'
List<String> filteredNames = names.stream()
    .filter(name -> name.startsWith("A"))
    .collect(Collectors.toList());

filteredNames.forEach(System.out::println); // Output: Alice

```
**What are default methods in interfaces? Why are they introduced?**

**Answer:** Default methods allow interfaces to have method implementations. They were introduced to provide a way to evolve interfaces with new methods without breaking the existing implementations.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
interface MyInterface {
    void abstractMethod();

    default void defaultMethod() {
        System.out.println("Default method implementation");
    }
}

class MyClass implements MyInterface {
    @Override
    public void abstractMethod() {
        System.out.println("Abstract method implementation");
    }
}

MyInterface obj = new MyClass();
obj.abstractMethod(); // Output: Abstract method implementation
obj.defaultMethod(); // Output: Default method implementation

```
**What is the Optional class and how can it be used?**

**Answer:** The Optional class is a container object which may or may not contain a non-null value. It is used to avoid null checks and prevent NullPointerException.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
// Example of Optional usage
Optional<String> optional = Optional.ofNullable("Hello");

// Check if value is present
if (optional.isPresent()) {
    System.out.println(optional.get()); // Output: Hello
}

// Example of using ifPresent
optional.ifPresent(System.out::println); // Output: Hello

// Example of using orElse
String value = optional.orElse("Default Value");
System.out.println(value); // Output: Hello

```
**What are method references and how are they useful?**

**Answer:** Method references provide a way to refer to methods of existing classes or objects without invoking them. They are useful for improving code readability and reusability. Method references can be used in place of lambda expressions to call existing methods.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
// Syntax: Class::methodName or instance::methodName

// Example with static method reference
List<String> list = Arrays.asList("a", "b", "c");
list.forEach(System.out::println);

// Example with instance method reference
class Printer {
    public void print(String str) {
        System.out.println(str);
    }
}

Printer printer = new Printer();
list.forEach(printer::print);

```
**What is the new Date and Time API in Java 8? How does it improve upon the old Date API?**

**Answer:** The new Date and Time API in Java 8, located in the java.time package, provides a more comprehensive and consistent model for date and time manipulation. It addresses many issues of the old java.util.Date and java.util.Calendar classes such as mutability and lack of thread-safety.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
// Example of using new Date and Time API
LocalDate date = LocalDate.now();
LocalTime time = LocalTime.now();
LocalDateTime dateTime = LocalDateTime.now();

System.out.println("Current Date: " + date);
System.out.println("Current Time: " + time);
System.out.println("Current DateTime: " + dateTime);

// Example of parsing and formatting
LocalDate parsedDate = LocalDate.parse("2023-06-18");
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formattedDate = parsedDate.format(formatter);
System.out.println("Formatted Date: " + formattedDate); // Output: 18-06-2023

```
**Explain the concept of streams parallelism in Java 8.**

**Answer:** Parallel streams in Java 8 allow operations to be executed concurrently on multiple threads, leveraging multi-core processors. By calling the parallel() method on a stream, the stream can be processed in parallel, improving performance for large datasets.

```java<span class="" data-state="closed"><button class="flex gap-1 items-center"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-sm"><path fill="currentColor" fill-rule="evenodd" d="M7 5a3 3 0 0 1 3-3h9a3 3 0 0 1 3 3v9a3 3 0 0 1-3 3h-2v2a3 3 0 0 1-3 3H5a3 3 0 0 1-3-3v-9a3 3 0 0 1 3-3h2zm2 2h5a3 3 0 0 1 3 3v5h2a1 1 0 0 0 1-1V5a1 1 0 0 0-1-1h-9a1 1 0 0 0-1 1zM5 9a1 1 0 0 0-1 1v9a1 1 0 0 0 1 1h9a1 1 0 0 0 1-1v-9a1 1 0 0 0-1-1z" clip-rule="evenodd"></path></svg>Copy code</button>
List<Integer> numbers = Arrays.asList(1, 2, 3, 4, 5, 6, 7, 8, 9, 10);

// Sequential stream
numbers.stream()
    .map(number -> number * 2)
    .forEach(System.out::println);

// Parallel stream
numbers.parallelStream()
    .map(number -> number * 2)
    .forEach(System.out::println);

```
**What are the new collectors introduced in Java 8? Provide examples.



------------------

**You:**

What are the new collectors introduced in Java 8? Provide examples.

Answer: Java 8 introduced several new collectors in the Collectors class for collecting stream elements into various forms like lists, sets, maps, and more complex structures like partitioning and grouping by.

```java
List<String> names = Arrays.asList("Alice", "Bob", "Charlie", "David");

// Collect to List
List<String> collectedList = names.stream().collect(Collectors.toList());

// Collect to Set
Set<String> collectedSet = names.stream().collect(Collectors.toSet());

// Collect to Map
Map<String, Integer> collectedMap = names.stream()
.collect(Collectors.toMap(name -> name, name -> name.length()));

// Grouping by length of the name
Map<Integer, List<String>> groupedByLength = names.stream()
.collect(Collectors.groupingBy(String::length));

// Partitioning by length of the name
Map<Boolean, List<String>> partitionedByLength = names.stream()
.collect(Collectors.partitioningBy(name -> name.length() > 3));

<span class="" data-state="closed"><button class="flex h-9 w-9 items-center justify-center rounded-full text-token-text-secondary transition hover:bg-token-main-surface-tertiary"><svg xmlns="http://www.w3.org/2000/svg" width="24" height="24" fill="none" viewBox="0 0 24 24" class="icon-md"><path fill="currentColor" fill-rule="evenodd" d="M13.293 4.293a4.536 4.536 0 1 1 6.414 6.414l-1 1-7.094 7.094A5 5 0 0 1 8.9 20.197l-4.736.79a1 1 0 0 1-1.15-1.151l.789-4.736a5 5 0 0 1 1.396-2.713zM13 7.414l-6.386 6.387a3 3 0 0 0-.838 1.628l-.56 3.355 3.355-.56a3 3 0 0 0 1.628-.837L16.586 11zm5 2.172L14.414 6l.293-.293a2.536 2.536 0 0 1 3.586 3.586z" clip-rule="evenodd"></path></svg></button>
```

