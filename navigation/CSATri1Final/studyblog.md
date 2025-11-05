---
layout: base
title: CSA Unit 1 Study Blog
description: CSA Unit 1 Study Blog
permalink: /csa1studyblog
hide: true
---

{% include nav/unit1hws.html %}

This unit introduced foundational concepts in Java programming—how programs are built, how data is represented and manipulated, and how classes and objects work together. The lessons below summarize what I learned in each section.

---

## 1.1 Introduction to Algorithms, Programming, and Compilers
**Summary:**  
Algorithms describe precise steps to solve a problem, and programming is how we implement those steps in a language like Java. A compiler translates human-readable code into machine code.

**Key Concepts:**
- Algorithms are finite and repeatable procedures.
- Compilers check syntax and convert Java source (`.java`) into bytecode (`.class`).
- The JVM executes bytecode on any system.

**Example:**
```java
public class Hello {
  public static void main(String[] args) {
    System.out.println("Hello, world!");
  }
}
````

**Resource:** [Java Overview – Oracle Docs](https://docs.oracle.com/javase/tutorial/getStarted/intro/definition.html)

---

## 1.2 Variables and Data Types (Partial)

**Summary:**
Variables store data, and each has a defined type that determines what operations are allowed.

**Key Concepts:**

* Primitive types: `int`, `double`, `boolean`, `char`
* Reference types: classes and objects
* Declaration and initialization syntax: `int score = 100;`

**Example:**

```java
int x = 5;
double y = 2.5;
boolean passed = true;
```

---

## 1.3 Expressions and Output

**Summary:**
Expressions combine literals, variables, and operators to compute values. Output is displayed using `System.out.println`.

**Key Concepts:**

* Operator precedence affects evaluation order.
* Concatenation joins strings with `+`.
* Parentheses clarify computation.

**Example:**

```java
System.out.println("Area: " + (3.14 * r * r));
```

---

## 1.4 Assignment Statements and Input

**Summary:**
Assignment changes a variable’s stored value. User input is handled through the `Scanner` class.

**Example:**

```java
Scanner sc = new Scanner(System.in);
System.out.print("Enter your name: ");
String name = sc.nextLine();
System.out.println("Welcome, " + name + "!");
```

---

## 1.5 Casting and Range of Variables

**Summary:**
Casting converts between numeric types and allows mixing of data types in expressions.
Type range limits must be respected to avoid overflow.

**Example:**

```java
int a = 3;
double b = 2;
System.out.println(a / b);        // 1.5
System.out.println((int) b / a);  // 0
```

---

## 1.6 Compound Assignment Operators

**Summary:**
Operators like `+=`, `-=`, and `*=` simplify arithmetic and assignment.

**Example:**

```java
int count = 5;
count += 2;   // same as count = count + 2;
```

---

## 1.7 Application Program Interface (API) and Libraries

**Summary:**
The Java API provides pre-built classes and methods for tasks like math, input/output, and string handling.
Understanding documentation is essential to use them correctly.

**Example:**

```java
import java.util.Random;
Random r = new Random();
int num = r.nextInt(10);  // 0–9
```

**Resource:** [Java SE API Specification](https://docs.oracle.com/en/java/javase/17/docs/api/index.html)

---

## 1.8 Documentation with Comments

**Summary:**
Comments explain code purpose and logic. They improve readability and maintainability.

**Example:**

```java
// Single-line comment
/*
 Multi-line
 comment
*/
/**
 * JavaDoc comment for methods or classes
 */
```

---

## 1.9 Method Signatures

**Summary:**
A method signature defines its name and parameter list. It allows overloading based on parameter types and counts.

**Example:**

```java
public static void greet(String name) {
  System.out.println("Hello " + name);
}
```

---

## 1.10 Calling Class Methods

**Summary:**
Class (static) methods belong to a class rather than a specific object.

**Example:**

```java
int maxVal = Math.max(5, 8);
System.out.println(maxVal);
```

---

## 1.11 `Math` Class

**Summary:**
The `Math` class provides mathematical constants and methods such as `pow`, `sqrt`, and `random`.

**Example:**

```java
double area = Math.PI * Math.pow(radius, 2);
```

---

## 1.12 Objects: Instances of Classes (Partial)

**Summary:**
Objects are created from classes, which define fields (attributes) and methods (behaviors).

**Example:**

```java
String word = new String("Hello");
System.out.println(word.length());
```

---

## 1.13 Object Creation and Storage (Partial)

**Summary:**
`new` allocates memory for objects. References store the address of that memory.

**Example:**

```java
Scanner input = new Scanner(System.in);
```

---

## 1.14 Calling Instance Methods

**Summary:**
Instance methods operate on a specific object and often modify its state or return a computed value.

**Example:**

```java
String name = "Anvay";
System.out.println(name.toUpperCase());
```

---

<style>
.card-grid {
  display: flex;
  flex-wrap: wrap;
  gap: 1rem;
}
.card {
  perspective: 1000px;
  width: 240px;
  height: 140px;
}
.card-inner {
  position: relative;
  width: 100%;
  height: 100%;
  text-align: center;
  transition: transform 0.8s;
  transform-style: preserve-3d;
  cursor: pointer;
}
.card:hover .card-inner { transform: rotateY(180deg); }
.card-front, .card-back {
  position: absolute;
  width: 100%;
  height: 100%;
  backface-visibility: hidden;
  display: flex;
  align-items: center;
  justify-content: center;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 1em;
  font-weight: bold;
}
.card-front { background: rgb(112,105,105); color: white; }
.card-back { background: rgb(63,76,88); color: white; transform: rotateY(180deg); }
</style>

<div class="card-grid">
  <div class="card"><div class="card-inner"><div class="card-front">Variable</div><div class="card-back">Stores data of a specific type for program use.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Casting</div><div class="card-back">Converting one data type into another.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Method</div><div class="card-back">Reusable block of code with parameters and return type.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Object</div><div class="card-back">Instance of a class with state and behavior.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">API</div><div class="card-back">Pre-defined set of classes and methods provided by Java.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Math Class</div><div class="card-back">Contains constants and methods for math operations.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Scanner</div><div class="card-back">Used to receive user input from the console.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Instance Method</div><div class="card-back">Operates on a specific object of a class.</div></div></div>
</div>
