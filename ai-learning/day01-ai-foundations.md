# Day 1 - AI Foundations for Enterprise Content Management

## Session Goal
Build a foundational understanding of the AI concepts required for an AI-powered Enterprise Content Management platform.

---

## Key Concepts Learned

### 1. Traditional Search vs Semantic Search

Traditional Search:
- Searches for exact words
- Relies on keywords
- Does not understand meaning

Example:
Searching for 'vendor payment' may miss a document titled 'Microsoft Invoice'.

Semantic Search:
- Searches by meaning
- Understands relationships between concepts
- Uses embeddings and vectors

---

### 2. What is an Embedding?

An embedding is a numerical representation of meaning.

Text:
Invoice

Embedding:
[0.22, 0.91, 0.45, ...]

Documents with similar meaning produce vectors that are close together.

---

### 3. What is a Vector?

A vector is simply a list of numbers.

Examples:
- 384 dimensions
- 768 dimensions
- 1024 dimensions
- 1536 dimensions

The dimensions depend on the embedding model being used.

---

### 4. What is a Vector Database?

A vector database stores embeddings and allows similarity search.

Possible technologies:
- OpenSearch Vector Search
- PostgreSQL + pgvector
- Qdrant
- Chroma

Project Decision:
We are using OpenSearch Vector Search.

---

### 5. What is an LLM?

LLM = Large Language Model.

Purpose:
Generate text.

Examples:
- Qwen
- Llama
- Gemini
- Claude

Important:
An LLM is different from an embedding model.

---

### 6. Model vs Runtime

Example:

Qwen = Model
Ollama = Runtime

The runtime hosts and executes the model.

---

### 7. What is RAG?

Retrieval-Augmented Generation.

Flow:
Question
↓
Search Documents
↓
Retrieve Relevant Content
↓
Send Context to LLM
↓
Generate Answer

RAG allows AI to answer using enterprise documents rather than relying solely on model knowledge.

---

### 8. Why Enterprise AI Uses RAG

Documents change frequently.

Instead of retraining models every time content changes:

Documents
↓
Embeddings
↓
Search
↓
RAG

Benefits:
- Lower cost
- Faster updates
- Better governance
- Easier maintenance

---

## Current Project Architecture

User
↓
OpenShift Route
↓
Django Application
↓
OCR
↓
PostgreSQL

Capabilities:
- Upload
- Search
- View
- OCR
- Authentication

---

## Future Architecture Vision

User
↓
Django
↓
Semantic Search
↓
OpenSearch
↓
Relevant Content
↓
LLM
↓
Answer

Additional Capabilities:
- AI Assistant
- Semantic Search
- Metadata Extraction
- RAG
- Intelligent Classification

---

## Biggest Takeaways

1. Keyword Search finds words.
2. Semantic Search finds meaning.
3. Embeddings represent meaning as vectors.
4. OpenSearch can store and search vectors.
5. RAG connects enterprise content with AI.

---

## Questions for Future Learning

1. How are embeddings generated?
2. How does OpenSearch compare vectors?
3. How does chunking improve search?
4. How should embeddings be stored and managed?
5. How does RAG work in practice?
