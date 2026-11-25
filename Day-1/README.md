# Role-Based AI Assistant with Identity Verification (LangChain & Groq)

## Task Description
This task implements a conversational AI assistant using LangChain and the Groq API that enforces **role-based system prompt guardrails**. The assistant is configured to act as an internal AI for Iron Man and the Avengers, verifying the user's identity and lore knowledge before answering sensitive queries.

## Tech Stack & Model
- **Language:** Python 3 (Google Colab)
- **Framework:** `langchain-groq` (`ChatGroq`)
- **LLM Model:** `openai/gpt-oss-120b`
- **Temperature:** `0.5`

## Implementation Overview
1. **Environment & API Setup:** Retrieves the `GROQ_API_KEY` securely from Google Colab Secrets (`userdata.get`) instead of hardcoding credentials.
2. **System Prompt Guardrail (`SYSTEM`):** Defines the assistant's persona, access boundary (Avengers team only), and an authentication rule requiring the user to verify their identity before receiving assistance.
3. **Inference Function (`ask`):** Sends a structured message list containing the `system` role prompt and the `human` prompt (identity verification + user query) to the Groq-hosted LLM and prints the response.

## Sample Verification Prompt Tested
- **Claimed Identity:** Steve Rogers
- **Verification Facts Provided:** Project Rebirth commanding officer (Colonel Chester Phillips), serum creator (Dr. Abraham Erskine), and timeline verification regarding Bucky Barnes.
- **Query:** Location of Wanda Maximoff and Vision following the Battle of Sokovia (post-*Age of Ultron*).
