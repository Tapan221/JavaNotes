# 📘 CHAPTER 6: EXCEPTION HANDLING

---

## 6.1 What is an Exception?

An exception is an **unwanted event** that disrupts the normal flow of a program.

```
Throwable
├── Error (serious, can't handle) → OutOfMemoryError, StackOverflowError
└── Exception
    ├── Checked Exceptions (compile-time) → IOException, SQLException
    └── Unchecked Exceptions (runtime) → NullPointerException, ArithmeticException
```

---

## 6.2 Common Exceptions

| Exception | When it occurs |
|-----------|---------------|
| `ArithmeticException` | Division by zero |
| `NullPointerException` | Calling method on null object |
| `ArrayIndexOutOfBoundsException` | Invalid array index |
| `NumberFormatException` | Invalid string to number conversion |
| `ClassCastException` | Invalid type casting |
| `StringIndexOutOfBoundsException` | Invalid string index |
| `StackOverflowError` | Infinite recursion |
| `FileNotFoundException` | File doesn't exist |

---

## 6.3 try-catch Block

```java
public class ExceptionDemo {
    public static void main(String[] args) {
        try {
            int result = 10 / 0;  // ArithmeticException
            System.out.println(result);
        } catch (ArithmeticException e) {
            System.out.println("Error: Cannot divide by zero!");
            System.out.println("Message: " + e.getMessage());
        }
        System.out.println("Program continues...");
    }
}
// Output:
// Error: Cannot divide by zero!
// Message: / by zero
// Program continues...
```

---

## 6.4 Multiple catch Blocks

```java
try {
    int[] arr = {1, 2, 3};
    System.out.println(arr[5]);     // ArrayIndexOutOfBoundsException
    int result = 10 / 0;            // ArithmeticException
} catch (ArrayIndexOutOfBoundsException e) {
    System.out.println("Invalid index: " + e.getMessage());
} catch (ArithmeticException e) {
    System.out.println("Math error: " + e.getMessage());
} catch (Exception e) {
    System.out.println("General error: " + e.getMessage());  // catches all
}
```

### Multi-catch (Java 7+)
```java
try {
    // some code
} catch (ArithmeticException | NullPointerException e) {
    System.out.println("Error: " + e.getMessage());
}
```

---

## 6.5 finally Block

**Always executes** — whether exception occurs or not. Used for **cleanup**.

```java
try {
    int result = 10 / 2;
    System.out.println("Result: " + result);
} catch (ArithmeticException e) {
    System.out.println("Error!");
} finally {
    System.out.println("Finally block always runs!");
}
// Output:
// Result: 5
// Finally block always runs!
```

**Real-world use:** Closing database connections, file streams, etc.

---

## 6.6 throw Keyword (Throw Exception Manually)

```java
static void checkAge(int age) {
    if (age < 18) {
        throw new ArithmeticException("Not eligible to vote!");
    } else {
        System.out.println("Welcome to vote!");
    }
}

public static void main(String[] args) {
    checkAge(15);  // Exception: Not eligible to vote!
}
```

---

## 6.7 throws Keyword (Declare Exception)

Tells the caller "this method **might throw** this exception — handle it."

```java
import java.io.*;

static void readFile() throws FileNotFoundException {
    FileReader fr = new FileReader("test.txt");  // may not exist
}

public static void main(String[] args) {
    try {
        readFile();
    } catch (FileNotFoundException e) {
        System.out.println("File not found!");
    }
}
```

### throw vs throws

| Feature | `throw` | `throws` |
|---------|---------|----------|
| Purpose | Actually throw an exception | Declare that method may throw |
| Where | Inside method body | In method signature |
| Number | One exception at a time | Multiple exceptions |
| Example | `throw new Exception("msg")` | `void m() throws IOException` |

---

## 6.8 Custom Exception

```java
// Create your own exception
class InsufficientBalanceException extends Exception {
    public InsufficientBalanceException(String message) {
        super(message);
    }
}

class BankAccount {
    private double balance = 10000;

    void withdraw(double amount) throws InsufficientBalanceException {
        if (amount > balance) {
            throw new InsufficientBalanceException(
                "Cannot withdraw " + amount + ". Balance is only " + balance
            );
        }
        balance -= amount;
        System.out.println("Withdrawn: " + amount + ", Remaining: " + balance);
    }
}

public class Main {
    public static void main(String[] args) {
        BankAccount acc = new BankAccount();
        try {
            acc.withdraw(5000);   // Withdrawn: 5000
            acc.withdraw(8000);   // Exception!
        } catch (InsufficientBalanceException e) {
            System.out.println("Error: " + e.getMessage());
        }
    }
}
```

---

## 6.9 try-with-resources (Java 7+)

Automatically closes resources. No need for `finally`.

```java
import java.io.*;

// Old way
BufferedReader br = null;
try {
    br = new BufferedReader(new FileReader("file.txt"));
    String line = br.readLine();
} catch (IOException e) {
    e.printStackTrace();
} finally {
    if (br != null) br.close();  // manual close
}

// New way – try-with-resources
try (BufferedReader br2 = new BufferedReader(new FileReader("file.txt"))) {
    String line = br2.readLine();
    System.out.println(line);
} catch (IOException e) {
    e.printStackTrace();
}
// br2 is automatically closed!
```

---

## 6.10 Checked vs Unchecked Exceptions

| Feature | Checked | Unchecked |
|---------|---------|-----------|
| When detected | Compile time | Runtime |
| Must handle? | Yes (try-catch or throws) | No (optional) |
| Extends | `Exception` | `RuntimeException` |
| Examples | IOException, SQLException | NullPointerException, ArithmeticException |

---

## 🔥 Interview Questions – Exception Handling

**Q1: Difference between Error and Exception?**
> - Error: Serious, unrecoverable (OutOfMemoryError). Don't catch.
> - Exception: Recoverable situations. Should handle.

**Q2: Difference between checked and unchecked exceptions?**
> Checked: Must handle at compile time. Unchecked: Detected at runtime, optional to handle.

**Q3: Can `finally` block not execute?**
> Only if `System.exit()` is called or JVM crashes.

**Q4: What is exception propagation?**
> If a method doesn't handle an exception, it passes (propagates) to the calling method.

**Q5: Can we have `try` without `catch`?**
> Yes, with `finally`: `try { } finally { }` is valid.

**Q6: What happens if exception occurs in `catch` block?**
> It propagates to the caller. The `finally` block still runs.

**Q7: Can we throw checked exception from a method without `throws`?**
> No. Checked exceptions must be declared with `throws` or handled with try-catch.

**Q8: What is `e.printStackTrace()`?**
> Prints the exception type, message, and the complete call stack trace.

---
