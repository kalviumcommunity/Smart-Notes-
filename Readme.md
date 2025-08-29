# Smart Notes – AI Summarizer
Smart Notes is a lightweight web app that helps you summarize long texts, extract key points, and generate quizzes using AI.  
Paste your notes, articles, or transcripts – and let AI do the hard work.
---
## Features
- Summarize long paragraphs into clear, concise text  
- Extract key points in bullet form  
- Generate quiz-style questions from your notes  
- Save summaries for later (optional)  
- Simple and clean web interface  
---
## Tech Stack
- Frontend: React + Tailwind (or plain HTML/JS)  
- Backend: Python (Flask / FastAPI) or Node.js  
- AI Engine: OpenAI GPT API (GPT-4o-mini or GPT-3.5-turbo)  
- Database (optional): SQLite / Firebase  

---

## 🧠 Zero-Shot Prompting

## 🔹 What is Zero-Shot Prompting?

**Zero-shot prompting** means giving an AI model (like GPT) a **task without providing any examples** beforehand.  
You only describe what you want in natural language, and the model uses its pretraining knowledge to respond correctly.  

👉 In short: **“Do this task, even though I haven’t shown you any examples.”**

---

## 🔹 Why "Zero-Shot"?

The name comes from ML terminology:

- **Few-shot learning** → Provide a few examples before asking the model to generalize.  
- **Zero-shot learning** → No examples, just instructions.

---

##  System Prompt  
You are an AI Learning Assistant. Your role is to take user-provided text (notes, articles, transcripts) and:  
- Summarize long passages into concise explanations  
- Extract key points in bullet form  
- Generate quiz-style questions for active recall  
- Provide outputs in a clean, structured format  

##  User Prompt  
“Summarize the following text, extract the main points, and generate 3 quiz questions.”  

---

## RTFC Framework Usage

- **R (Role):** AI assistant that summarizes, extracts, and quizzes from input text.  
- **T (Task):** Build Smart Notes through iterative AI integration milestones.  
- **F (Format):** Output should be structured (summary, key points, quiz).  
- **C (Context):** User provides raw text (notes, articles, transcripts).  

---

### 🔹 One-Shot Prompt  

**System Prompt:**  
You are an AI code reviewer. Analyze the given code, detect bugs, and suggest improvements.  
Always return results in JSON format with three fields: `issues`, `suggestions`, and `overall_feedback`.  

---

**User Prompt (with one example):**  

Example Input (Python):  
```python
def divide(a, b):
    return a * b  # intended to be division

{
  "issues": ["The operator used is multiplication instead of division."],
  "suggestions": ["Replace '*' with '/' to correctly divide the numbers."],
  "overall_feedback": "Logic error detected in the function implementation."
}

public int Subtract(int a, int b) {
    return a + b; // intended to be subtraction
}

Why One-Shot Prompting?

-Provides one guiding example to set the response pattern.
-Ensures the AI generates consistent, structured outputs.
-Reduces ambiguity compared to zero-shot prompting.

## 🎯 Multi-Shot Prompting  

In CodeSage, we apply **Multi-Shot Prompting**, where the AI is provided with **multiple examples** before being asked to solve the real task.  
This method ensures the AI clearly understands the **pattern, structure, and expectations** of the output.  

### 🔹 Multi-Shot Prompt  

**System Prompt:**  
You are an AI code reviewer. Analyze the given code, detect bugs, and suggest improvements.  
Always return results in JSON format with three fields: `issues`, `suggestions`, and `overall_feedback`.  

**User Prompt (with multiple examples):**  

Example 1 (Python):  
```python
def add(a, b):
    return a - b  # intended to be addition
````

Expected Output:

```json
{
  "issues": ["The operator used is subtraction instead of addition."],
  "suggestions": ["Replace '-' with '+' to correctly add the numbers."],
  "overall_feedback": "Logic error detected in the addition function."
}
```

Example 2 (JavaScript):

```javascript
function square(n) {
    return n + n; // intended to be square
}
```

Expected Output:

```json
{
  "issues": ["The function doubles the number instead of squaring it."],
  "suggestions": ["Replace 'n + n' with 'n * n' to correctly square the number."],
  "overall_feedback": "Incorrect mathematical operation for squaring."
}
```

Now review the following C++ code:

```cpp
int multiply(int a, int b) {
    return a - b; // intended to be multiplication
}
```

### 📌 Why Multi-Shot Prompting?

* Gives the AI **multiple reference patterns** to ensure consistent results.
* Helps in **complex tasks** where one example isn’t enough.
* Reduces errors and improves **accuracy of code reviews**.

##  Dynamic Prompting  

In CodeSage, we use **Dynamic Prompting**, where the prompt is automatically adapted based on the **user’s input context** (e.g., programming language, code style, or desired output format).  
This makes the system **flexible and personalized**, instead of relying on fixed instructions.  

---

### 🔹 Dynamic Prompt Example  

**System Prompt (Template):**  
You are an AI code reviewer. Analyze the given code in **{{language}}**, detect bugs, and suggest improvements.  
Always return results in JSON format with three fields: `issues`, `suggestions`, and `overall_feedback`.  

---

**User Prompt (Generated Dynamically):**  
Review the following **{{language}}** code:  

```{{language}}
{{code_snippet}}

### Example Execution

If the user provides **Python code**:
def divide(a, b):
    return a * b  # intended to be division



The dynamically generated prompt becomes:

```text

You are an AI code reviewer. Analyze the given code in Python, detect bugs, and suggest improvements.
Always return results in JSON format with three fields: issues, suggestions, and overall_feedback.

Review the following Python code:
def divide(a, b):
    return a * b  # intended to be division
```

Expected Output:

```json
{
  "issues": ["The function multiplies instead of dividing."],
  "suggestions": ["Replace '*' with '/' to correctly perform division."],
  "overall_feedback": "Incorrect operator used for division."
}
```

###  Why Dynamic Prompting?

* Automatically adapts prompts to **any programming language**.
* Makes the system more **scalable and user-specific**.
* Reduces manual work while ensuring **consistent structured outputs**.


## 🎯 Chain-of-Thought Prompting  

In CodeSage, we apply **Chain-of-Thought (CoT) Prompting**, where the AI is encouraged to **reason step by step** before providing the final answer.  
This helps the system explain *why* a piece of code is incorrect, not just point out the issue.  

### 🔹 Chain-of-Thought Prompt  

**System Prompt:**  
You are an AI code reviewer. Analyze the given code step by step (reasoning internally), then provide your final answer only in JSON format with three fields: `issues`, `suggestions`, and `overall_feedback`. Do not reveal the reasoning steps to the user.  

**User Prompt:**  
Review the following Python code:  

```python
def is_even(n):
    if n % 2 == 1:
        return True
    return False
````

### 🔹 Expected Reasoning (hidden to user)

1. The function is meant to check if a number is even.
2. Current condition checks `n % 2 == 1`, which actually detects **odd numbers**.
3. The return values are inverted.
4. Correct logic should be `n % 2 == 0`.

### 🔹 Final Output (shown to user)

```json
{
  "issues": ["The condition checks for odd numbers instead of even."],
  "suggestions": ["Change condition to 'n % 2 == 0' for even check."],
  "overall_feedback": "The function incorrectly identifies odd numbers as even."
}
```

###  Why Chain-of-Thought Prompting?

* Ensures **deeper reasoning** behind feedback.
* Reduces **false positives/negatives** in bug detection.
* Provides **explainable AI** code reviews with accurate fixes.

## 🧪 Evaluation Dataset & Testing Framework  

To ensure **CodeSage** works reliably, we created an **evaluation pipeline** with:  
- A dataset of **5+ sample code snippets**  
- A **judge prompt** to compare AI output with expected results  
- A lightweight **testing framework** to run all cases  

---

### 📂 Evaluation Dataset (5 Samples)  

```json
[
  {
    "id": 1,
    "language": "Python",
    "code": "def add(a, b): return a - b",
    "expected": "Bug: subtraction instead of addition"
  },
  {
    "id": 2,
    "language": "JavaScript",
    "code": "function isPositive(n) { return n < 0; }",
    "expected": "Bug: returns true for negative numbers"
  },
  {
    "id": 3,
    "language": "Java",
    "code": "boolean isEven(int n) { return n % 2 == 1; }",
    "expected": "Bug: detects odd numbers instead of even"
  },
  {
    "id": 4,
    "language": "C++",
    "code": "int divide(int a, int b) { return a / b; }",
    "expected": "Edge Case: No handling of division by zero"
  },
  {
    "id": 5,
    "language": "Python",
    "code": "def factorial(n): return n * factorial(n-1)",
    "expected": "Bug: No base case, leads to infinite recursion"
  }
]
````

---

### 🧑‍⚖️ Judge Prompt

```text
You are a judge. Compare the model's output with the expected result.  
Evaluation Parameters:  
1. **Correctness** – Did the model identify the main bug?  
2. **Completeness** – Did it also suggest a meaningful fix?  
3. **Format** – Is the response in the required JSON structure?  
4. **Clarity** – Is the feedback understandable?  

Return: Pass / Fail with justification.
```

---

### ⚙️ Testing Framework Setup

We built a **simple test runner** that:

1. Iterates over all dataset samples.
2. Sends each code snippet to the model.
3. Captures the AI output and passes it to the **judge prompt**.
4. Logs results as ✅ Pass / ❌ Fail with explanations.

```python
for test in dataset:
    ai_output = run_model(test["code"])
    verdict = judge(ai_output, test["expected"])
    print(f"Test {test['id']}: {verdict}")
```

---

### ✅ Why This Setup?

* Ensures **objective evaluation** of AI outputs.
* Provides **clear metrics** on accuracy and reliability.
* Makes the pipeline **reproducible** for future improvements.