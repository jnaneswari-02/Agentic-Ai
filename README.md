# Agentic-Ai
Day 1 · How LLMs Work & Your First API Call
Workshop: AI Agents Workshop · Level 1 Fundamentals (Day 1 of 2)

Case Study: Sweet Crumbs Home Bakery

Environment: Google Colab

Overview
This task introduces the core concepts behind Large Language Models (LLMs) and walks through making a first API call using the OpenAI Python SDK against Groq for the Sweet Crumbs Home Bakery case study.

Topics Covered
Why AI Is Everywhere Now: APIs and wrappers on top of ready-made models (such as Transformers).

What an LLM Does: Next-token prediction in a loop.

Tokens: The unit of text processing, context budgets, and pricing (roughly ¾ of an English word; Indian languages like Telugu require more tokens per word).

Temperature: Controlling determinism vs. creativity (e.g., low temperature around 0.2 for facts and pricing; higher values around 1.0 for creative ideas).

No Memory: Models are stateless; applications resend conversation history on each call.

Context Window: The combined token budget per call (system prompt, history, context/documents, and response).

Hallucination & Grounding (RAG): Why models can give plausible yet wrong answers, and how supplying facts in the prompt helps keep responses grounded.

The AI Engineer & 4-Step Pattern: Connect → Give context → Get the answer → Wrap in a UI.

First API Call in Colab: Setting up secrets, initializing the client, and sending a chat completion request.

Setup in Google Colab
Create an API key from Groq Console.

In Google Colab, open the Key (Secrets) icon in the left sidebar and add a secret named GROQ_API_KEY with Notebook access enabled.

Code
Python
!pip install -q openai

from google.colab import userdata
from openai import OpenAI

client = OpenAI(
    api_key=userdata.get("GROQ_API_KEY"),
    base_url="https://api.groq.com/openai/v1",
)

SYSTEM = """ROLE:   You are the assistant for Sweet Crumbs Home Bakery.
FACTS:  We bake to order. Orders need 24 hours' notice. All cakes have eggless versions.
        Plum cake Rs 500. Chocolate cake Rs 650. Cupcake Rs 80.
RULES:  Never promise a delivery time. If the answer isn't in FACTS, say "I'll check with the owner."
FORMAT: Under 50 words, friendly, English or Telugu matching the customer."""

response = client.chat.completions.create(
    model="openai/gpt-oss-20b",
    temperature=0.2,

print(response.choices[0].message.content)
print(response.usage)
