# Day 4 – Tools, Pydantic & Google Sheets

## Overview
Day 4 focuses on connecting AI agents with external tools, validating structured data using Pydantic, and storing information in Google Sheets.

In this session, I explored how AI agents can use Python functions to perform tasks and organize customer order details in a structured format.

## Concepts Covered

- **Tools:** Created Python functions that an AI agent can call to perform specific tasks.
- **Pydantic:** Used Pydantic models to validate and structure customer order information.
- **Structured Output:** Extracted customer details such as name, product, quantity, and date.
- **Google Sheets Integration:** Connected the application with Google Sheets to store order information.
- **Tool Calling:** Explored how an AI agent selects and uses tools based on customer requests.

## Project: Sweet Crumbs Home Bakery

Customized the workshop examples into a simple AI-powered bakery assistant.

### Bakery Menu

| Product | Price |
|---|---:|
| Plum Cake | ₹500 |
| Chocolate Cake | ₹650 |
| Cupcake | ₹80 |

### Features Implemented

1. Look up bakery product prices.
2. Check product availability.
3. Extract customer order details using Pydantic.
4. Validate structured order information.
5. Store customer orders in Google Sheets.
6. Use AI agent tools to process customer requests.

## Technologies Used

- Python
- LangChain
- Groq LLM
- Pydantic
- Google Colab
- Google Sheets
- gspread

## Learning Outcomes

- Understood how tools extend AI agent capabilities.
- Learned how to create Python functions as agent tools.
- Practiced structured data extraction with Pydantic.
- Learned how to connect Google Sheets with Python.
- Understood how agents interact with tools to complete tasks.

## Repository Structure

```text
24B11CS406_DriveReady_OPC_2026/
└── Day-4/
    ├── task.py
    └── README.md
```

## Conclusion

Day 4 helped me understand how AI agents can interact with external tools, validate customer information, and store structured data. I applied these concepts to my Sweet Crumbs Home Bakery example to understand a practical use case of AI agents.
