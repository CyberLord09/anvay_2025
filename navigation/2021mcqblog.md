---
layout: post 
search_exclude: true
show_reading_time: false
permalink: /anvaymcqblog2
title: Anvay's MCQ Blog - Practice Exam 2
categories: [Anvay Final Retrospective]
comments: true
---

## Overview

![Image](https://github.com/user-attachments/assets/871d1bff-5a7c-4c8b-a956-91ad3aea45e6)

I recently completed another AP Computer Science Principles MCQ practice exam. I answered **60/70** questions correctly, showing continued strength in algorithms, programming logic, and computing ethics. This time, I noticed a few key areas where improvement is needed, especially in abstract concepts like digital representation, floating-point numbers, and algorithmic limitations. Below is a full performance breakdown and analysis of the questions I missed.

---

## Performance Breakdown

### **Big Idea Analysis**

![Image](https://github.com/user-attachments/assets/c4b80884-f005-4bf0-bffe-47303b64e4a2)

| **Big Idea**                      | **Number of Questions** | **Average Performance %** |
|----------------------------------|--------------------------|---------------------------|
| AAP: Algorithms and Programming  | 24                       | 83%                       |
| CRD: Creative Development        | 7                        | 57%                       |
| CSN: Computing Systems and Networks | 9                     | 89%                       |
| DAT: Data                        | 14                       | 86%                       |
| IOC: Impact of Computing         | 16                       | 100%                      |

---

### **Practice Area Performance**

![Image](https://github.com/user-attachments/assets/22491b8c-679c-4039-ae61-fce0efcc61c4)

| **Practice**                                                        | **Number of Questions** | **Average Performance %** |
|----------------------------------------------------------------------|--------------------------|---------------------------|
| Practice 1: Design and evaluate computational solutions for a purpose. | 17                     | 82%                       |
| Practice 2: Develop and implement algorithms.                        | 17                       | 94%                       |
| Practice 3: Develop programs that incorporate abstractions.          | 6                        | 50%                       |
| Practice 4: Evaluate and test algorithms and programs.               | 8                        | 75%                       |
| Practice 5: Investigate computing innovations.                       | 22                       | 95%                       |

---

### **Skill-Based Performance**

![Image](https://github.com/user-attachments/assets/50f61e3d-9a62-41a5-bd45-992c03ed6e44)

| **Skill**                                                          | **Number of Questions** | **Average Performance %** |
|--------------------------------------------------------------------|--------------------------|---------------------------|
| Skill 1.A: Investigate the situation, context, or task.            | 1                        | 0%                        |
| Skill 1.B: Determine and design an appropriate method or approach. | 1                        | 100%                      |
| Skill 1.C: Explain how collaboration affects the development.       | 3                        | 100%                      |
| Skill 1.D: Evaluate solution options.                               | 12                       | 83%                       |
| Skill 2.A: Represent algorithmic processes w/o programming language.| 4                        | 100%                      |
| Skill 2.B: Implement and apply an algorithm.                        | 13                       | 92%                       |
| Skill 3.A: Generalize data sources through variables.               | 2                        | 50%                       |
| Skill 3.B: Use abstraction to manage complexity.                    | 3                        | 67%                       |
| Skill 3.C: Explain how abstraction manages complexity.              | 1                        | 0%                        |
| Skill 4.B: Determine the result of code segments.                   | 5                        | 100%                      |
| Skill 4.C: Identify and correct errors in programs.                 | 3                        | 33%                       |
| Skill 5.A: Explain how computing systems work.                      | 4                        | 75%                       |
| Skill 5.B: Explain how knowledge can be generated from data.        | 4                        | 100%                      |
| Skill 5.C: Describe the impact of a computing innovation.           | 3                        | 100%                      |
| Skill 5.D: Describe the impact of gathering data.                   | 2                        | 100%                      |
| Skill 5.E: Evaluate legal and ethical use of computing.             | 9                        | 100%                      |

---

## Questions I Got Wrong: Analysis and Improvement

---

### **1. How is analog audio represented by a computer?**

**Question:**  
Which of the following best explains how an analog audio signal is typically represented by a computer?

**Options:**
- **A.** An analog audio signal is measured as input parameters to a program or procedure. The inputs are represented at the lowest level as a collection of variables.  
- **B.** An analog audio signal is measured at regular intervals. Each measurement is stored as a sample, which is represented at the lowest level as a sequence of bits.  
- **C.** An analog audio signal is measured as a sequence of operations that describe how the sound can be reproduced. The operations are represented at the lowest level as programming instructions.  
- **D.** An analog audio signal is measured as text that describes the attributes of the sound. The text is represented at the lowest level as a string.  

**My Answer:** C  
**Correct Answer:** B  

**Why I Got It Wrong:**  
I confused how sound is *used* in code with how it's *stored*. Audio signals are sampled — not coded as operations — and then digitally stored as bits.

**How I Can Improve:**  
Review Unit 2 on **data representation**, especially how analog-to-digital conversion works.

---

### **2. Which statement about the Internet is true?**

**Question:**  
Which of the following statements about the Internet is true?

**Options:**
- **A.** The Internet is a computer network that uses proprietary communication protocols.  
- **B.** The Internet is designed to scale to support an increasing number of users.  
- **C.** The Internet requires all communications to use encryption protocols.  
- **D.** The Internet uses a centralized system to determine how packets are routed.  

**My Answer:** D  
**Correct Answer:** B  

**Why I Got It Wrong:**  
I misunderstood how Internet routing works — it’s not centralized. The Internet is designed to scale using **decentralized, fault-tolerant protocols**.

**How I Can Improve:**  
Re-study **packet switching and routing** from Unit 4.1 to understand how the Internet handles traffic dynamically.

---

### **3. Why are floating-point values imprecise?**

**Question:**  
A program developed for a Web store represents customer account balances using a format that approximates real numbers. While testing the program, a software developer discovers that some values appear to be mathematically imprecise.  
Which of the following is the most likely cause of the imprecision?

**Options:**
- **A.** The account balances are represented using a fixed number of bits, resulting in overflow errors.  
- **B.** The account balances are represented using a fixed number of bits, resulting in round-off errors.  
- **C.** The account balances are represented using an unlimited number of bits, resulting in overflow errors.  
- **D.** The account balances are represented using an unlimited number of bits, resulting in round-off errors.  

**My Answer:** C  
**Correct Answer:** B  

**Why I Got It Wrong:**  
I misunderstood how many bits are used in floating-point storage. It’s not unlimited — and **fixed-size binary approximations** lead to round-off, not overflow.

**How I Can Improve:**  
Review **floating-point number limitations** in Unit 2 and practice identifying **rounding vs. overflow errors**.

---

### **4. Can all problems be solved algorithmically?**

**Question:**  
Which of the following best explains the ability to solve problems algorithmically?

**Options:**
- **A.** Any problem can be solved algorithmically, though some algorithmic solutions may require humans to validate the results.  
- **B.** Any problem can be solved algorithmically, though some algorithmic solutions must be executed on multiple devices in parallel.  
- **C.** Any problem can be solved algorithmically, though some algorithmic solutions require a very large amount of data storage to execute.  
- **D.** There exist some problems that cannot be solved algorithmically using any computer.  

**My Answer:** A  
**Correct Answer:** D  

**Why I Got It Wrong:**  
I didn’t consider **undecidable problems** like the **Halting Problem**, which cannot be solved algorithmically.

**How I Can Improve:**  
Study Unit 3.18 on **undecidability** and understand the limits of what computers can solve.

---

### **5. Binary Search Element Count**

**Question:**  
A sorted list of numbers contains 128 elements. Which of the following is closest to the maximum number of list elements that can be examined when performing a binary search for a value in the list?

**Options:**
- **A.** 2  
- **B.** 8  
- **C.** 64  
- **D.** 128  

**My Answer:** C  
**Correct Answer:** B  

**Why I Got It Wrong:**  
I misunderstood the question. Binary search doesn’t examine 64 items — it takes up to **log₂(128) = 7** checks.

**How I Can Improve:**  
Practice **logarithmic reasoning** and remember that each binary search step halves the remaining list.

---

## Final Reflection & Next Steps

### **Strengths:**
- Scored 100% in ethics, computing impact, and most algorithm segments  
- Strong list and loop logic (Iteration, Boolean expressions)  
- Demonstrated clear understanding of how programs use data  

### **Areas for Improvement:**
- Better conceptual understanding of **binary search and logarithmic complexity**  
- Strengthen knowledge of **undecidable problems** and limits of algorithms  
- Solidify understanding of **how numbers and signals are stored** digitally  

### **Action Plan:**
- Rewatch videos on **algorithm efficiency and undecidable problems**  
- Practice **data representation** with sound, floats, and binary  
- Do more **binary search** questions and study log₂(n) logic

---

## Final Thoughts
This exam helped me recognize blind spots in deeper computing theory. While I’m proud of my strengths, focusing on precision in binary math, routing systems, and problem-solving limits will push my scores even higher.

