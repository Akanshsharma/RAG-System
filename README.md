# RAG-System
📄 Retrieval-Augmented Question Answering (RAG) Pipeline

A lightweight Retrieval-Augmented Generation (RAG) system that enables question answering over custom knowledge using semantic search + generative AI.
This project demonstrates how to ingest raw text, chunk it intelligently, embed it locally, retrieve relevant context using vector similarity, and generate grounded answers using an instruction-tuned language model.

🚀 Overview
Traditional language models can hallucinate or lack domain-specific knowledge.
This project solves that by:
  -Indexing your private knowledge
  -Retrieving only the most relevant content
  -Generating answers strictly grounded in retrieved context
  -The result is a hallucination-resistant, explainable QA system that runs fully on local or CPU-only environments.
	
🧠 Architecture
Text File (Knowledge Base)
        ↓
Text Chunking (Recursive Splitter)
        ↓
Sentence Embeddings (SentenceTransformers)
        ↓
Vector Index (FAISS)
        ↓
Query Embedding
        ↓
Similarity Search (Top-K Chunks)
        ↓
Prompt Augmentation
        ↓
LLM Generation (FLAN-T5)

🔧 Tech Stack
Python
LangChain – intelligent text splitting
SentenceTransformers – local semantic embeddings
FAISS – fast vector similarity search
Hugging Face Transformers – text generation
Google FLAN-T5 (Small) – instruction-tuned LLM
CPU-only (no GPU required)

📦 Installation
pip install transformers sentence-transformers faiss-cpu langchain
pip install -U langchain-text-splitters

📁 Project Structure
.
my_knowledge.txt        # Custom knowledge base
RAG_System.py         # Main RAG implementation
README.md               # Project documentation

📄 Knowledge Source
The system reads from a plain text file:
my_knowledge.txt
This can contain:
Company policies
FAQs
Documentation
Internal guides
Any unstructured text

🧩 How It Works
1️⃣ Text Chunking
The knowledge file is split into semantically meaningful chunks using a recursive strategy that prioritizes:
Paragraphs
Newlines
Words (as a last resort)
This preserves context while keeping chunks small enough for embeddings.

2️⃣ Semantic Embeddings
Each chunk is converted into a dense vector using:
all-MiniLM-L6-v2
Fast
Lightweight
High semantic quality
Fully local

3️⃣ Vector Indexing
All embeddings are stored in a FAISS L2 index, enabling fast and exact similarity search across the knowledge base.

4️⃣ Retrieval
When a user asks a question:
The query is embedded
The FAISS index retrieves the Top-K most relevant chunks
Retrieved chunks form the context

5️⃣ Generation (RAG)
The model generates an answer using a strict prompt:
Uses only retrieved context
Explicitly refuses to answer if the information is missing
This prevents hallucinations and ensures transparency.

🧪 Example Usage
query = "What is the WFH policy?"
answer = answer_question(query)
print(answer)

If the answer exists in the knowledge base → it is returned
If not → the model responds with:
"I don't have that information."

✅ Key Design Principles
Grounded generation
Local embeddings (privacy-friendly)
Modular and extensible
Minimal dependencies
CPU-friendly

🔒 Limitations
Designed for small to medium knowledge bases
No persistence layer (FAISS index is in-memory)
No conversational memory
Single-document ingestion (can be extended)

🔮 Possible Extensions
Add multiple documents / PDFs
Persist FAISS index to disk
Upgrade to larger LLMs
Add conversation history
Wrap with FastAPI / Streamlit
Integrate cloud vector stores
Add evaluation & confidence scoring

🎯 Use Cases
Internal policy Q&A
Knowledge assistants
Document search
AI copilots
Proof-of-concept RAG systems
Learning & experimentation

📌 Why This Project Matters
This repository demonstrates a production-relevant RAG pattern that mirrors real-world AI systems used in:
Enterprise search
Internal copilots
AI knowledge assistants
All without requiring GPUs or cloud services.
