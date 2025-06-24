> Java is a 100% object-oriented language (except for primitives), and mastering OOPs is essential to write real-world applications, especially in frameworks like **Spring Boot**, **Android**, **Maven**, etc.

---

## 🔰 What is OOP?

**Object-Oriented Programming** is a programming paradigm based on the **concept of "objects"** that contain **data (fields/attributes)** and **behavior (methods/functions)**.

---

## 🧱 4 Main Pillars of OOP in Java

| Pillar               | Meaning                                                 |
| -------------------- | ------------------------------------------------------- |
| **1. Encapsulation** | Wrapping data and code together                         |
| **2. Inheritance**   | One class inherits properties of another                |
| **3. Polymorphism**  | Same method behaves differently                         |
| **4. Abstraction**   | Hiding complex details and showing only essential parts |

---

Let’s explore each with **real-world analogies and Java code** ⤵️

---

## 🧩 1. **Encapsulation** – Data Hiding

**✅ Definition**: Binding variables and methods into a single unit (class), and **restricting direct access** to internal data using **getters/setters**.

### 🔐 Real Life:

Your ATM card has a PIN. The machine uses the PIN internally, but you can’t directly see or change it.

### ✅ Example:

```java
public class Employee {
    private String name; // private data

    // Public getter and setter
    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }
}
```

---

## 👨‍👧 2. **Inheritance** – Reusability

**✅ Definition**: One class (**child**) inherits properties and methods from another class (**parent**), avoiding duplicate code.

### 🔐 Real Life:

Son inherits traits from Father (name, height, habits...)

### ✅ Example:

```java
class Animal {
    void sound() {
        System.out.println("Animal makes sound");
    }
}

class Dog extends Animal {
    void bark() {
        System.out.println("Dog barks");
    }
}

public class Test {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.sound();  // Inherited from Animal
        d.bark();   // Own method
    }
}
```

> In Java: `extends` is used for classes and `implements` for interfaces.

---

## 🔁 3. **Polymorphism** – Many Forms

**✅ Definition**: Ability of an object to behave in **different ways** based on context.

### Types:

- **Compile-time Polymorphism** → Method Overloading
- **Runtime Polymorphism** → Method Overriding

---

### ✅ a) **Method Overloading** (Same method name, different parameters)

```java
class Calculator {
    int add(int a, int b) {
        return a + b;
    }

    double add(double a, double b) {
        return a + b;
    }
}
```

---

### ✅ b) **Method Overriding** (Same method name in parent and child)

```java
class Animal {
    void sound() {
        System.out.println("Animal sound");
    }
}

class Dog extends Animal {
    void sound() {
        System.out.println("Dog barks");
    }
}
```

---

### ✅ Polymorphism Example:

```java
Animal a = new Dog(); // Parent reference → Child object
a.sound();  // Dog barks (runtime polymorphism)
```

---

## 🚪 4. **Abstraction** – Hiding Complexity

**✅ Definition**: Showing only **relevant features** and hiding background details.

### 🔐 Real Life:

You drive a car using pedals and steering — you don’t care about how the engine works.

### ✅ Two ways in Java:

1. Using **abstract classes**
2. Using **interfaces**

---

### ✅ a) Abstract Class

```java
abstract class Shape {
    abstract void draw();  // abstract method
}

class Circle extends Shape {
    void draw() {
        System.out.println("Drawing Circle");
    }
}
```

---

### ✅ b) Interface

```java
interface Drawable {
    void draw();
}

class Rectangle implements Drawable {
    public void draw() {
        System.out.println("Drawing Rectangle");
    }
}
```

---

## 💡 Summary Table

| Concept       | Keyword                     | Use                  |
| ------------- | --------------------------- | -------------------- |
| Encapsulation | `private`, `get/set`        | Data hiding          |
| Inheritance   | `extends`, `super`          | Code reuse           |
| Polymorphism  | `overloading`, `overriding` | Flexibility          |
| Abstraction   | `abstract`, `interface`     | Hides internal logic |

---

## 🧠 Bonus: OOP Principles in Real Life (Bank App)

| Feature                                   | OOP Concept   |
| ----------------------------------------- | ------------- |
| Private account balance                   | Encapsulation |
| SavingsAccount extends Account            | Inheritance   |
| Same method for deposit in diff accounts  | Polymorphism  |
| Only show deposit/withdraw, hide DB logic | Abstraction   |

---

## 🛠 Mini Practice Questions

1. Create a `Vehicle` class and `Car` class that inherits from it.
2. Create a class `Calculator` with overloaded `add()` methods.
3. Create an interface `Animal` with method `sound()` and implement it in `Dog`, `Cat`.
4. Demonstrate encapsulation by creating a class `BankAccount` with private balance.



---

   # 4 Pillar of OOPS Short notes

   ## Abstraction:

   - Hide internal details only shows essential data,
   - Simple interface to user without asking for complex details to perform an action
     eg: Drive the car without requiring to understand tiny details of "how does the engine work"
     Advantages: it helps to reduce the operational complexity at the end user.

   ## Inheritance:

   - inherit data from parent class to child class
   - technique of taking properties from another class having features in common.
   - Parent -> Child -> is-a Relationship => child is a type of parent
     eg: Vehicle -> Car

   Advantages:

   - reusability and reduce duplication of code

   ## Encapsulation:

   - use for Security and restriction to user from directly modify the data member or variables of class to maintain the integrity of the data.
   - Restrict the access
     eg: integrity data in is not compromised

   ## Polymorphism:

   - poly -> multiple, Morphy -> Form
   - perform action in multiple or different ways
   - one Entity with many forms
   - can reuse the code via Polymorphism

   eg:

   1. Lord Vishnu -> has many -> avatar
   2. women -> can be => mother -> sister -> Wife -> grandmother

---
