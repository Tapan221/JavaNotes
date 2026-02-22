# 📘 CHAPTER 4: METHODS (FUNCTIONS) IN JAVA

---

## 4.1 What is a Method?

A method is a **block of code** that performs a specific task. It runs only when **called**.

**Why use methods?**
- Code **reusability** – write once, use many times
- Code **organization** – break big problems into small parts
- **Easy to debug** and maintain

---

## 4.2 Method Syntax

```
accessModifier returnType methodName(parameters) {
    // method body
    return value;  // if returnType is not void
}
```

---

## 4.3 Types of Methods

### Method with no parameters, no return
```java
public class MethodDemo {
    // Method definition
    static void greet() {
        System.out.println("Hello! Welcome to Java.");
    }

    public static void main(String[] args) {
        greet();  // Method call
        greet();  // Can call multiple times
    }
}
```

### Method with parameters
```java
static void greetUser(String name) {
    System.out.println("Hello, " + name + "!");
}

public static void main(String[] args) {
    greetUser("Rahul");   // Hello, Rahul!
    greetUser("Priya");   // Hello, Priya!
}
```

### Method with return value
```java
static int add(int a, int b) {
    return a + b;
}

public static void main(String[] args) {
    int result = add(10, 20);
    System.out.println("Sum: " + result);  // Sum: 30
}
```

### Method with multiple parameters
```java
static double calculateArea(double length, double width) {
    return length * width;
}

public static void main(String[] args) {
    double area = calculateArea(5.0, 3.0);
    System.out.println("Area: " + area);  // Area: 15.0
}
```

---

## 4.4 Method Overloading

**Same method name, different parameters** (number, type, or order).

```java
public class Calculator {
    // Method 1: two ints
    static int add(int a, int b) {
        return a + b;
    }

    // Method 2: three ints
    static int add(int a, int b, int c) {
        return a + b + c;
    }

    // Method 3: two doubles
    static double add(double a, double b) {
        return a + b;
    }

    public static void main(String[] args) {
        System.out.println(add(10, 20));         // 30      → calls Method 1
        System.out.println(add(10, 20, 30));     // 60      → calls Method 2
        System.out.println(add(10.5, 20.5));     // 31.0    → calls Method 3
    }
}
```

> **Note:** Overloading is NOT based on return type alone. Changing only return type causes a compile error.

---

## 4.5 Pass by Value in Java

Java is **always pass by value**. For primitives, the value is copied. For objects, the reference is copied.

```java
// Primitive: value is copied (original NOT affected)
static void changeValue(int x) {
    x = 100;
}

public static void main(String[] args) {
    int num = 10;
    changeValue(num);
    System.out.println(num);  // 10 ← NOT changed
}
```

```java
// Object: reference is copied (original CAN be affected)
static void changeName(StringBuilder sb) {
    sb.append(" World");
}

public static void main(String[] args) {
    StringBuilder name = new StringBuilder("Hello");
    changeName(name);
    System.out.println(name);  // Hello World ← Changed!
}
```

---

## 4.6 Recursion

A method that **calls itself**.

```java
// Factorial: 5! = 5 × 4 × 3 × 2 × 1 = 120
static int factorial(int n) {
    if (n == 0 || n == 1) {
        return 1;           // Base case
    }
    return n * factorial(n - 1);  // Recursive call
}

public static void main(String[] args) {
    System.out.println(factorial(5));  // 120
}
```

**How it works:**
```
factorial(5)
= 5 * factorial(4)
= 5 * 4 * factorial(3)
= 5 * 4 * 3 * factorial(2)
= 5 * 4 * 3 * 2 * factorial(1)
= 5 * 4 * 3 * 2 * 1
= 120
```

### Fibonacci Series using Recursion
```java
static int fibonacci(int n) {
    if (n <= 1) return n;
    return fibonacci(n - 1) + fibonacci(n - 2);
}

public static void main(String[] args) {
    for (int i = 0; i < 10; i++) {
        System.out.print(fibonacci(i) + " ");
    }
    // Output: 0 1 1 2 3 5 8 13 21 34
}
```

---

## 4.7 Variable Arguments (Varargs)

Accept **any number of arguments**.

```java
static int sum(int... numbers) {
    int total = 0;
    for (int num : numbers) {
        total += num;
    }
    return total;
}

public static void main(String[] args) {
    System.out.println(sum(1, 2));           // 3
    System.out.println(sum(1, 2, 3));        // 6
    System.out.println(sum(1, 2, 3, 4, 5)); // 15
}
```

> **Rule:** Varargs must be the **last parameter** in the method.

---

## 🔥 Interview Questions – Methods

**Q1: What is method overloading?**
> Same method name with different **number/type/order** of parameters. Decided at **compile time** (static polymorphism).

**Q2: Can we overload `main()` method?**
> Yes! But JVM always calls `public static void main(String[] args)` as the entry point.

**Q3: Is Java pass by value or pass by reference?**
> Java is **always pass by value**. For objects, the reference value is passed (not the object itself).

**Q4: What is recursion? Can it cause issues?**
> A method calling itself. Can cause **StackOverflowError** if no proper base case or too deep.

**Q5: What is the difference between method overloading and method overriding?**
> - Overloading: Same class, same name, different params (compile-time)
> - Overriding: Subclass redefines parent method, same signature (runtime)

**Q6: Can we have two methods with same name and parameters but different return type?**
> No. It causes a compile-time error. Return type alone doesn't differentiate overloaded methods.

---
