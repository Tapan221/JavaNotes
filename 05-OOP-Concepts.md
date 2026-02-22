# 📘 CHAPTER 5: OOP CONCEPTS (Object-Oriented Programming)

---

## 5.1 What is OOP?

OOP is a programming style based on the concept of **objects** that contain **data** (fields) and **behavior** (methods).

### 4 Pillars of OOP
```
┌──────────────────────────────────────────────┐
│              OOP PILLARS                     │
├────────────┬────────────┬──────────┬─────────┤
│Encapsulation│Inheritance │Polymorphism│Abstraction│
│(Data hiding)│(Reuse code)│(Many forms)│(Hide detail)│
└────────────┴────────────┴──────────┴─────────┘
```

---

## 5.2 Class and Object

**Class** = Blueprint/Template
**Object** = Instance of a class (real entity)

```java
// Class (Blueprint)
class Car {
    // Fields (Properties/Attributes)
    String brand;
    String color;
    int speed;

    // Method (Behavior)
    void drive() {
        System.out.println(brand + " is driving at " + speed + " km/h");
    }

    void brake() {
        speed = 0;
        System.out.println(brand + " stopped!");
    }
}

// Using the class
public class Main {
    public static void main(String[] args) {
        // Creating objects
        Car car1 = new Car();
        car1.brand = "Toyota";
        car1.color = "Red";
        car1.speed = 120;
        car1.drive();   // Toyota is driving at 120 km/h

        Car car2 = new Car();
        car2.brand = "BMW";
        car2.color = "Black";
        car2.speed = 180;
        car2.drive();   // BMW is driving at 180 km/h
    }
}
```

---

## 5.3 Constructors

A constructor is a **special method** called when an object is created. It **initializes** the object.

### Rules:
- Same name as the class
- No return type (not even `void`)
- Called automatically with `new`

### Default Constructor
```java
class Student {
    String name;
    int age;

    // Default constructor (no parameters)
    Student() {
        name = "Unknown";
        age = 0;
        System.out.println("Object created!");
    }
}

Student s = new Student();  // "Object created!"
System.out.println(s.name); // Unknown
```

### Parameterized Constructor
```java
class Student {
    String name;
    int age;

    // Parameterized constructor
    Student(String name, int age) {
        this.name = name;   // 'this' refers to current object
        this.age = age;
    }

    void display() {
        System.out.println(name + " - " + age);
    }
}

Student s1 = new Student("Rahul", 22);
Student s2 = new Student("Priya", 21);
s1.display();  // Rahul - 22
s2.display();  // Priya - 21
```

### Constructor Overloading
```java
class Employee {
    String name;
    double salary;

    // Constructor 1
    Employee() {
        this.name = "New Employee";
        this.salary = 25000;
    }

    // Constructor 2
    Employee(String name) {
        this.name = name;
        this.salary = 30000;
    }

    // Constructor 3
    Employee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }
}

Employee e1 = new Employee();                  // New Employee - 25000
Employee e2 = new Employee("Rahul");          // Rahul - 30000
Employee e3 = new Employee("Priya", 50000);   // Priya - 50000
```

### Constructor Chaining (using `this()`)
```java
class Product {
    String name;
    double price;
    
    Product() {
        this("Unknown", 0.0);  // calls parameterized constructor
    }
    
    Product(String name, double price) {
        this.name = name;
        this.price = price;
    }
}
```

### Copy Constructor (Java doesn't have built-in, we create manually)
```java
class Person {
    String name;
    int age;

    Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Copy constructor
    Person(Person other) {
        this.name = other.name;
        this.age = other.age;
    }
}

Person p1 = new Person("Rahul", 25);
Person p2 = new Person(p1);  // Copies p1
```

---

## 5.4 `this` Keyword

Refers to the **current object**.

```java
class Box {
    int length, width;

    Box(int length, int width) {
        this.length = length;  // this.length = instance variable
        this.width = width;    // length = parameter
    }

    Box getBox() {
        return this;  // return current object
    }

    void show() {
        System.out.println(this.length + " x " + this.width);
    }
}
```

**Uses of `this`:**
1. Distinguish instance variable from parameter
2. Call current class constructor: `this()`
3. Pass current object as argument
4. Return current object

---

## 5.5 PILLAR 1: Encapsulation (Data Hiding)

**Wrapping data and methods together** + restricting direct access using `private`.

```java
class BankAccount {
    // Private fields → cannot access directly from outside
    private String owner;
    private double balance;

    // Constructor
    public BankAccount(String owner, double balance) {
        this.owner = owner;
        this.balance = balance;
    }

    // Getter → read data
    public double getBalance() {
        return balance;
    }

    // Setter → write data (with validation)
    public void deposit(double amount) {
        if (amount > 0) {
            balance += amount;
            System.out.println("Deposited: " + amount);
        } else {
            System.out.println("Invalid amount!");
        }
    }

    public void withdraw(double amount) {
        if (amount > 0 && amount <= balance) {
            balance -= amount;
            System.out.println("Withdrawn: " + amount);
        } else {
            System.out.println("Insufficient balance!");
        }
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount("Rahul", 10000);

        // acc.balance = -5000;  ❌ Error! Cannot access private field

        acc.deposit(5000);
        acc.withdraw(3000);
        System.out.println("Balance: " + acc.getBalance());  // 12000
    }
}
```

### Access Modifiers

| Modifier | Class | Package | Subclass | World |
|----------|-------|---------|----------|-------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` (no keyword) | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

---

## 5.6 PILLAR 2: Inheritance (Code Reuse)

A class **acquires** the properties and methods of another class.

```
Parent/Super class → Child/Sub class
```

### Single Inheritance
```java
// Parent class
class Animal {
    String name;

    void eat() {
        System.out.println(name + " is eating");
    }

    void sleep() {
        System.out.println(name + " is sleeping");
    }
}

// Child class (inherits from Animal)
class Dog extends Animal {
    void bark() {
        System.out.println(name + " is barking: Woof!");
    }
}

public class Main {
    public static void main(String[] args) {
        Dog dog = new Dog();
        dog.name = "Buddy";
        dog.eat();    // Buddy is eating    → inherited
        dog.sleep();  // Buddy is sleeping  → inherited
        dog.bark();   // Buddy is barking: Woof!  → own method
    }
}
```

### Multilevel Inheritance
```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {
    void bark() { System.out.println("Barking"); }
}

class Puppy extends Dog {
    void play() { System.out.println("Playing"); }
}

Puppy p = new Puppy();
p.eat();   // From Animal
p.bark();  // From Dog
p.play();  // Own method
```

### Hierarchical Inheritance
```java
class Shape {
    void draw() { System.out.println("Drawing shape"); }
}

class Circle extends Shape {
    void area() { System.out.println("Circle area"); }
}

class Rectangle extends Shape {
    void area() { System.out.println("Rectangle area"); }
}
```

> **Note:** Java does NOT support **multiple inheritance** with classes (to avoid ambiguity). Use **interfaces** instead.

### `super` Keyword
```java
class Animal {
    String type = "Animal";

    Animal() {
        System.out.println("Animal constructor");
    }

    void sound() {
        System.out.println("Some sound");
    }
}

class Cat extends Animal {
    String type = "Cat";

    Cat() {
        super();  // calls parent constructor (automatically added if missing)
        System.out.println("Cat constructor");
    }

    void sound() {
        super.sound();  // call parent method
        System.out.println("Meow!");
    }

    void showType() {
        System.out.println(this.type);   // Cat
        System.out.println(super.type);  // Animal
    }
}
```

---

## 5.7 PILLAR 3: Polymorphism (Many Forms)

One thing behaving **differently** in different situations.

### Compile-Time Polymorphism (Method Overloading)
```java
class MathUtils {
    static int multiply(int a, int b) {
        return a * b;
    }

    static double multiply(double a, double b) {
        return a * b;
    }

    static int multiply(int a, int b, int c) {
        return a * b * c;
    }
}

System.out.println(MathUtils.multiply(2, 3));       // 6
System.out.println(MathUtils.multiply(2.5, 3.5));   // 8.75
System.out.println(MathUtils.multiply(2, 3, 4));    // 24
```

### Runtime Polymorphism (Method Overriding)
```java
class Animal {
    void sound() {
        System.out.println("Some sound");
    }
}

class Dog extends Animal {
    @Override
    void sound() {
        System.out.println("Woof! Woof!");
    }
}

class Cat extends Animal {
    @Override
    void sound() {
        System.out.println("Meow!");
    }
}

public class Main {
    public static void main(String[] args) {
        // Parent reference → Child object (Upcasting)
        Animal a1 = new Dog();
        Animal a2 = new Cat();

        a1.sound();  // Woof! Woof!  → Dog's method at runtime
        a2.sound();  // Meow!        → Cat's method at runtime
    }
}
```

**Why is this useful?** → You can write generic code that works with any subclass!

### Method Overloading vs Overriding

| Feature | Overloading | Overriding |
|---------|------------|------------|
| Where? | Same class | Parent-Child classes |
| Method name | Same | Same |
| Parameters | Different | Same |
| Return type | Can differ | Same or covariant |
| Binding | Compile-time | Runtime |
| Keyword | — | `@Override` |

---

## 5.8 PILLAR 4: Abstraction (Hiding Implementation)

Show **what** it does, hide **how** it does it.

### Abstract Class
```java
// Cannot create object of abstract class
abstract class Shape {
    String color;

    // Abstract method – no body, must be implemented by child
    abstract double area();

    // Concrete method – has body
    void displayColor() {
        System.out.println("Color: " + color);
    }
}

class Circle extends Shape {
    double radius;

    Circle(double radius, String color) {
        this.radius = radius;
        this.color = color;
    }

    @Override
    double area() {
        return Math.PI * radius * radius;
    }
}

class Rectangle extends Shape {
    double length, width;

    Rectangle(double length, double width, String color) {
        this.length = length;
        this.width = width;
        this.color = color;
    }

    @Override
    double area() {
        return length * width;
    }
}

public class Main {
    public static void main(String[] args) {
        Shape s1 = new Circle(5, "Red");
        Shape s2 = new Rectangle(4, 6, "Blue");

        System.out.println("Circle area: " + s1.area());     // 78.54
        System.out.println("Rectangle area: " + s2.area());  // 24.0
        s1.displayColor();  // Color: Red
    }
}
```

### Interface
An interface is a **100% abstract** contract. Classes that implement it MUST provide all methods.

```java
// Interface
interface Drawable {
    void draw();  // abstract by default (no need to write 'abstract')
}

interface Resizable {
    void resize(int percent);
}

// A class can implement MULTIPLE interfaces
class Circle implements Drawable, Resizable {
    @Override
    public void draw() {
        System.out.println("Drawing Circle");
    }

    @Override
    public void resize(int percent) {
        System.out.println("Resizing Circle by " + percent + "%");
    }
}
```

### Interface with Default & Static Methods (Java 8+)
```java
interface Vehicle {
    void start();  // abstract

    // Default method – has body
    default void honk() {
        System.out.println("Beep! Beep!");
    }

    // Static method
    static void info() {
        System.out.println("Vehicle interface");
    }
}

class Bike implements Vehicle {
    @Override
    public void start() {
        System.out.println("Bike started with kick");
    }
    // honk() is inherited as-is, or can be overridden
}
```

### Abstract Class vs Interface

| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Abstract + Concrete | Abstract (+ default/static in Java 8) |
| Variables | Any type | Only `public static final` |
| Constructor | Yes | No |
| Inheritance | `extends` (single) | `implements` (multiple) |
| When to use | Partial implementation | Full contract / multiple inheritance |

---

## 5.9 `static` Keyword

Belongs to the **class**, not to any object.

```java
class Counter {
    static int count = 0;  // shared by all objects
    String name;

    Counter(String name) {
        this.name = name;
        count++;  // increments for every object
    }

    static void showCount() {  // static method
        System.out.println("Total objects: " + count);
        // System.out.println(name);  ❌ Cannot access non-static from static
    }
}

public class Main {
    public static void main(String[] args) {
        Counter c1 = new Counter("A");
        Counter c2 = new Counter("B");
        Counter c3 = new Counter("C");

        Counter.showCount();  // Total objects: 3
    }
}
```

### Static Block
```java
class Config {
    static String dbUrl;

    // Static block – runs once when class is loaded
    static {
        System.out.println("Static block executed");
        dbUrl = "jdbc:mysql://localhost:3306/mydb";
    }
}
```

---

## 5.10 `final` Keyword

```java
// Final variable – constant, cannot change
final double PI = 3.14159;
// PI = 3.14;  ❌ Error!

// Final method – cannot be overridden
class Parent {
    final void show() {
        System.out.println("Cannot override this");
    }
}

// Final class – cannot be inherited
final class MathUtils {
    // ...
}
// class AdvancedMath extends MathUtils {}  ❌ Error!
```

| Usage | Effect |
|-------|--------|
| `final` variable | Cannot change value (constant) |
| `final` method | Cannot override in subclass |
| `final` class | Cannot extend/inherit |

---

## 5.11 `instanceof` Operator

Check if an object is an instance of a specific class.

```java
Animal a = new Dog();

System.out.println(a instanceof Dog);     // true
System.out.println(a instanceof Animal);  // true
System.out.println(a instanceof Cat);     // false
```

---

## 5.12 Object Class (Mother of all classes)

Every class in Java implicitly extends `java.lang.Object`.

### Important methods of Object class:
```java
class Student {
    String name;
    int age;

    Student(String name, int age) {
        this.name = name;
        this.age = age;
    }

    // Override toString()
    @Override
    public String toString() {
        return "Student{name='" + name + "', age=" + age + "}";
    }

    // Override equals()
    @Override
    public boolean equals(Object obj) {
        if (this == obj) return true;
        if (obj == null || getClass() != obj.getClass()) return false;
        Student other = (Student) obj;
        return this.age == other.age && this.name.equals(other.name);
    }

    // Override hashCode()
    @Override
    public int hashCode() {
        return name.hashCode() + age;
    }
}

Student s1 = new Student("Rahul", 22);
Student s2 = new Student("Rahul", 22);

System.out.println(s1);             // Student{name='Rahul', age=22}
System.out.println(s1.equals(s2));  // true
```

---

## 🔥 Interview Questions – OOP

**Q1: What are the 4 pillars of OOP?**
> Encapsulation, Inheritance, Polymorphism, Abstraction.

**Q2: What is the difference between class and object?**
> Class is a blueprint/template; Object is an instance of a class (real entity in memory).

**Q3: Can a constructor be private?**
> Yes! Used in **Singleton Design Pattern** to restrict object creation.

**Q4: Why doesn't Java support multiple inheritance with classes?**
> To avoid the **Diamond Problem** (ambiguity when two parent classes have the same method).

**Q5: Difference between abstract class and interface?**
> Abstract class: partial implementation, single inheritance, has constructors.
> Interface: full contract, multiple inheritance, no constructors.

**Q6: Can we create an object of an abstract class?**
> No. But we can create a reference of abstract class pointing to a child object.

**Q7: What is upcasting and downcasting?**
> - Upcasting: `Animal a = new Dog();` (automatic, safe)
> - Downcasting: `Dog d = (Dog) a;` (manual, may throw ClassCastException)

**Q8: What is the use of `super` keyword?**
> 1. Call parent constructor: `super()`
> 2. Call parent method: `super.method()`
> 3. Access parent field: `super.field`

**Q9: Can we override static methods?**
> No. Static methods belong to the class, not object. They are **hidden**, not overridden.

**Q10: What is the difference between `this` and `super`?**
> - `this` refers to current class object
> - `super` refers to parent class object

**Q11: Can an interface extend another interface?**
> Yes! `interface B extends A { }` — interfaces can extend multiple interfaces.

**Q12: What happens if we don't override all abstract methods?**
> The child class must also be declared `abstract`.

**Q13: What is the Singleton Pattern?**
> A class that allows only **one** object to be created:
```java
class Singleton {
    private static Singleton instance;
    private Singleton() {}  // private constructor
    public static Singleton getInstance() {
        if (instance == null) {
            instance = new Singleton();
        }
        return instance;
    }
}
```

**Q14: What is covariant return type?**
> In overriding, the child class method can return a **subtype** of the parent's return type.

**Q15: Why do we override `equals()` and `hashCode()` together?**
> Contract: If two objects are equal (`equals()` returns true), they must have the same `hashCode()`. Required for proper behavior in HashMap, HashSet, etc.

---
