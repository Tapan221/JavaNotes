# 📘 CHAPTER 8: COLLECTIONS FRAMEWORK

---

## 8.1 What is Collections Framework?

A **set of classes and interfaces** to store and manipulate groups of objects. Better than arrays because they are **dynamic in size**.

```
Collection (Interface)
├── List (Interface) → ordered, allows duplicates
│   ├── ArrayList     → fast read, slow insert/delete
│   ├── LinkedList    → slow read, fast insert/delete
│   └── Vector        → thread-safe (legacy, avoid)
│
├── Set (Interface) → no duplicates
│   ├── HashSet       → no order
│   ├── LinkedHashSet → insertion order
│   └── TreeSet       → sorted order
│
└── Queue (Interface) → FIFO
    ├── PriorityQueue  → sorted by priority
    └── LinkedList     → also implements Queue

Map (Interface) → key-value pairs (NOT part of Collection)
├── HashMap        → no order, allows one null key
├── LinkedHashMap  → insertion order
├── TreeMap        → sorted by keys
└── Hashtable      → thread-safe (legacy, avoid)
```

---

## 8.2 ArrayList

**Dynamic array** that grows automatically. Most commonly used.

```java
import java.util.ArrayList;
import java.util.Collections;

public class ArrayListDemo {
    public static void main(String[] args) {
        // Create
        ArrayList<String> fruits = new ArrayList<>();

        // Add elements
        fruits.add("Apple");
        fruits.add("Banana");
        fruits.add("Cherry");
        fruits.add("Apple");  // duplicates allowed!
        System.out.println(fruits);  // [Apple, Banana, Cherry, Apple]

        // Access by index
        System.out.println(fruits.get(0));   // Apple
        System.out.println(fruits.size());   // 4

        // Modify
        fruits.set(1, "Blueberry");
        System.out.println(fruits);  // [Apple, Blueberry, Cherry, Apple]

        // Remove
        fruits.remove("Apple");    // removes first occurrence
        fruits.remove(0);          // removes by index

        // Check
        System.out.println(fruits.contains("Cherry"));  // true
        System.out.println(fruits.isEmpty());            // false
        System.out.println(fruits.indexOf("Cherry"));    // index

        // Sort
        Collections.sort(fruits);

        // Iterate
        for (String fruit : fruits) {
            System.out.println(fruit);
        }

        // Clear all
        fruits.clear();
    }
}
```

### ArrayList of integers
```java
ArrayList<Integer> numbers = new ArrayList<>();
numbers.add(30);
numbers.add(10);
numbers.add(50);
numbers.add(20);

Collections.sort(numbers);          // ascending
System.out.println(numbers);        // [10, 20, 30, 50]

Collections.sort(numbers, Collections.reverseOrder());  // descending
System.out.println(numbers);        // [50, 30, 20, 10]

int max = Collections.max(numbers); // 50
int min = Collections.min(numbers); // 10
```

---

## 8.3 LinkedList

Uses **doubly-linked nodes**. Better for frequent insertions/deletions.

```java
import java.util.LinkedList;

LinkedList<String> list = new LinkedList<>();

list.add("A");
list.add("B");
list.add("C");

// Special methods
list.addFirst("Start");    // [Start, A, B, C]
list.addLast("End");       // [Start, A, B, C, End]
list.removeFirst();        // [A, B, C, End]
list.removeLast();         // [A, B, C]

System.out.println(list.getFirst());  // A
System.out.println(list.getLast());   // C
```

### ArrayList vs LinkedList

| Feature | ArrayList | LinkedList |
|---------|-----------|------------|
| Structure | Dynamic array | Doubly linked list |
| Read/Access | Fast (O(1)) | Slow (O(n)) |
| Insert/Delete | Slow (O(n)) | Fast (O(1)) |
| Memory | Less | More (stores pointers) |
| Best for | Frequent reads | Frequent inserts/deletes |

---

## 8.4 HashSet

Stores **unique elements** only. **No order** guaranteed. Uses **hashing**.

```java
import java.util.HashSet;

HashSet<String> set = new HashSet<>();

set.add("Java");
set.add("Python");
set.add("Java");     // duplicate → ignored!
set.add("C++");
set.add(null);       // allows ONE null

System.out.println(set);        // [null, Java, C++, Python] (random order)
System.out.println(set.size()); // 4

set.contains("Java");           // true
set.remove("C++");

// Iterate
for (String lang : set) {
    System.out.println(lang);
}
```

### LinkedHashSet (Maintains Insertion Order)
```java
import java.util.LinkedHashSet;

LinkedHashSet<String> lhs = new LinkedHashSet<>();
lhs.add("B");
lhs.add("A");
lhs.add("C");
System.out.println(lhs);  // [B, A, C] → insertion order kept!
```

### TreeSet (Sorted Order)
```java
import java.util.TreeSet;

TreeSet<Integer> ts = new TreeSet<>();
ts.add(30);
ts.add(10);
ts.add(50);
ts.add(20);
System.out.println(ts);  // [10, 20, 30, 50] → sorted!

System.out.println(ts.first());    // 10
System.out.println(ts.last());     // 50
System.out.println(ts.higher(20)); // 30 (next higher)
System.out.println(ts.lower(30));  // 20 (next lower)
```

---

## 8.5 HashMap

Stores **key-value** pairs. **Fast lookup** (O(1)). Keys must be unique.

```java
import java.util.HashMap;
import java.util.Map;

HashMap<String, Integer> map = new HashMap<>();

// Add entries
map.put("Rahul", 90);
map.put("Priya", 85);
map.put("Amit", 92);
map.put("Rahul", 95);  // overwrites! (duplicate key)

System.out.println(map);  // {Amit=92, Rahul=95, Priya=85}

// Access
System.out.println(map.get("Rahul"));     // 95
System.out.println(map.get("Unknown"));   // null

// Check
System.out.println(map.containsKey("Priya"));   // true
System.out.println(map.containsValue(92));       // true

// Size
System.out.println(map.size());  // 3

// Remove
map.remove("Amit");

// Default value if key not found
System.out.println(map.getOrDefault("Unknown", 0));  // 0

// Iterate
for (Map.Entry<String, Integer> entry : map.entrySet()) {
    System.out.println(entry.getKey() + " = " + entry.getValue());
}

// Iterate keys only
for (String key : map.keySet()) {
    System.out.println(key);
}

// Iterate values only
for (int value : map.values()) {
    System.out.println(value);
}
```

### TreeMap (Sorted by Keys)
```java
import java.util.TreeMap;

TreeMap<String, Integer> tm = new TreeMap<>();
tm.put("Banana", 2);
tm.put("Apple", 5);
tm.put("Cherry", 3);

System.out.println(tm);  // {Apple=5, Banana=2, Cherry=3} → sorted by key!
```

### LinkedHashMap (Insertion Order)
```java
import java.util.LinkedHashMap;

LinkedHashMap<String, Integer> lhm = new LinkedHashMap<>();
lhm.put("B", 2);
lhm.put("A", 1);
lhm.put("C", 3);
System.out.println(lhm);  // {B=2, A=1, C=3} → insertion order!
```

---

## 8.6 Stack and Queue

### Stack (LIFO – Last In First Out)
```java
import java.util.Stack;

Stack<String> stack = new Stack<>();

stack.push("A");
stack.push("B");
stack.push("C");

System.out.println(stack.peek());  // C (top element, doesn't remove)
System.out.println(stack.pop());   // C (removes top)
System.out.println(stack.pop());   // B
System.out.println(stack);         // [A]
System.out.println(stack.isEmpty()); // false
```

### Queue (FIFO – First In First Out)
```java
import java.util.LinkedList;
import java.util.Queue;

Queue<String> queue = new LinkedList<>();

queue.offer("A");  // add
queue.offer("B");
queue.offer("C");

System.out.println(queue.peek());  // A (front element)
System.out.println(queue.poll());  // A (removes front)
System.out.println(queue);         // [B, C]
```

### PriorityQueue (Sorted Queue)
```java
import java.util.PriorityQueue;

PriorityQueue<Integer> pq = new PriorityQueue<>();
pq.offer(30);
pq.offer(10);
pq.offer(20);

System.out.println(pq.poll());  // 10 (smallest first)
System.out.println(pq.poll());  // 20
System.out.println(pq.poll());  // 30
```

---

## 8.7 Iterator

A universal way to traverse any Collection.

```java
import java.util.ArrayList;
import java.util.Iterator;

ArrayList<String> list = new ArrayList<>();
list.add("A");
list.add("B");
list.add("C");

Iterator<String> it = list.iterator();
while (it.hasNext()) {
    String val = it.next();
    if (val.equals("B")) {
        it.remove();  // safe way to remove during iteration
    }
}
System.out.println(list);  // [A, C]
```

---

## 8.8 Comparable vs Comparator

### Comparable (Natural Ordering)
```java
class Student implements Comparable<Student> {
    String name;
    int marks;

    Student(String name, int marks) {
        this.name = name;
        this.marks = marks;
    }

    @Override
    public int compareTo(Student other) {
        return this.marks - other.marks;  // ascending by marks
    }

    @Override
    public String toString() {
        return name + "(" + marks + ")";
    }
}

List<Student> students = new ArrayList<>();
students.add(new Student("Rahul", 85));
students.add(new Student("Priya", 92));
students.add(new Student("Amit", 78));

Collections.sort(students);
System.out.println(students);  // [Amit(78), Rahul(85), Priya(92)]
```

### Comparator (Custom Ordering)
```java
import java.util.Comparator;

// Sort by name
students.sort(Comparator.comparing(s -> s.name));

// Sort by marks descending
students.sort((s1, s2) -> s2.marks - s1.marks);

// Using method reference
students.sort(Comparator.comparingInt(s -> s.marks));
```

### Comparable vs Comparator

| Feature | Comparable | Comparator |
|---------|-----------|------------|
| Package | `java.lang` | `java.util` |
| Method | `compareTo()` | `compare()` |
| Modifies class? | Yes | No |
| Sorting | Natural/default | Custom |
| Number of orderings | One | Multiple |

---

## 🔥 Interview Questions – Collections

**Q1: Difference between Array and ArrayList?**
> - Array: fixed size, holds primitives + objects
> - ArrayList: dynamic size, holds objects only

**Q2: Difference between ArrayList and LinkedList?**
> ArrayList is better for reads (index-based). LinkedList is better for inserts/deletes (pointer-based).

**Q3: Difference between HashSet and TreeSet?**
> - HashSet: unordered, allows null, O(1) operations
> - TreeSet: sorted, no null, O(log n) operations

**Q4: How does HashMap work internally?**
> Uses an **array of buckets**. Key's `hashCode()` determines the bucket. Collisions handled by linked list (or tree in Java 8+ when bucket > 8 entries).

**Q5: Difference between HashMap and Hashtable?**
> - HashMap: not synchronized, allows null key/values, faster
> - Hashtable: synchronized, no nulls, slower, legacy

**Q6: What is the difference between `fail-fast` and `fail-safe` iterators?**
> - Fail-fast: throws `ConcurrentModificationException` if collection is modified during iteration (ArrayList, HashMap)
> - Fail-safe: works on a copy, no exception (ConcurrentHashMap, CopyOnWriteArrayList)

**Q7: When to use which collection?**
> - Ordered list with duplicates → `ArrayList`
> - Unique elements → `HashSet`
> - Sorted unique elements → `TreeSet`
> - Key-value pairs → `HashMap`
> - Sorted key-value → `TreeMap`
> - Thread-safe map → `ConcurrentHashMap`
> - LIFO → `Stack` or `Deque`
> - FIFO → `Queue`

**Q8: Can we store null in collections?**
> - ArrayList: yes (multiple)
> - HashSet: one null
> - TreeSet: no (throws NullPointerException)
> - HashMap: one null key, multiple null values
> - TreeMap: no null keys

**Q9: What is the load factor in HashMap?**
> Default is 0.75. When 75% of buckets are filled, the map resizes (doubles capacity). Balances time and space.

**Q10: Difference between `Comparable` and `Comparator`?**
> Comparable defines natural ordering inside the class. Comparator defines custom ordering outside the class.

---
