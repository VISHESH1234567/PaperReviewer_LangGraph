# ARCH.md — Multi-Agent Research System Architecture

## 1. System Overview
This system is a linear **Directed Acyclic Graph (DAG)** built with **LangGraph**. It loads a PDF, structures its content, creates a research plan from a user query, and generates a cited academic-style answer. All cognitive steps use **Google Gemini 2.5 Flash**.

---

## 2. Agent Roles

### A. PDF Loader (`pdf_loader`)
**Type:** Tool Node  
Loads the PDF using `PyPDFLoader`, converts it into LangChain `Document` objects, and handles basic file I/O errors.

---

### B. Scheduler (`scheduler`)
**Type:** Orchestration Node  
Acts as a passthrough that logs state transitions and hands control to cognitive agents.

---

### C. Splitter (`splitter`)
**Type:** LLM Agent  
Chunks the raw PDF text into **10–15 semantic sections**, returning a sanitized **Python dictionary** of section → content.

---

### D. Planner (`planner`)
**Type:** LLM Agent  
Analyzes the user query and the Splitter’s sections, producing a **numbered step-by-step plan** for generating the final answer.

---

### E. Final Answer (`final_answer`)
**Type:** LLM Agent  
Executes the plan using only the Splitter’s dictionary and outputs a coherent answer with **mandatory citations** to the relevant sections.

---
