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









