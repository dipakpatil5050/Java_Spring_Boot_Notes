# Java_Spring_Boot_Notes





---

## ✅ What is Exception Handling?

**Exception Handling** is a mechanism in Java to **handle runtime errors** (exceptions) so the normal flow of the program is not disrupted.

🧠 Think of it as a **safety net** — when your code hits a problem (e.g., divide by 0), instead of crashing, Java lets you **handle it gracefully**.

---

## ⚠️ What is an Exception?

An **exception** is an **unexpected event** that occurs during program execution and disrupts the normal flow.

🧩 Example:

```java
int a = 5 / 0; // Throws ArithmeticException
```

---

## 🧰 Java Exception Hierarchy

```
        Throwable
         /     \
   Exception   Error
      |
Checked / Unchecked
```

| Type                    | Examples                                  | Description                 |
| ----------------------- | ----------------------------------------- | --------------------------- |
| **Checked Exception**   | IOException, SQLException                 | Handled during compile time |
| **Unchecked Exception** | NullPointerException, ArithmeticException | Occur at runtime            |

---

## 🛡️ Try-Catch Block

### 📌 Syntax:

```java
try {
    // Code that may throw an exception
} catch (ExceptionType e) {
    // Code to handle exception
}
```

### ✅ Example:

```java
public class TryCatchExample {
    public static void main(String[] args) {
        try {
            int a = 5 / 0; // risky
        } catch (ArithmeticException e) {
            System.out.println("Can't divide by zero!");
        }
    }
}
```

---

## 🔁 Try-Catch-Finally Block

* `finally` block **always runs** whether exception is thrown or not.
* Used to **close resources** (files, DB connection, etc.)

```java
try {
    int[] arr = {1, 2, 3};
    System.out.println(arr[5]); // Exception
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Invalid index!");
} finally {
    System.out.println("Always runs - clean up");
}
```

---

## 🔃 Multiple Catch Blocks

Catch multiple exception types separately.

```java
try {
    String s = null;
    System.out.println(s.length());
} catch (ArithmeticException e) {
    System.out.println("Math error");
} catch (NullPointerException e) {
    System.out.println("Null error");
}
```

---

## 🎯 Catching Multiple Exceptions in One Block (Java 7+)

```java
try {
    // code
} catch (IOException | SQLException e) {
    System.out.println("Either IO or SQL Exception occurred");
}
```

---

## 🎯 Throwing Exceptions

You can **manually throw** exceptions using `throw`.

```java
public class ThrowExample {
    public static void main(String[] args) {
        int age = 15;
        if (age < 18) {
            throw new ArithmeticException("You are not eligible");
        }
    }
}
```

---

## 🧾 `throws` Keyword

Used when a method might **throw a checked exception**, and you want to declare it.

```java
public void readFile() throws IOException {
    FileReader file = new FileReader("file.txt");
}
```

---

## 💡 Custom Exception

You can create your own exception class.

```java
class MyException extends Exception {
    public MyException(String msg) {
        super(msg);
    }
}

public class TestCustom {
    public static void main(String[] args) throws MyException {
        int num = -5;
        if (num < 0)
            throw new MyException("Negative number not allowed");
    }
}
```

---

## 🧪 Real-World Use Case

```java
public class LoginSystem {
    public static void main(String[] args) {
        String username = null;
        try {
            if (username == null) {
                throw new NullPointerException("Username can't be null");
            }
            System.out.println("Welcome, " + username);
        } catch (NullPointerException e) {
            System.out.println("Please enter your username");
        }
    }
}
```

---

## 📌 Summary Table

| Keyword   | Description                                   |
| --------- | --------------------------------------------- |
| `try`     | Code that may throw exception                 |
| `catch`   | Handles the exception                         |
| `finally` | Executes always                               |
| `throw`   | Manually throw exception                      |
| `throws`  | Declares an exception that a method can throw |

---

## 💻 Practice Task for You

1. Write a program to handle:

   * Divide by zero
   * NullPointerException
   * FileNotFoundException using `throws`
2. Create a custom exception class for “Invalid Age”

---
