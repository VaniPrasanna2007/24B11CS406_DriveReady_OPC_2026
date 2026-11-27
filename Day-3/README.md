# Day 3: Your First Agent — What an Agent Is, and LangChain

This folder contains the Day 3 implementation, evaluation tests, and hands-on experiments from the **AI Agents Workshop (Level 2 — Single Agent, Session 1 of 3)** in `24B11CS406_DriveReady_OPC_2026`.

---

## Overview

Day 3 transitions from raw single-model API scripts to **LangChain** building blocks, introducing the core anatomy of an AI agent (`Brain · Instructions · Tools · Memory`), the **ReAct agent loop (`Think → Act → Observe → Repeat`)**, automated prompt regression testing via `tests.csv`, and an initial `create_agent` setup.

### Key Topics Covered
1. **Chatbot vs. Agent**: Understanding the shift from answering in text to achieving goals by selecting and executing tools.
2. **The Four Parts of an Agent**:
   - **Brain**: `ChatGroq(model="openai/gpt-oss-20b")`
   - **Instructions**: Structured `SYSTEM` prompt (`Role · Facts · Rules · Format`)
   - **Tools**: Typed, documented Python functions (prepared for Day 4)
   - **Memory**: Conversation history passed via `MessagesPlaceholder("history")`
3. **The Agent Loop (`ReAct`)**: Iterative `Think → Act → Observe → Repeat` execution until a final response or round limit is reached.
4. **Three Levels of AI & Task Selection**: Choosing the simplest reliable solution—**plain code** (fixed rules/math), **one LLM call** (one-off text generation), or an **agent** (multi-step reasoning with tools).
5. **LangChain LCEL Chains**: Composing `ChatPromptTemplate | ChatGroq | StrOutputParser` for modular, model-agnostic pipelines.
6. **Automated Evaluation (`tests.csv`)**: Running regression checks (`question,must_include`) after every prompt or parameter change and tracking pass rates.

---

## Implementations Included

### 1. Main Build: Sweet Crumbs Assistant in LangChain
- **Conversational Chain (`prompt | llm | StrOutputParser()`)**: Built with `ChatPromptTemplate` and `MessagesPlaceholder("history")` to retain multi-turn context (`ask()`).
- **Automated Test Suite (`tests.csv` & `run_tests()`)**: Evaluated responses on menu pricing, eggless availability, advance-notice rules, and unknown delivery locations.
- **LangChain Agent Sneak Peek (`create_agent`)**: Initialized `create_agent(model=llm, tools=[], system_prompt=SYSTEM)` as the foundation for adding autonomous tools on Day 4.

### 2. "Your 30%" Hands-On Experiments (`CodeCraft Studio`)
1. **Custom Business Prompt (`{business}` Template)**: Rewrote `SYSTEM` for **CodeCraft Studio** (`Starter Kit`: ₹299, `Prompt Pack`: ₹199, `1-on-1 Review`: ₹499, 12-hour advance booking notice, email delivery).
2. **10-Question Evaluation Suite (`tests.csv`)**: Created 10 domain test cases covering pricing, multi-item totals, booking lead times, delivery method, and out-of-scope escalations (`8/10` baseline pass rate — **80%**).
3. **Prompt Iteration & Pass Rate Comparison**: Tightened the escalation rule for out-of-FACTS and guaranteed-time queries, improving the pass rate from **80% (8/10)** to **90% (9/10)**.
4. **Temperature Sensitivity Check (`temperature=1.0`)**: Ran the 10-question suite twice at `temperature=1.0`, observing **90% (9/10)** pass rates on both runs while **5/10** responses varied in phrasing between runs.
5. **Task Classification (`Agent or Not`)**:
   - *Calculate exact total price (`item * quantity`)* → **plain code**
   - *Draft a friendly welcome or festival promo message* → **one LLM call**
   - *Look up stock/availability, log a booking, and confirm details* → **agent**

### 3. Before Day 4 Preparation (Tool-Ready Functions)
Implemented two type-hinted, documented Python functions backed by `CATALOGUE` to be registered as agent tools on Day 4:
- `lookup_price(item: str, qty: int = 1) -> int`: Returns the total price in rupees for `qty` units of an item in `CATALOGUE`.
- `check_availability(item: str) -> bool`: Returns `True` if the item is currently available in `CATALOGUE`, otherwise `False`.

---

## Setup & How to Run

1. Open the notebook in **Google Colab** (`task.py`).
2. Add your `GROQ_API_KEY` in Colab **Secrets** (left sidebar key icon) and enable **Notebook access**.
3. Run the LangChain setup cell:
   ```python
   !pip install -q langchain langchain-groq
   import os
   from google.colab import userdata

   os.environ["GROQ_API_KEY"] = userdata.get("GROQ_API_KEY")
   from langchain_groq import ChatGroq

   llm = ChatGroq(model="openai/gpt-oss-20b", temperature=0.3)
