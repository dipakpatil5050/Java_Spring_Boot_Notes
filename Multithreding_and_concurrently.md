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

# v2

Absolutely! You're right — **Multithreading, lifecycle, synchronization, `wait()`/`notify()`** can feel tricky at first, but I’ll explain it in a **super easy, real-life relatable** way using simple words and examples.

Let’s go step by step 🔄

---

## 🧵 What is Multithreading (Quick Recap)?

- A **thread** is a small unit of a program that runs **independently**.
- **Multithreading** = running **multiple threads** in a single program.

🧠 **Real-life example**:
Think of your browser — one tab is loading YouTube, another is playing music, and another one is downloading a file. All at the same time.

---

## 🔄 Thread Life Cycle (Easy Understanding)

A thread goes through different **stages of life**:

```
New → Runnable → Running → Blocked/Waiting → Terminated
```

### ✅ 1. **New**

Thread is created but not started yet.

```java
Thread t = new Thread();
```

### ✅ 2. **Runnable**

Thread is ready to run but **waiting for CPU**.

```java
t.start();  // moves to Runnable state
```

### ✅ 3. **Running**

CPU picks the thread to run.

### ✅ 4. **Waiting/Blocked**

Thread waits for some time or resource (e.g., `sleep()`, `wait()`)

### ✅ 5. **Terminated**

Thread has finished or is stopped.

---

## 🔐 Synchronization (Solving Data Problems in Threads)

**Problem:**
When **2 threads change the same data at the same time**, data becomes **wrong** (race condition).

### 🧠 Real-life example:

Two people updating the same Excel file at the same time — changes may be lost or corrupted.

### ✅ Solution: Use `synchronized`

It locks a method or block so that **only one thread** can use it at a time.

---

### 🔧 Example Without Synchronization (Problem):

```java
class Counter {
    int count = 0;

    public void increment() {
        count++;
    }
}
```

2 threads incrementing at the same time might cause `count` to be wrong.

---

### ✅ With Synchronization (Solution):

```java
class Counter {
    int count = 0;

    public synchronized void increment() {
        count++;
    }
}
```

Now, only **one thread at a time** can access `increment()`.

---

## 🧘 wait(), notify(), and notifyAll()

### 🔍 Purpose:

Used for **communication between threads** (called **Inter-thread communication**).

---

### 🧠 Real-life Example:

Imagine a restaurant:

- **Customer**: Orders food and waits.
- **Cook**: Prepares food and notifies the customer.

We can simulate this using `wait()` and `notify()`.

---

### ✅ Key Concepts:

- `wait()` → Thread goes to waiting state and **releases the lock**.
- `notify()` → Wakes up **one** waiting thread.
- `notifyAll()` → Wakes up **all** waiting threads.
- Must be used **inside synchronized block**.

---

### 🔧 Easy Example:

```java
class Restaurant {
    boolean foodReady = false;

    synchronized void orderFood() {
        System.out.println("Customer: Waiting for food...");
        while (!foodReady) {
            try {
                wait();
            } catch (Exception e) {}
        }
        System.out.println("Customer: Got the food! Eating...");
    }

    synchronized void prepareFood() {
        System.out.println("Cook: Preparing food...");
        foodReady = true;
        notify();  // notify customer
    }
}
```

### ✅ Running both threads:

```java
public class Main {
    public static void main(String[] args) {
        Restaurant restaurant = new Restaurant();

        Thread customer = new Thread(() -> restaurant.orderFood());
        Thread cook = new Thread(() -> restaurant.prepareFood());

        customer.start();
        try { Thread.sleep(1000); } catch (Exception e) {}
        cook.start();
    }
}
```

> Output:

```
Customer: Waiting for food...
Cook: Preparing food...
Customer: Got the food! Eating...
```

---

## 🔂 Summary Table

| Concept         | Meaning                       | Keyword                        |
| --------------- | ----------------------------- | ------------------------------ |
| Create thread   | Run code in parallel          | `Thread`, `Runnable`           |
| Lifecycle       | Thread states                 | `start()`, `sleep()`, `join()` |
| Synchronization | Prevent data conflict         | `synchronized`                 |
| wait()          | Pause thread and release lock | `wait()`                       |
| notify()        | Wake one waiting thread       | `notify()`                     |
| notifyAll()     | Wake all waiting threads      | `notifyAll()`                  |

---
