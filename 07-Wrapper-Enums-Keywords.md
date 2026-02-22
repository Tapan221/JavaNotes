# 📘 CHAPTER 7: WRAPPER CLASSES, ENUMS & IMPORTANT KEYWORDS

---

## 7.1 Wrapper Classes

Wrapper classes convert **primitives** into **objects**. Needed for Collections (which only work with objects).

| Primitive | Wrapper Class |
|-----------|---------------|
| `byte` | `Byte` |
| `short` | `Short` |
| `int` | `Integer` |
| `long` | `Long` |
| `float` | `Float` |
| `double` | `Double` |
| `char` | `Character` |
| `boolean` | `Boolean` |

### Autoboxing and Unboxing
```java
// Autoboxing: primitive → object (automatic)
int num = 10;
Integer obj = num;  // auto-boxing

// Unboxing: object → primitive (automatic)
Integer obj2 = 20;
int num2 = obj2;  // unboxing

// Useful methods
int a = Integer.parseInt("123");          // String → int
String s = Integer.toString(123);         // int → String
int max = Integer.MAX_VALUE;              // 2147483647
int min = Integer.MIN_VALUE;              // -2147483648

// Compare
Integer x = 127, y = 127;
System.out.println(x == y);       // true  (cached -128 to 127)
Integer p = 128, q = 128;
System.out.println(p == q);       // false (not cached!)
System.out.println(p.equals(q));  // true  (always compare with equals!)
```

---

## 7.2 Enums

An enum is a special class representing a **fixed set of constants**.

```java
enum Day {
    MONDAY, TUESDAY, WEDNESDAY, THURSDAY, FRIDAY, SATURDAY, SUNDAY
}

public class EnumDemo {
    public static void main(String[] args) {
        Day today = Day.WEDNESDAY;

        System.out.println(today);           // WEDNESDAY
        System.out.println(today.ordinal()); // 2 (index)
        System.out.println(today.name());    // WEDNESDAY

        // Loop through all values
        for (Day d : Day.values()) {
            System.out.println(d);
        }

        // Use in switch
        switch (today) {
            case MONDAY:
                System.out.println("Start of week");
                break;
            case FRIDAY:
                System.out.println("Almost weekend!");
                break;
            case SATURDAY: case SUNDAY:
                System.out.println("Weekend!");
                break;
            default:
                System.out.println("Midweek");
        }
    }
}
```

### Enum with Fields and Methods
```java
enum Planet {
    MERCURY(3.303e+23, 2.4397e6),
    VENUS(4.869e+24, 6.0518e6),
    EARTH(5.976e+24, 6.37814e6);

    private final double mass;
    private final double radius;

    // Constructor (always private)
    Planet(double mass, double radius) {
        this.mass = mass;
        this.radius = radius;
    }

    double surfaceGravity() {
        final double G = 6.67300E-11;
        return G * mass / (radius * radius);
    }
}
```

---

## 7.3 Important Java Keywords Summary

### `static`
```java
class MyClass {
    static int count = 0;         // static variable (shared)
    static void show() { }        // static method (no object needed)
    static { /* static block */ } // runs once when class loads
    static class Inner { }        // static inner class
}
```

### `final`
```java
final int X = 10;                 // constant variable
final void method() { }          // cannot override
final class MyClass { }          // cannot extend
```

### `abstract`
```java
abstract class Shape {            // cannot instantiate
    abstract void draw();         // no body, must override
}
```

### `synchronized`
```java
synchronized void increment() {  // only one thread at a time
    count++;
}
```

### `volatile`
```java
volatile boolean running = true; // always read from main memory
```

### `transient`
```java
transient int tempData;          // excluded from serialization
```

---

## 🔥 Interview Questions

**Q1: What is autoboxing and unboxing?**
> - Autoboxing: automatic conversion of primitive → wrapper (int → Integer)
> - Unboxing: automatic conversion of wrapper → primitive (Integer → int)

**Q2: What is the Integer Cache?**
> Java caches Integer values from **-128 to 127**. So `Integer a = 127` and `Integer b = 127` are the same object. Beyond this range, new objects are created.

**Q3: Can enum have a constructor?**
> Yes, but it must be **private**. Cannot create enum objects with `new`.

**Q4: Difference between `final`, `finally`, `finalize`?**
> - `final`: keyword for constants, prevent overriding/inheritance
> - `finally`: block that always executes after try-catch
> - `finalize()`: method called by GC before destroying object (deprecated in Java 9+)

---
