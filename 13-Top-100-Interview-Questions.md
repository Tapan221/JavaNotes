# 📘 CHAPTER 13: TOP 100 JAVA INTERVIEW QUESTIONS & ANSWERS

---

## SECTION A: CORE JAVA BASICS (Q1–Q20)

---

**Q1: What is Java?**
> A high-level, object-oriented, platform-independent programming language developed by James Gosling at Sun Microsystems (1995).

**Q2: What does "Write Once, Run Anywhere" (WORA) mean?**
> Java code compiles to bytecode which runs on any platform with a JVM, regardless of the underlying OS.

**Q3: Difference between JDK, JRE, and JVM?**
> | Component | Purpose |
> |-----------|---------|
> | JVM | Executes bytecode |
> | JRE | JVM + libraries (run programs) |
> | JDK | JRE + dev tools (develop programs) |

**Q4: What are the primitive data types in Java?**
> `byte` (1B), `short` (2B), `int` (4B), `long` (8B), `float` (4B), `double` (8B), `char` (2B), `boolean` (1 bit)

**Q5: Difference between `==` and `.equals()`?**
> - `==` compares memory references
> - `.equals()` compares content/values

**Q6: What is type casting?**
> - **Widening** (auto): `int → double`
> - **Narrowing** (manual): `double → int` using `(int)`

**Q7: Difference between `break` and `continue`?**
> `break` exits the loop completely. `continue` skips current iteration.

**Q8: Difference between `while` and `do-while`?**
> `while` checks condition first. `do-while` executes once before checking.

**Q9: What is the default value of instance variables?**
> `int`→0, `double`→0.0, `boolean`→false, `Object`→null. Local variables have no default.

**Q10: Can a `.java` file have multiple classes?**
> Yes, but only ONE public class allowed, and the file name must match the public class name.

**Q11: What is the `main()` method signature?**
> `public static void main(String[] args)` — must be exact. Can overload but JVM only calls this one.

**Q12: What is a package?**
> A namespace for organizing classes. E.g., `java.util`, `java.io`. Avoids naming conflicts.

**Q13: What are access modifiers?**
> `private` (same class) → `default` (same package) → `protected` (same package + subclass) → `public` (everywhere)

**Q14: What is `static` keyword?**
> Belongs to class, not object. Can access without creating object. Shared across all instances.

**Q15: What is `final` keyword?**
> Variable → constant. Method → can't override. Class → can't extend.

**Q16: Difference between `final`, `finally`, `finalize`?**
> - `final`: keyword for constants/preventing override/inheritance
> - `finally`: block that always executes after try-catch
> - `finalize()`: GC calls before destroying object (deprecated)

**Q17: Can we overload `main()` method?**
> Yes, but JVM always calls `public static void main(String[] args)`.

**Q18: What is `var` keyword (Java 10)?**
> Local variable type inference: `var name = "Hello";` Compiler infers the type.

**Q19: Difference between `Array` and `ArrayList`?**
> Array: fixed size, holds primitives + objects. ArrayList: dynamic, only objects, more methods.

**Q20: What is an `enum`?**
> A special class for fixed set of constants. Has constructors (private), methods, and fields.

---

## SECTION B: OOP CONCEPTS (Q21–Q45)

---

**Q21: What are the 4 pillars of OOP?**
> 1. **Encapsulation** – data hiding with private + getters/setters
> 2. **Inheritance** – code reuse via extends
> 3. **Polymorphism** – one thing, many forms
> 4. **Abstraction** – hide implementation details

**Q22: Difference between class and object?**
> Class = blueprint. Object = instance of class (real entity in memory).

**Q23: What is encapsulation? How to achieve?**
> Wrapping data + methods, restricting access. Achieved using `private` fields + public getters/setters.

**Q24: Types of inheritance in Java?**
> Single, Multilevel, Hierarchical. Java does NOT support multiple inheritance with classes (uses interfaces).

**Q25: Why no multiple inheritance with classes?**
> To avoid the **Diamond Problem** — ambiguity when two parent classes have same method.

**Q26: Difference between method overloading and overriding?**
> | Feature | Overloading | Overriding |
> |---------|------------|------------|
> | Where | Same class | Parent-child |
> | Parameters | Different | Same |
> | Binding | Compile-time | Runtime |

**Q27: Can we override `static` methods?**
> No. They are **hidden** (method hiding), not overridden. Resolved at compile time.

**Q28: Can we override `private` methods?**
> No. Private methods are not visible to child classes.

**Q29: What is `super` keyword?**
> Refers to parent class. Uses: `super()` (parent constructor), `super.method()`, `super.field`.

**Q30: What is `this` keyword?**
> Refers to current object. Distinguish fields from parameters. Call constructors with `this()`.

**Q31: Can a constructor be `private`?**
> Yes! Used in Singleton pattern to prevent external object creation.

**Q32: What is constructor chaining?**
> Calling one constructor from another using `this()` or `super()`.

**Q33: Difference between abstract class and interface?**
> | Feature | Abstract Class | Interface |
> |---------|---------------|-----------|
> | Methods | Abstract + concrete | Abstract (+default Java 8) |
> | Variables | Any | public static final |
> | Constructor | Yes | No |
> | Extends | Single | Multiple |

**Q34: When to use abstract class vs interface?**
> Abstract class: partial implementation shared among related classes.
> Interface: contract for unrelated classes, or need multiple inheritance.

**Q35: Can we create an object of abstract class?**
> No, but can create reference: `Shape s = new Circle();`

**Q36: Can an interface have a constructor?**
> No. Interfaces cannot be instantiated.

**Q37: What are default methods in interfaces (Java 8)?**
> Concrete methods with `default` keyword. Allows adding methods without breaking existing implementations.

**Q38: What is the Diamond Problem? How does Java solve it?**
> When a class inherits from two classes with same method. Java prevents this for classes. For interfaces, the implementing class must override the conflicting method.

**Q39: What is upcasting and downcasting?**
> Upcasting: `Animal a = new Dog();` (automatic). Downcasting: `Dog d = (Dog) a;` (manual, risky).

**Q40: What is `instanceof` operator?**
> Checks if an object is an instance of a class: `obj instanceof String`

**Q41: What is covariant return type?**
> Overriding method can return a subtype of the parent's return type.

**Q42: What is association, aggregation, composition?**
> - Association: general relationship (teacher-student)
> - Aggregation: weak "has-a" (department-teacher; teacher exists independently)
> - Composition: strong "has-a" (house-room; room doesn't exist without house)

**Q43: What is marker interface?**
> Empty interface with no methods. E.g., `Serializable`, `Cloneable`. Acts as a tag/signal.

**Q44: What is the Object class?**
> Root class of all Java classes. Methods: `toString()`, `equals()`, `hashCode()`, `clone()`, `finalize()`, `getClass()`, `wait()`, `notify()`.

**Q45: Why override `equals()` and `hashCode()` together?**
> Contract: equal objects must have same hashCode. Required for correct behavior in HashMap, HashSet.

---

## SECTION C: STRINGS (Q46–Q55)

---

**Q46: Why is String immutable?**
> String Pool safety, security (passwords), thread safety, hashCode caching.

**Q47: How many objects: `String s = new String("Hello");`?**
> 2 objects — one in String Pool ("Hello"), one in Heap (new String).

**Q48: Difference between String, StringBuilder, StringBuffer?**
> String: immutable. StringBuilder: mutable, fast, not thread-safe. StringBuffer: mutable, thread-safe, slower.

**Q49: What is the String Pool?**
> Special memory area in heap where String literals are stored and shared.

**Q50: What does `intern()` method do?**
> Puts string into the String Pool if not already present, returns pooled reference.

**Q51: How to reverse a String?**
> `new StringBuilder(str).reverse().toString()`

**Q52: How to check if a String is a palindrome?**
> Compare with its reverse: `str.equals(new StringBuilder(str).reverse().toString())`

**Q53: Difference between `concat()` and `+`?**
> `concat()` throws NPE on null; `+` converts null to "null" string.

**Q54: How to convert String to int and vice versa?**
> `Integer.parseInt("123")` and `String.valueOf(123)`

**Q55: What is the difference between `length`, `length()`, `size()`?**
> `length` → array property, `length()` → String method, `size()` → Collection method.

---

## SECTION D: EXCEPTION HANDLING (Q56–Q65)

---

**Q56: Difference between checked and unchecked exceptions?**
> Checked: must handle (IOException). Unchecked: optional (NullPointerException).

**Q57: Difference between `throw` and `throws`?**
> `throw`: actually throw an exception. `throws`: declare in method signature.

**Q58: Can we have try without catch?**
> Yes, with finally: `try { } finally { }` is valid.

**Q59: What is `finally` block? When doesn't it execute?**
> Always runs after try-catch. Won't run only if `System.exit()` or JVM crash.

**Q60: What is try-with-resources?**
> Auto-closes resources. `try (BufferedReader br = ...) { }` — no need for finally.

**Q61: Can we catch multiple exceptions in one catch block?**
> Yes (Java 7+): `catch (IOException | SQLException e)`

**Q62: What is custom exception?**
> User-defined exception by extending `Exception` (checked) or `RuntimeException` (unchecked).

**Q63: What is exception propagation?**
> If a method doesn't handle an exception, it passes to the calling method up the call stack.

**Q64: Difference between `Error` and `Exception`?**
> Error: serious, unrecoverable (OutOfMemoryError). Exception: recoverable, should handle.

**Q65: Can we have a return statement in finally block?**
> Yes, but it overrides the return from try/catch. Avoid doing this!

---

## SECTION E: COLLECTIONS (Q66–Q80)

---

**Q66: What is the Collections Framework?**
> Set of interfaces and classes for storing/manipulating groups of objects. Includes List, Set, Map, Queue.

**Q67: Difference between List, Set, and Map?**
> List: ordered, duplicates allowed. Set: unordered, no duplicates. Map: key-value pairs.

**Q68: Difference between ArrayList and LinkedList?**
> ArrayList: fast read (O(1)), slow insert. LinkedList: fast insert (O(1)), slow read (O(n)).

**Q69: Difference between HashSet, LinkedHashSet, TreeSet?**
> HashSet: no order. LinkedHashSet: insertion order. TreeSet: sorted order.

**Q70: How does HashMap work internally?**
> Array of buckets. `hashCode()` determines bucket. Collisions handled via linked list (→ tree when >8 nodes in Java 8+).

**Q71: HashMap vs Hashtable?**
> HashMap: not synchronized, allows null. Hashtable: synchronized, no null (legacy).

**Q72: HashMap vs ConcurrentHashMap?**
> ConcurrentHashMap: thread-safe, segments-based locking (better performance than Hashtable).

**Q73: What is fail-fast vs fail-safe?**
> Fail-fast: `ConcurrentModificationException` if modified during iteration. Fail-safe: works on copy, no exception.

**Q74: Difference between Comparable and Comparator?**
> Comparable: `compareTo()`, natural ordering, in same class. Comparator: `compare()`, custom ordering, separate class.

**Q75: When to use which collection?**
> Ordered list → ArrayList. Unique elements → HashSet. Sorted → TreeSet/TreeMap. Key-value → HashMap. Thread-safe → ConcurrentHashMap.

**Q76: What is Iterator? Difference from ListIterator?**
> Iterator: forward-only traversal. ListIterator: bidirectional, can modify during traversal, only for Lists.

**Q77: What is the load factor of HashMap?**
> 0.75 by default. When 75% full, capacity doubles.

**Q78: Can we store null in different collections?**
> ArrayList → yes. HashSet → one null. TreeSet → no. HashMap → one null key. TreeMap → no null key.

**Q79: What is `Collections.unmodifiableList()`?**
> Returns a read-only view of the list. Any modification throws `UnsupportedOperationException`.

**Q80: What is `List.of()` and `Map.of()` (Java 9+)?**
> Create immutable collections: `List.of(1, 2, 3)`, `Map.of("a", 1, "b", 2)`.

---

## SECTION F: MULTITHREADING (Q81–Q90)

---

**Q81: What is a thread?**
> A lightweight subprocess — smallest unit of processing. Shares memory with other threads.

**Q82: Difference between Thread class and Runnable interface?**
> Thread: extends, can't extend another class. Runnable: implements, can extend other class (preferred).

**Q83: Difference between `start()` and `run()`?**
> `start()` creates new thread + calls `run()`. `run()` executes in current thread.

**Q84: What is synchronization?**
> Mechanism to allow only one thread to access shared resource at a time. Uses `synchronized` keyword.

**Q85: What is deadlock?**
> Two threads waiting for each other's locks forever. Avoided by consistent lock ordering.

**Q86: Difference between `wait()` and `sleep()`?**
> `wait()` releases lock, needs notify. `sleep()` doesn't release lock, wakes automatically.

**Q87: What is volatile keyword?**
> Ensures variable is read from main memory, not thread cache. Guarantees visibility.

**Q88: What is ThreadPool / ExecutorService?**
> Manages a pool of reusable threads. More efficient than creating new threads. `Executors.newFixedThreadPool(n)`.

**Q89: Difference between Callable and Runnable?**
> Runnable: `run()`, no return, no exception. Callable: `call()`, returns value, can throw exception.

**Q90: What is `Future` in Java?**
> Represents the result of an async computation. `future.get()` blocks until result is available.

---

## SECTION G: JAVA 8+ FEATURES (Q91–Q100)

---

**Q91: What is a Lambda expression?**
> Concise anonymous function: `(a, b) -> a + b`. Works with functional interfaces.

**Q92: What is a Functional Interface?**
> Interface with exactly one abstract method. `@FunctionalInterface`. Examples: `Predicate`, `Function`, `Consumer`, `Supplier`.

**Q93: What is Stream API?**
> Pipeline for functional-style collection processing: `filter()`, `map()`, `reduce()`, `collect()`.

**Q94: Difference between `map()` and `flatMap()`?**
> `map()`: one-to-one transformation. `flatMap()`: one-to-many, flattens nested streams.

**Q95: What is Optional?**
> Container that may or may not have a value. Avoids NullPointerException. `Optional.of()`, `orElse()`, `isPresent()`.

**Q96: What are intermediate vs terminal operations in streams?**
> Intermediate: lazy, return stream (`filter`, `map`, `sorted`). Terminal: eager, produce result (`collect`, `count`, `forEach`).

**Q97: What is method reference?**
> Short form of lambda: `System.out::println` instead of `x -> System.out.println(x)`.

**Q98: What is `Collectors.groupingBy()`?**
> Groups stream elements by a classifier: `stream.collect(Collectors.groupingBy(e -> e.dept))`.

**Q99: What is a Record (Java 14+)?**
> Concise immutable data class: `record Person(String name, int age) { }`. Auto-generates constructor, getters, toString, equals, hashCode.

**Q100: What are Sealed Classes (Java 17+)?**
> Restrict which classes can extend a class: `sealed class Shape permits Circle, Rectangle { }`.

---

## BONUS: CODING QUESTIONS FREQUENTLY ASKED

---

### 1. Reverse a String
```java
String reversed = new StringBuilder("Hello").reverse().toString();
```

### 2. Check Palindrome
```java
boolean isPalindrome = str.equals(new StringBuilder(str).reverse().toString());
```

### 3. Find Duplicate Characters
```java
Map<Character, Long> freq = str.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, Collectors.counting()));
freq.entrySet().stream()
    .filter(e -> e.getValue() > 1)
    .forEach(e -> System.out.println(e.getKey() + " = " + e.getValue()));
```

### 4. FizzBuzz
```java
for (int i = 1; i <= 100; i++) {
    if (i % 15 == 0) System.out.println("FizzBuzz");
    else if (i % 3 == 0) System.out.println("Fizz");
    else if (i % 5 == 0) System.out.println("Buzz");
    else System.out.println(i);
}
```

### 5. Find Second Largest in Array
```java
int[] arr = {5, 3, 8, 1, 9, 2};
int result = Arrays.stream(arr)
    .distinct()
    .sorted()
    .skip(arr.length - 2)  // or use boxed().sorted(reverseOrder()).skip(1)
    .findFirst()
    .getAsInt();
```

### 6. Check Anagram
```java
boolean isAnagram = Arrays.equals(
    s1.chars().sorted().toArray(),
    s2.chars().sorted().toArray()
);
```

### 7. Remove Duplicates from List
```java
List<Integer> unique = list.stream().distinct().collect(Collectors.toList());
// OR
Set<Integer> unique2 = new LinkedHashSet<>(list);
```

### 8. Fibonacci Series
```java
Stream.iterate(new int[]{0, 1}, f -> new int[]{f[1], f[0] + f[1]})
    .limit(10)
    .map(f -> f[0])
    .forEach(n -> System.out.print(n + " "));
// Output: 0 1 1 2 3 5 8 13 21 34
```

### 9. Sort a Map by Values
```java
Map<String, Integer> sorted = map.entrySet().stream()
    .sorted(Map.Entry.comparingByValue())
    .collect(Collectors.toMap(
        Map.Entry::getKey, Map.Entry::getValue,
        (e1, e2) -> e1, LinkedHashMap::new
    ));
```

### 10. Find First Non-Repeated Character
```java
Character result = str.chars()
    .mapToObj(c -> (char) c)
    .collect(Collectors.groupingBy(c -> c, LinkedHashMap::new, Collectors.counting()))
    .entrySet().stream()
    .filter(e -> e.getValue() == 1)
    .map(Map.Entry::getKey)
    .findFirst()
    .orElse(null);
```

---

## QUICK REVISION TABLE

| Topic | Key Points |
|-------|-----------|
| JVM/JRE/JDK | JVM ⊂ JRE ⊂ JDK |
| Primitive types | 8 types: byte, short, int, long, float, double, char, boolean |
| String | Immutable, String Pool, StringBuilder for modification |
| OOP | Encapsulation, Inheritance, Polymorphism, Abstraction |
| Overloading | Same class, different params, compile-time |
| Overriding | Parent-child, same signature, runtime |
| Abstract class | Partial implementation, single extends, has constructor |
| Interface | Full contract, multiple implements, no constructor |
| Exception | Checked (compile) vs Unchecked (runtime) |
| Collections | List (ordered), Set (unique), Map (key-value) |
| HashMap | Array of buckets, hashCode, O(1) avg |
| Threads | Thread/Runnable, synchronized, volatile |
| Lambda | `(params) -> body`, requires functional interface |
| Streams | filter → map → sort → collect |
| Optional | Avoid NPE, orElse, isPresent |

---

> **Tip:** Practice coding daily on LeetCode, HackerRank. Read Java docs. Build small projects. Good luck! 🎯

---
