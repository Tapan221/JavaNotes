# 📘 CHAPTER 2: CONTROL FLOW & ARRAYS

---

## 2.1 Conditional Statements

### if Statement
```java
int age = 20;

if (age >= 18) {
    System.out.println("You can vote!");
}
```

### if-else Statement
```java
int marks = 45;

if (marks >= 50) {
    System.out.println("PASS");
} else {
    System.out.println("FAIL");
}
```

### if-else-if Ladder
```java
int marks = 85;

if (marks >= 90) {
    System.out.println("Grade: A+");
} else if (marks >= 80) {
    System.out.println("Grade: A");
} else if (marks >= 70) {
    System.out.println("Grade: B");
} else if (marks >= 60) {
    System.out.println("Grade: C");
} else {
    System.out.println("Grade: F");
}
// Output: Grade: A
```

### Nested if
```java
int age = 25;
boolean hasID = true;

if (age >= 18) {
    if (hasID) {
        System.out.println("Entry allowed");
    } else {
        System.out.println("Bring your ID");
    }
} else {
    System.out.println("Too young");
}
```

---

## 2.2 Switch Statement

```java
int day = 3;

switch (day) {
    case 1:
        System.out.println("Monday");
        break;
    case 2:
        System.out.println("Tuesday");
        break;
    case 3:
        System.out.println("Wednesday");
        break;
    case 4:
        System.out.println("Thursday");
        break;
    case 5:
        System.out.println("Friday");
        break;
    default:
        System.out.println("Weekend");
}
// Output: Wednesday
```

### Enhanced Switch (Java 14+)
```java
int day = 3;
String dayName = switch (day) {
    case 1 -> "Monday";
    case 2 -> "Tuesday";
    case 3 -> "Wednesday";
    case 4 -> "Thursday";
    case 5 -> "Friday";
    default -> "Weekend";
};
System.out.println(dayName);  // Wednesday
```

---

## 2.3 Loops

### for Loop
```java
// Print 1 to 5
for (int i = 1; i <= 5; i++) {
    System.out.println(i);
}
```

### while Loop
```java
// Print 1 to 5
int i = 1;
while (i <= 5) {
    System.out.println(i);
    i++;
}
```

### do-while Loop (runs at least once)
```java
int i = 1;
do {
    System.out.println(i);
    i++;
} while (i <= 5);
```

### Difference between while and do-while
```java
// This prints nothing (condition false from start)
int x = 10;
while (x < 5) {
    System.out.println(x);  // Never executes
}

// This prints 10 (runs once even though condition is false)
int y = 10;
do {
    System.out.println(y);  // Prints 10
} while (y < 5);
```

### for-each Loop (Enhanced for Loop)
```java
int[] numbers = {10, 20, 30, 40, 50};

for (int num : numbers) {
    System.out.println(num);
}
```

---

## 2.4 Loop Control Statements

### break – exits the loop
```java
for (int i = 1; i <= 10; i++) {
    if (i == 5) {
        break;  // stops at 5
    }
    System.out.println(i);
}
// Output: 1 2 3 4
```

### continue – skips current iteration
```java
for (int i = 1; i <= 5; i++) {
    if (i == 3) {
        continue;  // skips 3
    }
    System.out.println(i);
}
// Output: 1 2 4 5
```

### Labeled break (nested loops)
```java
outer:
for (int i = 1; i <= 3; i++) {
    for (int j = 1; j <= 3; j++) {
        if (i == 2 && j == 2) {
            break outer;  // breaks both loops
        }
        System.out.println(i + " " + j);
    }
}
```

---

## 2.5 Pattern Programs (Common in Interviews)

### Right Triangle Star Pattern
```java
/*
 *
 * *
 * * *
 * * * *
 * * * * *
 */
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

### Inverted Triangle
```java
/*
 * * * * *
 * * * *
 * * *
 * *
 *
 */
for (int i = 5; i >= 1; i--) {
    for (int j = 1; j <= i; j++) {
        System.out.print("* ");
    }
    System.out.println();
}
```

### Number Pyramid
```java
/*
 1
 1 2
 1 2 3
 1 2 3 4
 1 2 3 4 5
 */
for (int i = 1; i <= 5; i++) {
    for (int j = 1; j <= i; j++) {
        System.out.print(j + " ");
    }
    System.out.println();
}
```

---

## 2.6 Arrays

An array is a **fixed-size container** that holds multiple values of the **same type**.

### Declaring & Initializing
```java
// Method 1: Declare and allocate
int[] numbers = new int[5];  // [0, 0, 0, 0, 0]
numbers[0] = 10;
numbers[1] = 20;

// Method 2: Declare and initialize
int[] marks = {90, 85, 78, 92, 88};

// Method 3
int[] arr = new int[]{1, 2, 3, 4, 5};
```

### Accessing & Iterating
```java
int[] marks = {90, 85, 78, 92, 88};

// Access by index (0-based)
System.out.println(marks[0]);  // 90
System.out.println(marks[4]);  // 88

// Length of array
System.out.println(marks.length);  // 5

// for loop
for (int i = 0; i < marks.length; i++) {
    System.out.println("Index " + i + ": " + marks[i]);
}

// for-each loop
for (int mark : marks) {
    System.out.println(mark);
}
```

### 2D Array (Matrix)
```java
int[][] matrix = {
    {1, 2, 3},
    {4, 5, 6},
    {7, 8, 9}
};

// Access element at row 1, col 2
System.out.println(matrix[1][2]);  // 6

// Print full matrix
for (int i = 0; i < matrix.length; i++) {
    for (int j = 0; j < matrix[i].length; j++) {
        System.out.print(matrix[i][j] + " ");
    }
    System.out.println();
}
```

### Common Array Operations
```java
import java.util.Arrays;

int[] arr = {5, 2, 8, 1, 9, 3};

// Sort
Arrays.sort(arr);
System.out.println(Arrays.toString(arr));  // [1, 2, 3, 5, 8, 9]

// Search (array must be sorted)
int index = Arrays.binarySearch(arr, 5);
System.out.println("Found at index: " + index);

// Fill
int[] filled = new int[5];
Arrays.fill(filled, 7);
System.out.println(Arrays.toString(filled));  // [7, 7, 7, 7, 7]

// Copy
int[] copy = Arrays.copyOf(arr, 3);
System.out.println(Arrays.toString(copy));  // [1, 2, 3]

// Compare
int[] a = {1, 2, 3};
int[] b = {1, 2, 3};
System.out.println(Arrays.equals(a, b));  // true
```

---

## 2.7 Jagged Array (Array of Different Sizes)
```java
int[][] jagged = new int[3][];
jagged[0] = new int[]{1, 2};
jagged[1] = new int[]{3, 4, 5};
jagged[2] = new int[]{6};

for (int[] row : jagged) {
    for (int val : row) {
        System.out.print(val + " ");
    }
    System.out.println();
}
/*
 1 2
 3 4 5
 6
 */
```

---

## 🔥 Interview Questions – Control Flow & Arrays

**Q1: Difference between `for` and `for-each` loop?**
> - `for` loop uses index, gives control over start/end/step
> - `for-each` loop is simpler, no index, reads only (can't modify)

**Q2: Difference between `break` and `continue`?**
> - `break` – exits the entire loop
> - `continue` – skips current iteration, continues next

**Q3: Can switch work with String?**
> Yes, from **Java 7** onwards. Switch supports `int`, `char`, `String`, `enum`, and wrapper types.

**Q4: What happens if we miss `break` in switch?**
> **Fall-through** happens – all cases after the matched one execute until a `break` is found.

**Q5: What is the default value of array elements?**
> - `int` → 0
> - `double` → 0.0
> - `boolean` → false
> - `String`/Object → null

**Q6: Difference between `length` and `length()`?**
> - `length` → property of **arrays** (e.g., `arr.length`)
> - `length()` → method of **String** (e.g., `str.length()`)

**Q7: Can we change the size of an array after creation?**
> No. Arrays are **fixed-size**. Use `ArrayList` for dynamic sizing.

**Q8: What is `ArrayIndexOutOfBoundsException`?**
> Thrown when trying to access an index that doesn't exist (e.g., `arr[10]` when array size is 5).

**Q9: Difference between `while` and `do-while`?**
> - `while` checks condition **first** → may not execute at all
> - `do-while` checks condition **after** → executes at least once

**Q10: How to compare two arrays in Java?**
> Use `Arrays.equals(arr1, arr2)` for 1D and `Arrays.deepEquals(arr1, arr2)` for multidimensional arrays. Using `==` only compares references.

---
