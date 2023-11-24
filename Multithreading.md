## Multithreading 

ability of a CPU to execute multiple threads independently at the **same time** but share the process resources **simultaneously**. It is a Java feature where one can subdivide the specific 
program into two or more threads to make the execution of the program fast and easy.


| Aspect                             | Multithreading                                          | Multiprocessing                                         |
|------------------------------------|--------------------------------------------------------|----------------------------------------------------------|
| **Memory Sharing**                 | Threads share the same memory space.                   | Processes have independent memory spaces.                 |
| **Communication**                  | Direct communication between threads (lower overhead). | Communication often involves message passing (higher overhead). |
| **Resource Overhead**              | Lower resource overhead, as threads share resources.   | Higher resource overhead, as each process has its own resources. |
| **Complexity and Synchronization** | Simplified data sharing but requires synchronization.  | Independent memory reduces the need for explicit synchronization. |
| **Scalability**                    | Well-suited for fine-grained parallelism on multi-core processors. | Well-suited for tasks with independent, parallelizable units and can scale across multiple processors. |
| **Fault Isolation**                | A bug or failure in one thread can potentially impact the entire process. | Processes are isolated, reducing the impact of failures. |
| **Suitability**                    | Effective for tasks with shared data and fine-grained parallelism. | Effective for tasks that can be divided into independent units and require more isolation. |
| **Examples**                       | Java threads, POSIX threads (Pthreads), .NET Threads.   | Separate processes in Unix/Linux, multiprocessing modules in Python. |

**Threads:** as lightweight units within a process, enable concurrent and efficient execution of tasks. They share a common address space while operating independently, simplifying the utilization of multiple CPUs.

To pass a parameter to the run method when using the Thread class, you can create a constructor in your Multithreading class to accept the parameter, and then set it before starting the thread. 

with Thread:
```
class Multithreading extends Thread {
    private int x;
    public Multithreading(int x) {
        this.x = x;
    }
    public void run() {
        System.out.println("Now thread is running " + x);
    }
}

class MultithreadingDemo{
    public static void main(String args[]) {
        Multithreading m = new Multithreading(5);
        m.start();
    }
}
```
With Runnable:
```
class MultithreadingDemo{
    public static void main(String[] args) {
        // new MyThread("world!").start();
        Thread t = new Thread(new Multithreading_runnable(80));
        t.start();
    }   
}
class Multithreading_runnable implements Runnable {
    private int t;
     public Multithreading_runnable(int t) {
      this.t = t;
  }
    @Override
    public void run() {
        System.out.println("Now thread is running " + t);
    }
}
```
• The run method in the Runnable interface or the Thread class in Java does not have a specified return type. It is a void method, meaning it does not return any value.
    Using @Override helps catch these types of errors at compile-time, providing a clear indication that a method is intended to override a method in the superclass.

• The synchronized block ensures that if one thread is currently executing this block, another thread that wants to execute the same block must wait until the first thread completes. This means that the order in which threads acquire the lock and enter the block is determined by the scheduler and other factors, and it's not guaranteed to be in the order in which threads started.

### Class level lock vs Object level lock:

- **Class-level lock:**
  - Manages shared resources that should be accessed serially, ensuring only one thread can access them at a time.
  - Every class has a unique lock, referred to as a class level lock. Generally used when one wants to prevent multiple threads from entering a synchronized block. 
  - Obtained by using synchronized (ClassName.class) { ... }.
- **Object-level lock:**
  - Ensures synchronization for operations specific to an instance of the class, allowing multiple instances to operate concurrently without interfering with each other.
  - Every object has a unique lock, referred to as an object-level lock. Generally used when one wants to synchronize a non-static method or block so that only the thread will be able to execute the code block on a given instance of the class.
  - Obtained by using, synchronized (objectInstance) { ... }.

```
    
    class Multithreading extends Thread {
    private int x;
    public Multithreading(int x) {
        this.x = x;
    }
    
    public void run() {
         synchronized (Multithreading.class) {
            System.out.println("CLASS Lock Now thread is running " + x);
            try{
                Thread.sleep(5000);
            } catch (InterruptedException e){
                e.printStackTrace();
            }
            System.out.println("Class lock, thread is run is to end " + x);
         }
    }
    public void objectLevelOperation() {
        synchronized (this) {
            // Code synchronized at the object level
            System.out.println("Thread is inside the object-level lock."+ x);
            try {
                Thread.sleep(2000);
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
            System.out.println("Thread is exiting the object-level lock." + x);
        }
    }
  }
  
  class MultithreadingDemo{

    public static void main(String args[]) {
        Multithreading m1 = new Multithreading(5);
        Multithreading m2 = new Multithreading(15);
        m1.start();
        m2.start();
        
        Multithreading m11 = new Multithreading(10);
        Multithreading m22 = new Multithreading(20);
        // Create multiple threads using the same object-level lock
        Thread thread1 = new Thread(() -> m11.objectLevelOperation());
        Thread thread2 = new Thread(() -> m22.objectLevelOperation());
        Thread thread3 = new Thread(() -> m11.objectLevelOperation());

        // Start the threads
        thread1.start();
        thread2.start();
        thread3.start();
    }
 }
```
### User vs Daemon Thread:

| Aspect              | User Thread                     | Daemon Thread                   |
|---------------------|---------------------------------|---------------------------------|
| **JVM Behavior**    | Waits for completion.           | Does not wait for completion.   |
| **Creation**        | Created by the user.            | Created by JVM.                 |
| **Purpose**         | Used for core tasks.             | Used for supporting tasks.      |
| **Priority**        | High-priority, therefore are required for running in the foreground. . | Low-priority, therefore are especially required for supporting background tasks like garbage collection, releasing memory of unused objects, etc. |

- But one can only call the setDaemon() method before start() method otherwise it will definitely throw IllegalThreadStateException.
  
```
public class DaemonThread extends Thread 
{ 
   public DaemonThread(String name){ 
       super(name); 
   } 
   public void run() 
  {
      System.out.println((Thread.currentThread().isDaemon() ? getName() + " is Daemon thread" : getName() + " is User thread"));

  }
   public static void main(String[] args) 
   {  
       DaemonThread t1 = new DaemonThread("t1"); 
       DaemonThread t2 = new DaemonThread("t2"); 
       DaemonThread t3 = new DaemonThread("t3");  
       // Setting user thread t1 to Daemon 
       t1.setDaemon(true);       
       // starting first 2 threads  
       t1.start();  
       t2.start();   
       // Setting user thread t3 to Daemon 
       t3.setDaemon(true);  
       t3.start();         
   }  
}
```
Wait/Notify vs. Thread.sleep():

Wait/Notify:
wait() can be "woken up" by another thread calling notify() or notifyAll() on the same monitor object.
wait() releases the lock and must be called within a synchronized context.
Spurious wakeups may occur, and it's common to use wait() in a loop with a condition check.
Thread.sleep():
sleep() does not release the lock; it simply pauses the thread's execution for a specified time.
Does not require synchronization and can be called from anywhere.
No wake-up mechanism like notify(); the thread resumes execution after the specified sleep duration.

In scenarios where the thread needs to pause without actively participating in synchronization, sleep() is suitable. On the other hand, when synchronization and communication between threads are essential, wait() is the appropriate choice, and it contributes to efficient CPU usage in a multithreaded environment.


**sleep() in Thread Class and wait() in Object Class:**

**sleep():**
   - Used to pause the execution of the current thread for a specified amount of time, introducing delays or pauses.
   - Example:
     ```java
     try {
         Thread.sleep(1000); // Sleep for 1 second
     } catch (InterruptedException e) {
         e.printStackTrace();
     }
     ```
**wait():**
   - Used for inter-thread communication. When a thread calls wait(), it releases the lock and waits until another thread notifies it using `notify()` or `notifyAll()`.
   - Example:
     ```java
     synchronized (someObject) {
         try {
             someObject.wait(); // Wait for notification from another thread
         } catch (InterruptedException e) {
             e.printStackTrace();
         }
     }
     ```

**Thread Class vs. Object Class:**
   - **Thread Class:**
     - Represents individual threads of execution in Java.
     - Provides built-in support for multithreading.
     - Used for thread-specific operations.
   - **Object Class:**
     - Fundamental class in Java; every class is a direct or indirect subclass of Object.
     - Provides basic functionality common to all objects, including synchronization features.

- sleep() in Thread is used for managing thread execution and introducing delays.
- wait() in Object is used for synchronization and inter-thread communication.
- Thread class is specialized for working with threads, while Object class provides fundamental functionality for all objects, including synchronization features, generic object-related operations.
- In scenarios where the thread needs to pause without actively participating in synchronization, sleep() is suitable. On the other hand, when synchronization and communication between threads are essential, wait() is the appropriate choice, and it contributes to efficient CPU usage in a multithreaded environment.

Example: 
```

public class Test {

    private volatile int n = 0;

    public synchronized void up() {
        n++;
        System.out.println("in up " + n);
        this.notify(); // notify waiting threads that n has changed
        System.out.println("notified " + n);
    }

    public synchronized void down() {
        while (n <= 0) {
            try {
                System.out.println("in wait " + n);
                this.wait(); // wait while n <= 0. It is not sufficient to receive a notification and proceed since multiple threads may call down(). Also, the
                             // thread may wake up due to an interrupt, so it is advised putting wait() in a loop.
            } catch (InterruptedException e) {
                e.printStackTrace();
            }
        }
        n--;
        System.out.println(n);
    }
 
public static void main(String[] args) {
        Test t = new Test();

        // Thread to demonstrate down()
        Thread downThread = new Thread(() -> {
            t.down();
        });

        // Thread to demonstrate up()
        Thread upThread = new Thread(() -> {
            t.up();
        });

        // Start both threads
        downThread.start();
        upThread.start();
    }

}
```

### **Volatile: **
  used to modify the value of a variable by different threads. It is also used to make classes thread safe. multiple threads can use a method and instance of the classes at the same time without any problem.

- **Visibility:** Ensures changes made by one thread are immediately visible to all other threads.

- **Atomicity:** Guarantees that reads and writes are atomic, even for long and double variables.

- **No Caching:** Threads always read the variable directly from main memory, preventing visibility issues.

- **Memory Barriers:** Includes memory barriers to ensure certain operations complete before and after accessing the variable.

- **No Mutual Exclusion:** While it ensures visibility and atomicity, it doesn't provide mutual exclusion. It's not a substitute for synchronized blocks for exclusive access to shared resources.


 **Runnable Interface:**
   - **Return Result:** The `run()` method in the `Runnable` interface does not return any result explicitly. It is a `void` method, which means it does not produce a result that can be retrieved.
   - **Throw Exception:** Since the `run()` method does not return any result, it also cannot declare that it throws a checked exception. This is because checked exceptions are associated with the return type of a method. If there is no return type, there is no opportunity to throw a checked exception in the method signature.
```java
   public interface Runnable {
       void run();
   }
```

**Callable Interface:**
   - **Return Result:** The `call()` method in the `Callable` interface returns a result. It is parameterized with a type parameter that represents the type of result it produces.
   - **Throw Exception:** Because `call()` returns a result, it can declare that it may throw checked exceptions. The method signature includes the `throws Exception` clause (or a more specific exception type) to indicate the possibility of throwing an exception.

```java
   public interface Callable<V> {
       V call() throws Exception;
   }
```
### **Thread Pool:**
- A thread pool is a group of pre-instantiated, idle threads which stand ready to be given work. These are preferred over instantiating new threads for each task when there is a large number of short tasks to be done rather than a small number of long ones. This prevents having to incur the overhead of creating a thread a large number of times.

Implementation will vary by environment, you need the following:

    - A way to create threads and hold them in an idle state. This can be accomplished by having each thread wait at a barrier until the pool hands it work. (This could be done with mutexes as well.)
    - A container to store the created threads, such as a queue or any other structure that has a way to add a thread to the pool and pull one out.
    - A standard interface or abstract class for the threads to use in doing work. This might be an abstract class called Task with an execute() method that does the work and then returns.
    - When the thread pool is created, it will either instantiate a certain number of threads to make available or create new ones as needed depending on the needs of the implementation.

- When the pool is handed a Task, it takes a thread from the container (or waits for one to become available if the container is empty), hands it a Task, and meets the barrier. This causes the idle thread to resume execution, invoking the execute() method of the Task it was given. Once execution is complete, the thread hands itself back to the pool to be put into the container for re-use and then meets its barrier, putting itself to sleep until the cycle repeats.

