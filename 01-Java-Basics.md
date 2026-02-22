# 📘 CHAPTER 1: JAVA BASICS

---

## 1.1 What is Java?

Java is a **high-level, object-oriented, platform-independent** programming language developed by **James Gosling** at **Sun Microsystems** in **1995** (now owned by Oracle).

**Key Features:**
- **Simple** – Easy syntax (similar to C++)
- **Object-Oriented** – Everything is an object
- **Platform Independent** – Write Once, Run Anywhere (WORA)
- **Secure** – No explicit pointers
- **Robust** – Strong memory management
- **Multithreaded** – Supports concurrent execution

---

## 1.2 JDK vs JRE vs JVM

```
┌─────────────────────────────────────┐
│           JDK (Java Development Kit)│
│  ┌───────────────────────────────┐  │
│  │      JRE (Java Runtime Env)   │  │
│  │  ┌─────────────────────────┐  │  │
│  │  │   JVM (Java Virtual     │  │  │
│  │  │       Machine)          │  │  │
│  │  └─────────────────────────┘  │  │
│  │  + Libraries (rt.jar etc.)    │  │
│  └───────────────────────────────┘  │
│  + Compiler (javac)                 │
│  + Debugger                         │
│  + Other Dev Tools                  │
└─────────────────────────────────────┘
```

| Component | Purpose |
|-----------|---------|
| **JVM** | Executes bytecode. Platform-dependent. |
| **JRE** | JVM + Libraries. Needed to **run** Java programs. |
| **JDK** | JRE + Development tools. Needed to **develop** Java programs. |

---

## 1.3 How Java Program Executes

```
Source Code (.java)  →  Compiler (javac)  →  Bytecode (.class)  →  JVM  →  Machine Code
```

---

## 1.4 First Java Program – Hello World

```java
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World!");
    }
}
```

**Line-by-line Explanation:**
| Code | Meaning |
|------|---------|
| `public` | Accessible from anywhere |
| `class HelloWorld` | Defines a class named HelloWorld |
| `public static void main(String[] args)` | Entry point of the program |
| `static` | Can run without creating an object |
| `void` | Returns nothing |
| `String[] args` | Command-line arguments |
| `System.out.println()` | Prints output to console |

---

## 1.5 Data Types in Java

### Primitive Data Types (8 types)

| Type | Size | Default | Example |
|------|------|---------|---------|
| `byte` | 1 byte | 0 | `byte b = 10;` |
| `short` | 2 bytes | 0 | `short s = 1000;` |
| `int` | 4 bytes | 0 | `int i = 50000;` |
| `long` | 8 bytes | 0L | `long l = 100000L;` |
| `float` | 4 bytes | 0.0f | `float f = 3.14f;` |
| `double` | 8 bytes | 0.0d | `double d = 3.14159;` |
| `char` | 2 bytes | '\u0000' | `char c = 'A';` |
| `boolean` | 1 bit | false | `boolean flag = true;` |

### Non-Primitive Data Types
- String, Arrays, Classes, Interfaces

```java
public class DataTypesDemo {
    public static void main(String[] args) {
        // Primitive types
        byte age = 25;
        short salary = 30000;
        int population = 1000000;
        long worldPopulation = 7800000000L;
        float pi = 3.14f;
        double precisePi = 3.141592653589;
        char grade = 'A';
        boolean isJavaFun = true;

        System.out.println("Age: " + age);
        System.out.println("Grade: " + grade);
        System.out.println("Is Java Fun? " + isJavaFun);
    }
}
```

---

## 1.6 Variables

A variable is a **container** that holds a value.

### Types of Variables

```java
public class VariableTypes {
    // Instance variable – belongs to object
    String name = "Rahul";
    
    // Static variable – belongs to class
    static String company = "Google";
    
    public void show() {
        // Local variable – inside method
        int age = 22;
        System.out.println(name + " " + age + " " + company);
    }

    public static void main(String[] args) {
        VariableTypes obj = new VariableTypes();
        obj.show();
    }
}
```

| Variable Type | Where Declared | Scope |
|---------------|----------------|-------|
| **Local** | Inside method/block | Only within that method/block |
| **Instance** | Inside class, outside method | Throughout the class (per object) |
| **Static** | With `static` keyword | Shared across all objects |

---

## 1.7 Type Casting

```java
public class TypeCasting {
    public static void main(String[] args) {
        // Widening (Automatic) – small to large
        int num = 100;
        double d = num;  // int → double
        System.out.println("Widening: " + d);  // 100.0

        // Narrowing (Manual) – large to small
        double price = 99.99;
        int roundedPrice = (int) price;  // double → int
        System.out.println("Narrowing: " + roundedPrice);  // 99
    }
}
```

**Widening order:** `byte → short → int → long → float → double`

---

## 1.8 Operators

### Arithmetic Operators
```java
int a = 10, b = 3;
System.out.println(a + b);   // 13  (Addition)
System.out.println(a - b);   // 7   (Subtraction)
System.out.println(a * b);   // 30  (Multiplication)
System.out.println(a / b);   // 3   (Division)
System.out.println(a % b);   // 1   (Modulus/Remainder)
```

### Comparison (Relational) Operators
```java
System.out.println(10 > 5);    // true
System.out.println(10 < 5);    // false
System.out.println(10 == 10);  // true
System.out.println(10 != 5);   // true
System.out.println(10 >= 10);  // true
System.out.println(10 <= 5);   // false
```

### Logical Operators
```java
boolean x = true, y = false;
System.out.println(x && y);  // false  (AND – both must be true)
System.out.println(x || y);  // true   (OR – at least one true)
System.out.println(!x);      // false  (NOT – reverses)
```

### Increment / Decrement
```java
int count = 5;
System.out.println(count++);  // 5 (prints first, then increments)
System.out.println(count);    // 6
System.out.println(++count);  // 7 (increments first, then prints)
```

### Ternary Operator
```java
int age = 20;
String result = (age >= 18) ? "Adult" : "Minor";
System.out.println(result);  // Adult
```

---

## 1.9 Taking User Input

```java
import java.util.Scanner;

public class UserInput {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter your name: ");
        String name = sc.nextLine();

        System.out.print("Enter your age: ");
        int age = sc.nextInt();

        System.out.print("Enter your salary: ");
        double salary = sc.nextDouble();

        System.out.println("Name: " + name);
        System.out.println("Age: " + age);
        System.out.println("Salary: " + salary);

        sc.close();
    }
}
```

| Method | Reads |
|--------|-------|
| `nextLine()` | Full line (String) |
| `nextInt()` | Integer |
| `nextDouble()` | Double |
| `nextFloat()` | Float |
| `next()` | Single word |
| `nextBoolean()` | Boolean |

---

## 1.10 Comments in Java

```java
// This is a single-line comment

/*
   This is a
   multi-line comment
*/

/**
 * This is a Javadoc comment
 * Used for documentation
 * @param args command line arguments
 */
```

---

## 🔥 Interview Questions – Java Basics

**Q1: Why is Java platform-independent?**
> Java code is compiled into **bytecode** (.class file), which runs on any OS that has a **JVM**. The JVM is platform-dependent, but bytecode is not.

**Q2: What is the difference between JDK, JRE, and JVM?**
> - JVM executes bytecode
> - JRE = JVM + libraries (to run programs)
> - JDK = JRE + dev tools (to develop programs)

**Q3: Can we run Java without `main()` method?**
> No (from Java 7 onwards). Before Java 7, you could use a `static` block, but not anymore.

**Q4: What is the difference between `==` and `.equals()`?**
> - `==` compares **reference** (memory address)
> - `.equals()` compares **value/content**

**Q5: What is type casting? Types?**
> Converting one data type to another.
> - **Widening** (automatic): smaller → larger type
> - **Narrowing** (manual): larger → smaller type

**Q6: Why is `String[] args` in `main()` method?**
> To accept **command-line arguments** when running the program.

**Q7: What is the default value of local variables?**
> Local variables have **no default value**. They must be initialized before use, or the compiler gives an error.

**Q8: Difference between `float` and `double`?**
> - `float` = 4 bytes, 6-7 decimal digits precision
> - `double` = 8 bytes, 15-16 decimal digits precision

**Q9: What is `System.out.println()`?**
> - `System` – a final class in `java.lang` package
> - `out` – a static object of `PrintStream` class
> - `println()` – a method that prints and adds a new line

**Q10: What happens if file name doesn't match class name?**
> If the class is `public`, the file name **must** match the class name. If not public, it can be different (but not recommended).

---
