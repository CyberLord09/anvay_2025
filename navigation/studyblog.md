---
layout: base
title: Study Blog
description: Study Blog
hide: true
---

{% include nav/blogs.html %}

# Tri 1 Summary Of My Learning

### Variables:

> A variable acts as a storage location for data, allowing a programmer to use and manipulate that data easily by referring to the variable name instead of the actual value.

### Data Abstraction:

> Data abstraction involves simplifying complex data structures by focusing only on the necessary details while underlying others. This allows programmers to work with data in a more efficient and understandable way, without needing to manage all the details of how the data is processed.

### Mathematical Expressions:

> Mathematical expressions are combinations of numbers, variables, and mathematical operators (such as +, -, *, or /) that produce a result when evaluated. In programming, these expressions are used to perform calculations, solve problems, and manipulate numerical data.

### Strings:

> A string is a sequence of characters used to represent text in programming. Strings can contain letters, numbers, and symbols, and are often used to store and manipulate textual data like words, sentences, or even entire paragraphs.

### Booleans:

> Booleans represent one of two possible values: true or false. In programming, boolean values are used to make decisions or control the flow of a program by evaluating conditions or expressions that result in a true or false outcome.

### Conditionals:

> Conditionals are statements in programming that allow decisions to be made based on whether a certain condition is true or false. If the condition is true, the program executes a specific block of code and if it is false, the program may execute a different block or skip the execution entirely.

### Nested Conditionals:

> Nested conditionals occur when one conditional statement is placed inside another. This allows for more complex decision-making processes, like evaluating multiple conditions. The program will first check the outer condition, and if it is true, it will then evaluate the inner condition.

### Iteration:

> Iteration is the process of repeatedly executing a block of code. This is typically done using loops, which allow a program to repeat a set of instructions a specified number of times or until a certain condition is met. 

### Lists:

> A list is a data structure that stores multiple values in a single variable. Lists can contain any type of data, including numbers, strings, or even other lists. They allow programmers to organize and manage collections of data, making it easier to access, modify, or iterate over the values stored within them.


---

## Big Idea 3: Algorithms and Programming

### Lesson 3.1: Variables and Assignment  
**Summary:**  
Variables are used to store data values that can change throughout the program. They help make programs flexible, readable, and efficient.

**Key Concepts:**

- Variables are created using the assignment operator `=`.
- A variable name should be descriptive (e.g., `score`, `temperature`) and follow naming conventions (no spaces, must start with a letter or underscore).
- Values assigned can be updated and reused.

**Example Code:**
```python
age = 16
print(age)  # Output: 16

age = age + 1
print(age)  # Output: 17
```

**Resources:**

- [W3Schools: Python Variables](https://www.w3schools.com/python/python_variables.asp)  
- [Python Naming Conventions (PEP8)](https://peps.python.org/pep-0008/#naming-conventions)

---

### Lesson 3.2: Data Types and Input  
**Summary:**  
Understanding data types allows you to handle and process user input correctly.

**Key Concepts:**

- Python’s common data types: `int` (integer), `float` (decimal), `str` (string), `bool` (true/false).
- The `input()` function takes input as a string by default.
- Use type casting (`int()`, `float()`, `str()`, `bool()`) to convert between types.

**Example Code:**
```python
name = input("Enter your name: ")
print("Hello, " + name)

age = int(input("Enter your age: "))
print("In 5 years you will be", age + 5)
```

**Resources:**

- [Python Data Types – GeeksForGeeks](https://www.geeksforgeeks.org/python-data-types/)  
- [Python Input and Output – W3Schools](https://www.w3schools.com/python/python_user_input.asp)

---

### Lesson 3.4: Operators and Expressions  
**Summary:**  
Operators are symbols that perform operations on variables and values. Expressions combine these to compute results.

**Key Concepts:**

- **Arithmetic Operators**: `+`, `-`, `*`, `/`, `//`, `%`, `**`
- **Comparison Operators**: `==`, `!=`, `<`, `>`, `<=`, `>=`
- **Logical Operators**: `and`, `or`, `not` — used in conditionals

**Example Code:**
```python
x = 10
y = 3

print(x % y)             # Output: 1
print(x > y and x < 20)  # Output: True
```

**Resources:**

- [Python Operators – Programiz](https://www.programiz.com/python-programming/operators)

---

### Lesson 3.6 – 3.8: Conditionals & If Statements  
**Summary:**  
Conditionals allow a program to choose between different paths of execution depending on whether a condition is true or false.

**Key Concepts:**

- `if`, `elif`, and `else` structure logic flow
- Conditions evaluate to a boolean (`True` or `False`)
- Nesting allows checking multiple conditions

**Example Code:**
```python
temp = 90

if temp > 100:
    print("Too hot!")
elif temp < 60:
    print("Too cold!")
else:
    print("Just right.")
```

**Resources:**

- [Python Conditionals – Real Python](https://realpython.com/python-conditional-statements/)  
- [Draw flowcharts for logic – diagrams.net](https://app.diagrams.net/)

---

### Lesson 3.10: Iteration  
**Summary:**  
Loops automate repetitive tasks, allowing code to execute multiple times based on a condition or over a sequence.

**Key Concepts:**

- `for` loops are used to iterate over sequences like lists or ranges.
- `while` loops run until a condition becomes false.
- Loops need exit conditions to avoid infinite repetition.

**Example Code:**
```python
# For loop
for i in range(5):
    print("Loop iteration", i)

# While loop
count = 0
while count < 5:
    print("Counting:", count)
    count += 1
```

**Resources:**

- [Python Loops – W3Schools](https://www.w3schools.com/python/python_for_loops.asp)

---

### Self Study: Functions  
**Summary:**  
Functions are reusable blocks of code that perform a specific task. They help make programs modular and organized.

**Key Concepts:**

- Define with `def` keyword
- Can accept parameters and return values
- Variables inside functions are local by default

**Example Code:**
```python
def greet(name):
    return "Hello, " + name

message = greet("Anvay")
print(message)  # Output: Hello, Anvay
```

**Resources:**

- [Python Functions – GeeksForGeeks](https://www.geeksforgeeks.org/python-functions/)  
- [Function Scope – Python Docs](https://docs.python.org/3/tutorial/classes.html#scopes-and-namespaces)


---

## Big Idea 5: Impact of Computing

---

### Lesson 5.1: Beneficial and Harmful Effects  
**Summary:**  
Computing innovations have transformed communication, education, business, and healthcare. However, these innovations can also cause harm when misused or implemented without considering ethical consequences.

**Key Concepts:**

- **Benefits**:
  - Automates repetitive tasks and increases productivity
  - Enhances communication (email, video calls, messaging)
  - Provides access to global information and learning
- **Harms**:
  - Algorithms may reflect and reinforce societal biases
  - Automation may displace workers and lead to job loss
  - Personal data may be tracked or exploited

**Example Scenario:**  
AI used in hiring may speed up decisions, but if trained on biased data, it might favor certain groups unfairly.

**Resources:**

- [CS50 AI Ethics Week](https://cs50.harvard.edu/ai/2020/weeks/1/)  
- [World Economic Forum: AI and the Future of Jobs](https://www.weforum.org/agenda/2020/10/future-of-jobs-report-2020/)

---

### Lesson 5.2: Digital Divide  
**Summary:**  
The digital divide describes the unequal access to computing technologies across different regions or socioeconomic groups. It affects education, job opportunities, and participation in a digital society.

**Key Concepts:**

- **Global Divide**: Countries without reliable internet or electricity
- **Local Divide**: Families lacking devices or stable Wi-Fi connections
- **Equity Initiatives**:
  - Public libraries and school laptop programs
  - Broadband expansion projects
  - Nonprofit and government efforts

**Example Scenario:**  
Students in rural or low-income areas may not have reliable access to online classes, causing them to fall behind academically.

**Resources:**

- [Pew Research: The Digital Divide](https://www.pewresearch.org/topic/internet-technology/digital-divide/)  
- [National Digital Inclusion Alliance](https://www.digitalinclusion.org/)

---

### Lesson 5.3: Bias in Computing  
**Summary:**  
Computing systems can unintentionally inherit bias from the data used to build them. This can lead to unfair treatment or discrimination in real-world applications.

**Key Concepts:**

- Biased training data can produce biased models
- Examples include facial recognition errors and loan denial algorithms
- Solutions include using diverse data, testing for fairness, and transparent design

**Example Scenario:**  
A healthcare AI tool recommends fewer services for certain populations due to a lack of representation in the training data.

**Resources:**

- [Algorithmic Justice League](https://www.ajl.org/)  
- [ProPublica: Machine Bias](https://www.propublica.org/article/machine-bias-risk-assessments-in-criminal-sentencing)

---

### Lesson 5.4: Crowdsourcing  
**Summary:**  
Crowdsourcing is the process of gathering information or work from a large group of people, typically via the internet. It allows large-scale collaboration, but it can also raise ethical concerns.

**Key Concepts:**

- Used in platforms like Wikipedia, reCAPTCHA, and Galaxy Zoo
- Helps with tasks too big for individuals or small teams
- Must balance usefulness with potential misuse (e.g., unpaid labor, misinformation)

**Example Scenario:**  
Users labeling images for a machine learning project may not realize their work is training an AI used for commercial profit.

**Resources:**

- [Zooniverse: Crowdsourced Science Projects](https://www.zooniverse.org/)  
- [reCAPTCHA and AI](https://www.google.com/recaptcha/about/)

---

### Lesson 5.5: Randomness  
**Summary:**  
Randomness is used in computing for simulations, games, and security. It adds unpredictability and mimics chance in programs.

**Key Concepts:**

- Used in simulations (e.g., predicting weather), games (e.g., dice rolls), and security (e.g., password generation)
- Python provides the `random` module for generating random values
- Computers use pseudorandom number generators (PRNGs)

**Example Code:**
```python
import random

print(random.randint(1, 6))  # Simulates a dice roll from 1 to 6
```

**Resources:**

- [Python Random Module – W3Schools](https://www.w3schools.com/python/ref_random.asp)

---

### Lesson 5.6: Legal and Ethical Concerns  
**Summary:**  
Technology is governed by laws that protect user rights and define ethical practices. Understanding these helps developers build responsible and legal computing systems.

**Key Concepts:**

- **Legal Protections**:
  - **GDPR**: Protects user data and requires consent in the EU
  - **DMCA**: Prevents illegal copying or distribution of digital content
  - **COPPA**: Protects children's privacy online
- **Ethical Practices**:
  - Do not collect unnecessary personal data
  - Respect intellectual property and give proper credit
  - Inform users how their data is used

**Example Scenario:**  
A company stores children’s data without parental consent, violating COPPA.

**Resources:**

- [GDPR Summary](https://gdpr-info.eu/)  
- [FTC COPPA Guide](https://www.ftc.gov/business-guidance/privacy-security/children-privacy)

---

### Lesson 5.7: Safe Computing  
**Summary:**  
Safe computing means protecting yourself, your device, and your data from digital threats. It involves using secure practices and staying alert.

**Key Concepts:**

- Use **strong passwords** and enable **two-factor authentication**
- Avoid clicking suspicious links or opening unknown attachments
- Install antivirus software and keep your system updated
- Backup important data regularly

**Checklist:**
- Use a password manager  
- Don't reuse the same password across accounts  
- Only download software from trusted sources  
- Lock your devices when not in use

**Resources:**

- [Google Safety Center](https://safety.google/)  
- [CISA: Online Safety Tips](https://www.cisa.gov/stay-safe-online)

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
.card:hover .card-inner {
  transform: rotateY(180deg);
}
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
.card-front {
  background: rgb(112, 105, 105);
  color: white;
}
.card-back {
  background: rgb(63, 76, 88);
  color: white;
  transform: rotateY(180deg);
}
</style>

<div class="card-grid">
  <div class="card"><div class="card-inner"><div class="card-front">Algorithm</div><div class="card-back">A finite set of instructions to accomplish a specific task.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Sequencing</div><div class="card-back">Steps executed in the order they appear.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Selection</div><div class="card-back">Code that runs based on a true/false condition.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Iteration</div><div class="card-back">Repeats a block of code using loops.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Variable</div><div class="card-back">An abstraction that stores a value.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Procedure</div><div class="card-back">Reusable group of instructions with optional parameters.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Modulus</div><div class="card-back">Returns the remainder of a division: <code>%</code>.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Boolean</div><div class="card-back">True or false value used in conditionals.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">List</div><div class="card-back">An ordered collection of elements.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">String</div><div class="card-back">A sequence of characters (e.g., text).</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">API</div><div class="card-back">Rules for how to use functions from a library.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Big O</div><div class="card-back">Describes algorithm efficiency (e.g., O(n), O(n²)).</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Undecidable</div><div class="card-back">Problem no algorithm can solve for all cases.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Binary Search</div><div class="card-back">Efficient search in a sorted list.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Metadata</div><div class="card-back">Data about data (e.g., image resolution).</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Phishing</div><div class="card-back">Tricking users into giving personal data.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Encryption</div><div class="card-back">Converts data to unreadable form for protection.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Machine Learning</div><div class="card-back">Systems that learn from data without explicit programming.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Bias</div><div class="card-back">A systematic error in data or outcomes.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Open Data</div><div class="card-back">Data freely available to the public.</div></div></div>
  <div class="card"><div class="card-inner"><div class="card-front">Citizen Science</div><div class="card-back">Public participation in scientific research.</div></div></div>
</div>


