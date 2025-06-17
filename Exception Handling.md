# Java_Spring_Boot_Notes

---

## ✅ What is Exception Handling?

**Exception Handling** is a mechanism in Java to **handle runtime errors** (exceptions) so the normal flow of the program is not disrupted.

🧠 Think of it as a **safety net** — when your code hits a problem (e.g., divide by 0), instead of crashing, Java lets you **handle it gracefully**.

---

## ⚠️ What is an Exception?

An **exception** is an **unexpected event** that occurs during program execution and disrupts the normal flow.

---

## Exception Types :

### 1. Checked Exception:

These are exceptions that are checked at compile-time. They must be either caught or declared in the method signature using the `throws` keyword. Examples include `IOException`, `SQLException`, ClassNOt FoundException, etc.

### 2. Unchecked Exception:

These are exceptions that are not checked at compile-time. They are subclasses of `RuntimeException` and do not need to be declared or caught. Examples include `ArithmaticException`, `NullPointerException`, `NumberFormat Exception`, `ArrayIndexOutOfBoundsException`, etc.

---

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

- `finally` block **always runs** whether exception is thrown or not.
- Used to **close resources** (files, DB connection, etc.)

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

## Exception Chart

![image](https://github.com/user-attachments/assets/3c96a854-6dca-4c96-b9ae-a39d7426daf9)

### Important keywords in Exception Handling:

### 1. try:

This block contains code that might throw an exception. If an exception occurs, the control is transferred to the catch block.

### 2. catch:

This block is used to handle exceptions that occur in the try block.

### 3. finally:

This block is optional and is always executed after the try-catch blocks, regardless of whether an exception was thrown or caught. It is typically used for cleanup operations, such as closing resources.

### 4. throw:

This keyword is used to explicitly throw an exception.

### 5. throws:

This keyword is used in method signatures to declare that a method can throw a specific exception. It allows the caller of the method to handle the exception.

### 6. try-with-resources:

This is a feature introduced in Java 7 that

allows automatic resource management. It ensures that resources like files or database connections are closed automatically when they are no longer needed, even if an exception occurs.

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

## Example 1:

```java
package Exception_Handling;

import java.util.Scanner;


public class Test {


    public static void main(String[] args) {


        try {

            Scanner sc = new Scanner(System.in);
            System.out.print("Enter a divident (non-negative): ");
            int divident = sc.nextInt();

            System.out.print("Enter a diviser: ");
            int diviser = sc.nextInt();


            int result  = divident / diviser;
            sc.close();
            System.out.println("Result: " + result);

        } catch (ArithmeticException e) {
            System.out.println("Can't devide by Zero");
        }

    }



}


```

## Example 2 :

Multiple exception

```java

package Exception_Handling;



public class Test {


    public static void main(String[] args) {

        int arr[] = new int[5];
        try {
            arr[60] = 60/0;
        } catch (ArithmeticException | ArrayIndexOutOfBoundsException e) {
            System.out.println(e.getMessage());
        }

    }


}
```

## Example 3 : Throw

```java

import java.util.Scanner;

public class Main {
    public static void main(String[] args) {




        Scanner sc =new Scanner(System.in);
        System.out.println("Enter a Age: ");
        int age = sc.nextInt();
        sc.close();


        if (age < 18) {

            throw new RuntimeException("Sorry you can't Vote");
        }
        else{
            System.out.println("Age is greater than 18 so you can Vote");
        }



    }
}




```

## Example 4 : Throws

```java


import java.util.Scanner;

public class Main {



    public static void DivisionDemo(int dividend, int divisor) throws ArithmeticException{
        System.out.println("The result is : "+ dividend / divisor );
    }

    public static void main(String[] args) {
        DivisionDemo(10,0);
    }
}

```

## 💻 Practice Task for You

1. Write a program to handle:

   - Divide by zero
   - NullPointerException
   - FileNotFoundException using `throws`

2. Create a custom exception class for “Invalid Age”

---
