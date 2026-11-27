# Day 2: Prompts, Memory, and Python Essentials for AI Agents

This folder contains the Day 2 implementation and hands-on experiments from the **AI Agents Workshop (Level 1 — Fundamentals)** in `24B11CS406_DriveReady_OPC_2026`.

---

## Overview

Day 2 builds upon single-turn API calls from Day 1 to construct a stateful, rule-following customer assistant (**Sweet Crumbs Home Bakery**) and explores core prompt engineering and Python patterns needed for agentic workflows.

### Key Topics Covered
1. **Messages & Roles (`system`, `user`, `assistant`)**: Structuring multi-turn conversation scripts.
2. **Structured System Prompts (`Role · Facts · Rules · Format`)**: Grounding responses in business facts and preventing risky promises.
3. **Few-Shot Prompting**: Providing worked input–output examples to enforce consistent classification labels (`order`, `question`, `complaint`).
4. **Structured JSON Output & Parsing**: Extracting customer orders into clean JSON fields and parsing with `json.loads()` inside `try / except`.
5. **Manual Conversation Memory & Window Trimming**: Maintaining a rolling `history` list (`[history[0]] + history[1:][-MAX_TURNS:]`) to balance context retention and token usage.
6. **Python Foundations for Agents**:
   - Dictionaries & JSON serialization (`json.dumps`, `json.loads`)
   - Type-hinted functions with clear docstrings (`get_price(item: str, qty: int = 1) -> int`)
   - Function decorators (`@log_call` using `functools.wraps`)
   - Graceful exception handling (`RateLimitError`, `APIConnectionError`, `JSONDecodeError`)

---

## Implementations Included

### 1. Main Build: Sweet Crumbs Home Bakery Chatbot
- **Menu & Knowledge Grounding**: Stores product prices (`plum cake`: ₹500, `chocolate cake`: ₹650, `cupcake`: ₹80), 24-hour advance notice policy, and eggless options inside the `SYSTEM` prompt.
- **Guardrails**: Enforces strict rules against promising delivery times and instructs the bot to escalate unknown queries (`"I'll check with the owner."`).
- **Multilingual & Concise Format**: Replies in under 50 words in English or Telugu matching the user's language.
- **Decorated Pricing Utility**: Uses `@log_call` on `get_price()` to trace inputs and outputs.
- **Sliding-Window Chat Loop**: Retains the system message plus the latest `MAX_TURNS = 8` messages until the user enters `bye`, `exit`, or `quit`.

### 2. "Your 10%" Hands-On Experiments
1. **System Prompt Guardrail Comparison**: Tested `"Can you deliver in 1 hour?"` with and without `RULES` to verify that restoring `RULES` prevents unverified delivery commitments.
2. **Few-Shot Message Classifier**: Trained with 3 labeled examples (`order`, `question`, `complaint`) and evaluated across 5 unseen customer messages with `temperature=0`.
3. **Order Extraction to JSON**: Extracted `name`, `item`, `qty`, `date`, and `eggless` fields from natural language orders into a Python dictionary with `json.loads()` and `try / except`.
4. **Memory Trimming Behavior (`MAX_TURNS = 2`)**: Demonstrated how narrowing the context window drops earlier turns (such as the customer's name) once they fall outside the recent window.
5. **Custom Business Adaptation (`CodeCraft Studio`)**: Built a custom catalogue (`starter kit`, `prompt pack`, `1-on-1 review`), a `@log_call`-decorated pricing helper (`get_biz_price`), and a domain-specific `SYSTEM` prompt.

---

## Setup & How to Run

1. Open the notebook in **Google Colab** (`task.py`).
2. Add your `GROQ_API_KEY` in Colab **Secrets** (left sidebar key icon) and enable **Notebook access**.
3. Run the setup cell to install dependencies and initialize the Groq client:
   ```python
   !pip install -q groq openai
   import os
   from google.colab import userdata

   os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")

   from groq import Groq
   client = Groq()
