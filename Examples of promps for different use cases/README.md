# **Prompts (Examples) for Different Use-Cases**

## **Overview**  
This repository provides a collection of prompt examples for various technical use cases, such as software development, debugging, API integrations, and automation. It covers different prompt types to help developers optimize their interactions with AI models for more accurate and useful results.

---

## **Types of Prompts and Examples**  

AI models can be prompted in various ways depending on the complexity of the task. Below are the primary types of prompting, explained with practical coding examples.

---

### **1. Zero-Shot Prompting (No Example Given)**  
In zero-shot prompting, the AI is asked to perform a task without being given any prior examples or context. It relies solely on its pre-trained knowledge to provide an answer.

**Example Prompt:**  
```plaintext
"Write a Python function to check if a number is prime."
```

**Expected Output:**  
```python
def is_prime(n):
    if n <= 1:
        return False
    for i in range(2, int(n**0.5) + 1):
        if n % i == 0:
            return False
    return True
```

**Use Case:**  
- When you need quick answers for well-known problems.  
- Suitable for factual or common programming tasks.  

---

### **2. One-Shot Prompting (One Example Given)**  
In one-shot prompting, a single example is provided to guide the AI in generating responses that follow the same pattern.

**Example Prompt:**  
```plaintext
"Example: The factorial of 5 is 120. Now, find the factorial of 7."
```

**Expected Output:**  
```plaintext
"The factorial of 7 is 5040."
```

**Use Case:**  
- When a specific format or style is required.  
- Helps AI align better with user expectations.  

---

### **3. Few-Shot Prompting (Multiple Examples Given)**  
Few-shot prompting provides multiple examples to help the AI understand the desired pattern and improve accuracy.

**Example Prompt:**  
```plaintext
"Example 1: 2 + 2 = 4  
Example 2: 3 + 5 = 8  
Now, solve: 6 + 7 = ?"
```

**Expected Output:**  
```plaintext
"6 + 7 = 13"
```

**Use Case:**  
- For tasks requiring consistent responses.  
- Useful for generating structured outputs or matching specific patterns.

---

### **4. Chain-of-Thought (CoT) Prompting (Step-by-Step Reasoning)**  
This type of prompting encourages the AI to break down a problem into logical steps to arrive at an accurate answer.

**Example Prompt:**  
```plaintext
"If a car travels at 60 km/h for 3 hours, how far does it travel? Let's think step by step."
```

**Expected Output:**  
```plaintext
"1. Speed = 60 km/h  
2. Time = 3 hours  
3. Distance = Speed × Time = 60 × 3  
4. Answer: 180 km"
```

**Use Case:**  
- For complex problems requiring intermediate steps.  
- Ideal for mathematical calculations and logical reasoning tasks.  

---

### **5. Instruction-Based Prompting (Detailed Guidelines Given)**  
In instruction-based prompting, the AI is given clear, step-by-step guidelines on how to complete a task.

**Example Prompt:**  
```plaintext
"Write a Python script to read a CSV file and display the first 5 rows. Ensure error handling for missing files."
```

**Expected Output:**  
```python
import pandas as pd

def read_csv_file(file_path):
    try:
        df = pd.read_csv(file_path)
        print(df.head())
    except FileNotFoundError:
        print("Error: File not found.")

read_csv_file("data.csv")
```

**Use Case:**  
- Useful for generating detailed outputs with clear structure.  
- Great for instructional or tutorial-based responses.

---

### **6. Contextual Prompting (Providing Background Information)**  
This involves providing relevant background information to help AI generate more tailored and accurate responses.

**Example Prompt:**  
```plaintext
"You are an experienced software engineer. Explain the concept of multithreading in Python in simple terms."
```

**Expected Output:**  
```plaintext
"Multithreading in Python allows multiple threads to run concurrently, helping perform tasks like I/O operations efficiently."
```

**Use Case:**  
- When the task requires domain-specific knowledge.  
- Useful for personalized responses and recommendations.

---

### **7. Prompt Chaining (Sequential Prompts)**  
Prompt chaining involves breaking down complex tasks into smaller, sequential prompts to get better results.

**Example Prompt (Step 1):**  
```plaintext
"List the top 3 web development frameworks."
```

**Step 1 Output:**  
```plaintext
"React, Angular, Vue"
```

**Example Prompt (Step 2):**  
```plaintext
"Explain why React is popular among developers."
```

**Expected Output:**  
```plaintext
"React is popular due to its component-based architecture, virtual DOM, and strong community support."
```

**Use Case:**  
- When dealing with multi-step workflows.  
- Helps build upon previous answers for deeper understanding.

---

## **Best Practices for Effective Prompting**  

To get the best results from AI, follow these prompting tips:

1. **Be Specific:**  
   - Clearly state the programming language or technology (e.g., "Write a Python function" instead of "Write a function").  

2. **Provide Context:**  
   - Give necessary background information to guide the AI.  

3. **Break Down Complex Requests:**  
   - Ask step-by-step instead of requesting everything at once.  

4. **Refine and Iterate:**  
   - If the response isn’t accurate, tweak your prompt and try again.  

---
Here's an updated version with additional examples for each type of prompt, specifically focusing on **code generation**, **error solving**, and other technical use cases.

---

# **Examples of Technical Prompts for Code Generation and Error Solving**

## **Overview**  
This document provides categorized examples of AI prompts for various technical use cases, including code generation, debugging, and optimization. The examples cover different prompting techniques to help you achieve better results from AI models.

---

## **Types of Prompts and Examples**  

### **1. Zero-Shot Prompting (No Example Given)**  
In zero-shot prompting, the AI generates output without any examples, relying solely on pre-trained knowledge.

#### **Code Generation Examples**  
**Prompt:**  
```plaintext
"Write a Python function to check if a string is a palindrome."
```

**Expected Output:**  
```python
def is_palindrome(s):
    s = s.lower().replace(" ", "")
    return s == s[::-1]
```

**Prompt:**  
```plaintext
"Create a basic HTML form with fields for name, email, and message."
```

**Expected Output:**  
```html
<form action="/submit" method="POST">
  <label>Name:</label>
  <input type="text" name="name" required>
  <label>Email:</label>
  <input type="email" name="email" required>
  <label>Message:</label>
  <textarea name="message" required></textarea>
  <button type="submit">Submit</button>
</form>
```

---

### **2. One-Shot Prompting (One Example Given)**  
In one-shot prompting, one example is provided to guide the AI in generating output.

#### **Code Generation Examples**  
**Prompt:**  
```plaintext
"Example: A function to calculate the square of a number:  
def square(num):  
    return num * num  
Now, write a function to calculate the cube of a number."
```

**Expected Output:**  
```python
def cube(num):
    return num * num * num
```

#### **Error Solving Example**  
**Prompt:**  
```plaintext
"Example: If code throws a 'division by zero' error, check for zero denominator.  
Now, fix this code: def divide(a, b): return a / b"
```

**Expected Output:**  
```python
def divide(a, b):
    if b == 0:
        return "Cannot divide by zero"
    return a / b
```

---

### **3. Few-Shot Prompting (Multiple Examples Given)**  
Few-shot prompting uses multiple examples to guide the AI.

#### **Code Generation Examples**  
**Prompt:**  
```plaintext
"Example 1: Reverse a string in Python:  
def reverse_string(s):  
    return s[::-1]  

Example 2: Convert a string to uppercase:  
def to_uppercase(s):  
    return s.upper()  

Now, write a function to convert a string to lowercase."
```

**Expected Output:**  
```python
def to_lowercase(s):
    return s.lower()
```

#### **Error Solving Example**  
**Prompt:**  
```plaintext
"Example 1: Handling index errors in a list:  
try:  
    value = my_list[5]  
except IndexError:  
    value = None  

Example 2: Fixing file read errors:  
try:  
    with open('file.txt', 'r') as f:  
        content = f.read()  
except FileNotFoundError:  
    content = 'File not found'  

Now, handle a key error in a dictionary."
```

**Expected Output:**  
```python
try:
    value = my_dict['key']
except KeyError:
    value = None
```

---

### **4. Chain-of-Thought (CoT) Prompting (Step-by-Step Reasoning)**  
Encourages AI to break down complex tasks into step-by-step solutions.

#### **Code Generation Example**  
**Prompt:**  
```plaintext
"Write a function to calculate the factorial of a number. Think step by step."
```

**Expected Output:**  
```plaintext
1. If the number is 0 or 1, return 1.  
2. Otherwise, multiply the number by the factorial of (number - 1).  
3. Use recursion to achieve this.
```

**Code Output:**  
```python
def factorial(n):
    if n == 0 or n == 1:
        return 1
    return n * factorial(n - 1)
```

---

### **5. Instruction-Based Prompting (Detailed Guidelines Given)**  
AI is provided with specific step-by-step instructions to generate responses.

#### **Code Generation Examples**  
**Prompt:**  
```plaintext
"Write a Python function that:  
1. Accepts a list of numbers.  
2. Removes duplicates.  
3. Sorts the list in ascending order.  
4. Returns the cleaned list."
```

**Expected Output:**  
```python
def clean_and_sort_list(numbers):
    unique_numbers = list(set(numbers))
    unique_numbers.sort()
    return unique_numbers
```

---

### **6. Contextual Prompting (Providing Background Information)**  
Relevant background information is given to help AI tailor responses.

#### **Code Generation Examples**  
**Prompt:**  
```plaintext
"You are an experienced Python developer. Write an optimized function to find the largest number in a list."
```

**Expected Output:**  
```python
def find_largest(nums):
    return max(nums)
```

#### **Error Solving Example**  
**Prompt:**  
```plaintext
"You are an expert in debugging. Suggest improvements to the following code for performance optimization."
```

**Code Input:**  
```python
for i in range(len(arr)):
    if arr[i] == target:
        print("Found")
```

**Expected Output:**  
```python
if target in arr:
    print("Found")
```

---

### **7. Prompt Chaining (Sequential Prompts)**  
Complex tasks are broken down into multiple, linked prompts.

#### **Example of Step-by-Step Chaining:**  
**Prompt 1:**  
```plaintext
"List three sorting algorithms used in Python."
```

**Response:**  
```plaintext
"Bubble Sort, Merge Sort, Quick Sort."
```

**Prompt 2 (using previous answer):**  
```plaintext
"Explain how Quick Sort works with code example."
```

**Expected Output:**  
```python
def quick_sort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quick_sort(left) + middle + quick_sort(right)
```

---

## **Best Practices for Effective Prompting**  

- **Be Clear and Specific:** Provide detailed instructions to improve AI understanding.  
- **Iterate and Refine:** Adjust prompts based on output quality.  
- **Use Examples:** Guide AI with sample data or patterns.  
- **Break Complex Problems:** Split large tasks into smaller, manageable prompts.  

---

## **Conclusion**  
Using the right type of prompt can significantly improve the accuracy and usefulness of AI-generated code and debugging solutions. Experiment with different styles to achieve the best results.

---

Let me know if you need additional examples or explanations!