# 📘 CHAPTER 10: MULTITHREADING

---

## 10.1 What is Multithreading?

Running **multiple threads simultaneously** within a single program. Each thread is an independent path of execution.

```
Process (your Java program)
├── Thread-1 (main)
├── Thread-2 (background task)
└── Thread-3 (another task)
```

**Why use?** → Better performance, responsive UI, efficient CPU usage.

---

## 10.2 Creating Threads

### Method 1: Extend Thread class
```java
class MyThread extends Thread {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
            try { Thread.sleep(500); } catch (InterruptedException e) { }
        }
    }
}

public class Main {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        MyThread t2 = new MyThread();
        t1.setName("Thread-A");
        t2.setName("Thread-B");
        t1.start();  // start() creates a new thread
        t2.start();  // Both run simultaneously!
    }
}
```

### Method 2: Implement Runnable interface (Preferred)
```java
class MyTask implements Runnable {
    @Override
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(Thread.currentThread().getName() + " - " + i);
        }
    }
}

public class Main {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyTask(), "Worker-1");
        Thread t2 = new Thread(new MyTask(), "Worker-2");
        t1.start();
        t2.start();
    }
}
```

### Method 3: Lambda (simplest)
```java
Thread t = new Thread(() -> {
    System.out.println("Running in: " + Thread.currentThread().getName());
});
t.start();
```

---

## 10.3 Thread Lifecycle

```
NEW → RUNNABLE → RUNNING → (BLOCKED/WAITING/TIMED_WAITING) → TERMINATED
```

| State | Description |
|-------|-------------|
| NEW | Thread created, not yet started |
| RUNNABLE | Ready to run, waiting for CPU |
| RUNNING | Currently executing |
| BLOCKED | Waiting for a lock |
| WAITING | Waiting indefinitely (wait()) |
| TIMED_WAITING | Waiting for a time (sleep()) |
| TERMINATED | Finished execution |

---

## 10.4 Thread Methods

```java
Thread t = new Thread(() -> { });

t.start();                        // Start thread
t.setName("MyThread");            // Set name
t.getName();                      // Get name
t.setPriority(Thread.MAX_PRIORITY); // 1-10 (default 5)
t.isAlive();                      // Is thread running?
Thread.currentThread();           // Get current thread
Thread.sleep(1000);               // Pause for 1 second
t.join();                         // Wait for thread to finish
t.setDaemon(true);                // Set as daemon thread
```

### join() – Wait for thread to finish
```java
Thread t1 = new Thread(() -> {
    for (int i = 1; i <= 3; i++) {
        System.out.println("Thread 1: " + i);
    }
});

t1.start();
t1.join();  // Main thread waits here until t1 finishes

System.out.println("Thread 1 finished. Main continues.");
```

---

## 10.5 Synchronization (Thread Safety)

When multiple threads access shared data, results can be **unpredictable**. Use `synchronized`.

### Without Synchronization (PROBLEM)
```java
class Counter {
    int count = 0;
    void increment() {
        count++;  // Not atomic! Race condition!
    }
}
```

### With Synchronization (SOLUTION)
```java
class Counter {
    int count = 0;

    // Only one thread can execute this at a time
    synchronized void increment() {
        count++;
    }
}

public class Main {
    public static void main(String[] args) throws InterruptedException {
        Counter counter = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });
        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) counter.increment();
        });

        t1.start();
        t2.start();
        t1.join();
        t2.join();

        System.out.println("Count: " + counter.count);  // Always 2000
    }
}
```

### Synchronized Block (more fine-grained)
```java
void addItem(String item) {
    synchronized (this) {
        list.add(item);
    }
}
```

---

## 10.6 Inter-Thread Communication (wait, notify)

```java
class SharedResource {
    int data;
    boolean hasData = false;

    synchronized void produce(int value) throws InterruptedException {
        while (hasData) {
            wait();  // wait until consumer consumes
        }
        data = value;
        hasData = true;
        System.out.println("Produced: " + value);
        notify();  // wake up consumer
    }

    synchronized int consume() throws InterruptedException {
        while (!hasData) {
            wait();  // wait until producer produces
        }
        hasData = false;
        System.out.println("Consumed: " + data);
        notify();  // wake up producer
        return data;
    }
}
```

---

## 10.7 ExecutorService (Thread Pool)

Better way to manage threads — reuses threads instead of creating new ones.

```java
import java.util.concurrent.*;

public class ExecutorDemo {
    public static void main(String[] args) {
        // Create pool of 3 threads
        ExecutorService executor = Executors.newFixedThreadPool(3);

        for (int i = 1; i <= 5; i++) {
            final int taskId = i;
            executor.submit(() -> {
                System.out.println("Task " + taskId + " by " +
                    Thread.currentThread().getName());
            });
        }

        executor.shutdown();  // no new tasks, finish existing
    }
}
```

### Callable + Future (Thread that returns a result)
```java
ExecutorService executor = Executors.newSingleThreadExecutor();

Future<Integer> future = executor.submit(() -> {
    Thread.sleep(2000);
    return 42;
});

System.out.println("Doing other work...");
Integer result = future.get();  // blocks until result is ready
System.out.println("Result: " + result);  // 42

executor.shutdown();
```

---

## 🔥 Interview Questions – Multithreading

**Q1: Difference between `start()` and `run()`?**
> - `start()` creates a new thread and calls `run()` in that thread
> - `run()` called directly executes in the current thread (no new thread)

**Q2: Difference between `Thread` class and `Runnable` interface?**
> - Thread: can't extend another class (single inheritance)
> - Runnable: can extend another class + implement Runnable (preferred)

**Q3: What is a daemon thread?**
> A background thread (e.g., garbage collector). JVM exits when only daemon threads remain. Set with `t.setDaemon(true)`.

**Q4: What is a race condition?**
> When multiple threads access shared data simultaneously, causing unpredictable results.

**Q5: What is deadlock?**
> Two or more threads waiting for each other to release locks, causing infinite waiting.

**Q6: Difference between `wait()` and `sleep()`?**
> - `wait()`: releases lock, called on object, used for inter-thread communication
> - `sleep()`: doesn't release lock, called on Thread class, just pauses

**Q7: What is `volatile` keyword?**
> Ensures a variable is always read from **main memory** (not thread cache). Guarantees visibility but not atomicity.

**Q8: What is `ThreadLocal`?**
> Provides thread-local variables — each thread has its own copy.

---
