# ☕ Core Java — Complete Notes

> **Topic:** Core Java Fundamentals  
> **Level:** Beginner to Intermediate  
> **IDE Used:** Eclipse

---

## 📋 Table of Contents

1. [Classes in Java](#1-classes-in-java)
2. [Objects & the `new` Keyword](#2-objects--the-new-keyword)
3. [Types of Variables](#3-types-of-variables)
4. [Methods in Java](#4-methods-in-java)
5. [Data Types in Java](#5-data-types-in-java)
6. [The `var` Type (Java 10+)](#6-the-var-type-java-10)
7. [Memory Management](#7-memory-management)
8. [Constructors in Java](#8-constructors-in-java)
9. [The `this` Keyword](#9-the-this-keyword)
10. [Packages in Java](#10-packages-in-java)
11. [OOP — The Four Pillars](#11-oop--the-four-pillars)
12. [Access Specifiers](#12-access-specifiers)
13. [Polymorphism](#13-polymorphism)
14. [The `final` Keyword](#14-the-final-keyword)
15. [Interfaces](#15-interfaces)
16. [Abstract Classes](#16-abstract-classes)
17. [Exception Handling](#17-exception-handling)
18. [Encapsulation](#18-encapsulation)
19. [Type Casting (Upcasting & Downcasting)](#19-type-casting-upcasting--downcasting)
20. [Arrays](#20-arrays)
21. [Wrapper Classes](#21-wrapper-classes)
22. [Unary Operators](#22-unary-operators)
23. [Scanner Class (User Input)](#23-scanner-class-user-input)
24. [Loops in Java](#24-loops-in-java)
25. [Control Statements](#25-control-statements)
26. [File Handling](#26-file-handling)
27. [Serialization & Deserialization](#27-serialization--deserialization)
28. [JDBC — Java Database Connectivity](#28-jdbc--java-database-connectivity)
29. [Custom Exceptions](#29-custom-exceptions)
30. [Threads in Java](#30-threads-in-java)
31. [Eclipse Shortcuts](#31-eclipse-shortcuts)
32. [Quick Reference Tables](#32-quick-reference-tables)

---

## 1. Classes in Java

A **class** is a blueprint used to create objects in Java. It is defined using the `class` keyword (always lowercase).

```java
class A {
    // class body defined inside flower brackets { }
}
```

### Class Naming Conventions

| Rule                                      | Example                     | Valid?                 |
| ----------------------------------------- | --------------------------- | ---------------------- |
| Start with uppercase                      | `class Bank`                | Yes                    |
| CamelCase for multi-word names            | `class BankAccountNumber`   | Yes                    |
| Space in name                             | `class Bank Account Number` | No                     |
| Starts with a number                      | `class 1Bank`               | No                     |
| Starts with letter, followed by number    | `class Bank1`               | Yes                    |
| Snake_case                                | `class Bank_Account_Number` | Works, not recommended |
| Special character `$`                     | `class $A`                  | Works, not recommended |
| Other special chars (`#`, `@`, `%`, etc.) | `class #Bank`               | No                     |

> **Best Practice:** Always use **PascalCase** (UpperCamelCase) for class names.

---

## 2. Objects & the `new` Keyword

### Creating an Object

```java
ClassName variableName = new ClassName();
```

The `new` keyword:

- Sends a request to the class to **create an object in heap memory**
- Returns the object's memory address and stores it in a **reference variable**

```java
public class A {
    public static void main(String[] args) {
        A a1 = new A();
        A a2 = new A();
        System.out.println(a1); // e.g., p1.A@4517d9a3
        System.out.println(a2); // different address
    }
}
```

---

## 3. Types of Variables

Java has **four types of variables**:

### 3.1 Local Variables

- Declared **inside a method**
- Accessible **only within that method**
- **Must be initialized** before use — no automatic default value

```java
public void test() {
    int x = 10;
    System.out.println(x); // Correct
}

public void anotherMethod() {
    System.out.println(x); // Error: x is not accessible here
}
```

```java
public static void main(String[] args) {
    int x;                  // declared but NOT initialized
    System.out.println(x); // Error: variable x might not have been initialized
}
```

---

### 3.2 Static Variables

- Declared **inside class, outside methods**, using the `static` keyword
- Have **global access** — accessible from any method in the class
- Automatically assigned **default values** if not initialized
- **Shared across all objects** — changing the value in one place reflects everywhere

```java
public class A {
    static int x = 10;

    public static void main(String[] args) {
        System.out.println(A.x);  // Recommended: ClassName.variableName
        System.out.println(x);    // Also valid within same class

        A a1 = new A();
        System.out.println(a1.x); // Works but NOT recommended
    }
}
// Output: 10, 10, 10
```

> Modifying a static variable changes it **everywhere**:

```java
A.x = 100;
System.out.println(A.x); // 100
System.out.println(A.x); // 100 (same value for all objects)
```

---

### 3.3 Non-Static / Instance Variables

- Declared **inside class, outside methods**, **without** `static`
- Each object gets its **own independent copy**
- Changes in one object's variable do **not** affect another object
- Automatically assigned **default values** if not initialized
- Require an object to be accessed

```java
public class A {
    int x = 10; // instance variable

    public static void main(String[] args) {
        A a1 = new A();
        a1.x = 20;          // modifying a1's copy

        A a2 = new A();
        System.out.println(a1.x); // 20
        System.out.println(a2.x); // 10 (unaffected)
    }
}
```

---

### 3.4 Reference Variables

- Can hold either an **object's memory address** or `null`
- The **data type** of a reference variable is the **class name**
- If a static reference variable is not initialized, its default value is `null`

```java
A a1 = null;       // reference variable created, no object
A a2 = new A();    // reference variable holding an object's address

System.out.println(a1); // null
System.out.println(a2); // p1.A@4517d9a3
```

---

### Default Values by Data Type

| Data Type                      | Default Value       |
| ------------------------------ | ------------------- |
| `byte`, `short`, `int`, `long` | `0`                 |
| `float`, `double`              | `0.0`               |
| `boolean`                      | `false`             |
| `char`                         | `' '` (blank space) |
| `String` / Any Object          | `null`              |

---

## 4. Methods in Java

### 4.1 `void` Methods

A `void` method **cannot return any value**.

```java
public void test() {
    System.out.println(100); // Correct
    return 100;              // Error: void method cannot return a value
}
```

### 4.2 Non-void Methods

Must use a `return <value>` statement — it is **mandatory**.

```java
public int test() {
    return 100;       // Correct
}

public String test() {
    return "mike";    // Correct
}

public int test() {
    // Error: missing return statement
}
```

### 4.3 The `return` Keyword

| Form            | Method Type | Purpose                             |
| --------------- | ----------- | ----------------------------------- |
| `return;`       | `void`      | Exits method early (optional)       |
| `return value;` | non-void    | Returns value and exits (mandatory) |

> Any code written **after** a `return` statement will never execute — this is an **Unreachable Code Error**:

```java
public void test() {
    System.out.println(100);
    return;
    System.out.println(200); // Error: Unreachable code
}
```

---

### 4.4 Method Arguments

Values supplied to a method when calling it. Method arguments are treated as **local variables**.

```java
// Single argument
public void test(int x) {
    System.out.println(x);
}
// Call: c1.test(100);

// Multiple arguments
public void test(int x, String y) {
    System.out.println(x + " " + y);
}
// Call: c1.test(100, "mike");
```

**Accepting any type using `Object`:**

```java
public void test(Object x) {
    System.out.println(x); // accepts any data type
}
```

**Variable-length arguments (`varargs`):**

```java
public void test(int ...x) {
    System.out.println(x[0]); // 1
    System.out.println(x[1]); // 2
}
// Call: a1.test(1, 2, 3, 4, 5);
```

> `varargs` must always be the **last parameter** in a method signature:

```java
public void test(String y, int ...x) { ... }
// Call: a1.test("mike", 1, 2, 3, 4, 5);
```

---

### 4.5 Static Methods

Static methods belong to the class, not to any object. Called using `ClassName.methodName()`.

```java
public class A {
    public static void main(String[] args) {
        A.test();                       // void static call
        int result = A.test(100, 200); // static call with return value
        System.out.println(result);     // 300
    }

    public static int test(int a, int b) {
        return a + b;
    }
}
```

---

## 5. Data Types in Java

### Primitive Data Types

| Category  | Type      | Size    | Default | Range                               |
| --------- | --------- | ------- | ------- | ----------------------------------- |
| Integer   | `byte`    | 1 byte  | `0`     | -128 to 127                         |
| Integer   | `short`   | 2 bytes | `0`     | -32,768 to 32,767                   |
| Integer   | `int`     | 4 bytes | `0`     | -2,147,483,648 to 2,147,483,647     |
| Integer   | `long`    | 8 bytes | `0`     | -9.2 quintillion to 9.2 quintillion |
| Floating  | `float`   | 4 bytes | `0.0`   | ~±3.4E+38 (32-bit IEEE 754)         |
| Floating  | `double`  | 8 bytes | `0.0`   | ~±1.8E+308 (64-bit IEEE 754)        |
| Boolean   | `boolean` | N/A     | `false` | `true` or `false`                   |
| Character | `char`    | 2 bytes | `' '`   | 0 to 65,535 (Unicode)               |

### Non-Primitive

| Type              | Size      | Default | Description                                          |
| ----------------- | --------- | ------- | ---------------------------------------------------- |
| `String`          | Dynamic   | `null`  | tores sequence of characters (text)                  |
| `Array`           | Fixed     | `null`  | Collection of elements of same type                  |
| `Class`           | Dynamic   | `null`  | Blueprint to create objects                          |
| `Object`          | Dynamic   | `null`  | Parent of all classes in Java                        |
| `Interface`       | Dynamic   | `null`  | Used to achieve abstraction                          |
| `Enum`            | Fixed Set | `null`  | Collection of predefined constants                   |
| `Wrapper Classes` | Depends   | `null`  | Converts primitive to object (Integer, Double, etc.) |
| `Collection`      | Dynamic   | `null`  | Group of objects (List, Set, Map, etc.)              |

### Important Literal Syntax

```java
static long   x4 = 9632629033L;  // 'L' suffix required for long literals
static float  x5 = 10.3F;        // 'F' suffix required for float literals
static int    x3 = 23_567;       // underscores allowed in numbers (Java 7+)
```

---

## 6. The `var` Type (Java 10+)

`var` provides **local variable type inference** — the compiler automatically determines the data type based on the assigned value.

```java
var x1 = 100;        // inferred as int
var x2 = 10.3F;      // inferred as float
var x3 = "mike";     // inferred as String
var x4 = false;      // inferred as boolean
var x5 = new A();    // inferred as A
var x6 = 'a';        // inferred as char
```

### Restrictions of `var`

| Usage              | Allowed? |
| ------------------ | -------- |
| Local variable     | Yes      |
| Static variable    | No       |
| Instance variable  | No       |
| Method argument    | No       |
| Method return type | No       |

```java
public class C {
    var x1;              // Error: instance variable
    static var x2;       // Error: static variable

    public static void main(String[] args) {
        var x5 = 100;    // Correct: local variable
    }

    public var test(var x3) { // Error: return type and argument
    }
}
```

---

## 7. Memory Management

### Stack vs Heap

| Feature    | Stack                               | Heap              |
| ---------- | ----------------------------------- | ----------------- |
| Stores     | Local variables, method call frames | Objects           |
| Order      | LIFO (Last In, First Out)           | No specific order |
| Managed by | JVM automatically                   | Garbage Collector |

### Garbage Collector

- Automatically **removes objects from heap memory** that are no longer referenced
- Prevents `OutOfMemoryError`
- Runs in the background — you cannot control exactly when it runs
- You can _suggest_ GC to run using `System.gc()`, but it's not guaranteed

---

## 8. Constructors in Java

A constructor is a special block that runs **automatically when an object is created**. It is used to initialize the object.

**Rules:**

- Must have the **same name as the class**
- Is **always void by default** — cannot have an explicit return type
- Is **not inherited** by child classes
- Is **not loaded** into the object — it only initializes it

```java
public class A {
    A() {
        System.out.println("Constructor called");
    }
}
```

```java
public class A {
    A() {
        return 100; // Error: constructor cannot return a value
    }
}
```

> If you add a return type (like `void`) to a constructor, Java treats it as a **regular method**, not a constructor.

```java
void A() { ... }  // This is a METHOD, not a constructor — no output when object is created
```

---

### 8.1 Default Constructor

When you do **not** explicitly write any constructor, the Java compiler **automatically adds an empty no-argument constructor** during compilation. This is called the **default constructor**.

> The default constructor is **not added** when:
>
> - You define a constructor with arguments
> - You define both argument and no-argument constructors

```java
// Default constructor IS added (no constructor defined)
public class A {
    public static void main(String[] args) {
        A a1 = new A(); // Works fine
    }
}

// Default constructor NOT added
public class A {
    A(int x) { }
    public static void main(String[] args) {
        A a1 = new A();      // Error
        A a2 = new A(100);   // OK
    }
}
```

---

### 8.2 Constructor Overloading

Multiple constructors in the same class with **different number or type of arguments**.

```java
public class A {
    A() {                     // 0 arguments
        System.out.println("A");
    }
    A(int x) {                // 1 int argument
        System.out.println(x);
    }
    A(int x, int y) {         // 2 int arguments
        System.out.println(x + " " + y);
    }
    A(float x) {              // 1 float argument
        System.out.println(x);
    }

    public static void main(String[] args) {
        A a1 = new A();          // A
        A a2 = new A(100);       // 100
        A a3 = new A(200, 300);  // 200 300
        A a4 = new A(10.3f);     // 10.3
    }
}
```

---

### 8.3 Constructor Chaining with `this()`

`this()` calls **one constructor from another constructor** in the same class.

**Rules:**

- `this()` can **only be called from another constructor** (not from a method)
- It must always be the **first statement** inside the constructor

```java
public class A {
    A() {
        System.out.println("No-arg constructor");
    }
    A(int x) {
        this();  // Calls the no-arg constructor first
        System.out.println("int constructor: " + x);
    }
    public static void main(String[] args) {
        A a1 = new A(100);
        // Output:
        // No-arg constructor
        // int constructor: 100
    }
}
```

```java
public class A {
    A() {
        System.out.println(200);
        this(100); // Error: this() must be the FIRST statement
    }
}
```

```java
// Practical use: setting default values
public class A {
    int x;
    A(int x) {
        this.x = x; // 'this.x' = instance variable; 'x' = argument
    }
    A() {
        this(100);  // Calls A(int x) with value 100
    }
    public static void main(String[] args) {
        A a1 = new A();
        System.out.println(a1.x); // 100
    }
}
```

---

## 9. The `this` Keyword

`this` is a **special reference variable** that holds the address of the **current object** executing the method or constructor.

```java
public class A {
    public static void main(String[] args) {
        A a1 = new A();
        System.out.println(a1);  // p1.A@79fc0f2f
        a1.test();
    }
    public void test() {
        System.out.println(this); // prints the same address as a1
    }
}
```

**Uses of `this`:**

```java
// 1. Access instance variables when shadowed by a local variable or argument
public class A {
    int x = 10;
    public void test() {
        System.out.println(this.x); // refers to instance variable x
    }
}

// 2. Call instance methods from within another instance method
public void test1() {
    this.test2();
}

// 3. Call a constructor from another constructor
A() {
    this(100); // calls A(int x)
}
```

> `this` **cannot be used inside a static method** — static methods belong to the class, not to any object.

```java
public static void main(String[] args) {
    System.out.println(this); // Error
}
```

---

## 10. Packages in Java

Packages are **folders** used to organize Java classes, making large projects easier to maintain.

**Rules:**

- Package names should be **all lowercase**
- Cannot use Java **keywords** as package names (`new`, `static`, `public`, etc.)
- Do not start with capital letters
- Do not name a package `java`
- Classes in the same package do **not need imports**
- Classes in different packages **require an import statement**

```java
// Class in package p1
package p1;
public class A { }

// Class in same package p1 — no import needed
package p1;
public class B extends A { }

// Class in different package p2 — import required
package p2;
import p1.A;
public class C extends A { }

// Import all classes from a package
import p1.*;

// When two packages have a class with the same name, use fully qualified names
p1.A a1 = new p1.A();
p2.A a2 = new p2.A();
```

**Real-world naming example:**

```java
package com.tcs.service;

public class EmailService {
    public void sendEmail() {
        System.out.println("Sending Email....");
    }
}
```

```java
package com.tcs.auth;
import com.tcs.service.EmailService;

public class MainClass {
    public static void main(String[] args) {
        EmailService es = new EmailService();
        es.sendEmail(); // Sending Email....
    }
}
```

---

## 11. OOP — The Four Pillars

| Pillar            | Description                                                   |
| ----------------- | ------------------------------------------------------------- |
| **Inheritance**   | Reuse members of a parent class in a child class              |
| **Polymorphism**  | A feature takes more than one form (overloading & overriding) |
| **Encapsulation** | Wrap data and methods together; restrict direct access        |
| **Abstraction**   | Hide implementation details; define _what_, not _how_         |

---

### 11.1 Inheritance

Child class **inherits members** (non-static, non-private) from the parent class using the `extends` keyword.

```java
public class Animal {
    public void eat()   { System.out.println("Eating"); }
    public void sleep() { System.out.println("Sleeping"); }
}

public class Dog extends Animal {
    public static void main(String[] args) {
        Dog d = new Dog();
        d.eat();   // Inherited from Animal
        d.sleep(); // Inherited from Animal
    }
}
```

**Multilevel Inheritance:**

```java
public class A {
    public void test1() { System.out.println(1); }
}
public class B extends A {
    public void test2() { System.out.println(2); }
}
public class C extends B {
    public static void main(String[] args) {
        C c1 = new C();
        c1.test1(); // 1 — inherited from A via B
        c1.test2(); // 2 — inherited from B
    }
}
```

**Multiple Inheritance — NOT supported with classes:**

> Java does **not support multiple inheritance** with classes due to the **Diamond Problem** — ambiguity about which parent's method to use when two parents share the same method name.

Diamond Problem:Suppose we inherit a method from A->B->D and Same method is inherited from A->C->D, then confusion from which parent class method is inherited to child class D. This is called as DIAMOND PROBLEM. Hence in java classes does not support multiple inheritance

```java
public class C extends A, B { } // Error
```

> Multiple inheritance **is supported with interfaces**.

**Drawback of Inheritance:** It creates **tight coupling** — the child class is heavily dependent on the parent class. Interfaces are preferred to achieve **loose coupling**.

---

### Inheritance Keywords Summary

| Relationship           | Keyword      |
| ---------------------- | ------------ |
| Class to Class         | `extends`    |
| Interface to Interface | `extends`    |
| Class to Interface     | `implements` |

---

## 12. Access Specifiers

Access specifiers define the **visibility** of variables, methods, constructors, and classes.

### On Variables and Methods

| Specifier   | Same Class | Same Package (subclass) | Same Package (non-subclass) | Different Package (subclass) | Different Package (non-subclass) |
| ----------- | ---------- | ----------------------- | --------------------------- | ---------------------------- | -------------------------------- |
| `private`   | Yes        | No                      | No                          | No                           | No                               |
| `default`   | Yes        | Yes                     | Yes                         | No                           | No                               |
| `protected` | Yes        | Yes                     | Yes                         | Yes                          | No                               |
| `public`    | Yes        | Yes                     | Yes                         | Yes                          | Yes                              |

```java
// private: accessible only within same class
private int x = 10;
private void test() { }

// default: no keyword — accessible within same package only
int x = 10;
void test() { }

// protected: same package + different package via inheritance only
protected int x = 10;
protected void test() { }

// public: accessible everywhere
public int x = 10;
public void test() { }
```

---

### On Constructors

| Constructor Access | Object Creation   | Inheritance Allowed of That Class |
| ------------------ | ----------------- | --------------------------------- |
| `private`          | Same class only   | Not allowed                       |
| `default`          | Same package only | Same package only                 |
| `protected`        | Same package only | Same + different package          |
| `public`           | Everywhere        | Same + different package          |

> **Constructors are never inherited** — access specifier only affects where objects can be created and whether a class can be extended.

---

### On Classes

> A top-level class can only be `public` or `default`. It **cannot** be `private` or `protected`.

| Class Access | Object Creation | Inheritance              |
| ------------ | --------------- | ------------------------ |
| `default`    | Same package    | Same package only        |
| `public`     | Everywhere      | Same + different package |

---

## 13. Polymorphism

Polymorphism means **"one feature, many forms"**. In Java, it applies to methods only (not variables).

### 13.1 Method Overriding (Runtime Polymorphism)

The child class **modifies the behavior** of an inherited method from the parent class.

```java
public class GoldAccount {
    public void rateOfInterest() { System.out.println("nil"); }
    public void onlineBanking()  { System.out.println("yes"); }
}

public class PlatinumAccount extends GoldAccount {
    @Override
    public void rateOfInterest() {
        System.out.println("6% PA"); // overriding parent method
    }

    public static void main(String[] args) {
        PlatinumAccount p = new PlatinumAccount();
        p.rateOfInterest(); // 6% PA (overridden)
        p.onlineBanking();  // yes   (inherited)

        GoldAccount g = new GoldAccount();
        g.rateOfInterest(); // nil   (original)
    }
}
```

**Rules for Overriding:**

| Rule             | Detail                                                                      |
| ---------------- | --------------------------------------------------------------------------- |
| Method name      | Must be **exactly the same**                                                |
| Return type      | Must **match**                                                              |
| Access specifier | Can be **increased** but not **reduced**                                    |
| Static methods   | **Cannot be overridden** (but they are inherited and follow method hiding.) |
| Private methods  | **Private methods are NOT inherited** (so they cannot be overridden.)       |
| `final` methods  | **Cannot be overridden**                                                    |

```java
// Increasing access scope is allowed
// Parent: default  →  Child: public     OK
// Parent: default  →  Child: protected  OK

// Reducing access scope is NOT allowed
// Parent: public   →  Child: default    Error
```

**`@Override` Annotation** (introduced in Java 5):

Instructs the compiler to verify that overriding is actually happening. If the method name is wrong, you get a compile-time error.

```java
@Override
public void rateOfInterests() { } // Error: method name mismatch — no such method to override
```

---

### 13.2 Method Overloading (Compile-time Polymorphism)

Multiple methods with the **same name** in the same class, but with **different arguments**.

```java
public class EmailService {
    // Without attachment
    public void sendEmail(String to, String subject, String message) {
        System.out.println("Sending email...");
    }

    // With attachment — overloaded
    public void sendEmail(String to, String subject, String message, String filePath) {
        System.out.println("Sending email with attachment...");
    }
}
```

---

## 14. The `final` Keyword

| Applied To               | Effect                                                              |
| ------------------------ | ------------------------------------------------------------------- |
| Variable                 | Value cannot be changed (constant)                                  |
| Static/Instance variable | Initialization is **mandatory** — blank final field error otherwise |
| Method                   | Cannot be **overridden**                                            |
| Class                    | Cannot be **inherited**                                             |

```java
// Final variable — value cannot change
final int x = 10;
x = 20; // Error

// Blank final field error
final int x;         // Error: must initialize
final static int y;  // Error: must initialize

// Final method — cannot override
public final void test() { ... }
// @Override — Error: cannot override a final method

// Final class — cannot inherit
final public class A { }
public class B extends A { } // Error: cannot inherit from final class
```

---

## 15. Interfaces

An **interface** defines _what_ needs to be done — not _how_. It is a **contract** that implementing classes must follow.

**Key Points:**

- Can only contain **abstract (incomplete) methods** (Java 7 and earlier)
- All variables are **implicitly `public static final`** (constants)
- Cannot create an object of an interface
- An interface **reference variable** can be created
- Promotes **loose coupling** and good design

```java
public interface NotificationService {
    public void emailService();    // abstract
    public void smsService();      // abstract
    public void whatsAppService(); // abstract
}

public class NotificationServiceImpl implements NotificationService {
    @Override
    public void emailService()    { System.out.println("Sending Email"); }
    @Override
    public void smsService()      { System.out.println("Sending SMS"); }
    @Override
    public void whatsAppService() { System.out.println("Sending WhatsApp"); }

    public static void main(String[] args) {
        NotificationServiceImpl impl = new NotificationServiceImpl();
        impl.emailService();
        impl.smsService();
        impl.whatsAppService();
    }
}
```

---

### Interface Variables

```java
public interface A {
    int MAX_VAL = 100;              // implicitly: public static final int MAX_VAL = 100
    static final int MIN_VAL = 0;
}

System.out.println(A.MAX_VAL); // 100
System.out.println(A.MIN_VAL); // 0
```

---

### Interface Rules Summary

```java
// Method access can only be public or default (package-private)
void test3();           // default — OK
public void test4();    // public  — OK
protected void test1(); // Error
private void test2();   // Error

// Cannot instantiate an interface
A a1 = new A(); // Error
A a2;           // OK — reference variable is fine

// Static incomplete methods are NOT allowed
public static void test2(); // Error
```

---

### Inheritance with Interfaces

```java
// Interface extending interface
interface B extends A { ... }

// Class implementing interface
class C implements A { ... }

// Multiple inheritance with interfaces (supported)
interface C extends A, B { ... }
class C implements A, B { ... }

// Class can both extend and implement — extends must come FIRST
class C extends B implements A { ... }
```

---

### Marker Interface

An **empty interface** (no methods or variables) is called a **Marker Interface**.

```java
public interface Serializable { }  // Example from Java standard library
```

---

### Java 8 — `default` Methods in Interfaces

Java 8 introduced the `default` keyword to allow **complete methods** inside interfaces.

```java
public interface A {
    default public void test1() {
        System.out.println("Complete method in interface");
    }
    public void test2(); // still abstract
}

public class B implements A {
    @Override
    public void test2() {
        System.out.println("Implemented test2");
    }

    public static void main(String[] args) {
        B b1 = new B();
        b1.test1(); // From interface default method
        b1.test2(); // From class
    }
}
```

---

### Functional Interface

A **functional interface** has **exactly one abstract method**. It can have any number of `default` methods.

```java
@FunctionalInterface
public interface A {
    public void test1(); // exactly ONE abstract method
    default public void test2() { System.out.println(2); }
    default public void test3() { System.out.println(3); }
}

@FunctionalInterface
public interface A { }                       // Error: zero abstract methods
@FunctionalInterface
public interface A { void t1(); void t2(); } // Error: two abstract methods
```

---

### Lambda Expressions (Java 8)

Lambda expressions provide a **concise way to implement a functional interface** without writing a full class. Internally Java creates an **anonymous class** and implements the method.

```java
// Traditional way
A a1 = new A() {
    public void test1() { System.out.println(100); }
};

// Lambda expression
A a1 = () -> { System.out.println(100); };
a1.test1(); // 100
```

**Lambda with arguments:**

```java
@FunctionalInterface
public interface A {
    public void test1(int x);
}

A a1 = (int x) -> { System.out.println(x); };
a1.test1(100); // 100
```

**Lambda with `default` methods:**

```java
A a1 = (int y) -> { System.out.println(y); };
a1.test1(100); // 100
a1.test2();    // 2
a1.test3();    // 3
```

---

### Java 8 — Static Methods in Interfaces

```java
public interface A {
    static int x = 100;

    public static void test1() {
        System.out.println("Static method in interface");
    }

    public static void main(String[] args) {
        System.out.println(A.x); // 100
        A.test1();               // Static method in interface
    }
}
```

---

## 16. Abstract Classes

An **abstract class** can have **both complete and incomplete methods**, sitting between a regular class and an interface.

**Key Points:**

- Use `abstract` keyword to declare the class and its incomplete non-static methods
- Can have static, non-static, and final variables
- **Cannot create an object** of an abstract class
- **Does not support multiple inheritance**
- Can have a `main` method
- Cannot have **static incomplete methods**

```java
abstract public class A {
    public void test1() { }          // complete method — OK
    abstract public void test2();    // incomplete method — OK
    public static void test3() { }   // complete static method — OK
    public static void test4();      // Error: static incomplete not allowed
    public static void main(String[] args) {
        A a1 = new A();              // Error: cannot instantiate abstract class
    }
}
```

### Example

```java
abstract public class A {
    int x = 10;
    public void test() { System.out.println(100); }
}

public class B extends A {
    public static void main(String[] args) {
        B b1 = new B();
        System.out.println(b1.x); // 10
        b1.test();                // 100
    }
}
```

---

### Abstract Class + Interface Together

```java
public interface A {
    public void test1();
}

public abstract class B implements A {
    abstract public void test2();
}

public class C extends B {
    @Override
    public void test1() { System.out.println("From test1"); }
    @Override
    public void test2() { System.out.println("From test2"); }

    public static void main(String[] args) {
        C c1 = new C();
        c1.test1(); // From test1
        c1.test2(); // From test2
    }
}
```

---

### Interface vs Abstract Class

| Feature              | Interface                  | Abstract Class                       |
| -------------------- | -------------------------- | ------------------------------------ |
| Multiple inheritance | Supported                  | Not supported                        |
| Variables            | Only `public static final` | Any type (static, non-static, final) |
| Complete methods     | Java 8+ via `default`      | Always supported                     |
| Object creation      | Not allowed                | Not allowed                          |
| Constructor          | Not allowed                | Allowed                              |

---

## 17. Exception Handling

An **exception** is an unexpected event at runtime that disrupts normal program flow.

```java
// Without handling — program stops abruptly
int x = 10, y = 0;
int z = x / y;             // ArithmeticException: / by zero
System.out.println("This line never runs");
```

### try-catch Block

```java
try {
    int z = 10 / 0;
} catch (Exception e) {
    e.printStackTrace();   // handles the exception
}
System.out.println("Program continues..."); // This runs
```

---

### Types of Exceptions

| Type                       | When Occurs                           | Example                                       |
| -------------------------- | ------------------------------------- | --------------------------------------------- |
| **Checked (Compile-time)** | During `.java` → `.class` compilation | `IOException`, `FileNotFoundException`        |
| **Unchecked (Runtime)**    | While running `.class` file           | `ArithmeticException`, `NullPointerException` |

---

### Common Runtime Exceptions

**1. `ArithmeticException`** — invalid math operation

```java
int z = 10 / 0;  // ArithmeticException: / by zero
int z = 11 % 0;  // ArithmeticException: / by zero
```

**2. `NullPointerException`** — accessing members on a `null` reference

```java
A a1 = null;
System.out.println(a1.x);          // Error: NullPointerException

// Static variable accessed via null reference does NOT throw NPE
// (the compiler resolves it to the class name at compile time)
A a1 = null;
System.out.println(a1.staticVar);  // Works — compiles as A.staticVar
```

**3. `NumberFormatException`** — invalid String-to-number conversion

```java
Double.parseDouble("10.3abc"); // NumberFormatException
```

**4. `ArrayIndexOutOfBoundsException`** — invalid array index

```java
int[] age = new int[3];
age[3] = 103; // Error: Index 3 out of bounds for length 3
```

---

### Multi-catch Blocks

```java
try {
    Integer.parseInt("invalid");
} catch (ArithmeticException e) {
    System.out.println("Arithmetic error");
} catch (NullPointerException e) {
    System.out.println("Null error");
} catch (Exception e) { // Parent class — must come LAST
    System.out.println("Some other error");
}
```

> Always catch **child exception classes before parent** exception classes.

---

### `finally` Block

The `finally` block **always executes** — whether or not an exception occurred. Ideal for cleanup tasks like closing files or database connections.

```java
try {
    int x = 100 / 0;
} catch (Exception e) {
    e.printStackTrace();
} finally {
    System.out.println("Finally block — always runs");
}
```

---

### `throws` Keyword

Used to **declare exceptions** that a method or constructor may throw, passing the responsibility to the caller.

```java
public void test() throws Exception {
    FileReader fr = new FileReader("G:\\test\\t1.txt");
}

public static void main(String[] args) throws Exception {
    A a1 = new A();
    a1.test();
}
```

---

### `final` vs `finally` vs `finalize()`

| Keyword      | Purpose                                                                               |
| ------------ | ------------------------------------------------------------------------------------- |
| `final`      | Makes variable constant; prevents method override; prevents class inheritance         |
| `finally`    | Block that always executes after try-catch; used for cleanup                          |
| `finalize()` | Method in `Object` class; called by the Garbage Collector before destroying an object |

---

## 18. Encapsulation

**Encapsulation** wraps variables and methods into a single unit and **restricts direct access** to internal data.

**How to implement:**

1. Make variables `private` (data hiding)
2. Provide `public` getter and setter methods

```java
public class A {
    private int x;  // data hidden
    private int y;

    public int getX()       { return x; }
    public void setX(int x) { this.x = x; }

    public int getY()       { return y; }
    public void setY(int y) { this.y = y; }
}

public class B {
    public static void main(String[] args) {
        A a1 = new A();
        a1.setX(100);
        a1.setY(200);
        System.out.println(a1.getX()); // 100
        System.out.println(a1.getY()); // 200
    }
}
```

**Benefits:**

- Protects data from unintended modification
- You can add validation logic inside setters
- Increases code maintainability and readability

---

## 19. Type Casting (Upcasting & Downcasting)

### 19.1 Upcasting

Storing a **child class object address** into a **parent class reference variable**. Makes the reference reusable for multiple child types and enables polymorphism.

```java
A a1 = new B();  // B's object stored in A's reference variable
a1 = new C();    // now holding C's object — same reference reused
```

**Polymorphism via upcasting:**

```java
public class A {
    void display() { System.out.println("Inside A"); }
}
public class B extends A {
    @Override
    void display() { System.out.println("Inside B"); }
}
public class C extends A {
    @Override
    void display() { System.out.println("Inside C"); }
    public static void main(String[] args) {
        A a1 = new B();
        a1.display(); // Inside B  (runtime polymorphism)
        a1 = new C();
        a1.display(); // Inside C
    }
}
```

> **Why use upcasting?**
>
> - Reuse one reference variable for multiple child objects
> - Enable polymorphism across multiple child classes
> - Write flexible, generic code

---

### `instanceof` Operator

Checks **which class object** is currently held by a reference variable.

```java
A a1 = new B();
System.out.println(a1 instanceof B); // true
System.out.println(a1 instanceof C); // false
```

---

### 19.2 Downcasting

Converting a **parent class reference** back to a **child class reference** to access child-specific members. Always perform upcasting first, then downcast safely using `instanceof`.

```java
public class A {
    public void display() { System.out.println("Inside A"); }
}
public class B extends A {
    public void showB() { System.out.println("Inside B"); }
}
public class C extends A {
    public void showC() { System.out.println("Inside C"); }
}

public class MainClass {
    public static void processObject(A obj) {
        if (obj instanceof B) {
            B b = (B) obj;  // downcast to B
            b.showB();
        } else if (obj instanceof C) {
            C c = (C) obj;  // downcast to C
            c.showC();
        } else {
            obj.display();
        }
    }
    public static void main(String[] args) {
        processObject(new B()); // Inside B
        processObject(new C()); // Inside C
    }
}
```

---

## 20. Arrays

Arrays hold a **fixed-size ordered collection of values** of the same type. Arrays are objects in Java and are stored in heap memory. Indexing starts at `0`.

```java
int[] age = new int[4];
age[0] = 90;
age[1] = 89;
age[2] = 67;
age[3] = 97;

System.out.println(age.length); // 4 — built-in final field
System.out.println(age[0]);     // 90
```

**Iterating with for loop:**

```java
for (int i = 0; i < age.length; i++) {
    System.out.println(age[i]);
}
```

**Iterating with for-each loop:**

```java
for (int x : age) {
    System.out.println(x);
}
```

> Accessing an index beyond the array size throws `ArrayIndexOutOfBoundsException`.

---

### Bubble Sort

Compares adjacent elements and swaps them if out of order. After each pass, the largest unsorted element moves to the end.

```java
int[] x = {35, 21, 22, 14};
int temp;

for (int j = 0; j < x.length - 1; j++) {
    for (int i = 0; i < x.length - 1; i++) {
        if (x[i] > x[i + 1]) {
            temp      = x[i + 1];
            x[i + 1]  = x[i];
            x[i]      = temp;
        }
    }
}
// Sorted output: 14, 21, 22, 35
```

---

### Removing Duplicates (from a sorted array)

```java
int[] x    = {3, 3, 4, 5, 6, 6};
int[] temp = new int[x.length];
int j = 0;

for (int i = 0; i < x.length - 1; i++) {
    if (x[i] != x[i + 1]) {
        temp[j++] = x[i];
    }
}
temp[j] = x[x.length - 1]; // always copy the last element
```

---

### Swapping Two Variables

```java
int x = 10, y = 20, temp;
temp = y;
y    = x;
x    = temp;
System.out.println(x); // 20
System.out.println(y); // 10
```

---

### Swapping Two Variables without using Third Variables

```java
int x = 10, y = 20;
x    = x + y; //x=10+20=30
y    = x - y; //y=30-20=10
x    = x - y; //x=30-10=20
System.out.println(x); // 20
System.out.println(y); // 10
```

---

## 21. Wrapper Classes

Wrapper classes wrap a primitive data type inside an object. They also provide useful utility methods for conversion.

| Primitive | Wrapper Class |
| --------- | ------------- |
| `byte`    | `Byte`        |
| `short`   | `Short`       |
| `int`     | `Integer`     |
| `long`    | `Long`        |
| `float`   | `Float`       |
| `double`  | `Double`      |
| `char`    | `Character`   |
| `boolean` | `Boolean`     |

**String to Primitive conversion:**

```java
String s = "100";
int    y = Integer.parseInt(s);          // String → int
double d = Double.parseDouble("10.3");   // String → double
```

**Handling invalid input:**

```java
try {
    double y = Double.parseDouble("10.3abc"); // invalid
} catch (NumberFormatException e) {
    e.printStackTrace();
}
System.out.println("Welcome"); // still runs
```

---

## 22. Unary Operators

### Post-Increment (`i++`)

Increments the value **after** the current expression is evaluated (next time the variable is seen).

```java
int i = 10;
int j = i++;        // j = 10, then i becomes 11
// i = 11, j = 10

int i = 10;
int j = i++ + i++ + i++; // 10 + 11 + 12 = 33; i becomes 13
// i = 13, j = 33
```

### Pre-Increment (`++i`)

Increments the value **in the same step**, before the expression is evaluated.

```java
int i = 10;
int j = ++i;        // i becomes 11, j = 11
// i = 11, j = 11

int i = 10;
int j = ++i + ++i + ++i; // 11 + 12 + 13 = 36; i becomes 13
// i = 13, j = 36
```

### Post-Decrement (`i--`)

```java
int i = 10;
int j = i-- + i--; // 10 + 9 = 19; i becomes 8
// i = 8, j = 19
```

### Pre-Decrement (`--i`)

```java
int i = 10;
int j = --i + --i; // 9 + 8 = 17; i becomes 8
// i = 8, j = 17
```

---

## 23. Scanner Class (User Input)

The `Scanner` class reads user input from the console.

```java
import java.util.Scanner;

Scanner scan = new Scanner(System.in);

String name   = scan.next();         // reads one word (stops at space)
String line   = scan.nextLine();     // reads full line including spaces
int    age    = scan.nextInt();      // reads integer
float  weight = scan.nextFloat();    // reads float
boolean ans   = scan.nextBoolean();  // reads boolean

scan.close(); // always close the scanner when done
```

---

## 24. Loops in Java

### `for` Loop

```java
for (int i = 0; i < 4; i++) {
    System.out.println(i); // 0, 1, 2, 3
}
```

### `while` Loop

Checks condition **before** entering the loop body.

```java
int i = 0;
while (i < 3) {
    System.out.println(i);
    i++;
}
// Output: 0, 1, 2
```

### `do-while` Loop

**Always runs at least once** — condition is checked after the first execution.

```java
int i = 100;
do {
    System.out.println(i); // runs once even though condition is false
    i++;
} while (i < 3);
// Output: 100
```

### `for-each` Loop

Iterates over arrays and collections. Can only **read** values sequentially.

```java
int[] age = {100, 101, 120};
for (int x : age) {
    System.out.println(x);
}
```

---

## 25. Control Statements

### `break`

Immediately exits the loop or switch statement.

```java
for (int i = 0; i < 3; i++) {
    if (i == 2) break;
    System.out.println(i); // 0, 1
}
```

### `continue`

Skips the **current iteration** and moves to the next.

```java
for (int i = 0; i < 5; i++) {
    if (i == 3) continue; // skips when i is 3
    System.out.println(i); // 0, 1, 2, 4
}
```

### `if / else if / else`

```java
String value = "yes";
if (value.equals("yes")) {
    System.out.println("Pass");
} else if (value.equals("no")) {
    System.out.println("Fail");
} else {
    System.out.println("Invalid Input");
}
```

### `switch` Statement

```java
int key = 2;
switch (key) {
    case 1:
        System.out.println("1st Floor");
        break;
    case 2:
        System.out.println("2nd Floor");
        break;
    case 3:
        System.out.println("3rd Floor");
        break;
    default:
        System.out.println("Invalid input");
        break;
}
```

### Comparison Operators

```java
System.out.println(2 == 3); // false
System.out.println(2 > 1);  // true
System.out.println(2 < 1);  // false
System.out.println(2 >= 2); // true
System.out.println(2 <= 2); // true
System.out.println(2 != 3); // true
```

---

## 26. File Handling

### `File` Class — Common Methods

```java
import java.io.File;

File f = new File("G:\\folder\\t1.txt");

f.exists();        // boolean — checks if file/folder exists
f.delete();        // boolean — deletes the file or folder
f.mkdir();         // boolean — creates a directory
f.length();        // long    — number of characters in file
f.createNewFile(); // boolean — creates new file (throws IOException — must handle)
f.list();          // String[] — lists names of files/folders in a directory
```

---

### `FileReader` — Reading Text Files

```java
import java.io.*;

File f = new File("G:\\folder\\t1.txt");
FileReader fr = new FileReader(f);

// Read character by character
for (int i = 0; i < f.length(); i++) {
    System.out.print((char) fr.read());
}
fr.close();
```

```java
// Read all at once into a char array
char[] ch = new char[(int) f.length()];
fr.read(ch);
for (char c : ch) System.out.print(c);
fr.close();
```

---

### `FileWriter` — Writing to Text Files

```java
import java.io.FileWriter;

// false = replace existing content; creates file if not present
FileWriter fw = new FileWriter("G:\\folder\\t4.txt", false);

fw.write(97);            // writes character 'a' (ASCII 97)
fw.write("Hello");       // writes string
fw.write('\n');          // newline
char[] ch = {'a','b','c'};
fw.write(ch);            // writes char array

fw.close(); // IMPORTANT: always close to flush and save content
```

**Append mode:**

```java
FileWriter fw = new FileWriter("G:\\folder\\t4.txt", true); // true = append, don't replace
```

---

### `BufferedReader` — Faster File Reading

Wraps `FileReader` to improve performance and provides the `readLine()` method.

```java
import java.io.*;

FileReader fr = new FileReader("G:\\folder\\t1.txt");
BufferedReader br = new BufferedReader(fr);

for (int i = 0; i < 3; i++) {
    System.out.println(br.readLine()); // reads one complete line
}

br.close();
fr.close();
```

---

### `BufferedWriter` — Faster File Writing

Wraps `FileWriter` to improve performance and provides the `newLine()` method.

```java
import java.io.*;

FileWriter fw = new FileWriter("G:\\folder\\t1.txt", true);
BufferedWriter bw = new BufferedWriter(fw);

bw.write("mike");
bw.newLine();             // platform-independent newline
bw.write("stallin");
bw.newLine();
bw.write(new char[]{'a','b','c'});

bw.close();
fw.close();
```

---

## 27. Serialization & Deserialization

**Serialization** converts an object into a byte stream and saves it to a file.
**Deserialization** reads that byte stream and reconstructs the object.

Use the `transient` keyword to **exclude a field** from serialization.

```java
import java.io.Serializable;

public class A implements Serializable {
    String name = "mike";
    transient String password = "testing"; // will NOT be serialized
}
```

**Serializing (writing object to file):**

```java
import java.io.*;

A a1 = new A();
FileOutputStream fos = new FileOutputStream("G:\\folder\\file.ser");
ObjectOutputStream oos = new ObjectOutputStream(fos);
oos.writeObject(a1);
oos.close();
fos.close();
```

**Deserializing (reading object from file):**

```java
import java.io.*;

FileInputStream fis = new FileInputStream("G:\\folder\\file.ser");
ObjectInputStream ois = new ObjectInputStream(fis);
A a1 = (A) ois.readObject();

System.out.println(a1.name);     // mike
System.out.println(a1.password); // null (transient — not saved)

ois.close();
fis.close();
```

---

## 28. JDBC — Java Database Connectivity

JDBC allows Java programs to **interact with relational databases** (MySQL, Oracle, PostgreSQL, etc.).

**Setup:**

- Install MySQL: https://dev.mysql.com/downloads/windows/installer/8.0.html
- Create database and table in MySQL Workbench

```sql
CREATE DATABASE psaDB;
USE psaDB;

CREATE TABLE student (
    name   VARCHAR(45),
    email  VARCHAR(128),
    mobile VARCHAR(10)
);
```

---

### JDBC Operations

**Insert:**

```java
import java.sql.*;

Connection con = DriverManager.getConnection(
    "jdbc:mysql://localhost:3306/psadb1", "root", "test");

Statement stmnt = con.createStatement();
stmnt.executeUpdate("INSERT INTO student VALUES('adam','adam@gmail.com','9632629555')");
con.close();
```

**Delete:**

```java
stmnt.executeUpdate("DELETE FROM student WHERE email='adam@gmail.com'");
```

**Update:**

```java
stmnt.executeUpdate("UPDATE student SET mobile='9632882052' WHERE email='mike@gmail.com'");
```

**Read / Select:**

```java
ResultSet result = stmnt.executeQuery("SELECT * FROM student");

while (result.next()) {
    System.out.println(result.getString(1)); // name
    System.out.println(result.getString(2)); // email
    System.out.println(result.getString(3)); // mobile
}
con.close();
```

**Best practice — close connection in `finally`:**

```java
Connection con = null;
try {
    con = DriverManager.getConnection("jdbc:mysql://localhost:3306/psadb1", "root", "test");
    Statement stmnt = con.createStatement();
    stmnt.executeUpdate("INSERT INTO student VALUES('adam','adam@gmail.com','9632629555')");
} catch (Exception e) {
    e.printStackTrace();
} finally {
    try { con.close(); } catch (Exception e2) { e2.printStackTrace(); }
}
```

---

## 29. Custom Exceptions

Create your own exception classes by extending `RuntimeException` (unchecked) or `Exception` (checked).

**Defining a custom exception:**

```java
public class InsufficientFunds extends RuntimeException {
    public InsufficientFunds(String msg) {
        super(msg); // passes message to parent Exception class
    }
}
```

**Throwing with `throw`:**

```java
int balance = 250, amount = 500;

if (balance < amount) {
    try {
        throw new InsufficientFunds("Low Balance");
    } catch (InsufficientFunds e) {
        System.out.println(e.getMessage()); // Low Balance
        e.printStackTrace();
    }
} else {
    System.out.println("Please collect cash!!");
}
```

> **`throw`** — throws an exception explicitly at a specific point in code.  
> **`throws`** — declares in a method signature that the method may throw an exception.

---

## 30. Threads in Java

A **thread** is a lightweight unit of execution. Java supports **multithreading** — multiple threads running concurrently within a program.

> **Recommended Resource:** Watch lectures 44–49 from PSA playlist (note: lectures after 49 are outdated):  
> https://www.youtube.com/watch?v=Uw1tocKJNZw&list=PLbLiFkJgsmq6j_fFlZuy0xIs6upvrML26&index=44

---

## 31. Eclipse Shortcuts

| Shortcut       | Name              | Description                                                          |
| -------------- | ----------------- | -------------------------------------------------------------------- |
| `Ctrl + Space` | Content Assist    | Autocomplete. Type `syso` then `Ctrl+Space` → `System.out.println()` |
| `Ctrl + 1`     | Quick Fix         | Suggests solutions for errors and warnings                           |
| `Ctrl + O`     | Quick Outline     | Shows all methods and fields in the current class                    |
| `F3`           | Go to Declaration | Jumps to where a variable, method, or class is declared              |
| `Ctrl + .`     | Next Problem      | Jumps to the next error or warning in the file                       |

---

## 32. Quick Reference Tables

### Variable Types Summary

| Variable Type         | Where Declared               | `static`? | Needs Object? | Default Value?              |
| --------------------- | ---------------------------- | --------- | ------------- | --------------------------- |
| Local                 | Inside method                | No        | No            | Must initialize manually    |
| Static                | Inside class, outside method | Yes       | No            | Auto-assigned               |
| Instance (Non-static) | Inside class, outside method | No        | Yes           | Auto-assigned               |
| Reference             | Anywhere                     | Optional  | Depends       | `null` (if static/instance) |

---

### Access Specifier Quick Reference

| Specifier   | Same Class | Same Package | Different Package (subclass) | Different Package |
| ----------- | ---------- | ------------ | ---------------------------- | ----------------- |
| `private`   | Yes        | No           | No                           | No                |
| `default`   | Yes        | Yes          | No                           | No                |
| `protected` | Yes        | Yes          | Yes                          | No                |
| `public`    | Yes        | Yes          | Yes                          | Yes               |

---

### OOP Concepts at a Glance

| Concept       | Keyword/Feature             | Key Idea                       |
| ------------- | --------------------------- | ------------------------------ |
| Inheritance   | `extends`                   | Reuse parent class members     |
| Polymorphism  | Override / Overload         | One method, multiple behaviors |
| Encapsulation | `private` + getters/setters | Hide and protect data          |
| Abstraction   | `interface` / `abstract`    | Define _what_, hide _how_      |

---

### Exception Hierarchy (Simplified)

```
Throwable
├── Error              (JVM-level errors — do not catch)
└── Exception
    ├── IOException          (Checked)
    ├── SQLException         (Checked)
    └── RuntimeException     (Unchecked)
        ├── ArithmeticException
        ├── NullPointerException
        ├── NumberFormatException
        ├── ArrayIndexOutOfBoundsException
        └── ClassCastException
```

---

### File Handling Classes Summary

| Class            | Purpose                       | Key Method                                                     |
| ---------------- | ----------------------------- | -------------------------------------------------------------- |
| `File`           | File/folder operations        | `exists()`, `delete()`, `mkdir()`, `createNewFile()`, `list()` |
| `FileReader`     | Read text files               | `read()`, `read(char[])`                                       |
| `FileWriter`     | Write to text files           | `write()`, `close()`                                           |
| `BufferedReader` | Faster reading + line-by-line | `readLine()`                                                   |
| `BufferedWriter` | Faster writing                | `write()`, `newLine()`                                         |

---

> **Note:** These notes cover Core Java fundamentals to advanced topics including OOP, Collections prerequisite topics, File I/O, JDBC, and Java 8 features. All examples are verified and ready to run in Eclipse or any Java IDE.  
> Assignments and additional video resources are linked inline throughout the notes.
