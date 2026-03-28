
# ☕ Core Java — Complete Notes

**A structured, beginner-to-intermediate reference for Core Java**  
*Covering everything from classes and OOP to JDBC, file handling, and Java 8 features*


## 📖 About This Repository

This repository contains **comprehensive, well-structured Core Java notes** built for learners who want a clear, example-driven reference they can actually understand and revisit.

Every topic is explained with:
- **Concise theory** — the *what* and *why* before the code
- **Verified code examples** — tested and ready to run in Eclipse or any Java IDE
- **Comparison tables** — quick rules for access specifiers, data types, exceptions, and more
- **Common mistakes** — what to avoid and why it breaks
- **Quick reference summaries** at the end of each section

Whether you're learning Java for the first time, preparing for an interview, or looking for a fast refresher — this is your go-to reference.

---

## 🗂️ Topics Covered

| # | Topic | Key Concepts |
|---|-------|-------------|
| 1 | **Classes in Java** | Class syntax, naming conventions, PascalCase |
| 2 | **Objects & `new` Keyword** | Object creation, heap memory, reference variables |
| 3 | **Types of Variables** | Local, static, instance, reference variables |
| 4 | **Methods in Java** | void, return types, arguments, varargs, static methods |
| 5 | **Data Types** | All primitives, String, ranges, default values |
| 6 | **`var` Type (Java 10+)** | Type inference, restrictions |
| 7 | **Memory Management** | Stack vs heap, Garbage Collector |
| 8 | **Constructors** | Default, overloading, constructor chaining with `this()` |
| 9 | **`this` Keyword** | Current object reference, shadowing, `this()` |
| 10 | **Packages** | Organization, import, fully qualified names |
| 11 | **OOP — Four Pillars** | Inheritance, Polymorphism, Encapsulation, Abstraction |
| 12 | **Access Specifiers** | private, default, protected, public — on variables, constructors, classes |
| 13 | **Polymorphism** | Overriding (runtime), Overloading (compile-time), `@Override` |
| 14 | **`final` Keyword** | Constants, preventing override and inheritance |
| 15 | **Interfaces** | Abstract methods, default methods, Functional Interface, Lambda, Java 8 features |
| 16 | **Abstract Classes** | Partial implementation, interface vs abstract class comparison |
| 17 | **Exception Handling** | try-catch, multi-catch, finally, throws, throw, exception hierarchy |
| 18 | **Encapsulation** | Private fields, getters, setters, data hiding |
| 19 | **Type Casting** | Upcasting, downcasting, `instanceof` |
| 20 | **Arrays** | Declaration, iteration, bubble sort, duplicate removal, swapping |
| 21 | **Wrapper Classes** | Primitive wrappers, `parseInt`, `parseDouble`, `NumberFormatException` |
| 22 | **Unary Operators** | Post/pre increment and decrement with step-by-step examples |
| 23 | **Scanner Class** | Reading user input — `next()`, `nextLine()`, `nextInt()`, etc. |
| 24 | **Loops** | for, while, do-while, for-each |
| 25 | **Control Statements** | break, continue, if-else, switch, comparison operators |
| 26 | **File Handling** | File, FileReader, FileWriter, BufferedReader, BufferedWriter |
| 27 | **Serialization** | Object to byte stream, deserialization, `transient` keyword |
| 28 | **JDBC** | Connect to MySQL, INSERT, DELETE, UPDATE, SELECT with ResultSet |
| 29 | **Custom Exceptions** | Extending RuntimeException, `throw` vs `throws` |
| 30 | **Threads** | Overview + resource links |
| 31 | **Eclipse Shortcuts** | Ctrl+Space, Ctrl+1, Ctrl+O, F3, Ctrl+. |
| 32 | **Quick Reference Tables** | Variables, access specifiers, OOP summary, exception hierarchy |

---

## 🚀 How to Use These Notes

**For learning a new topic:**  
Read the theory at the top of each section, then trace through the code examples one by one.

**For interview prep:**  
Jump to the [Quick Reference Tables](#32-quick-reference-tables) at the end and drill the comparison tables.

**For debugging or revising:**  
Use the [Table of Contents](core-java-notes.md#-table-of-contents) to jump directly to what you need.

---

## 📁 Repository Structure

```
📦 core-java-notes
 ┣ 📄 README.md            ← You are here
 ┗ 📄 core-java-notes.md   ← Complete notes (all 32 topics)
```

---

## 💡 Sample — What the Notes Look Like

Here's a small preview of how concepts are presented:

```java
// Static vs Instance variable — key difference
public class A {
    static int staticX = 10;   // shared across ALL objects
    int instanceX = 10;        // each object gets its OWN copy

    public static void main(String[] args) {
        A a1 = new A();
        A a2 = new A();

        A.staticX = 99;         // changes for everyone
        a1.instanceX = 99;      // changes only for a1

        System.out.println(a2.instanceX); // 10 — unaffected
        System.out.println(A.staticX);    // 99 — shared
    }
}
```

And tables like this appear throughout for quick scanning:

| Specifier | Same Class | Same Package | Diff Package (subclass) | Diff Package |
|-----------|-----------|--------------|--------------------------|-------------|
| `private` | ✅ | ❌ | ❌ | ❌ |
| `default` | ✅ | ✅ | ❌ | ❌ |
| `protected` | ✅ | ✅ | ✅ | ❌ |
| `public` | ✅ | ✅ | ✅ | ✅ |

---

## 🧰 Prerequisites

To run the code examples locally you need:

- **Java JDK 11+** — [Download here](https://www.oracle.com/java/technologies/downloads/)
- **Eclipse IDE** (recommended) — [Download here](https://www.eclipse.org/downloads/)  
  or any IDE: IntelliJ IDEA, VS Code with Java Extension Pack, etc.
- **MySQL** (for JDBC examples only) — [Download here](https://dev.mysql.com/downloads/windows/installer/8.0.html)

---

## 🎯 Who Is This For?

| You are... | This helps you... |
|-----------|-----------------|
| A complete beginner | Learn Java from the ground up with clear examples |
| A student preparing for exams | Revise all core topics quickly with summaries |
| A developer refreshing Java knowledge | Find syntax, rules, and patterns fast |
| Someone preparing for interviews | Drill access specifiers, OOP rules, exception hierarchy |

---

## 📌 Key Java Versions Referenced

| Feature | Java Version |
|---------|-------------|
| `@Override` annotation | Java 5 |
| Numeric literals with `_` (e.g., `23_567`) | Java 7 |
| Lambda expressions, `default` in interfaces, Stream API | Java 8 |
| `var` type (local variable type inference) | Java 10 |

---

## 📚 Additional Resources

| Resource | Link |
|---------|------|
| Unary Operators (Assignment 1) | [YouTube Playlist](https://www.youtube.com/playlist?list=PLQVUMrcSsQIRZOM2vZoh8bPG1nq6X-nTe) |
| Data Types & Type Casting (Assignment 2) | [YouTube Video](https://www.youtube.com/watch?v=h3TxueBRxnE) |
| IIB Assignment 3 | [YouTube Video](https://www.youtube.com/watch?v=_3O2bPWckoI) |
| SIB Assignment 4 | [YouTube Video](https://www.youtube.com/watch?v=tQmvABQgi8k) |
| Super Keyword Assignment 5 | [YouTube Video](https://www.youtube.com/watch?v=KETJakbA6tw) |
| Threads (Lectures 44–49) | [YouTube Playlist](https://www.youtube.com/watch?v=Uw1tocKJNZw&list=PLbLiFkJgsmq6j_fFlZuy0xIs6upvrML26&index=44) |
| MySQL Installation Guide | [Prowesstics Blog](https://www.prowesstics.com/blogs/mysql-workbench-installation/) |

---

## 🤝 Contributing

Found a mistake, want to add an example, or want to extend a topic?

1. Fork this repository
2. Create a new branch: `git checkout -b fix/topic-name`
3. Make your changes to `core-java-notes.md`
4. Open a Pull Request with a brief description of what you changed

All contributions are welcome — corrections, additional examples, new topics, or better formatting.

---

## 📄 License

This project is licensed under the **MIT License** — feel free to use, share, and build on these notes with attribution.



**If these notes helped you, consider giving the repo a ⭐ — it helps others find it!**

*Happy coding! ☕*

</div>
