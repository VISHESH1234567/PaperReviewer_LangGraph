# LangGraph Academic Paper Review Agent

This repository contains a **LangGraph-based Multi-Agent System** designed to assist students and researchers in reviewing, summarizing, and querying academic papers (PDFs).

The agent uses a graph architecture to break down the PDF, plan a response based on the user's query, and synthesize a final answer using strictly cited sources from the text.

## 📦 Installation

1.  **Clone the repository:**
    ```bash
    git clone <repository_url>
    cd <repository_name>
    ```

2.  **Install dependencies:**
    ```bash
    pip install langchain-community pypdf langchain-google-genai langgraph langchain-core
    ```

3.  **API Key Setup:**
    You need a Google AI Studio API Key (Gemini).
    - Go to [Google AI Studio](https://aistudio.google.com/).
    - Create a new API key.
    - Set it in your environment:
    ```bash
    export GOOGLE_API_KEY="your_api_key_here"
    ```
    *Alternatively, simply run the script and paste the key when prompted by the secure input.*

## 🚀 How to Run

1.  **Place your PDF file** in the `/data` directory (or any accessible path).
2.  **Run the main script:**
    ```bash
    python main.py
    ```
3.  **Inputs:**
    * **PDF Path:** Enter the absolute or relative path to your PDF (e.g., `data/paper.pdf`).
    * **Prompt:** Enter your specific question (e.g., "Summarize the methodology" or "What are the limitations?").

## 🏗️ Architecture

The system follows a linear Directed Acyclic Graph (DAG) workflow:

```mermaid
graph TD
    Start --> PDF_Loader
    PDF_Loader --> Scheduler
    Scheduler --> Splitter_Agent
    Splitter_Agent --> Planner_Agent
    Planner_Agent --> Final_Answer_Agent
    Final_Answer_Agent --> End