# Stateful Customer Support Chatbot with Guardrails & Conversation Memory

## Task Description
This task builds a multi-turn, stateful customer support assistant for **Sweet Crumbs Home Bakery** using the OpenAI-compatible Chat Completions API. The assistant enforces strict system prompt guardrails, maintains sliding-window conversation memory, handles API exceptions gracefully, and includes a Python decorator for logging helper function calls.

## Tech Stack & Model
- **Language:** Python 3
- **SDK:** `openai` (OpenAI-compatible client for Groq)
- **Model:** `openai/gpt-oss-20b`
- **Temperature:** `0.3`

## Key Features Implemented
1. **Role-Based System Prompt (`SYSTEM`):**
   - **Role & Facts:** Grounds the model strictly in the bakery's menu prices (`plum cake`, `chocolate cake`, `cupcake`), 24-hour advance order policy, and eggless options.
   - **Guardrails:** Prohibits promising delivery times and instructs the bot to say *"I'll check with the owner"* for out-of-scope queries.
   - **Bilingual & Concise Format:** Responds in under 50 words in either English or Telugu, matching the customer's language.
2. **Sliding-Window Conversation Memory (`history` & `MAX_TURNS`):**
   - Retains the system prompt alongside the last 8 conversation messages so the bot remembers the customer's name and order details without exceeding token limits.
3. **Function Call Logging Decorator (`@log_call`):**
   - Wraps the `get_price(item, qty)` utility using `functools.wraps` to trace function arguments and return values during execution.
4. **Error Handling:**
   - Catches `RateLimitError` and `APIConnectionError` to return user-friendly fallback responses instead of crashing the chat loop.

## How to Run
1. Install the OpenAI Python SDK:
   ```bash
   pip install openai
