# Day 3: Stateful Chatbot & Automated Testing

## Overview
This program builds a customer support assistant for **Sweet Crumbs Home Bakery** using **LangChain** and **Groq** (`openai/gpt-oss-120b`). It demonstrates how to build a reliable business chatbot by **giving the AI conversation memory** and **automatically testing that it follows company rules**.

---

## What This Program Does & Why We Use It

### 1. Controlled AI Behavior (`SYSTEM` Prompt & Low Temperature)
* **What it does:** Sets strict role boundaries, menu prices (Plum cake Rs 500, Chocolate cake Rs 650, Cupcake Rs 80), a 24-hour notice requirement, bilingual support (English/Telugu), and a fallback phrase (*"I'll check with the owner"*) for unknown questions. It runs at `temperature=0.3`.
* **Why we use it:** Prevents the AI from hallucinating discounts, promising same-day deliveries, or giving inconsistent answers to customers.

### 2. Conversation Memory (`MessagesPlaceholder` & `history`)
* **What it does:** Saves every `(human, ai)` exchange inside a `history` list and injects it back into the prompt on each turn using `MessagesPlaceholder`.
* **Why we use it:** LLMs are stateless by default and forget everything after one reply. Passing `history` lets the bot remember context—such as the customer's name (*Ravi*)—so users can have natural, multi-turn conversations without repeating themselves.

### 3. Automated Prompt Testing (`run_tests`)
* **What it does:** Reads test questions and expected keywords (`must_include`) from `test.csv`, runs each question with a blank memory (`history=[]`), and prints a pass/fail accuracy score.
* **Why we use it:** Eliminates manual testing every time you tweak your prompt or change models. It quickly catches silent regressions and formatting edge cases (such as the model generating `egg‑less` with a non-breaking hyphen instead of `eggless`).

---

## Setup & Usage

1. **Install Dependencies:**
   ```bash
   pip install -q langchain langchain-groq
   ```

2. **Add API Key:**
   Save your `GROQ_API_KEY` in Google Colab Secrets (`userdata`).

3. **Chat with Memory:**
   Call `ask("your message")` to chat while retaining session context in `history`.

4. **Run Automated Tests:**
   Upload `test.csv` (with `question` and `must_include` columns) to `/content/test.csv` and call `run_tests()`.
