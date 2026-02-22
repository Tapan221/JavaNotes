# JAVA COMPLETE INTERVIEW GUIDE
### Every Concept Explained in Question & Answer Format with Simple Examples

---

# SECTION 1: JAVA FUNDAMENTALS

---

### Q1: What is Java?
**A:** Java is a high-level, object-oriented, platform-independent programming language created by **James Gosling** at Sun Microsystems in 1995 (now owned by Oracle).

---

### Q2: What are the main features of Java?
**A:**
| Feature | Meaning |
|---------|---------|
| Object-Oriented | Everything is based on objects |
| Platform Independent | Write Once, Run Anywhere (WORA) |
| Simple | Easy syntax similar to C++ but no pointers |
| Secure | No direct memory access, runs inside JVM |
| Robust | Strong memory management + exception handling |
| Multithreaded | Supports running multiple threads simultaneously |
| Distributed | Supports network programming (RMI, Socket) |

---

### Q3: What is the difference between JDK, JRE, and JVM?
**A:**
```
JDK (Java Development Kit)
 └── JRE (Java Runtime Environment)
      └── JVM (Java Virtual Machine)
```
- **JVM** → Executes bytecode. Platform-dependent.
- **JRE** → JVM + Libraries. Needed to **run** Java.
- **JDK** → JRE + Compiler + Dev Tools. Needed to **develop** Java.

---

### Q4: How does a Java program execute?
**A:**
```
.java file → javac compiler → .class file (bytecode) → JVM → Machine Code → Runs
```
```java
// Step 1: Write code (HelloWorld.java)
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello World!");
    }
}
// Step 2: Compile → javac HelloWorld.java
// Step 3: Run → java HelloWorld
```

---

### Q5: Why is Java platform-independent?
**A:** Java code compiles to **bytecode** (.class file), not machine code. This bytecode runs on **any OS** that has a JVM installed. The JVM is platform-dependent, but bytecode is not.

---

### Q6: What is the `main()` method? Can we change its signature?
**A:** `main()` is the entry point of every Java application.
```java
public static void main(String[] args) { }
```
- `public` → JVM can access it from anywhere
- `static` → no object needed to call it
- `void` → returns nothing
- `String[] args` → accepts command-line arguments

**We can overload `main()` but JVM always calls this exact signature.**

---

### Q7: What are the 8 primitive data types in Java?
**A:**
```java
byte   b = 10;          // 1 byte  (-128 to 127)
short  s = 1000;         // 2 bytes
int    i = 100000;       // 4 bytes (most used for numbers)
long   l = 99999999L;    // 8 bytes
float  f = 3.14f;        // 4 bytes (decimal)
double d = 3.14159;      // 8 bytes (more precise decimal)
char   c = 'A';          // 2 bytes (single character)
boolean flag = true;     // 1 bit   (true/false only)
```

---

### Q8: What are the types of variables in Java?
**A:**
```java
public class VariableDemo {
    int x = 10;              // Instance variable → belongs to object
    static int y = 20;       // Static variable → belongs to class
    
    void method() {
        int z = 30;          // Local variable → exists only in this method
    }
}
```
| Type | Scope | Default Value |
|------|-------|---------------|
| Local | Inside method only | None (must initialize) |
| Instance | Entire class (per object) | 0, null, false |
| Static | Entire class (shared by all objects) | 0, null, false |

---

### Q9: What is type casting in Java?
**A:** Converting one data type to another.
```java
// Widening (Automatic) → small to large (safe)
int num = 100;
double d = num;           // 100.0

// Narrowing (Manual) → large to small (may lose data)
double price = 99.99;
int rounded = (int) price; // 99
```
**Widening order:** `byte → short → int → long → float → double`

---

### Q10: What is the difference between `==` and `.equals()`?
**A:**
```java
String a = "Hello";
String b = "Hello";
String c = new String("Hello");

System.out.println(a == b);       // true  → same reference (String Pool)
System.out.println(a == c);       // false → different reference (Heap)
System.out.println(a.equals(c));  // true  → same content
```
- `==` compares **memory address** (reference)
- `.equals()` compares **actual content** (value)

---

### Q11: What are operators in Java?
**A:**
```java
// Arithmetic
int sum = 10 + 5;   // 15
int mod = 10 % 3;   // 1 (remainder)

// Comparison → returns boolean
boolean result = (10 > 5);  // true

// Logical
boolean x = true, y = false;
System.out.println(x && y);  // false (AND)
System.out.println(x || y);  // true  (OR)
System.out.println(!x);      // false (NOT)

// Ternary → shorthand if-else
String status = (10 > 5) ? "Yes" : "No"; // "Yes"

// Increment
int a = 5;
System.out.println(a++); // 5 (post: use then increment)
System.out.println(++a); // 7 (pre: increment then use)
```

---

### Q12: What is the Scanner class?
**A:** Used to take **user input** from the console.
```java
import java.util.Scanner;

Scanner sc = new Scanner(System.in);
System.out.print("Enter name: ");
String name = sc.nextLine();     // reads full line
System.out.print("Enter age: ");
int age = sc.nextInt();          // reads integer
System.out.println("Hello " + name + ", age " + age);
sc.close();
```

---

# SECTION 2: CONTROL FLOW

---

### Q13: What are the conditional statements in Java?
**A:**
```java
// if-else
int marks = 75;
if (marks >= 90) {
    System.out.println("A+");
} else if (marks >= 70) {
    System.out.println("A");    // ← This prints
} else {
    System.out.println("B");
}

// switch
int day = 3;
switch (day) {
    case 1: System.out.println("Mon"); break;
    case 2: System.out.println("Tue"); break;
    case 3: System.out.println("Wed"); break;  // ← prints
    default: System.out.println("Other");
}

// Enhanced switch (Java 14+)
String result = switch (day) {
    case 1 -> "Mon";
    case 2 -> "Tue";
    case 3 -> "Wed";
    default -> "Other";
};
```

---

### Q14: What happens if you forget `break` in switch?
**A:** **Fall-through** occurs — all cases after the matched one execute until a `break` is found.
```java
int x = 1;
switch (x) {
    case 1: System.out.println("One");   // prints
    case 2: System.out.println("Two");   // also prints (fall-through!)
    case 3: System.out.println("Three"); // also prints!
        break;
    case 4: System.out.println("Four");  // stops here
}
// Output: One Two Three
```

---

### Q15: What are the types of loops in Java?
**A:**
```java
// for loop → know the count
for (int i = 1; i <= 5; i++) {
    System.out.print(i + " ");  // 1 2 3 4 5
}

// while loop → condition-based
int i = 1;
while (i <= 5) {
    System.out.print(i + " ");
    i++;
}

// do-while → runs at least ONCE
int j = 10;
do {
    System.out.println(j);  // prints 10 even though condition is false
} while (j < 5);

// for-each → iterate collections/arrays
int[] nums = {10, 20, 30};
for (int num : nums) {
    System.out.print(num + " ");  // 10 20 30
}
```

---

### Q16: Difference between `while` and `do-while`?
**A:**
| Feature | while | do-while |
|---------|-------|----------|
| Checks condition | Before execution | After execution |
| Minimum executions | 0 | 1 (always runs at least once) |

---

### Q17: What is `break` vs `continue`?
**A:**
```java
// break → exits the loop entirely
for (int i = 1; i <= 5; i++) {
    if (i == 3) break;
    System.out.print(i + " ");  // 1 2
}

// continue → skips current iteration
for (int i = 1; i <= 5; i++) {
    if (i == 3) continue;
    System.out.print(i + " ");  // 1 2 4 5
}
```

---

### Q18: Can switch work with String?
**A:** Yes, from **Java 7** onwards. Supports: `int`, `char`, `String`, `enum`, and wrapper types, but NOT `long`, `float`, `double`, or `boolean`.

---

# SECTION 3: ARRAYS

---

### Q19: What is an Array? How to declare one?
**A:** A fixed-size container for multiple values of the same type.
```java
// Declaration
int[] marks = new int[5];          // [0, 0, 0, 0, 0]
int[] ages = {25, 30, 35, 40};    // initialized

// Access
System.out.println(ages[0]);       // 25
System.out.println(ages.length);   // 4

// Loop
for (int age : ages) {
    System.out.print(age + " ");
}
```

---

### Q20: What is a 2D Array?
**A:** An array of arrays (like a table/matrix).
```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};
System.out.println(matrix[1][2]); // 6 (row 1, col 2)

// Loop through 2D array
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

---

### Q21: What is `ArrayIndexOutOfBoundsException`?
**A:** Thrown when accessing an index that doesn't exist.
```java
int[] arr = {1, 2, 3};
System.out.println(arr[5]); // ArrayIndexOutOfBoundsException!
```

---

### Q22: Can we change the size of an array after creation?
**A:** No. Arrays are **fixed-size**. Use `ArrayList` if you need dynamic sizing.

---

### Q23: Difference between `length`, `length()`, and `size()`?
**A:**
| What | Usage | Example |
|------|-------|---------|
| `length` | Array property | `arr.length` |
| `length()` | String method | `str.length()` |
| `size()` | Collection method | `list.size()` |

---

### Q24: How to sort and search an array?
**A:**
```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1, 9};
Arrays.sort(arr);                    // [1, 2, 5, 8, 9]
int idx = Arrays.binarySearch(arr, 5); // index of 5
System.out.println(Arrays.toString(arr));
System.out.println(Arrays.equals(new int[]{1,2}, new int[]{1,2})); // true
```

---

# SECTION 4: STRINGS

---

### Q25: What is a String in Java? Is it a primitive?
**A:** String is an **object** of `java.lang.String` class, NOT a primitive. It is **immutable** — once created, cannot be changed.

---

### Q26: What is the String Pool?
**A:** A special area in heap memory where String literals are stored. If two strings have the same value, they share the same reference.
```java
String a = "Hello";   // stored in String Pool
String b = "Hello";   // points to SAME object
String c = new String("Hello");  // NEW object in Heap

System.out.println(a == b);       // true  (same pool reference)
System.out.println(a == c);       // false (different objects)
System.out.println(a.equals(c));  // true  (same content)
```

---

### Q27: Why is String immutable in Java?
**A:**
1. **String Pool** — Safe sharing of strings
2. **Security** — Passwords, DB URLs can't be modified
3. **Thread Safety** — No synchronization needed
4. **Hashing** — hashCode is cached (efficient for HashMap keys)

---

### Q28: How many objects does `String s = new String("Hello");` create?
**A:** **2 objects** — one in the String Pool (`"Hello"` literal), one in the Heap (`new String`).

---

### Q29: What are the most important String methods?
**A:**
```java
String s = "Hello World";

s.length();               // 11
s.charAt(0);              // 'H'
s.substring(0, 5);        // "Hello"
s.toUpperCase();          // "HELLO WORLD"
s.toLowerCase();          // "hello world"
s.trim();                 // removes leading/trailing spaces
s.contains("World");      // true
s.indexOf("World");       // 6
s.replace("World","Java");// "Hello Java"
s.startsWith("Hello");    // true
s.endsWith("World");      // true
s.isEmpty();              // false
s.split(" ");             // ["Hello", "World"]
s.equals("Hello World");  // true
s.equalsIgnoreCase("hello world"); // true
s.toCharArray();          // ['H','e','l','l','o',' ','W','o','r','l','d']
String.join("-", "a","b");// "a-b"
String.valueOf(123);      // "123"
```

---

### Q30: Difference between String, StringBuilder, StringBuffer?
**A:**
```java
// String → IMMUTABLE (creates new object on change)
String s = "Hello";
s = s + " World";  // creates NEW string object each time

// StringBuilder → MUTABLE, FAST, NOT thread-safe
StringBuilder sb = new StringBuilder("Hello");
sb.append(" World");  // modifies same object
sb.reverse();          // "dlroW olleH"
sb.insert(0, "Hi ");
sb.delete(0, 3);

// StringBuffer → MUTABLE, SLOWER, THREAD-SAFE
StringBuffer sbuf = new StringBuffer("Hello");
sbuf.append(" World");  // same as StringBuilder but synchronized
```

| Feature | String | StringBuilder | StringBuffer |
|---------|--------|--------------|-------------|
| Mutable | No | Yes | Yes |
| Thread-safe | Yes (immutable) | No | Yes |
| Speed | Slowest (on modify) | Fastest | Medium |
| Use when | Few changes | Single thread, many changes | Multi-thread |

---

### Q31: How to reverse a String?
**A:**
```java
String str = "Hello";
String rev = new StringBuilder(str).reverse().toString(); // "olleH"
```

---

### Q32: How to check if a String is a palindrome?
**A:**
```java
String word = "madam";
boolean isPalin = word.equals(new StringBuilder(word).reverse().toString());
System.out.println(isPalin); // true
```

---

### Q33: What does `intern()` method do?
**A:** Puts the string into the String Pool. If already present, returns the existing pool reference.
```java
String a = new String("Hello");
String b = a.intern();  // returns pooled "Hello"
String c = "Hello";
System.out.println(b == c); // true (both point to pool)
```

---

# SECTION 5: METHODS

---

### Q34: What is a method in Java?
**A:** A reusable block of code that performs a specific task.
```java
// Method with return value
static int add(int a, int b) {
    return a + b;
}

// Method with no return
static void greet(String name) {
    System.out.println("Hello " + name);
}

public static void main(String[] args) {
    int sum = add(5, 3);   // 8
    greet("Rahul");        // Hello Rahul
}
```

---

### Q35: What is method overloading?
**A:** Same method name, **different parameters** (number, type, or order). Resolved at **compile time**.
```java
static int add(int a, int b)       { return a + b; }
static int add(int a, int b, int c){ return a + b + c; }
static double add(double a, double b){ return a + b; }

// Java picks the right method based on arguments
add(2, 3);       // calls first
add(2, 3, 4);    // calls second
add(2.5, 3.5);   // calls third
```
**Note:** You CANNOT overload by changing only the return type.

---

### Q36: Is Java pass-by-value or pass-by-reference?
**A:** Java is **always pass-by-value**. For objects, the value of the reference is passed (not the object itself).
```java
// Primitives: value copied → original NOT affected
static void change(int x) { x = 100; }
int num = 10;
change(num);
System.out.println(num); // 10 (unchanged)

// Objects: reference copied → original CAN be modified
static void modify(StringBuilder sb) { sb.append(" World"); }
StringBuilder s = new StringBuilder("Hello");
modify(s);
System.out.println(s); // "Hello World" (modified!)
```

---

### Q37: What is recursion?
**A:** A method calling itself. Must have a **base case** to stop.
```java
static int factorial(int n) {
    if (n <= 1) return 1;          // base case
    return n * factorial(n - 1);   // recursive call
}
System.out.println(factorial(5)); // 120 = 5×4×3×2×1
```
**Risk:** Can cause `StackOverflowError` if no base case or too deep.

---

### Q38: What are Varargs?
**A:** Variable arguments — accept any number of parameters.
```java
static int sum(int... numbers) {  // varargs must be last param
    int total = 0;
    for (int n : numbers) total += n;
    return total;
}

sum(1, 2);        // 3
sum(1, 2, 3, 4);  // 10
```

---

# SECTION 6: OOP — CLASSES & OBJECTS

---

### Q39: What is the difference between a Class and an Object?
**A:**
```java
// Class = Blueprint/Template
class Car {
    String brand;
    int speed;
    void drive() {
        System.out.println(brand + " driving at " + speed);
    }
}

// Object = Real instance created from the class
Car car1 = new Car();
car1.brand = "Toyota";
car1.speed = 120;
car1.drive(); // Toyota driving at 120
```
- **Class** = Design/recipe
- **Object** = Actual thing created from that design

---

### Q40: What is a Constructor? What are its rules?
**A:** A special method that initializes an object. Called automatically when `new` is used.
```java
class Student {
    String name;
    int age;

    // Default constructor
    Student() {
        name = "Unknown";
        age = 0;
    }

    // Parameterized constructor
    Student(String name, int age) {
        this.name = name;    // 'this' refers to current object
        this.age = age;
    }
}

Student s1 = new Student();             // calls default
Student s2 = new Student("Rahul", 22);  // calls parameterized
```
**Rules:** Same name as class, no return type, called with `new`, can be overloaded.

---

### Q41: Can a constructor be `private`?
**A:** Yes! Used in the **Singleton Design Pattern** to prevent external object creation.
```java
class Singleton {
    private static Singleton instance;
    
    private Singleton() { }  // private constructor
    
    public static Singleton getInstance() {
        if (instance == null)
            instance = new Singleton();
        return instance;
    }
}
// Only ONE object ever created
Singleton obj = Singleton.getInstance();
```

---

### Q42: What is `this` keyword?
**A:** Refers to the **current object**.
```java
class Box {
    int size;
    Box(int size) {
        this.size = size;  // distinguishes field from parameter
    }
    Box getThis() {
        return this;       // return current object
    }
}
```
**Uses:** Resolve name conflict, call another constructor (`this()`), pass current object, return current object.

---

### Q43: What is `super` keyword?
**A:** Refers to the **parent class** object.
```java
class Animal {
    String type = "Animal";
    Animal() { System.out.println("Animal created"); }
    void sound() { System.out.println("Some sound"); }
}

class Dog extends Animal {
    String type = "Dog";
    Dog() {
        super();  // calls parent constructor (added automatically if missing)
    }
    void show() {
        super.sound();            // call parent method
        System.out.println(super.type);  // access parent field
    }
}
```

---

# SECTION 7: OOP — FOUR PILLARS

---

### Q44: What is Encapsulation?
**A:** Wrapping data (fields) and methods together + **hiding data** using `private` and exposing through getters/setters.
```java
class BankAccount {
    private double balance;  // hidden

    public double getBalance() {         // getter
        return balance;
    }
    public void deposit(double amount) { // setter with validation
        if (amount > 0) balance += amount;
    }
}

BankAccount acc = new BankAccount();
// acc.balance = -5000;  ← ERROR! Private
acc.deposit(1000);                     // ← Controlled access
System.out.println(acc.getBalance());  // 1000
```
**Benefit:** Data protection, validation, flexibility to change internals.

---

### Q45: What are access modifiers?
**A:**
| Modifier | Same Class | Same Package | Subclass | Everywhere |
|----------|-----------|-------------|----------|-----------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

---

### Q46: What is Inheritance?
**A:** A class **acquires** properties and methods of another class using `extends`.
```java
class Animal {
    void eat() { System.out.println("Eating"); }
}

class Dog extends Animal {  // Dog inherits eat()
    void bark() { System.out.println("Barking"); }
}

Dog d = new Dog();
d.eat();   // inherited from Animal
d.bark();  // own method
```
**Types:** Single, Multilevel, Hierarchical. Java does NOT support multiple inheritance with classes.

---

### Q47: Why doesn't Java support multiple inheritance with classes?
**A:** To avoid the **Diamond Problem** — ambiguity when two parent classes have the same method.
```java
// NOT ALLOWED:
// class C extends A, B { }  ← Which method to inherit if both have same method?

// SOLUTION: Use interfaces
interface A { void show(); }
interface B { void show(); }
class C implements A, B {
    public void show() { System.out.println("C's show"); } // must override
}
```

---

### Q48: What is Polymorphism?
**A:** One thing behaving **differently** in different situations. Two types:

**Compile-time (Method Overloading):**
```java
class Calc {
    int add(int a, int b)    { return a + b; }
    double add(double a, double b) { return a + b; }
}
```

**Runtime (Method Overriding):**
```java
class Animal {
    void sound() { System.out.println("Some sound"); }
}
class Dog extends Animal {
    @Override
    void sound() { System.out.println("Woof!"); }
}
class Cat extends Animal {
    @Override
    void sound() { System.out.println("Meow!"); }
}

// Parent reference, child object (Upcasting)
Animal a1 = new Dog();
Animal a2 = new Cat();
a1.sound(); // Woof!  → decided at RUNTIME
a2.sound(); // Meow!  → decided at RUNTIME
```

---

### Q49: Difference between method overloading and overriding?
**A:**
| Feature | Overloading | Overriding |
|---------|------------|------------|
| Where | Same class | Parent-Child classes |
| Parameters | Different | Same |
| Return type | Can differ | Same (or covariant) |
| Binding | Compile-time | Runtime |
| `static`? | Can overload | Cannot override |

---

### Q50: Can we override `static` methods?
**A:** No. Static methods belong to the **class**, not the object. They are **hidden** (method hiding), not overridden.

---

### Q51: What is Abstraction?
**A:** Showing **what** an object does, hiding **how** it does it.

**Abstract Class:**
```java
abstract class Shape {
    abstract double area();  // no body — child MUST implement
    void display() {         // concrete method — has body
        System.out.println("I am a shape");
    }
}

class Circle extends Shape {
    double radius;
    Circle(double r) { radius = r; }
    
    @Override
    double area() { return Math.PI * radius * radius; }
}

Shape s = new Circle(5);
System.out.println(s.area());  // 78.54
```

---

### Q52: What is an Interface?
**A:** A **contract** — defines what methods a class must implement. Supports **multiple inheritance**.
```java
interface Flyable {
    void fly();  // abstract by default
}
interface Swimmable {
    void swim();
}

class Duck implements Flyable, Swimmable {  // multiple interfaces!
    public void fly()  { System.out.println("Duck flying"); }
    public void swim() { System.out.println("Duck swimming"); }
}
```

**Java 8+ additions:**
```java
interface Vehicle {
    void start();                          // abstract
    default void honk() {                  // default method (has body)
        System.out.println("Beep!");
    }
    static void info() {                   // static method
        System.out.println("Vehicle interface");
    }
}
```

---

### Q53: Abstract Class vs Interface?
**A:**
| Feature | Abstract Class | Interface |
|---------|---------------|-----------|
| Methods | Abstract + concrete | Abstract + default + static |
| Variables | Any type | Only `public static final` |
| Constructor | Yes | No |
| Inheritance | Single (`extends`) | Multiple (`implements`) |
| When to use | Shared code among related classes | Contract for unrelated classes |

---

### Q54: What is Upcasting and Downcasting?
**A:**
```java
// Upcasting → child to parent (automatic, always safe)
Animal a = new Dog();
a.sound(); // calls Dog's sound()

// Downcasting → parent to child (manual, risky)
Dog d = (Dog) a;  // works because 'a' is actually a Dog
d.bark();

// Safe downcasting with instanceof
if (a instanceof Dog) {
    Dog d2 = (Dog) a;
}

// Java 16+ pattern matching
if (a instanceof Dog d3) {
    d3.bark();  // d3 already cast
}
```

---

# SECTION 8: IMPORTANT KEYWORDS

---

### Q55: What is `static` keyword?
**A:** Belongs to the **class**, not any object. Shared across all instances.
```java
class Counter {
    static int count = 0;  // shared by all objects
    
    Counter() { count++; }
    
    static void showCount() {
        System.out.println("Objects: " + count);
    }
}

new Counter();
new Counter();
new Counter();
Counter.showCount(); // Objects: 3  (no object needed to call)
```
**Uses:** static variable, static method, static block, static inner class.

---

### Q56: What is `final` keyword?
**A:**
```java
// final variable → CONSTANT (can't change)
final double PI = 3.14159;
// PI = 3.14;  ← ERROR!

// final method → can't be OVERRIDDEN
class Parent {
    final void show() { System.out.println("Can't override me"); }
}

// final class → can't be EXTENDED
final class Utility { }
// class MyUtil extends Utility { }  ← ERROR!
```

---

### Q57: Difference between `final`, `finally`, and `finalize()`?
**A:**
| Keyword | Purpose |
|---------|---------|
| `final` | Constant variable / prevent override / prevent inheritance |
| `finally` | Block that always runs after try-catch (cleanup) |
| `finalize()` | Method called by GC before destroying object (deprecated since Java 9) |

---

### Q58: What is `instanceof` operator?
**A:** Checks if an object is an instance of a class.
```java
Animal a = new Dog();
System.out.println(a instanceof Dog);    // true
System.out.println(a instanceof Animal); // true
System.out.println(a instanceof Cat);    // false
```

---

# SECTION 9: EXCEPTION HANDLING

---

### Q59: What is an Exception? Types?
**A:** An unwanted event that disrupts program flow.
```
Throwable
├── Error (can't handle) → OutOfMemoryError, StackOverflowError
└── Exception
    ├── Checked (compile-time) → IOException, SQLException
    └── Unchecked (runtime) → NullPointerException, ArithmeticException
```

---

### Q60: How does try-catch-finally work?
**A:**
```java
try {
    int result = 10 / 0;  // ArithmeticException
} catch (ArithmeticException e) {
    System.out.println("Error: " + e.getMessage());  // "/ by zero"
} finally {
    System.out.println("Always runs!");  // cleanup
}
System.out.println("Program continues...");
```

---

### Q61: Difference between `throw` and `throws`?
**A:**
```java
// throw → actually throw an exception
static void checkAge(int age) {
    if (age < 18) {
        throw new IllegalArgumentException("Too young!");
    }
}

// throws → declare that method might throw exception
static void readFile() throws IOException {
    FileReader fr = new FileReader("file.txt");
}

// Caller must handle
try {
    readFile();
} catch (IOException e) {
    System.out.println("File error!");
}
```

---

### Q62: Difference between checked and unchecked exceptions?
**A:**
| Feature | Checked | Unchecked |
|---------|---------|-----------|
| When detected | Compile time | Runtime |
| Must handle? | Yes (try-catch or throws) | Optional |
| Extends | `Exception` | `RuntimeException` |
| Examples | IOException, SQLException | NullPointerException, ArithmeticException |

---

### Q63: How to create a custom exception?
**A:**
```java
class AgeException extends Exception {
    AgeException(String msg) { super(msg); }
}

static void validate(int age) throws AgeException {
    if (age < 0) throw new AgeException("Age can't be negative!");
}

try {
    validate(-5);
} catch (AgeException e) {
    System.out.println(e.getMessage()); // "Age can't be negative!"
}
```

---

### Q64: What is try-with-resources?
**A:** Automatically closes resources. No need for `finally`.
```java
// Resource (BufferedReader) is auto-closed after try block
try (BufferedReader br = new BufferedReader(new FileReader("file.txt"))) {
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
}
```

---

### Q65: Can `finally` block NOT execute?
**A:** Only if `System.exit()` is called or JVM crashes. Otherwise, it **always** runs.

---

### Q66: Can we have multiple catch blocks?
**A:** Yes. Order from **most specific to most general**.
```java
try {
    int[] arr = {1};
    System.out.println(arr[5]);
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Invalid index");
} catch (Exception e) {  // general catch last
    System.out.println("Some error");
}

// Multi-catch (Java 7+)
catch (IOException | SQLException e) {
    System.out.println(e.getMessage());
}
```

---

# SECTION 10: WRAPPER CLASSES & ENUMS

---

### Q67: What are Wrapper Classes?
**A:** Convert primitives to objects. Needed for Collections.
```java
// Autoboxing: primitive → object (automatic)
int num = 10;
Integer obj = num;

// Unboxing: object → primitive (automatic)
Integer obj2 = 20;
int num2 = obj2;

// Useful methods
int x = Integer.parseInt("123");      // String → int
String s = String.valueOf(456);       // int → String
int max = Integer.MAX_VALUE;          // 2147483647
```

---

### Q68: What is the Integer Cache?
**A:** Java caches Integer values from **-128 to 127**. Same-value Integers in this range share the same object.
```java
Integer a = 127, b = 127;
System.out.println(a == b);    // true  (cached!)

Integer c = 128, d = 128;
System.out.println(c == d);    // false (not cached!)
System.out.println(c.equals(d)); // true  (always use equals!)
```

---

### Q69: What is an Enum?
**A:** A special class for a **fixed set of constants**.
```java
enum Status { ACTIVE, INACTIVE, PENDING }

Status s = Status.ACTIVE;
System.out.println(s);           // ACTIVE
System.out.println(s.ordinal()); // 0 (index)

// Enum with fields
enum Planet {
    EARTH(5.97e24), MARS(6.42e23);
    private final double mass;
    Planet(double mass) { this.mass = mass; } // constructor always private
    double getMass() { return mass; }
}
```

---

# SECTION 11: COLLECTIONS FRAMEWORK

---

### Q70: What is the Collections Framework?
**A:** A set of classes and interfaces for storing and manipulating groups of objects.
```
Collection
├── List (ordered, duplicates allowed)
│   ├── ArrayList   → fast read
│   └── LinkedList  → fast insert/delete
├── Set (no duplicates)
│   ├── HashSet     → no order
│   ├── LinkedHashSet → insertion order
│   └── TreeSet     → sorted
└── Queue (FIFO)
    └── PriorityQueue → sorted

Map (key-value pairs, NOT part of Collection)
├── HashMap       → no order
├── LinkedHashMap → insertion order
└── TreeMap       → sorted by key
```

---

### Q71: How does ArrayList work?
**A:**
```java
import java.util.*;

ArrayList<String> list = new ArrayList<>();
list.add("Apple");
list.add("Banana");
list.add("Cherry");
list.add("Apple");          // duplicates OK!

list.get(0);                // "Apple"
list.size();                // 4
list.set(1, "Blueberry");  // replace at index 1
list.remove("Apple");       // removes first occurrence
list.contains("Cherry");    // true
Collections.sort(list);     // sort alphabetically

for (String item : list) {
    System.out.println(item);
}
```

---

### Q72: ArrayList vs LinkedList?
**A:**
| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| Structure | Dynamic array | Doubly linked list |
| Read/Get | Fast O(1) | Slow O(n) |
| Insert/Delete | Slow O(n) | Fast O(1) |
| Memory | Less | More (stores pointers) |
| Best for | Frequent reads | Frequent inserts/deletes |

---

### Q73: How does HashSet work?
**A:** Stores **unique** elements only. Uses hashing. **No order** guaranteed.
```java
HashSet<String> set = new HashSet<>();
set.add("Java");
set.add("Python");
set.add("Java");    // duplicate → IGNORED!

System.out.println(set.size());     // 2
System.out.println(set.contains("Java")); // true

// LinkedHashSet → keeps insertion order
// TreeSet → keeps sorted order, no nulls
```

---

### Q74: How does HashMap work?
**A:** Stores **key-value pairs**. Keys must be unique.
```java
import java.util.*;

HashMap<String, Integer> map = new HashMap<>();
map.put("Rahul", 90);
map.put("Priya", 85);
map.put("Rahul", 95);   // overwrites! (duplicate key)

map.get("Rahul");        // 95
map.containsKey("Priya");// true
map.size();              // 2
map.remove("Priya");
map.getOrDefault("Amit", 0); // 0 (not found)

// Iterate
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " = " + entry.getValue());
}
```

---

### Q75: How does HashMap work internally?
**A:**
1. Uses an **array of buckets** (default 16)
2. Key's `hashCode()` determines which bucket
3. If collision → stored as **linked list** in that bucket
4. Java 8+: linked list → **tree** when bucket has >8 entries
5. **Load factor** = 0.75 → resizes when 75% full

---

### Q76: HashMap vs Hashtable vs ConcurrentHashMap?
**A:**
| Feature | HashMap | Hashtable | ConcurrentHashMap |
|---------|---------|-----------|-------------------|
| Thread-safe | No | Yes | Yes |
| Null keys | 1 allowed | Not allowed | Not allowed |
| Performance | Fastest | Slowest | Fast (segment locking) |
| Legacy? | No | Yes (avoid it) | No |

---

### Q77: What is the difference between Comparable and Comparator?
**A:**
```java
// Comparable → natural ordering (inside the class)
class Student implements Comparable<Student> {
    String name; int marks;
    Student(String n, int m) { name = n; marks = m; }
    
    @Override
    public int compareTo(Student other) {
        return this.marks - other.marks;  // ascending
    }
}
Collections.sort(students); // uses compareTo

// Comparator → custom ordering (outside the class)
students.sort((s1, s2) -> s1.name.compareTo(s2.name));  // sort by name
students.sort(Comparator.comparingInt(s -> s.marks));     // sort by marks
```

| Feature | Comparable | Comparator |
|---------|-----------|------------|
| Method | `compareTo()` | `compare()` |
| Defined in | Same class | Separate class / lambda |
| Orderings | One only | Multiple |

---

### Q78: What is Iterator?
**A:** A universal way to traverse any collection. Allows safe removal during iteration.
```java
ArrayList<String> list = new ArrayList<>(List.of("A", "B", "C"));

Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String val = it.next();
    if (val.equals("B")) it.remove();  // safe removal
}
System.out.println(list); // [A, C]
```

---

### Q79: What is fail-fast vs fail-safe?
**A:**
- **Fail-fast:** Throws `ConcurrentModificationException` if collection modified during iteration (ArrayList, HashMap)
- **Fail-safe:** Works on a copy. No exception. (ConcurrentHashMap, CopyOnWriteArrayList)

---

### Q80: Stack and Queue?
**A:**
```java
// Stack → LIFO (Last In, First Out)
Stack<String> stack = new Stack<>();
stack.push("A"); stack.push("B"); stack.push("C");
stack.peek();  // C (view top, don't remove)
stack.pop();   // C (remove top)

// Queue → FIFO (First In, First Out)
Queue<String> queue = new LinkedList<>();
queue.offer("A"); queue.offer("B"); queue.offer("C");
queue.peek();  // A (view front)
queue.poll();  // A (remove front)

// PriorityQueue → sorted
PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(30); pq.offer(10); pq.offer(20);
pq.poll(); // 10 (smallest first)
```

---

# SECTION 12: JAVA 8+ FEATURES

---

### Q81: What is a Lambda Expression?
**A:** A concise way to write anonymous functions. Works only with **functional interfaces**.
```java
// Old way
Runnable old = new Runnable() {
    @Override
    public void run() { System.out.println("Old"); }
};

// Lambda way
Runnable lambda = () -> System.out.println("Lambda!");

// More examples
(a, b) -> a + b             // two params, returns sum
x -> x * x                  // one param, returns square
(a, b) -> { return a + b; } // with block body
```

---

### Q82: What is a Functional Interface?
**A:** An interface with **exactly one abstract method**. Lambda works only with these.
```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

Calculator add = (a, b) -> a + b;
Calculator multiply = (a, b) -> a * b;

System.out.println(add.calculate(5, 3));      // 8
System.out.println(multiply.calculate(5, 3)); // 15
```

**Built-in functional interfaces:**
```java
import java.util.function.*;

Predicate<Integer> isEven = n -> n % 2 == 0;   // returns boolean
Function<String, Integer> len = s -> s.length(); // transforms
Consumer<String> print = s -> System.out.println(s); // no return
Supplier<Double> random = () -> Math.random();  // no input
```

---

### Q83: What is Method Reference?
**A:** A shorter form of lambda when calling an existing method.
```java
List<String> names = List.of("Rahul", "Priya", "Amit");

// Lambda
names.forEach(n -> System.out.println(n));

// Method reference (same thing)
names.forEach(System.out::println);

// Types:
Integer::parseInt        // static method
str::toUpperCase         // instance method of specific object
String::toUpperCase      // instance method of any String
ArrayList::new           // constructor reference
```

---

### Q84: What is the Stream API?
**A:** A pipeline for processing collections in functional style. Does NOT modify the original.
```java
List<Integer> nums = List.of(5, 3, 8, 1, 9, 2, 4);

// filter → keep elements matching condition
List<Integer> evens = nums.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());     // [8, 2, 4]

// map → transform each element
List<Integer> doubled = nums.stream()
    .map(n -> n * 2)
    .collect(Collectors.toList());     // [10, 6, 16, 2, 18, 4, 8]

// sorted
List<Integer> sorted = nums.stream()
    .sorted()
    .collect(Collectors.toList());     // [1, 2, 3, 4, 5, 8, 9]

// chained operations
List<Integer> result = nums.stream()
    .filter(n -> n > 3)         // keep > 3
    .map(n -> n * 10)           // multiply by 10
    .sorted()                   // sort
    .collect(Collectors.toList()); // [50, 80, 90]
```

---

### Q85: What are intermediate vs terminal operations in Streams?
**A:**
| Type | Returns | Execution | Examples |
|------|---------|-----------|---------|
| Intermediate | Stream (chainable) | Lazy | `filter`, `map`, `sorted`, `distinct`, `limit`, `skip` |
| Terminal | Result | Eager | `collect`, `count`, `forEach`, `reduce`, `min`, `max`, `findFirst` |

```java
// Terminal operations
long count = nums.stream().filter(n -> n > 3).count();             // 3
int sum = nums.stream().mapToInt(Integer::intValue).sum();          // 32
Optional<Integer> max = nums.stream().max(Integer::compare);       // 9
boolean anyEven = nums.stream().anyMatch(n -> n % 2 == 0);        // true
int total = nums.stream().reduce(0, Integer::sum);                 // 32
```

---

### Q86: Stream with Strings and Objects?
**A:**
```java
List<String> names = List.of("Rahul", "Priya", "Amit", "Ravi");

// Filter + transform + join
String result = names.stream()
    .filter(n -> n.startsWith("R"))
    .map(String::toUpperCase)
    .collect(Collectors.joining(", "));
System.out.println(result); // "RAHUL, RAVI"

// Group by first letter
Map<Character, List<String>> grouped = names.stream()
    .collect(Collectors.groupingBy(n -> n.charAt(0)));
// {R=[Rahul, Ravi], P=[Priya], A=[Amit]}

// Stream with objects
List<Employee> employees = List.of(
    new Employee("Rahul", "IT", 50000),
    new Employee("Priya", "HR", 60000),
    new Employee("Amit", "IT", 70000)
);

// Highest salary
Employee richest = employees.stream()
    .max(Comparator.comparingDouble(e -> e.salary))
    .get();

// Names of IT employees
List<String> itNames = employees.stream()
    .filter(e -> e.dept.equals("IT"))
    .map(e -> e.name)
    .collect(Collectors.toList()); // [Rahul, Amit]
```

---

### Q87: Difference between `map()` and `flatMap()`?
**A:**
```java
// map → one-to-one
List<String> words = List.of("Hello", "World");
List<Integer> lengths = words.stream()
    .map(String::length)
    .collect(Collectors.toList()); // [5, 5]

// flatMap → one-to-many (flattens nested structures)
List<List<Integer>> nested = List.of(List.of(1,2), List.of(3,4));
List<Integer> flat = nested.stream()
    .flatMap(Collection::stream)
    .collect(Collectors.toList()); // [1, 2, 3, 4]
```

---

### Q88: Can we reuse a Stream?
**A:** **No.** A stream can be consumed only once. Trying to reuse throws `IllegalStateException`.

---

### Q89: What is Optional?
**A:** A container that may or may not hold a value. Avoids `NullPointerException`.
```java
Optional<String> name = Optional.of("Rahul");
Optional<String> empty = Optional.empty();
Optional<String> nullable = Optional.ofNullable(null);

name.isPresent();              // true
name.get();                    // "Rahul"
empty.orElse("Default");       // "Default"
nullable.orElseGet(() -> "Computed");
name.ifPresent(n -> System.out.println(n));
name.map(String::toUpperCase); // Optional["RAHUL"]
```

---

### Q90: What is the Java 8 Date/Time API?
**A:**
```java
import java.time.*;
import java.time.format.DateTimeFormatter;

LocalDate today = LocalDate.now();          // 2026-02-22
LocalTime now = LocalTime.now();            // 14:30:45
LocalDateTime dt = LocalDateTime.now();     // 2026-02-22T14:30:45

LocalDate birthday = LocalDate.of(2000, 5, 15);
LocalDate nextWeek = today.plusDays(7);

// Format
DateTimeFormatter fmt = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = today.format(fmt);       // 22-02-2026

// Parse
LocalDate parsed = LocalDate.parse("15-05-2000", fmt);

// Period (difference)
Period age = Period.between(birthday, today);
System.out.println(age.getYears() + " years");
```

---

# SECTION 13: MULTITHREADING

---

### Q91: What is a Thread? How to create one?
**A:** A lightweight subprocess — smallest unit of execution.
```java
// Method 1: Extend Thread
class MyThread extends Thread {
    public void run() { System.out.println("Thread running"); }
}
new MyThread().start();

// Method 2: Implement Runnable (preferred)
Thread t = new Thread(() -> System.out.println("Runnable running"));
t.start();

// Method 3: Lambda
new Thread(() -> System.out.println("Lambda thread")).start();
```

---

### Q92: Difference between `start()` and `run()`?
**A:**
- `start()` → Creates **new thread** + calls `run()` in it
- `run()` → Executes in **current** thread (no new thread)

---

### Q93: What is synchronization?
**A:** Allowing only **one thread** to access shared resource at a time.
```java
class Counter {
    int count = 0;
    synchronized void increment() {  // only one thread at a time
        count++;
    }
}
```

---

### Q94: Difference between `wait()` and `sleep()`?
**A:**
| Feature | `wait()` | `sleep()` |
|---------|----------|-----------|
| Called on | Object | Thread class |
| Lock | Releases lock | Keeps lock |
| Wake up | `notify()` / `notifyAll()` | After timeout |
| Use | Inter-thread communication | Pause execution |

---

### Q95: What is deadlock?
**A:** Two threads waiting for each other's locks forever.
```
Thread A holds Lock1, waits for Lock2
Thread B holds Lock2, waits for Lock1
→ Both stuck forever!
```
**Prevention:** Always acquire locks in the **same order**.

---

### Q96: What is ExecutorService?
**A:** A thread pool manager — reuses threads instead of creating new ones.
```java
ExecutorService executor = Executors.newFixedThreadPool(3);
for (int i = 0; i < 5; i++) {
    int task = i;
    executor.submit(() -> System.out.println("Task " + task));
}
executor.shutdown();
```

---

# SECTION 14: GENERICS & MISCELLANEOUS

---

### Q97: What are Generics?
**A:** Write type-safe code that works with any data type.
```java
// Generic class
class Box<T> {
    T item;
    void set(T item) { this.item = item; }
    T get() { return item; }
}

Box<String> sBox = new Box<>();
sBox.set("Hello");
String val = sBox.get();  // no casting needed!

Box<Integer> iBox = new Box<>();
iBox.set(42);

// Generic method
static <T> void print(T item) {
    System.out.println(item);
}

// Bounded generic → only Number or subclasses
static <T extends Number> double sum(T a, T b) {
    return a.doubleValue() + b.doubleValue();
}
```

---

### Q98: What is Type Erasure?
**A:** Generic type info is removed at compile time. At runtime, `List<String>` and `List<Integer>` are both just `List`.

---

### Q99: What is Serialization?
**A:** Converting an object to byte stream (to save to file or send over network).
```java
class Student implements Serializable {
    String name;
    transient String password;  // NOT serialized
}

// Save
ObjectOutputStream oos = new ObjectOutputStream(new FileOutputStream("data.ser"));
oos.writeObject(student);

// Load
ObjectInputStream ois = new ObjectInputStream(new FileInputStream("data.ser"));
Student loaded = (Student) ois.readObject();
```

---

### Q100: What are Records (Java 14+)?
**A:** Concise immutable data classes.
```java
// Old way → 30+ lines of boilerplate
class PersonOld {
    private final String name;
    private final int age;
    // constructor, getters, toString, equals, hashCode...
}

// Record → 1 line!
record Person(String name, int age) { }

Person p = new Person("Rahul", 25);
p.name();  // "Rahul"  (getter)
p.age();   // 25
System.out.println(p); // Person[name=Rahul, age=25]
```

---

### Q101: What are Sealed Classes (Java 17+)?
**A:** Restrict which classes can extend a class.
```java
sealed class Shape permits Circle, Rectangle { }
final class Circle extends Shape { }
final class Rectangle extends Shape { }
// class Triangle extends Shape { }  ❌ Not permitted!
```

---

### Q102: What is the Object class?
**A:** Root of all Java classes. Every class implicitly extends `Object`.
**Key methods:**
| Method | Purpose |
|--------|---------|
| `toString()` | String representation |
| `equals()` | Content comparison |
| `hashCode()` | Hash code for HashMap |
| `clone()` | Create copy |
| `getClass()` | Get class info |
| `wait()`, `notify()` | Thread communication |

---

### Q103: What is Garbage Collection?
**A:** JVM automatically destroys objects with no references.
```java
Student s = new Student();
s = null;  // object eligible for GC
System.gc(); // request GC (not guaranteed)
```

---

### Q104: What is Immutable Class? How to create?
**A:** A class whose objects can't be modified after creation.
```java
final class Money {                    // 1. final class
    private final double amount;        // 2. private final fields
    private final String currency;
    
    public Money(double amt, String cur) { // 3. Constructor
        this.amount = amt;
        this.currency = cur;
    }
    
    public double getAmount() { return amount; }    // 4. Only getters
    public String getCurrency() { return currency; }
    // NO setters!
}
```

---

### Q105: What is the `volatile` keyword?
**A:** Ensures a variable is always read from **main memory**, not thread cache. Guarantees visibility but not atomicity.
```java
volatile boolean running = true;
```

---

# SECTION 15: COMMON CODING PROBLEMS

---

### Q106: Reverse a String
```java
String rev = new StringBuilder("Hello").reverse().toString(); // "olleH"
```

### Q107: Check Palindrome
```java
String s = "madam";
boolean isPalin = s.equals(new StringBuilder(s).reverse().toString()); // true
```

### Q108: FizzBuzz
```java
for (int i = 1; i <= 100; i++) {
    if (i % 15 == 0) System.out.println("FizzBuzz");
    else if (i % 3 == 0) System.out.println("Fizz");
    else if (i % 5 == 0) System.out.println("Buzz");
    else System.out.println(i);
}
```

### Q109: Find Duplicate Characters
```java
String str = "programming";
str.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()))
    .entrySet().stream()
    .filter(e -> e.getValue() > 1)
    .forEach(e -> System.out.println(e.getKey() + " = " + e.getValue()));
// r = 2, g = 2, m = 2
```

### Q110: Find Second Largest in Array
```java
int[] arr = {5, 3, 8, 1, 9, 2};
int secondMax = Arrays.stream(arr)
    .boxed()
    .sorted(Comparator.reverseOrder())
    .distinct()
    .skip(1)
    .findFirst()
    .get();  // 8
```

### Q111: Check Anagram
```java
boolean isAnagram = Arrays.equals(
    "listen".chars().sorted().toArray(),
    "silent".chars().sorted().toArray()
); // true
```

### Q112: Remove Duplicates from List
```java
List<Integer> list = List.of(1, 2, 2, 3, 3, 4);
List<Integer> unique = list.stream().distinct().collect(Collectors.toList());
// [1, 2, 3, 4]
```

### Q113: Find First Non-Repeated Character
```java
Character result = "aabcbd".chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(e -> e.getValue() == 1)
    .map(Map.Entry::getKey)
    .findFirst()
    .orElse(null); // 'c'
```

### Q114: Fibonacci Series
```java
// Using loop
int a = 0, b = 1;
for (int i = 0; i < 10; i++) {
    System.out.print(a + " ");
    int temp = a + b;
    a = b;
    b = temp;
}
// 0 1 1 2 3 5 8 13 21 34

// Using Stream
Stream.iterate(new int[]{0, 1}, f -> new int[]{f[1], f[0] + f[1]})
    .limit(10).map(f -> f[0]).forEach(n -> System.out.print(n + " "));
```

### Q115: Sort Map by Values
```java
Map<String, Integer> map = Map.of("Banana", 2, "Apple", 5, "Cherry", 1);
Map<String, Integer> sorted = map.entrySet().stream()
    .sorted(Map.Entry.comparingByValue())
    .collect(Collectors.toMap(Map.Entry::getKey, Map.Entry::getValue,
        (e1, e2) -> e1, LinkedHashMap::new));
// {Cherry=1, Banana=2, Apple=5}
```

---

# QUICK REVISION CHEAT SHEET

| Topic | Key Points |
|-------|-----------|
| JVM/JRE/JDK | JVM ⊂ JRE ⊂ JDK |
| Primitives | 8 types: byte, short, int, long, float, double, char, boolean |
| String | Immutable, String Pool, use StringBuilder for modification |
| `==` vs `equals()` | Reference vs content comparison |
| OOP Pillars | Encapsulation, Inheritance, Polymorphism, Abstraction |
| Overloading | Same name, different params, compile-time |
| Overriding | Same signature in child, runtime |
| Abstract Class | Partial implementation, single `extends`, has constructor |
| Interface | Contract, multiple `implements`, no constructor |
| Exceptions | Checked (compile) vs Unchecked (runtime) |
| ArrayList | Dynamic array, fast read O(1), slow insert O(n) |
| LinkedList | Doubly linked, slow read O(n), fast insert O(1) |
| HashMap | Key-value, array of buckets, O(1) avg, load factor 0.75 |
| HashSet | No duplicates, backed by HashMap |
| Threads | Thread/Runnable, synchronized, volatile, start() not run() |
| Lambda | `(params) -> body`, needs functional interface |
| Stream | filter → map → sort → collect, lazy until terminal op |
| Optional | Avoid NPE, orElse(), isPresent(), map() |
| Generics | Type safety, type erasure at runtime |
| Records | Concise immutable data class (Java 14+) |

---

> **Study Tip:** Read this file top to bottom. Try to answer each question BEFORE reading the answer. Practice coding daily. Good luck!

---
