# 📘 CHAPTER 11: FILE I/O (Input/Output)

---

## 11.1 File Class

```java
import java.io.File;

File file = new File("test.txt");

System.out.println(file.exists());        // false
System.out.println(file.getName());       // test.txt
System.out.println(file.getAbsolutePath());
System.out.println(file.isFile());        // true/false
System.out.println(file.isDirectory());   // true/false
System.out.println(file.length());        // size in bytes

// Create file
file.createNewFile();

// Create directory
File dir = new File("myFolder");
dir.mkdir();

// Delete
file.delete();

// List files in a directory
File folder = new File(".");
String[] files = folder.list();
for (String f : files) {
    System.out.println(f);
}
```

---

## 11.2 Writing to a File

### Using FileWriter
```java
import java.io.FileWriter;
import java.io.IOException;

try (FileWriter writer = new FileWriter("output.txt")) {
    writer.write("Hello, World!\n");
    writer.write("Learning Java File I/O\n");
    System.out.println("File written successfully!");
} catch (IOException e) {
    e.printStackTrace();
}
```

### Using BufferedWriter (more efficient)
```java
import java.io.*;

try (BufferedWriter bw = new BufferedWriter(new FileWriter("output.txt"))) {
    bw.write("Line 1");
    bw.newLine();
    bw.write("Line 2");
    bw.newLine();
    bw.write("Line 3");
}
```

### Using PrintWriter
```java
import java.io.PrintWriter;

try (PrintWriter pw = new PrintWriter("output.txt")) {
    pw.println("Line 1");
    pw.println("Line 2");
    pw.printf("Name: %s, Age: %d%n", "Rahul", 25);
}
```

---

## 11.3 Reading from a File

### Using BufferedReader
```java
import java.io.*;

try (BufferedReader br = new BufferedReader(new FileReader("output.txt"))) {
    String line;
    while ((line = br.readLine()) != null) {
        System.out.println(line);
    }
} catch (IOException e) {
    e.printStackTrace();
}
```

### Using Scanner
```java
import java.io.File;
import java.util.Scanner;

try (Scanner sc = new Scanner(new File("output.txt"))) {
    while (sc.hasNextLine()) {
        System.out.println(sc.nextLine());
    }
} catch (Exception e) {
    e.printStackTrace();
}
```

### Using Files class (Java 7+)
```java
import java.nio.file.*;
import java.util.List;

// Read all lines
List<String> lines = Files.readAllLines(Paths.get("output.txt"));
lines.forEach(System.out::println);

// Read as single string
String content = Files.readString(Path.of("output.txt"));  // Java 11+

// Write
Files.writeString(Path.of("output.txt"), "Hello World");   // Java 11+
```

---

## 11.4 Serialization (Convert Object to File)

```java
import java.io.*;

class Student implements Serializable {
    private static final long serialVersionUID = 1L;
    String name;
    int age;
    transient String password;  // NOT serialized

    Student(String name, int age, String password) {
        this.name = name;
        this.age = age;
        this.password = password;
    }
}

// Serialize (save object to file)
Student s = new Student("Rahul", 22, "secret123");
try (ObjectOutputStream oos = new ObjectOutputStream(
        new FileOutputStream("student.ser"))) {
    oos.writeObject(s);
    System.out.println("Serialized!");
}

// Deserialize (read object from file)
try (ObjectInputStream ois = new ObjectInputStream(
        new FileInputStream("student.ser"))) {
    Student loaded = (Student) ois.readObject();
    System.out.println(loaded.name);      // Rahul
    System.out.println(loaded.age);       // 22
    System.out.println(loaded.password);  // null (transient!)
}
```

---

## 🔥 Interview Questions – File I/O

**Q1: Difference between FileReader and BufferedReader?**
> FileReader reads character by character. BufferedReader reads chunks (buffered) — much faster.

**Q2: What is serialization?**
> Converting an object to a byte stream to save to file or send over network. Class must implement `Serializable`.

**Q3: What is `transient` keyword?**
> Marks a field to be excluded from serialization.

**Q4: What is `serialVersionUID`?**
> A version identifier for serialized class. Ensures compatibility during deserialization.

**Q5: Difference between `byte stream` and `character stream`?**
> - Byte stream: `InputStream`/`OutputStream` (for binary data: images, etc.)
> - Character stream: `Reader`/`Writer` (for text data)

---
