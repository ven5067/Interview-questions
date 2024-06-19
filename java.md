
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
