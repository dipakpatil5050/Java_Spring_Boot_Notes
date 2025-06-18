**Java 8** introduced powerful features that changed the way we write Java code — more **concise**, **functional**, and **streamlined**.

---

## ✅ 1. **Lambda Expressions** (Anonymous functions)

Lambda allows you to **pass behavior (code)** as a method argument.

### 🧠 Syntax:

```java
(parameter) -> expression

// or

(parameter1, parameter2) -> {
    // multiple statements
}
```

### ✅ Example:

```java
// Without lambda
Runnable r1 = new Runnable() {
    public void run() {
        System.out.println("Running thread...");
    }
};
r1.run();

// With lambda
Runnable r2 = () -> System.out.println("Running thread using Lambda!");
r2.run();
```

---

## ✅ 2. **Functional Interfaces**

A **Functional Interface** has exactly **one abstract method**.

> You can annotate it with `@FunctionalInterface` (optional but recommended)

### ✅ Example:

```java
@FunctionalInterface
interface Calculator {
    int operate(int a, int b);
}

public class Test {
    public static void main(String[] args) {
        Calculator add = (a, b) -> a + b;
        Calculator mul = (a, b) -> a * b;

        System.out.println(add.operate(5, 3));  // 8
        System.out.println(mul.operate(5, 3));  // 15
    }
}
```

> Predefined functional interfaces are in `java.util.function` package like:
> ✅ `Predicate<T>`, `Function<T,R>`, `Consumer<T>`, `Supplier<T>`

---

## ✅ 3. **Method Reference**

A short-hand for writing lambda expressions when calling **existing methods**.

### 🧠 Syntax:

```java
ClassName::methodName
```

### ✅ Example:

```java
import java.util.Arrays;

public class MethodRefExample {
    public static void main(String[] args) {
        String[] names = {"Dipak", "Rahul", "Ankit"};
        Arrays.sort(names, String::compareToIgnoreCase); // Method reference
        for (String name : names) {
            System.out.println(name);
        }
    }
}
```

Types of method references:

* `ClassName::staticMethod`
* `object::instanceMethod`
* `ClassName::instanceMethod`

---

## ✅ 4. **Stream API** (💥 Powerful for Collections)

Used to **process collections (List, Set, etc.)** using a **functional style**.

### 🧠 Common Operations:

* `filter()`: filters elements
* `map()`: transforms elements
* `collect()`: collect results
* `forEach()`: loop through elements
* `sorted()`, `distinct()`, `count()`...

### ✅ Example:

```java
import java.util.*;
import java.util.stream.*;

public class StreamExample {
    public static void main(String[] args) {
        List<String> names = Arrays.asList("Rahul", "Dipak", "Raj", "Ram");

        // Filter names starting with R, convert to uppercase and print
        names.stream()
             .filter(name -> name.startsWith("R"))
             .map(String::toUpperCase)
             .forEach(System.out::println);
    }
}
```

### 🧠 Collecting into List

```java
List<Integer> nums = Arrays.asList(1, 2, 3, 4, 5);
List<Integer> squared = nums.stream()
                            .map(n -> n * n)
                            .collect(Collectors.toList());
System.out.println(squared); // [1, 4, 9, 16, 25]
```

---

## ✅ 5. **New Date and Time API (`java.time`)**

Java 8 introduced a **modern date/time** package that is **immutable, thread-safe**, and easy to use.

### 🧠 Key Classes:

* `LocalDate` – only date
* `LocalTime` – only time
* `LocalDateTime` – date + time
* `ZonedDateTime` – with timezone
* `DateTimeFormatter` – format/parse

### ✅ Examples:

```java
import java.time.*;

public class DateExample {
    public static void main(String[] args) {
        LocalDate date = LocalDate.now();
        System.out.println("Date: " + date);

        LocalTime time = LocalTime.now();
        System.out.println("Time: " + time);

        LocalDateTime dt = LocalDateTime.now();
        System.out.println("DateTime: " + dt);
    }
}
```

### ✅ Formatting:

```java
import java.time.format.DateTimeFormatter;

LocalDateTime dt = LocalDateTime.now();
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy HH:mm");
String formatted = dt.format(formatter);
System.out.println("Formatted: " + formatted);
```

---

## 🚀 BONUS: Predefined Functional Interfaces

| Interface       | Description                  | Example                      |
| --------------- | ---------------------------- | ---------------------------- |
| `Predicate<T>`  | returns true/false           | `str -> str.isEmpty()`       |
| `Function<T,R>` | maps input to output         | `x -> x * 2`                 |
| `Consumer<T>`   | performs action on input     | `x -> System.out.println(x)` |
| `Supplier<T>`   | returns result without input | `() -> "Hello"`              |

---

## 🧠 Interview-Friendly Summary

| Feature                  | Use                                      |
| ------------------------ | ---------------------------------------- |
| **Lambda**               | Short function implementation            |
| **Functional Interface** | Used in Lambda expressions               |
| **Method Reference**     | Call existing methods in short syntax    |
| **Stream API**           | Efficient data processing in collections |
| **Date Time API**        | Improved date/time handling              |

---

## ✅ Practice Ideas

1. Filter all even numbers from a list using Stream.
2. Write a lambda that multiplies two integers.
3. Create a functional interface `SayHello` with a method `say()`.
4. Print all `.txt` files in a directory using `File` + Stream API.
5. Parse a date string `"2025-06-16"` into `LocalDate`.

---
