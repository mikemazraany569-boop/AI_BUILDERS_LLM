# Math Mistake Detective — LLM Chatbot

## 📌 Project Overview

**Math Mistake Detective** is an educational AI chatbot developed using **Python, Ollama, and the Llama 3.2 language model**.

The chatbot is designed to help high-school and first-year university students understand their mathematical mistakes. Instead of simply providing an answer, it analyzes the student's attempted solution, identifies the **first incorrect step**, explains the mistake, and guides the student toward the correct reasoning.

This project was developed as part of an **LLM tutorial** covering the fundamentals of working with Large Language Models through an API, including prompting, conversation history, streaming responses, and generation parameters.

---

## 🎯 Project Objectives

The main objectives of this project are to:

* Learn how to interact with an LLM through Python.
* Connect a Python application to a locally running LLM using Ollama.
* Design a specific and effective system prompt.
* Maintain conversation history between user and chatbot.
* Stream LLM responses progressively.
* Experiment with generation parameters.
* Build a simple but usable chatbot interface.
* Evaluate the chatbot using different mathematical prompts.
* Understand the strengths and limitations of LLM-based applications.

---

# 🤖 Math Mistake Detective

The chatbot acts as a specialized mathematics tutor.

When a student provides a mathematical problem and an attempted solution, the chatbot is instructed to:

1. Break the solution into clear steps.
2. Check each step in order.
3. Identify the **first incorrect step**.
4. Explain why the step is incorrect.
5. Classify the type of mistake when possible.
6. Give the student a useful hint.
7. Provide the complete solution when requested.
8. Encourage the student to try a similar problem.

The chatbot is also instructed to recognize when a student's solution is already correct and to ask for clarification when a problem is incomplete or ambiguous.

---

# 🧠 LLM Tutorial

Before developing the final chatbot, the project covered several important concepts related to Large Language Models.

## 1. What is an LLM?

A **Large Language Model (LLM)** is a machine-learning model trained on large amounts of text to understand and generate natural language.

LLMs can be used for tasks such as:

* Question answering
* Text generation
* Summarization
* Translation
* Programming assistance
* Educational tutoring
* Conversational applications

In this project, the LLM is used as an educational mathematics assistant.

---

## 2. Using Ollama

**Ollama** allows language models to run locally on a computer.

The project uses the:

```text
llama3.2
```

model.

The Python application communicates with the local Ollama service using the Python `ollama` package.

Basic connection:

```python
import ollama

response = ollama.chat(
    model="llama3.2",
    messages=messages
)
```

This allows the Python program to send messages to the model and receive generated responses.

---

## 3. System Prompt

A system prompt defines the chatbot's role, behavior, and communication style.

For this project, the system prompt defines the chatbot as:

```text
Math Mistake Detective
```

The prompt instructs the model to focus on **understanding mathematical mistakes rather than simply providing answers**.

This demonstrates an important LLM concept: **prompt engineering**.

A specific system prompt can influence the model's behavior by providing:

* Role
* Objective
* Rules
* Expected reasoning process
* Communication style
* Handling of incorrect and correct answers
* Handling of ambiguous questions

---

## 4. Conversation History

The chatbot stores messages in a Python list:

```python
messages = [
    {
        "role": "system",
        "content": system_prompt
    }
]
```

User messages are then added:

```python
messages.append({
    "role": "user",
    "content": user_input
})
```

The assistant's response is also stored:

```python
messages.append({
    "role": "assistant",
    "content": full_response
})
```

This allows the chatbot to understand follow-up questions and maintain the context of the conversation.

For example:

```text
User: I don't understand the distributive property.

Bot: ...

User: Can you give me another example?

Bot: ...
```

The second question can be understood because the previous conversation is included in the message history.

---

# 🌊 Streaming Responses

The chatbot uses streaming so that the response appears progressively instead of waiting for the complete answer.

```python
response = ollama.chat(
    model="llama3.2",
    messages=messages,
    stream=True
)
```

The response is then displayed chunk by chunk:

```python
for chunk in response:
    text = chunk["message"]["content"]
    print(text, end="", flush=True)
```

This creates a more natural chatbot experience because the user can see the response being generated.

---

# ⚙️ Generation Parameters

The chatbot allows experimentation with generation parameters.

## Temperature

Temperature controls the amount of variation in the model's generated responses.

The project experiments with values such as:

```text
0.2  → low
0.7  → medium
1.2  → high
```

Lower values generally produce more consistent and predictable responses, while higher values can produce more variation.

For a mathematics chatbot, consistency is particularly important because the chatbot should provide clear and reliable explanations.

## Maximum Output Tokens

The project also uses:

```python
num_predict = 500
```

This controls the maximum number of tokens that the model can generate for a response.

For example:

```text
50 tokens   → short response
150 tokens  → moderate response
500 tokens  → longer response
```

The application allows these parameters to be changed while the chatbot is running.

---

# 💻 User Interface

The chatbot uses a simple terminal-based interface.

The user can:

1. Enter a message.
2. Send the message.
3. Receive a streamed response.
4. Continue the conversation.
5. Change generation parameters.
6. Clear the conversation history.
7. Exit the application.

Example:

```text
=============================================================
                 MATH MISTAKE DETECTIVE
=============================================================
Model: llama3.2
Temperature: 0.3
Maximum output tokens: 500

Commands:
  settings  - change temperature or maximum output tokens
  clear     - clear the conversation history
  exit      - quit the chatbot
=============================================================

You: (x-5)^2 = x^2 - 25

Bot: Let's investigate your calculation...
```

---

# 🧪 Evaluation

The chatbot was evaluated using different types of mathematical prompts.

## Test 1 — Algebraic Error

```text
A student says that x = 5.5 is a solution to the equation
2(x+3)=14. Is the student's answer correct?
Check the reasoning and identify any mistake.
```

This tests whether the chatbot can identify a
