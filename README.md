# 🧠 Multi-Agent AI Projects with LLM Fine-Tuning & LangGraph Workflows

This repository contains two experimental AI projects exploring different applications of Large Language Models (LLMs) and agent frameworks:

1. 🏡 **Real Estate Price Prediction**
2. 📅 **Meeting Room Booking Agent using LangGraph**

Both projects focus on applying modern tools like **LoRA**, **Unsloth**, **LangGraph**, and **vLLM**, with an emphasis on understanding their workflows rather than producing production-ready code.

---

## 🏡 Real Estate Price Prediction (LLM Fine-Tuning)

### What I Did

I fine-tuned a pre-trained LLM (using **LoRA** and **Unsloth**) to predict real estate prices from natural language descriptions (e.g., “A house in Texas with 3 bedrooms...” → `$325,000`).

### Tools & Techniques

* **LoRA** with `r=8`, `alpha=16`, and `dropout=0.05`
* **Unsloth** for efficient fine-tuning
* **4-bit quantization** with `bitsandbytes`
* **Evaluation** with MAE, MSE, and R²
* **vLLM** explored for optimized inference (not fully integrated yet)

### Status

Each part worked well **individually**, but combining them in one notebook caused some errors due to compatibility and runtime complexity. However, fine-tuning and inference *in isolation* worked 100%.

---

## 📅 Meeting Room Booking Agent (LangGraph)

### What I Built

A LangGraph-based agent to help users book meeting rooms by checking availability, resolving conflicts, and handling reservations through state-driven logic.

### Agent Flow

* Parses user input → finds suitable rooms → checks calendar conflicts
* If no conflict, it books the room; if conflict, it suggests alternatives
* Includes error handling and confirmation generation

### Status

I tested each node (room lookup, conflict checking, reservation) **separately** with success. However, the full LangGraph workflow had issues when merging everything—mainly due to state structure and async handling.

---

## 🔍 Lessons & Outcome

* I learned a lot about **LLM fine-tuning**, **stateful agents**, and tool integration.
* While both projects ran into **integration issues**, I confirmed that all concepts work **independently**.
* I now have a solid foundation to build more complex, multi-agent systems or deploy refined versions with some cleanup.

---

## ⚙️ Requirements

* Python 3.10+
* `transformers`, `peft`, `unsloth`, `langgraph`, `bitsandbytes`, `torch`, `vllm`

---

## 🚧 Known Issues

* Full notebook execution (especially merging fine-tuning with inference or LangGraph agents) may break due to memory or compatibility.
* Both systems are designed more for **learning and demonstration** than full deployment at this stage.
