# 📘 CHAPTER 12: GENERICS, INNER CLASSES & MISCELLANEOUS

---

## 12.1 Generics

Write code that works with **any data type** while maintaining type safety.

### Generic Class
```java
// Without Generics – no type safety
class OldBox {
    Object item;
    void set(Object item) { this.item = item; }
    Object get() { return item; }
}

// With Generics – type safe!
class Box<T> {
    T item;

    void set(T item) { this.item = item; }
    T get() { return item; }
}

public class Main {
    public static void main(String[] args) {
        Box<String> stringBox = new Box<>();
        stringBox.set("Hello");
        String value = stringBox.get();  // No casting needed!

        Box<Integer> intBox = new Box<>();
        intBox.set(42);
        int num = intBox.get();

        // intBox.set("Hello");  ❌ Compile error! Type safety!
    }
}
```

### Generic Method
```java
static <T> void printArray(T[] array) {
    for (T item : array) {
        System.out.print(item + " ");
    }
    System.out.println();
}

String[] names = {"A", "B", "C"};
Integer[] numbers = {1, 2, 3};

printArray(names);    // A B C
printArray(numbers);  // 1 2 3
```

### Bounded Generics
```java
// Only accepts Number or its subclasses (Integer, Double, etc.)
static <T extends Number> double sum(T a, T b) {
    return a.doubleValue() + b.doubleValue();
}

System.out.println(sum(10, 20));     // 30.0
System.out.println(sum(1.5, 2.5));   // 4.0
// sum("hello", "world");  ❌ Compile error!
```

### Wildcards
```java
import java.util.*;

// ? → unknown type
static void printList(List<?> list) {
    for (Object item : list) {
        System.out.println(item);
    }
}

// ? extends Number → Number or its subclasses (upper bound)
static double sumList(List<? extends Number> list) {
    double sum = 0;
    for (Number n : list) {
        sum += n.doubleValue();
    }
    return sum;
}

// ? super Integer → Integer or its superclasses (lower bound)
static void addNumbers(List<? super Integer> list) {
    list.add(1);
    list.add(2);
}
```

---

## 12.2 Inner Classes

A class defined **inside another class**.

### Regular Inner Class
```java
class Outer {
    int x = 10;

    class Inner {
        void show() {
            System.out.println("x = " + x);  // can access outer's members
        }
    }
}

Outer outer = new Outer();
Outer.Inner inner = outer.new Inner();
inner.show();  // x = 10
```

### Static Inner Class
```java
class Outer {
    static int x = 10;

    static class Inner {
        void show() {
            System.out.println("x = " + x);  // can access static members only
        }
    }
}

Outer.Inner inner = new Outer.Inner();  // no outer object needed
inner.show();
```

### Anonymous Inner Class
```java
// Used to implement interface/abstract class on the fly
interface Greeting {
    void sayHello();
}

Greeting g = new Greeting() {
    @Override
    public void sayHello() {
        System.out.println("Hello!");
    }
};
g.sayHello();

// With Lambda (better)
Greeting g2 = () -> System.out.println("Hello from Lambda!");
g2.sayHello();
```

---

## 12.3 Annotations

Metadata about code. Provides information to compiler/runtime.

```java
// Built-in Annotations

@Override               // Checks if method correctly overrides parent
void toString() { }

@Deprecated             // Marks as deprecated (avoid using)
void oldMethod() { }

@SuppressWarnings("unchecked")  // Suppress compiler warnings
void method() { }

@FunctionalInterface    // Ensures interface has only one abstract method
interface MyFunc { void run(); }
```

### Custom Annotation
```java
import java.lang.annotation.*;

@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.METHOD)
@interface MyAnnotation {
    String value() default "default";
    int priority() default 0;
}

class MyClass {
    @MyAnnotation(value = "important", priority = 1)
    void myMethod() { }
}
```

---

## 12.4 Garbage Collection

Java automatically manages memory. The **Garbage Collector (GC)** destroys objects that are no longer referenced.

```java
Student s = new Student("Rahul");
s = null;  // Object becomes eligible for GC

// Request GC (not guaranteed)
System.gc();

// finalize() – called before GC destroys object (deprecated since Java 9)
@Override
protected void finalize() throws Throwable {
    System.out.println("Object destroyed");
}
```

**When is object eligible for GC?**
1. Assigned `null`
2. Re-assigned to another object
3. Created inside a method (after method ends)

---

## 12.5 Immutable Class (Create Your Own)

```java
final class ImmutablePerson {
    private final String name;
    private final int age;

    public ImmutablePerson(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() { return name; }
    public int getAge() { return age; }
    // No setters!
}
```

**Rules for immutability:**
1. Class is `final` (can't extend)
2. All fields are `private final`
3. No setter methods
4. For mutable fields (like Date, List), return deep copies in getters

---

## 12.6 Record (Java 14+)

A concise way to create **immutable data classes**.

```java
// Old way (lots of boilerplate)
class PersonOld {
    private final String name;
    private final int age;
    PersonOld(String name, int age) { this.name = name; this.age = age; }
    String getName() { return name; }
    int getAge() { return age; }
    // toString, equals, hashCode...
}

// New way with Record
record Person(String name, int age) { }

// Automatically generates: constructor, getters, toString, equals, hashCode
Person p = new Person("Rahul", 25);
System.out.println(p.name());     // Rahul (getter is name(), not getName())
System.out.println(p.age());      // 25
System.out.println(p);            // Person[name=Rahul, age=25]
```

---

## 12.7 Sealed Classes (Java 17+)

Restrict which classes can extend a class.

```java
sealed class Shape permits Circle, Rectangle, Triangle { }

final class Circle extends Shape { }
final class Rectangle extends Shape { }
non-sealed class Triangle extends Shape { }  // allows further extension
// class Square extends Shape { }  ❌ Not permitted!
```

---

## 12.8 Pattern Matching for instanceof (Java 16+)

```java
// Old way
if (obj instanceof String) {
    String s = (String) obj;
    System.out.println(s.length());
}

// New way
if (obj instanceof String s) {
    System.out.println(s.length());  // 's' is already cast!
}
```

---

## 🔥 Interview Questions – Miscellaneous

**Q1: What are Generics? Why use them?**
> Generics provide type safety at compile time. Avoid ClassCastException and eliminate need for casting.

**Q2: What is Type Erasure?**
> Generics info is removed at compile time. At runtime, `List<String>` and `List<Integer>` are both just `List`.

**Q3: Difference between `? extends T` and `? super T`?**
> - `? extends T`: upper bound – T or its subclasses (read/get)
> - `? super T`: lower bound – T or its superclasses (write/add)

**Q4: What is an immutable class? How to create one?**
> A class whose objects cannot be modified after creation. Use `final` class, `private final` fields, no setters, deep copy for mutable fields.

**Q5: Types of inner classes?**
> 1. Regular inner class
> 2. Static inner class
> 3. Local inner class (inside method)
> 4. Anonymous inner class

**Q6: What is a Record in Java?**
> A concise way to create immutable data classes. Auto-generates constructor, getters, toString, equals, hashCode.

---
