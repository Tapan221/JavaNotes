# 📘 CHAPTER 3: STRINGS IN JAVA

---

## 3.1 What is a String?

A String is a **sequence of characters**. In Java, String is an **object** (not a primitive) from `java.lang.String` class. Strings are **immutable** — once created, they cannot be changed.

---

## 3.2 Creating Strings

```java
// Method 1: String Literal (stored in String Pool)
String s1 = "Hello";

// Method 2: Using new keyword (stored in Heap)
String s2 = new String("Hello");
```

### String Pool Concept
```java
String a = "Hello";  // Creates in String Pool
String b = "Hello";  // Points to SAME object in pool

String c = new String("Hello");  // Creates NEW object in Heap

System.out.println(a == b);       // true  (same reference)
System.out.println(a == c);       // false (different reference)
System.out.println(a.equals(c));  // true  (same content)
```

```
          HEAP MEMORY
┌─────────────────────────────┐
│   String Pool               │
│   ┌───────────┐             │
│   │  "Hello"  │ ← a, b     │
│   └───────────┘             │
│                             │
│   ┌───────────┐             │
│   │  "Hello"  │ ← c (new)  │
│   └───────────┘             │
└─────────────────────────────┘
```

---

## 3.3 Important String Methods

```java
String str = "Hello World";

// Length
System.out.println(str.length());           // 11

// Character at index
System.out.println(str.charAt(0));          // H
System.out.println(str.charAt(6));          // W

// Substring
System.out.println(str.substring(6));       // World
System.out.println(str.substring(0, 5));    // Hello

// Case conversion
System.out.println(str.toUpperCase());      // HELLO WORLD
System.out.println(str.toLowerCase());      // hello world

// Trim (remove leading/trailing spaces)
String padded = "  Hello  ";
System.out.println(padded.trim());          // Hello

// Contains
System.out.println(str.contains("World")); // true

// Index of
System.out.println(str.indexOf("World"));  // 6
System.out.println(str.indexOf("Java"));   // -1 (not found)

// Replace
System.out.println(str.replace("World", "Java")); // Hello Java

// Starts/Ends with
System.out.println(str.startsWith("Hello")); // true
System.out.println(str.endsWith("World"));   // true

// Check empty
System.out.println(str.isEmpty());           // false
System.out.println("".isEmpty());            // true

// Split
String csv = "apple,banana,cherry";
String[] fruits = csv.split(",");
for (String fruit : fruits) {
    System.out.println(fruit);
}
// apple
// banana
// cherry

// Join
String joined = String.join("-", "2026", "02", "22");
System.out.println(joined);  // 2026-02-22

// Equals (case-sensitive)
System.out.println("hello".equals("Hello"));           // false
System.out.println("hello".equalsIgnoreCase("Hello")); // true

// Compare
System.out.println("apple".compareTo("banana"));  // negative (a < b)
System.out.println("banana".compareTo("apple"));  // positive (b > a)
System.out.println("apple".compareTo("apple"));   // 0 (equal)

// Convert other types to String
int num = 100;
String numStr = String.valueOf(num);       // "100"
String numStr2 = Integer.toString(num);    // "100"
String numStr3 = "" + num;                 // "100"
```

---

## 3.4 String Immutability

```java
String s = "Hello";
s.concat(" World");
System.out.println(s);  // Hello  ← Original NOT changed!

// You must reassign
s = s.concat(" World");
System.out.println(s);  // Hello World  ← New object assigned
```

**Why is String immutable?**
1. **String Pool** – Enables sharing of strings safely
2. **Security** – Database passwords, URLs can't be changed
3. **Thread Safety** – Safe to use in multithreading
4. **Hashing** – hashCode is cached, efficient for HashMap keys

---

## 3.5 StringBuilder (Mutable, Not Thread-Safe)

Use when you need to **modify strings frequently** (like in loops).

```java
StringBuilder sb = new StringBuilder("Hello");

sb.append(" World");         // Hello World
sb.insert(5, ",");          // Hello, World
sb.replace(0, 5, "Hi");    // Hi, World
sb.delete(2, 4);            // Hi World
sb.reverse();               // dlroW iH

System.out.println(sb.toString());

// Performance comparison
// BAD – creates many String objects
String result = "";
for (int i = 0; i < 1000; i++) {
    result += i;  // Creates new String each time!
}

// GOOD – uses single StringBuilder
StringBuilder sb2 = new StringBuilder();
for (int i = 0; i < 1000; i++) {
    sb2.append(i);  // Modifies same object
}
String result2 = sb2.toString();
```

---

## 3.6 StringBuffer (Mutable, Thread-Safe)

Same as StringBuilder but **synchronized** (thread-safe). Slightly slower.

```java
StringBuffer sbuf = new StringBuffer("Hello");
sbuf.append(" World");
System.out.println(sbuf);  // Hello World
```

### String vs StringBuilder vs StringBuffer

| Feature | String | StringBuilder | StringBuffer |
|---------|--------|---------------|--------------|
| **Mutable?** | No (Immutable) | Yes | Yes |
| **Thread-Safe?** | Yes (immutable) | No | Yes (synchronized) |
| **Performance** | Slow (if modified) | Fastest | Slower than SB |
| **Use When** | Few modifications | Single thread, many modifications | Multi-thread, many modifications |

---

## 3.7 String Conversion Programs

```java
// String to int
String numStr = "123";
int num = Integer.parseInt(numStr);

// int to String
int val = 456;
String valStr = String.valueOf(val);

// String to char array
String word = "Hello";
char[] chars = word.toCharArray();

// char array to String
char[] letters = {'J', 'a', 'v', 'a'};
String fromChars = new String(letters);

// Check if string is a number
String test = "12345";
boolean isNumber = test.matches("\\d+");
System.out.println(isNumber);  // true
```

---

## 3.8 Common String Programs

### Reverse a String
```java
String original = "Hello";
String reversed = new StringBuilder(original).reverse().toString();
System.out.println(reversed);  // olleH

// Without StringBuilder
String str = "Hello";
String rev = "";
for (int i = str.length() - 1; i >= 0; i--) {
    rev += str.charAt(i);
}
System.out.println(rev);  // olleH
```

### Check Palindrome
```java
String word = "madam";
String reversed = new StringBuilder(word).reverse().toString();
if (word.equals(reversed)) {
    System.out.println(word + " is a palindrome");
} else {
    System.out.println(word + " is NOT a palindrome");
}
```

### Count Vowels and Consonants
```java
String str = "Hello World";
int vowels = 0, consonants = 0;

for (char c : str.toLowerCase().toCharArray()) {
    if (c >= 'a' && c <= 'z') {
        if ("aeiou".indexOf(c) != -1) {
            vowels++;
        } else {
            consonants++;
        }
    }
}
System.out.println("Vowels: " + vowels);       // 3
System.out.println("Consonants: " + consonants); // 7
```

### Count Character Frequency
```java
String str = "programming";
for (int i = 0; i < str.length(); i++) {
    char ch = str.charAt(i);
    int count = 0;
    for (int j = 0; j < str.length(); j++) {
        if (str.charAt(j) == ch) count++;
    }
    // Print only first occurrence
    if (str.indexOf(ch) == i) {
        System.out.println(ch + " = " + count);
    }
}
```

### Check Anagram
```java
import java.util.Arrays;

String s1 = "listen";
String s2 = "silent";

char[] arr1 = s1.toCharArray();
char[] arr2 = s2.toCharArray();
Arrays.sort(arr1);
Arrays.sort(arr2);

if (Arrays.equals(arr1, arr2)) {
    System.out.println("Anagram!");
} else {
    System.out.println("Not an Anagram");
}
```

---

## 🔥 Interview Questions – Strings

**Q1: Why is String immutable in Java?**
> For String Pool efficiency, security (passwords, URLs), thread safety, and hashCode caching.

**Q2: Difference between `==` and `.equals()` for Strings?**
> - `==` compares references (memory addresses)
> - `.equals()` compares actual content/values

**Q3: Difference between `String`, `StringBuilder`, and `StringBuffer`?**
> - String: Immutable
> - StringBuilder: Mutable, fast, not thread-safe
> - StringBuffer: Mutable, slower, thread-safe

**Q4: What is the String Pool?**
> A special memory area in heap where String literals are stored. If two strings have the same value, they share the same reference in the pool.

**Q5: How many objects are created: `String s = new String("Hello");`?**
> **2 objects** – One in the String Pool ("Hello"), one in the Heap (new String).

**Q6: Can we use String in switch statement?**
> Yes, from Java 7 onwards.

**Q7: What is the difference between `concat()` and `+` operator?**
> - `concat()` throws NullPointerException if string is null
> - `+` converts null to "null" string
> - Under the hood, `+` uses StringBuilder in modern Java

**Q8: How to make a String mutable?**
> Use `StringBuilder` or `StringBuffer`.

**Q9: What does `intern()` method do?**
> It puts the string into the String Pool (or returns the existing reference from the pool). `new String("Hello").intern()` returns the pooled reference.

**Q10: How to convert String to char array and vice versa?**
> - String to char[]: `str.toCharArray()`
> - char[] to String: `new String(charArray)` or `String.valueOf(charArray)`

---
