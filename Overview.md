# CoreLex: Advanced Document Analysis and Retrieval System

## 1. Project Overview

CoreLex is a comprehensive, multi-service application designed to ingest, process, and analyze large volumes of documents. It uses a Retrieval-Augmented Generation (RAG) architecture to provide accurate, context-aware answers based on the content of a provided document library.

The system is fully containerized using Docker and Docker Compose, allowing for a consistent, one-command startup process across different development environments. It leverages a local, open-source Large Language Model (LLM) to ensure data privacy and eliminate the need for external API keys or manual configuration.

---

## 2. System Architecture

The application is composed of several interconnected microservices, each playing a specific role:

* **Frontend (Streamlit):** A web-based user interface built with Streamlit. This is the primary entry point for users to upload documents, ask questions, and view the AI-generated responses and their sources.

* **Backend (FastAPI):** The central nervous system of the application. This Python-based API handles business logic, orchestrates the flow of data between services, manages document processing pipelines, and exposes endpoints for the frontend to consume.

* **Ollama (LLM Service):** Provides local, open-source LLM capabilities. Instead of relying on external APIs like Gemini or OpenAI, Ollama runs models such as Llama 3 directly within the Docker environment. This service is responsible for the final synthesis and reasoning steps.

* **ChromaDB (Vector Database):** The core of the retrieval system. When documents are processed, their text is broken into chunks and converted into numerical representations (embeddings). ChromaDB stores these embeddings and allows for lightning-fast semantic similarity searches to find the most relevant context for a given query.

* **PostgreSQL (Relational Database):** The primary store for structured data. This includes user information, document metadata (filenames, upload dates, processing status), chat history, and any other relational data required by the application.

* **Redis (In-Memory Cache):** A high-speed cache used to store frequently accessed data, reducing latency and offloading work from the database. It can also be used as a message broker for managing background tasks in more complex workflows.

* **Document Processors (Tesseract & Sentence-Transformers):** These are not services but critical libraries baked into the backend's Docker image.
    * **Tesseract OCR:** An optical character recognition engine used to extract text from scanned documents and images.
    * **Sentence-Transformers:** A library used to generate the high-quality semantic embeddings from text chunks that are stored in ChromaDB.



