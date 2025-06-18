## Let’s now explore **Multithreading and Concurrency in Java** — a super important topic for writing efficient and parallel applications.

## 🔰 What is Multithreading?

**Multithreading** is the ability of a program to execute **multiple threads** (lightweight sub-processes) **concurrently**.

🧠 Example Use Cases:

- Running background tasks
- Handling multiple client requests (like in web servers)
- Animations in games or apps
- File downloading and processing at the same time

---

## 🧵 What is a Thread?

A **Thread** is a single unit of execution inside a process.

> One Java program (process) can have multiple threads.

---

## 🛠 Ways to Create Threads in Java

### ✅ 1. **By extending `Thread` class**

```java
class MyThread extends Thread {
    public void run() {
        System.out.println("Thread is running...");
    }
}

public class Test {
    public static void main(String[] args) {
        MyThread t1 = new MyThread();
        t1.start();  // starts the thread
    }
}
```

---

### ✅ 2. **By implementing `Runnable` interface**

```java
class MyRunnable implements Runnable {
    public void run() {
        System.out.println("Thread using Runnable...");
    }
}

public class Test {
    public static void main(String[] args) {
        Thread t1 = new Thread(new MyRunnable());
        t1.start();
    }
}
```

> **Runnable** is preferred in real-world apps because Java supports **multiple interface inheritance**, but not multiple class inheritance.

---

### ✅ 3. **Using Lambda (Java 8)**

```java
public class Test {
    public static void main(String[] args) {
        Runnable r = () -> System.out.println("Thread using lambda!");
        new Thread(r).start();
    }
}
```

---

## ⏳ Thread Lifecycle

A thread goes through several stages:

```
New → Runnable → Running → (Blocked/Waiting) → Terminated
```

---

## ⚙️ Common Thread Methods

| Method      | Description                                            |
| ----------- | ------------------------------------------------------ |
| `start()`   | Starts the thread                                      |
| `run()`     | Executes the task (don’t call directly, use `start()`) |
| `sleep(ms)` | Pauses thread for milliseconds                         |
| `join()`    | Waits for another thread to die                        |
| `isAlive()` | Checks if thread is still running                      |

---

## 🧠 Example: Sleep & Join

```java
class MyThread extends Thread {
    public void run() {
        for (int i = 1; i <= 5; i++) {
            System.out.println(i);
            try {
                Thread.sleep(1000);  // 1 second delay
            } catch (InterruptedException e) {
                System.out.println(e);
            }
        }
    }
}

public class Test {
    public static void main(String[] args) throws InterruptedException {
        MyThread t1 = new MyThread();
        t1.start();
        t1.join(); // Wait for t1 to finish before continuing
        System.out.println("Main thread ends.");
    }
}
```

---

## 🔄 Concurrency vs Parallelism

| Concept         | Meaning                                                              |
| --------------- | -------------------------------------------------------------------- |
| **Concurrency** | Tasks appear to run at the same time (interleaved execution)         |
| **Parallelism** | Tasks run **exactly at the same time** using **multiple CPUs/cores** |

---

## ⚠️ Synchronization in Java

When **multiple threads access shared data**, it may cause **inconsistency** (Race Conditions).

✅ Solution: Use `synchronized` keyword.

### 🔐 Example:

```java
class Counter {
    int count = 0;

    public synchronized void increment() {
        count++;
    }
}

public class SyncExample {
    public static void main(String[] args) throws Exception {
        Counter c = new Counter();

        Thread t1 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) c.increment();
        });

        Thread t2 = new Thread(() -> {
            for (int i = 0; i < 1000; i++) c.increment();
        });

        t1.start(); t2.start();
        t1.join(); t2.join();

        System.out.println("Count: " + c.count);  // Expected: 2000
    }
}
```

---

## 🧰 Thread Pooling (ExecutorService)

Instead of creating new threads every time, use a **Thread Pool**.

```java
import java.util.concurrent.*;

public class ThreadPoolExample {
    public static void main(String[] args) {
        ExecutorService executor = Executors.newFixedThreadPool(3);

        Runnable task = () -> System.out.println("Task executed by: " + Thread.currentThread().getName());

        for (int i = 0; i < 5; i++) {
            executor.submit(task);
        }

        executor.shutdown();
    }
}
```

---

## 🧠 Advanced Java Concurrency Tools (from `java.util.concurrent`)

| Tool                | Use                                          |
| ------------------- | -------------------------------------------- |
| `ExecutorService`   | Manages thread pool                          |
| `Future`            | Holds result of async computation            |
| `CountDownLatch`    | Wait for threads to finish                   |
| `Semaphore`         | Limit number of threads accessing a resource |
| `ReentrantLock`     | Advanced lock mechanism                      |
| `ConcurrentHashMap` | Thread-safe map                              |
| `AtomicInteger`     | Thread-safe integer increment                |

---

## ✅ Best Practices

- Use **synchronized** carefully – can cause **deadlocks**
- Use **thread pool** for better performance
- Don’t use `Thread.sleep()` in production logic
- Always call `.join()` when you want to wait for thread completion
- Prefer `ExecutorService` over manually creating threads

---

## 🔚 Summary Table

| Concept             | Keyword/API                        | Use                  |
| ------------------- | ---------------------------------- | -------------------- |
| Create thread       | `Thread`, `Runnable`, Lambda       | Run background tasks |
| Thread safety       | `synchronized`, `Atomic*`, `Locks` | Avoid data issues    |
| Concurrency utils   | `ExecutorService`, `Future`        | Manage async tasks   |
| Thread coordination | `join()`, `wait()/notify()`        | Sync threads         |

---
