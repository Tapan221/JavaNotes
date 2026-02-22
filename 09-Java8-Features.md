# 📘 CHAPTER 9: JAVA 8+ FEATURES (Lambda, Streams, Functional Interfaces)

---

## 9.1 Lambda Expressions

A **short way to write anonymous functions**. Makes code concise.

**Syntax:** `(parameters) -> { body }`

```java
// Without Lambda (old way)
Runnable oldWay = new Runnable() {
    @Override
    public void run() {
        System.out.println("Hello from thread");
    }
};

// With Lambda (new way)
Runnable newWay = () -> System.out.println("Hello from thread");

// More examples
// No parameter
() -> System.out.println("Hello")

// One parameter (parentheses optional)
x -> x * x

// Two parameters
(a, b) -> a + b

// Multiple statements
(a, b) -> {
    int sum = a + b;
    return sum;
}
```

---

## 9.2 Functional Interface

An interface with **exactly ONE abstract method**. Lambda works only with functional interfaces.

```java
@FunctionalInterface
interface Calculator {
    int calculate(int a, int b);
}

public class LambdaDemo {
    public static void main(String[] args) {
        // Different operations using same interface
        Calculator add = (a, b) -> a + b;
        Calculator subtract = (a, b) -> a - b;
        Calculator multiply = (a, b) -> a * b;

        System.out.println(add.calculate(10, 5));      // 15
        System.out.println(subtract.calculate(10, 5)); // 5
        System.out.println(multiply.calculate(10, 5)); // 50
    }
}
```

### Built-in Functional Interfaces (java.util.function)

| Interface | Method | Description | Example |
|-----------|--------|-------------|---------|
| `Predicate<T>` | `test(T)` → boolean | Condition check | `x -> x > 10` |
| `Function<T,R>` | `apply(T)` → R | Transform input | `x -> x * 2` |
| `Consumer<T>` | `accept(T)` → void | Use input, no return | `x -> System.out.println(x)` |
| `Supplier<T>` | `get()` → T | No input, returns value | `() -> new Random().nextInt()` |

```java
import java.util.function.*;

// Predicate – returns boolean
Predicate<Integer> isEven = n -> n % 2 == 0;
System.out.println(isEven.test(4));   // true
System.out.println(isEven.test(7));   // false

// Function – takes input, returns output
Function<String, Integer> length = str -> str.length();
System.out.println(length.apply("Hello"));  // 5

// Consumer – takes input, no return
Consumer<String> printer = msg -> System.out.println(">> " + msg);
printer.accept("Hello");  // >> Hello

// Supplier – no input, returns value
Supplier<Double> random = () -> Math.random();
System.out.println(random.get());  // 0.xxxxx
```

---

## 9.3 Method References

A **shorter way** to write lambdas when calling an existing method.

```java
import java.util.Arrays;
import java.util.List;

List<String> names = Arrays.asList("Rahul", "Priya", "Amit");

// Lambda
names.forEach(name -> System.out.println(name));

// Method reference (same thing, shorter)
names.forEach(System.out::println);
```

### Types of Method References
```java
// 1. Static method reference
Function<String, Integer> parser = Integer::parseInt;
System.out.println(parser.apply("123"));  // 123

// 2. Instance method reference
String str = "Hello World";
Supplier<String> upper = str::toUpperCase;
System.out.println(upper.get());  // HELLO WORLD

// 3. Instance method of arbitrary object
Function<String, String> toUpper = String::toUpperCase;
System.out.println(toUpper.apply("hello"));  // HELLO

// 4. Constructor reference
Supplier<ArrayList> listMaker = ArrayList::new;
ArrayList list = listMaker.get();
```

---

## 9.4 Streams API

A **pipeline** for processing collections in a functional style. Does NOT modify the original collection.

```
Source → Filter → Map → Sort → Collect
```

### Basic Stream Operations
```java
import java.util.*;
import java.util.stream.*;

List<Integer> numbers = Arrays.asList(5, 3, 8, 1, 9, 2, 7, 4, 6);

// Filter: keep only even numbers
List<Integer> evens = numbers.stream()
    .filter(n -> n % 2 == 0)
    .collect(Collectors.toList());
System.out.println(evens);  // [8, 2, 4, 6]

// Map: transform each element
List<Integer> doubled = numbers.stream()
    .map(n -> n * 2)
    .collect(Collectors.toList());
System.out.println(doubled);  // [10, 6, 16, 2, 18, 4, 14, 8, 12]

// Sort
List<Integer> sorted = numbers.stream()
    .sorted()
    .collect(Collectors.toList());
System.out.println(sorted);  // [1, 2, 3, 4, 5, 6, 7, 8, 9]

// Sort descending
List<Integer> desc = numbers.stream()
    .sorted(Comparator.reverseOrder())
    .collect(Collectors.toList());

// Distinct (remove duplicates)
List<Integer> nums = Arrays.asList(1, 2, 2, 3, 3, 4);
List<Integer> unique = nums.stream()
    .distinct()
    .collect(Collectors.toList());
System.out.println(unique);  // [1, 2, 3, 4]

// Limit & Skip
List<Integer> firstThree = numbers.stream().limit(3).collect(Collectors.toList());
List<Integer> skipTwo = numbers.stream().skip(2).collect(Collectors.toList());
```

### Terminal Operations
```java
List<Integer> numbers = Arrays.asList(5, 3, 8, 1, 9, 2, 7);

// forEach
numbers.stream().forEach(System.out::println);

// count
long count = numbers.stream().filter(n -> n > 5).count();
System.out.println("Count > 5: " + count);  // 3

// min & max
int min = numbers.stream().min(Integer::compare).get();
int max = numbers.stream().max(Integer::compare).get();

// sum & average
int sum = numbers.stream().mapToInt(Integer::intValue).sum();
double avg = numbers.stream().mapToInt(Integer::intValue).average().orElse(0);

// reduce (combine all elements)
int total = numbers.stream().reduce(0, Integer::sum);
System.out.println("Total: " + total);  // 35

// anyMatch, allMatch, noneMatch
boolean hasEven = numbers.stream().anyMatch(n -> n % 2 == 0);  // true
boolean allPositive = numbers.stream().allMatch(n -> n > 0);    // true
boolean noneNegative = numbers.stream().noneMatch(n -> n < 0);  // true

// findFirst, findAny
Optional<Integer> first = numbers.stream().filter(n -> n > 5).findFirst();
System.out.println(first.get());  // 8

// toArray
Integer[] arr = numbers.stream().toArray(Integer[]::new);
```

### Stream with Strings
```java
List<String> names = Arrays.asList("Rahul", "Priya", "Amit", "Priya", "Ravi");

// Filter names starting with 'R'
List<String> rNames = names.stream()
    .filter(n -> n.startsWith("R"))
    .collect(Collectors.toList());
System.out.println(rNames);  // [Rahul, Ravi]

// Convert to uppercase
List<String> upper = names.stream()
    .map(String::toUpperCase)
    .collect(Collectors.toList());

// Sort + unique + join
String result = names.stream()
    .distinct()
    .sorted()
    .collect(Collectors.joining(", "));
System.out.println(result);  // Amit, Priya, Rahul, Ravi

// Group by first letter
Map<Character, List<String>> grouped = names.stream()
    .collect(Collectors.groupingBy(n -> n.charAt(0)));
System.out.println(grouped);  // {A=[Amit], P=[Priya, Priya], R=[Rahul, Ravi]}

// Counting occurrences
Map<String, Long> freq = names.stream()
    .collect(Collectors.groupingBy(n -> n, Collectors.counting()));
System.out.println(freq);  // {Amit=1, Priya=2, Rahul=1, Ravi=1}
```

### Stream with Objects
```java
class Employee {
    String name;
    String dept;
    double salary;

    Employee(String name, String dept, double salary) {
        this.name = name;
        this.dept = dept;
        this.salary = salary;
    }
}

List<Employee> employees = Arrays.asList(
    new Employee("Rahul", "IT", 50000),
    new Employee("Priya", "HR", 45000),
    new Employee("Amit", "IT", 60000),
    new Employee("Ravi", "HR", 55000),
    new Employee("Neha", "IT", 70000)
);

// Highest paid employee
Employee richest = employees.stream()
    .max(Comparator.comparingDouble(e -> e.salary))
    .get();
System.out.println(richest.name);  // Neha

// Average salary
double avgSalary = employees.stream()
    .mapToDouble(e -> e.salary)
    .average()
    .orElse(0);

// Employees by department
Map<String, List<Employee>> byDept = employees.stream()
    .collect(Collectors.groupingBy(e -> e.dept));

// Names of IT employees sorted by salary
List<String> itEmployees = employees.stream()
    .filter(e -> e.dept.equals("IT"))
    .sorted(Comparator.comparingDouble(e -> e.salary))
    .map(e -> e.name)
    .collect(Collectors.toList());
System.out.println(itEmployees);  // [Rahul, Amit, Neha]
```

---

## 9.5 Optional (Avoid NullPointerException)

```java
import java.util.Optional;

// Creating Optional
Optional<String> name = Optional.of("Rahul");
Optional<String> empty = Optional.empty();
Optional<String> nullable = Optional.ofNullable(null);

// Check and get
if (name.isPresent()) {
    System.out.println(name.get());  // Rahul
}

// OrElse – default value
String value = nullable.orElse("Default");
System.out.println(value);  // Default

// OrElseGet – lazy default
String value2 = nullable.orElseGet(() -> "Computed Default");

// OrElseThrow
// String value3 = nullable.orElseThrow(() -> new RuntimeException("Not found!"));

// ifPresent
name.ifPresent(n -> System.out.println("Hello, " + n));

// map
Optional<Integer> len = name.map(String::length);
System.out.println(len.get());  // 5
```

---

## 9.6 Date & Time API (Java 8+)

```java
import java.time.*;
import java.time.format.DateTimeFormatter;

// Current date and time
LocalDate today = LocalDate.now();
LocalTime now = LocalTime.now();
LocalDateTime dateTime = LocalDateTime.now();

System.out.println("Date: " + today);      // 2026-02-22
System.out.println("Time: " + now);        // 14:30:45.123
System.out.println("DateTime: " + dateTime);

// Specific date
LocalDate birthday = LocalDate.of(2000, 5, 15);
System.out.println("Birthday: " + birthday);

// Operations
LocalDate tomorrow = today.plusDays(1);
LocalDate lastMonth = today.minusMonths(1);
LocalDate nextYear = today.plusYears(1);

// Compare
System.out.println(today.isBefore(tomorrow));  // true
System.out.println(today.isAfter(lastMonth));  // true

// Format
DateTimeFormatter formatter = DateTimeFormatter.ofPattern("dd-MM-yyyy");
String formatted = today.format(formatter);
System.out.println(formatted);  // 22-02-2026

// Parse
LocalDate parsed = LocalDate.parse("15-05-2000", formatter);

// Period (difference between dates)
Period period = Period.between(birthday, today);
System.out.println(period.getYears() + " years, " + period.getMonths() + " months");
```

---

## 🔥 Interview Questions – Java 8

**Q1: What is a Lambda Expression?**
> A concise way to represent an anonymous function. Syntax: `(params) -> { body }`. Works only with functional interfaces.

**Q2: What is a Functional Interface?**
> An interface with exactly **one abstract method**. Annotated with `@FunctionalInterface`. Examples: Runnable, Comparator, Predicate.

**Q3: What is Stream API?**
> A pipeline for processing collections in a functional style. Supports `filter`, `map`, `reduce`, `collect`, etc. Does not modify the original collection.

**Q4: Difference between `map()` and `flatMap()`?**
> - `map()`: transforms each element (one-to-one)
> - `flatMap()`: transforms each element into a stream and flattens (one-to-many)

**Q5: What is Optional?**
> A container that may or may not hold a value. Used to avoid NullPointerException. Methods: `of()`, `empty()`, `isPresent()`, `orElse()`.

**Q6: Difference between `Collection.forEach()` and `Stream.forEach()`?**
> `Collection.forEach()` iterates over the collection directly. `Stream.forEach()` processes through a stream pipeline (can include filter, map, etc.).

**Q7: What are intermediate vs terminal operations?**
> - Intermediate: return a stream (lazy) – `filter()`, `map()`, `sorted()`
> - Terminal: produce a result (eager) – `collect()`, `count()`, `forEach()`

**Q8: Can we reuse a Stream?**
> No. A stream can be consumed only once. Trying to reuse throws `IllegalStateException`.

**Q9: What is `Collectors.groupingBy()`?**
> Groups elements of a stream by a classifier function, returning a `Map<K, List<V>>`.

**Q10: Difference between `findFirst()` and `findAny()`?**
> - `findFirst()`: always returns the first element
> - `findAny()`: returns any element (useful in parallel streams for performance)

---
