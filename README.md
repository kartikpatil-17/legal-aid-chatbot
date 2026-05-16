# ⚖️ Legal Aid Chatbot API (RAG-Powered)

An interactive, full-stack, serverless web application designed to bridge the legal literacy gap by translating complex, country-specific statutes, laws, and pamphlets into clear, plain language. 

By leveraging a **Retrieval-Augmented Generation (RAG)** pipeline, the chatbot answers legal inquiries with high accuracy based strictly on verified legal documents, avoiding LLM hallucinations and providing direct document source citations for full transparency.

---

## 🏗️ Project Architecture

The application is built around a standard RAG workflow seamlessly connecting an asynchronous backend API to a lightweight, responsive user interface:

1. **Client/Frontend Layer:** A single-page, responsive interface (`index.html` + vanilla JS) that handles real-time messaging, input sanitization to block invalid control characters, and dynamic UI updates.
2. **Backend/API Server Layer:** Powered by **FastAPI** and hosted locally via **Uvicorn**, managing a high-performance `POST /ask` endpoint.
3. **Data & Embedding Layer:** Text blocks are vectorized using the multilingual `BAAI/bge-m3` embedding model via `langchain-huggingface` and indexed in a local, serverless **Chroma DB** vector store.
4. **Retrieval & LLM Generation Layer:** A LangChain `RetrievalQA` workflow isolates the top-3 most semantically similar context pieces from the database, builds a secure prompt matrix, and sends it to Google's cloud-hosted **Gemini 2.5 Flash** model for optimized, clear generation.

---

## 🛠️ Tech Stack

- **Backend Framework:** FastAPI (Python)
- **ASGI Server:** Uvicorn
- **Orchestration Framework:** LangChain (`RetrievalQA`)
- **Embedding Model:** HuggingFace `BAAI/bge-m3`
- **Vector Database:** Chroma DB (Stored locally)
- **LLM Engine:** Google Gemini 2.5 Flash (via Google AI Studio Developer API)
- **Frontend:** Vanilla HTML5, CSS3, and JavaScript (served directly from the FastAPI static mount)

---

## 📂 Project Structure

```text
Legal Aid Chatbot/
│
├── model.py            # Main FastAPI server & LangChain RAG pipeline
├── .env                # Local environment keys (Gemini API token)
├── requirements.txt    # Managed project dependencies
├── legal_db/           # Persistent Chroma vector store directory
│
└── static/             # Frontend website files served by FastAPI
    ├── index.html      # User Interface structural layout and styling
    └── app.js          # Asynchronous fetch and input optimization logic
