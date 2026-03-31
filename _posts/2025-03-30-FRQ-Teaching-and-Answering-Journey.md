---
layout: post
title: "Teaching and Answering FRQs: My Journey Through AP CSA Problem Solving"
description: "Reflecting on teaching the 2017 Phrase FRQ and how FRQ practice shaped my understanding of CS 113 requirements"
categories: [CSA, FRQ, Reflection]
permalink: /csa/frq-teaching-journey/
---

## Introduction: The Value of FRQs

Free Response Questions (FRQs) on the AP Computer Science A exam are more than just evaluation tools—they're comprehensive problem-solving exercises that force you to think deeply about code design, algorithm implementation, and real-world applications. Over the past few months, I've both *answered* multiple FRQs as part of my learning journey and recently begun *teaching* them to others. This dual experience has fundamentally changed how I approach Java programming and understand the competencies required for college-level CS work.

This blog post reflects on:
- The Phrase FRQ (2017 Question 3) that I taught
- How different FRQs built my understanding across multiple domains
- The direct connection between FRQ practice and CS 113 course requirements
- Key lessons learned from both teaching and answering FRQs

---

## Part 1: Teaching the 2017 Phrase FRQ

### The Problem: String Processing and Method Reuse

The Phrase FRQ presents a deceptively simple-sounding problem: work with a string-based `Phrase` class to implement two methods that manipulate and search for substring occurrences. However, this problem actually tests several critical programming concepts:

1. **Method dependency** - Understanding how to properly use a provided helper method
2. **String manipulation** - Using `substring()` correctly to split and reconstruct strings
3. **Loop design** - Building algorithms that iterate to find patterns
4. **Index arithmetic** - Managing precise calculations with string positions
5. **Edge case handling** - Ensuring robustness when occurrences don't exist

### Part A: replaceNthOccurrence

The first method asks students to replace the nth occurrence of a substring with another string. The key insight is that this problem can be solved in three steps:

```java
public void replaceNthOccurrence(String str, int n, String repl) {
    int index = findNthOccurrence(str, n);
    if (index != -1) {
        currentPhrase = currentPhrase.substring(0, index) + repl +
                        currentPhrase.substring(index + str.length());
    }
}
```

**Why this works:**
- Use the provided helper method rather than reinventing the search logic
- Check for -1 (occurrence doesn't exist) before attempting manipulation
- Reconstruct the string in three parts: [before] + [replacement] + [after]
- The critical detail: skip `str.length()` characters, not `repl.length()`

**Teaching insight:** Students often struggle with the index arithmetic. I had to emphasize that after finding the occurrence, you need to skip over the *original* substring length, regardless of how long the replacement is. This is a subtle but essential detail.

### Part B: findLastOccurrence

The second method challenges students to find the position of the *last* occurrence of a substring. There's no convenient built-in method for this, so students must implement a loop that calls the helper method repeatedly:

```java
public int findLastOccurrence(String str) {
    int occurrence = 1;
    int lastIndex = -1;
    
    while (true) {
        int index = findNthOccurrence(str, occurrence);
        if (index == -1) {
            return lastIndex;
        }
        lastIndex = index;
        occurrence++;
    }
}
```

**Why this approach works:**
- Incrementally search for the 1st, 2nd, 3rd, ... occurrences
- When `findNthOccurrence` returns -1, you know the previous index was the last
- Automatically handles cases where no occurrences exist (returns -1 on first iteration)

**Teaching insight:** This problem beautifully demonstrates how a single helper method can be leveraged in creative ways. Students must understand that repeatedly calling the same method with different parameters can solve a different problem entirely. This kind of algorithmic thinking is fundamental to CS.

### Key Scoring Points

**Part A (4 points):**
- 1 point: Correctly call findNthOccurrence
- 1 point: Check if the result is valid (not -1)
- 2 points: Properly construct the new string using substring

**Part B (5 points):**
- 2 points: Call findNthOccurrence multiple times in a loop
- 1 point: Continue looping while occurrences are found
- 1 point: Track the last valid occurrence found
- 1 point: Return the correct value or -1

The scoring structure reveals what the exam makers value: demonstrating understanding of method reuse, conditional logic, loop design, and string reconstruction.

---

## Part 2: How Other FRQs Built My Understanding

Beyond just teaching one FRQ, I've worked through several others as homework. Each one built different skills that are essential for the Phrase FRQ and beyond.

### FRQ #1: Bird Feeder Simulation (2024)

**What it taught:** Simulation logic and state management

The bird feeder problem required tracking the food level in a feeder as birds visited and (rarely) a bear emptied it. This taught me:

- **Conditional logic** - Determining normal vs. abnormal days
- **Random number generation** - Modeling unpredictable real-world events
- **State tracking** - Maintaining a variable (food level) that must remain valid across multiple method calls
- **Loop control** - Deciding when to end a simulation based on conditions

This FRQ directly connects to Part B of the Phrase FRQ in that both require looping and counting. The bird feeder taught me how loops can control simulations, while the Phrase FRQ showed how loops can search for patterns.

### FRQ #4: LightBoard (2019)

**What it taught:** 2D array traversal and column-based logic

The LightBoard problem required:

- **2D array initialization** - Creating a grid where each cell has specific properties
- **Column traversal** - Fixing one index while iterating the other
- **Modulus operations** - Checking evenness and divisibility
- **Rule-based logic** - Applying different return values based on conditions

The key insight from this FRQ was understanding that 2D arrays require careful index management. When traversing a column, you fix the column index and vary the row index.

**Connection to Phrase:** While the Phrase FRQ works with 1D strings, the principles of index management and logical rule application are similar. Both require precise understanding of how to access and manipulate data structures.

### FRQ Digits: Constructor & List Traversal

**What it taught:** ArrayList manipulation and digit extraction

This problem required:

- **ArrayList operations** - Adding elements at specific positions
- **Integer arithmetic** - Using modulus (%) and division (/) to extract digits
- **Element comparison** - Comparing adjacent elements in a list
- **Edge case handling** - Dealing with zero and single-digit numbers

The Digits FRQ taught me that how you construct data (the order in which you add items to a list) affects how you can later process it. This principle of thoughtful data construction appears throughout programming.

**Direct connection to Phrase:** Both problems work with sequences of elements and require processing them in order. The Phrase FRQ processes substrings; the Digits FRQ processes digit lists. The algorithmic thinking is similar.

### FRQ WordChecker: String Analysis

**What it taught:** Working with ArrayList<String> and complex string methods

This problem involved:

- **String method distinction** - Understanding the differences between `contains()`, `startsWith()`, and `substring()`
- **Adjacent element comparison** - A pattern that appears frequently in FRQs
- **Filtering and transformation** - Creating new collections based on conditions
- **Order preservation** - Maintaining sequence when creating new data structures

**Connection to Phrase:** The WordChecker FRQ showed me how string methods could be used to analyze patterns. The Phrase FRQ goes deeper by requiring string *manipulation* using substring operations, not just analysis.

### FRQ Successors: 2D Arrays and Method Reuse

**What it taught:** Using helper methods effectively and maintaining data structure relationships

This problem required:

- **2D array creation** - Constructing new arrays with specific dimensions
- **Helper method design** - One method (`findPosition`) supporting another
- **Object creation** - Using Position objects to represent results
- **Null handling** - Representing cases where data doesn't exist

**Connection to Phrase:** The Successors FRQ brilliantly demonstrates the power of method reuse. The `getSuccessorArray` method works by repeatedly calling `findPosition`. This is exactly what the Phrase FRQ Part B does—repeatedly call `findNthOccurrence` to solve a different problem.

---

## Part 3: How FRQs Align with CS 113 Requirements

The college course CS 113 requires competency across several domains. Let me map how FRQ practice directly builds these competencies:

### Data Structures

| Competency | FRQs That Build It | Why It Matters |
|---|---|---|
| **Collections (ArrayList, HashMap)** | WordChecker, Digits | Both use ArrayLists to store sequences of data |
| **Lists (add, remove, search, iterate)** | Digits, WordChecker | Repeatedly add, iterate, and search through collections |
| **Stacks/Queues** | Bird Feeder | The simulation concept extends to undo/redo stacks |
| **Sets** | Not directly, but concepts apply | Phrase FRQ could use Sets to track found positions |
| **Graphs** | Not covered in these FRQs | Would require more complex relationship modeling |

### Algorithms

| Competency | FRQs That Build It | Why It Matters |
|---|---|---|
| **Searching** | Phrase (both parts), LightBoard, WordChecker | Finding specific values or patterns in data |
| **Sorting** | Not directly tested, but comparison logic applies | Comparing elements (even if not sorting them) |
| **Hashing** | Not directly, but String operations use hashing | String manipulation relies on hash-based operations |
| **Algorithm Analysis** | All FRQs | Must analyze time complexity of helper methods |

### Object-Oriented Design

Every single FRQ tested these principles:

| Principle | Application |
|---|---|
| **Abstraction** | Each FRQ provides a class (Phrase, LightBoard, etc.) hiding implementation details |
| **Encapsulation** | Private instance variables like `currentPhrase` are modified only through methods |
| **Method Design** | Each method has a single responsibility; Part A and Part B of FRQs separate concerns |
| **Reusability** | Helper methods like `findNthOccurrence` are designed to be reused |

### Software Development Practices

| Practice | FRQs That Build It |
|---|---|
| **Testing** | Thinking through edge cases (zero in Digits, missing occurrence in Phrase) |
| **Debugging** | Understanding how methods interact and tracing execution |
| **Code Comments** | Explaining algorithm choices in my reflection documents |
| **Clear Variable Names** | Using names like `lastIndex`, `occurrence`, `index` clarifies intent |

---

## Part 4: Key Lessons from Teaching vs. Solving FRQs

### Lesson 1: Precision in Problem Interpretation

When I *solved* FRQs, I focused on getting the right answer. When I *taught* the Phrase FRQ, I realized that wording precision matters enormously:

- "Replace the *nth* occurrence" - emphasizes that we're looking for a *specific* instance
- "The last occurrence" - requires a different algorithm than "the first occurrence"
- "If the nth occurrence does not exist, currentPhrase remains unchanged" - prevents off-by-one errors

Teaching forced me to articulate *why* each word matters, not just what the code does.

### Lesson 2: Method Reuse as a Design Pattern

The Phrase FRQ teaches a subtle but powerful lesson: **good helper methods enable creative problem-solving**.

In Part A, `findNthOccurrence` is used straightforwardly to locate where to replace.
In Part B, the same method is called repeatedly with incrementing parameters to solve a completely different problem.

This is the essence of algorithmic thinking: recognizing that existing tools can be repurposed in unexpected ways.

### Lesson 3: Edge Cases Reveal Deeper Understanding

Teaching forced me to think about edge cases that I might have glossed over:

- What if n is 0 or negative?
- What if the string is empty?
- What if we're replacing with an empty string?
- What if the phrase only has one word?

These cases separate students who memorized a solution from those who truly understand the algorithm.

### Lesson 4: Loop Design is Harder Than It Looks

The loops in Part B of the Phrase FRQ look simple:

```java
while (true) {
    int index = findNthOccurrence(str, occurrence);
    if (index == -1) return lastIndex;
    lastIndex = index;
    occurrence++;
}
```

But designing this from scratch requires understanding:
- Why we need a `lastIndex` variable
- Why we check for -1 *before* updating lastIndex
- Why we increment `occurrence` at the end
- Why the loop will eventually terminate

Teaching these details revealed that students often copy loop patterns without understanding the logic flow.

### Lesson 5: Comments Matter More Than I Thought

When listing the scored requirements for Parts A and B earlier in this blog, I realized that understanding the *scoring rubric* is itself helpful. Each point in the rubric corresponds to a specific concept: calling the method (1), checking the return value (1), using substrings (2), etc.

Good documentation breaks problems into these exact pieces, making both teaching and solving easier.

---

## Part 5: How This Experience Shapes My CS 113 Capstone Project

Understanding FRQs deeply will help my capstone project in several ways:

### 1. Data Structure Choices
FRQs taught me that **choosing the right data structure is half the battle**. Using an ArrayList vs. a simple array, choosing to track state with instance variables, and organizing data efficiently all directly apply to capstone design.

### 2. Method Design
I now understand that **smaller, focused methods are better than large methods that do everything**. The Phrase FRQ shows this: Part A and Part B are separate methods, and both rely on a helper. This same principle will guide my capstone architecture.

### 3. Algorithm Analysis
Every FRQ I solved taught me to think about **time and space complexity**. The Phrase FRQ's Part B actually calls `findNthOccurrence` multiple times. Understanding this is O(n*m) behavior (where m is the number of occurrences) is part of good algorithm analysis.

### 4. Edge Case Handling
The hours I spent thinking about edge cases in FRQs directly transfer to building a robust capstone project. Real users will find the edge cases I didn't anticipate.

### 5. Code Comments and Documentation
FRQs taught me that **clarity of intent matters**. My capstone code will benefit from JavaDoc comments and clear variable names, lessons learned from teaching FRQs.

---

## Part 6: Reflections on Teaching

Teaching the Phrase FRQ was profoundly different from solving it. Some observations:

- **Teaching forces precision.** I couldn't wave my hand and say "then you search for the occurrence." I had to explain *how* the search works, *why* we check for -1, and *what* happens if it's not found.

- **Teaching reveals gaps.** When a student asked, "Why do we increment by 1 and not by `str.length()`?" I had to think deeply about the answer. (Answer: because we want to find *all* occurrences, including overlapping ones. A simple but important detail.)

- **Teaching is humbling.** I realized that problems I thought I fully understood still had depths I hadn't explored. The interaction between methods, the precise ordering of operations in a loop, the subtle differences between similar string methods—all became clearer when explaining to others.

- **Teaching reinforces learning.** By preparing to teach the Phrase FRQ, I learned it better than I learned any of the FRQs I simply solved for homework.

---

## Conclusion: The FRQ Journey Continues

FRQs are far more than exam questions. They're carefully designed problems that build fundamental CS competencies:

- **Data structures**: How to organize information effectively
- **Algorithms**: How to solve problems systematically
- **OOP principles**: How to design classes and methods that work together
- **Problem-solving**: How to break complex tasks into manageable pieces

By both solving FRQs and teaching them, I've developed a deeper appreciation for algorithmic thinking and software design. This experience directly prepares me for the CS 113 capstone project, where I'll need to apply these principles to a larger, more complex system.

The journey from student to teacher-of-algorithms is just beginning, but FRQs have been invaluable guides along the way.

---

## Appendix: Key FRQ Patterns to Remember

As I continue through CS work, these patterns from my FRQ practice will serve me well:

| Pattern | Example | Use Case |
|---|---|---|
| **Compare adjacent elements** | WordChecker and Digits | Many problems require checking pairs |
| **Loop until a condition** | Phrase Part B | Searching for the last of something |
| **Track state across iterations** | Bird Feeder | Simulations and accumulations |
| **Reconstruct data** | Phrase Part A | String manipulation and data transformation |
| **Use helper methods creatively** | Phrase Part B | Method reuse in unexpected ways |
| **Handle -1 returns** | Phrase both parts | Many search methods return -1 for "not found" |
| **Preserve order** | WordChecker | Data structures that maintain sequence matter |

---

**References:**
- [AP Computer Science A FRQ Archive](https://apcentral.collegeboard.org/courses/ap-computer-science-a)
- CS 113 Course Alignment Rubric
- Personal FRQ reflections from homework assignments
- Teaching notes for 2017 Question 3 (Phrase FRQ)
