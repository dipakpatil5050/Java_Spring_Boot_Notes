Let's learn! **Generics in Java** from **basic to advanced**, in the **simplest way**, with clear examples. This is a **core Java concept**, especially useful for building **type-safe and reusable code**.

---

## 🧠 What are Generics?

**Generics** allow you to write **a class, interface, or method** that works with **different data types** — while still maintaining **compile-time type safety**.

---

## ✅ Why Use Generics?

1. ✅ **Type Safety** – Catch errors at compile-time instead of runtime.
2. ✅ **Code Reusability** – Same class or method works for different types.
3. ✅ **Avoid Type Casting** – No need for manual casting.
4. ✅ **Cleaner Code** – More readable and maintainable.

---

## 🧩 Without Generics Example (Old Java)

```java
List names = new ArrayList();  // no type defined
names.add("Dipak");
names.add(123);  // no error, even though it's a number

String name = (String) names.get(0);  // requires casting
```

> Problem: Can add any type, and must use casting

---

## 🧩 With Generics Example

```java
List<String> names = new ArrayList<>();
names.add("Dipak");
// names.add(123); // ❌ Compile-time error

String name = names.get(0);  // ✅ No casting required
```

> ✅ Safer, no runtime error, no casting needed.

---

## ✅ Generic Class Example

```java
// T is a Type Parameter
class Box<T> {
    T value;

    public void setValue(T val) {
        value = val;
    }

    public T getValue() {
        return value;
    }
}
```

### ✅ Usage:

```java
Box<String> strBox = new Box<>();
strBox.setValue("Hello");
System.out.println(strBox.getValue());

Box<Integer> intBox = new Box<>();
intBox.setValue(123);
System.out.println(intBox.getValue());
```

---

## ✅ Generic Method Example

```java
public class Utils {
    public static <T> void printArray(T[] arr) {
        for (T element : arr) {
            System.out.println(element);
        }
    }

    public static void main(String[] args) {
        String[] names = {"A", "B", "C"};
        Integer[] nums = {1, 2, 3};

        printArray(names);
        printArray(nums);
    }
}
```

---

## ✅ Bounded Type (Generics with extends)

Used to restrict the types that can be passed.

```java
class MathUtil<T extends Number> {
    public void showDoubleValue(T value) {
        System.out.println(value.doubleValue());
    }
}
```

### ✅ Usage:

```java
MathUtil<Integer> m1 = new MathUtil<>();
m1.showDoubleValue(10);

MathUtil<Double> m2 = new MathUtil<>();
m2.showDoubleValue(5.5);

// MathUtil<String> m3 = new MathUtil<>(); // ❌ Error
```

---

## ✅ Generic Interface Example

```java
interface Printer<T> {
    void print(T item);
}

class StringPrinter implements Printer<String> {
    public void print(String item) {
        System.out.println("Printing: " + item);
    }
}
```

---

## ✅ Wildcards in Generics

Used when you don’t know the exact type.

### `<?>` – Unknown type

```java
public void printList(List<?> list) {
    for (Object obj : list) {
        System.out.println(obj);
    }
}
```

### `<? extends T>` – Any class that is subclass of T

```java
public void printNumbers(List<? extends Number> list) {
    for (Number n : list) {
        System.out.println(n);
    }
}
```

### `<? super T>` – Any class that is superclass of T

```java
public void addNumbers(List<? super Integer> list) {
    list.add(1);
    list.add(2);
}
```

---

## 🚀 Real World Use in Java Collection Framework

All collections use generics:

```java
List<String> list = new ArrayList<>();
Map<String, Integer> map = new HashMap<>();
```

## 🧩 With and Without Generics

![image](https://github.com/user-attachments/assets/ca18f432-b134-4369-93db-5ef67e041a43)


---

## 📌 Summary Table

| Concept        | Description                | Example                 |
| -------------- | -------------------------- | ----------------------- |
| Generic Class  | Class with type parameter  | `class Box<T>`          |
| Generic Method | Method with type parameter | `<T> void print(T val)` |
| Bounded Types  | Restrict to certain types  | `<T extends Number>`    |
| Wildcards      | Unknown types              | `<?>`, `<? extends T>`  |

---

## 🧪 Practice Task for You

1. Create a `GenericBox<T>` class that stores any value.
2. Write a method that takes `List<? extends Number>` and prints the average.
3. Create a generic method `swapElements` that swaps two items in an array.

---
