Let's now dive into **I/O (Input/Output) and File Handling in Java**, explained from **basic to advanced**, with **real examples** and use cases.

---

## 📘 What is Java I/O?

Java I/O (Input/Output) is used to **read data from** and **write data to**:

- Files
- Input devices (keyboard)
- Output devices (console, file, etc.)

Java provides the `java.io` and `java.nio` packages to handle I/O operations.

---

## 🔑 Core Concepts

| Concept                      | Use                                 |
| ---------------------------- | ----------------------------------- |
| **Streams**                  | Read/write sequence of data         |
| **Reader/Writer**            | For **character** data (text)       |
| **InputStream/OutputStream** | For **binary** data (images, files) |
| **File** class               | To manage file and directory paths  |

---

## 🔁 Java I/O Types

### 1. **Byte Streams** (`InputStream`, `OutputStream`)

- For binary files: images, videos, etc.

### 2. **Character Streams** (`Reader`, `Writer`)

- For text data: `.txt`, `.csv`, etc.

---

## 📂 File Handling in Java (with `java.io.File`)

### ✅ Create a File

```java
import java.io.File;

public class CreateFile {
    public static void main(String[] args) {
        File file = new File("test.txt");

        try {
            if (file.createNewFile()) {
                System.out.println("File created: " + file.getName());
            } else {
                System.out.println("File already exists.");
            }
        } catch (Exception e) {
            e.printStackTrace();
        }
    }
}
```

---

## 📝 Write to File

### ✅ Using `FileWriter`

```java
import java.io.FileWriter;
import java.io.IOException;

public class WriteFile {
    public static void main(String[] args) {
        try {
            FileWriter writer = new FileWriter("test.txt");
            writer.write("Hello Dipak!\nWelcome to File Handling.");
            writer.close();
            System.out.println("Successfully written to file.");
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## 📖 Read from File

### ✅ Using `FileReader`

```java
import java.io.FileReader;
import java.io.IOException;

public class ReadFile {
    public static void main(String[] args) {
        try {
            FileReader reader = new FileReader("test.txt");
            int ch;
            while ((ch = reader.read()) != -1) {
                System.out.print((char) ch);
            }
            reader.close();
        } catch (IOException e) {
            e.printStackTrace();
        }
    }
}
```

---

## ✅ Read Line by Line using `BufferedReader`

```java
import java.io.BufferedReader;
import java.io.FileReader;

public class BufferedRead {
    public static void main(String[] args) throws Exception {
        BufferedReader br = new BufferedReader(new FileReader("test.txt"));
        String line;
        while ((line = br.readLine()) != null) {
            System.out.println(line);
        }
        br.close();
    }
}
```

---

## 📤 Append to File

```java
FileWriter writer = new FileWriter("test.txt", true); // true = append mode
writer.write("\nAppended line!");
writer.close();
```

---

## ❌ Delete File

```java
File file = new File("test.txt");
if (file.delete()) {
    System.out.println("Deleted: " + file.getName());
} else {
    System.out.println("Failed to delete the file.");
}
```

---

## 🧪 Copy File using Streams

```java
import java.io.*;

public class CopyFile {
    public static void main(String[] args) throws IOException {
        FileInputStream in = new FileInputStream("source.txt");
        FileOutputStream out = new FileOutputStream("destination.txt");

        int ch;
        while ((ch = in.read()) != -1) {
            out.write(ch);
        }

        in.close();
        out.close();

        System.out.println("File copied.");
    }
}
```

---

## 🧰 Java NIO (New I/O) - Easy File Read/Write

```java
import java.nio.file.*;
import java.io.IOException;

public class NIOExample {
    public static void main(String[] args) throws IOException {
        Path path = Paths.get("nio.txt");

        // Write
        Files.write(path, "Hello from NIO!".getBytes());

        // Read
        String content = Files.readString(path);
        System.out.println(content);
    }
}
```

---

## 📌 Summary Table

| Task                     | Class                             |
| ------------------------ | --------------------------------- |
| Create/Check/Delete file | `File`                            |
| Write to file            | `FileWriter`, `BufferedWriter`    |
| Read from file           | `FileReader`, `BufferedReader`    |
| Binary file operations   | `InputStream`, `OutputStream`     |
| Line/Word/File reading   | `Scanner`, `Files.readAllLines()` |
| High-performance I/O     | Java NIO (`Path`, `Files`)        |

---

## 🎯 Real-world Use Cases

| Scenario             | What to Use                    |
| -------------------- | ------------------------------ |
| Logging              | `BufferedWriter`, `FileWriter` |
| Config file read     | `FileReader`, `BufferedReader` |
| Upload/download file | `InputStream`, `OutputStream`  |
| CSV Processing       | `Scanner`, `BufferedReader`    |
| Fast text read/write | Java NIO (`Files.readString`)  |

---
