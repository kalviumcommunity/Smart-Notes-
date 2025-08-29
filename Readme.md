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
