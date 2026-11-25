# Day 1: Sweet Crumbs Home Bakery Assistant

For Day 1 of the AI Agents training program, I built a small customer-support assistant for a fictional bakery called **Sweet Crumbs Home Bakery** using LangChain and Groq, and tested a prompt-injection check on it.

## What This Does
- **Bakery assistant:** Answers customer questions using a system prompt with clear ground rules—cakes are baked to order, need at least 24 hours' notice, and have eggless options, while the bot shouldn't promise exact delivery times, should say when it doesn't know something, and should keep replies polite and under 60 words.
- **Prompt guard test:** Runs a sample prompt-injection input through `meta-llama/llama-prompt-guard-2-22m` via the Groq API to see how strongly it flags an instruction-override attempt.

## How I Built & Tested It
I wrote the code in a Google Colab notebook (`agenticAI.ipynb`):
- Installed `langchain_groq` and pulled `GROQ_API_KEY` from Colab's Secrets tab.
- Set up `ChatGroq` with `openai/gpt-oss-120b` (`temperature=0`) and a simple `ask(question)` helper function.
- Tested it with a sample question (`"can i get my order tommorrow"`) and checked the prompt-guard score on an adversarial prompt.

## Running It
1. Open the notebook in Google Colab and add `GROQ_API_KEY` under **Secrets** on the left panel.
2. Run the cells in order to install dependencies, initialize the model, test `ask(...)`, and run the prompt-guard snippet.
