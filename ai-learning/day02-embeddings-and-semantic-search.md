# Day 2 - Embeddings, Chunking and Semantic Search

## Session Goal
Understand how documents become searchable by meaning instead of keywords.

---

## Key Concepts Learned

### 1. Embeddings
An embedding is a numerical representation of meaning.

Example:

Invoice
↓
Embedding Model
↓
Vector [x1,x2,x3,...]

Documents with similar meaning produce vectors that are close together.

---

### 2. Embedding Models vs LLMs

Embedding Models:
- Generate vectors
- Used for semantic search

Examples:
- Amazon Titan Embeddings
- BGE
- Nomic Embed
- E5

LLMs:
- Generate text
- Used for question answering

Examples:
- Qwen
- Llama
- Gemini
- Claude

Important:
Model and runtime are different concepts.

Example:
- Qwen = model
- Ollama = runtime

---

### 3. Semantic Search

Keyword Search:
Searches words.

Semantic Search:
Searches meaning.

Example:

Query:
"cloud billing records"

May return:
- Azure invoice
- AWS monthly bill
- Vendor payment request

Even when exact words are different.

---

### 4. Chunking

Major architect takeaway.

Do NOT create one embedding for a large document.

Bad:
200 page handbook
↓
1 embedding

Good:
200 page handbook
↓
100 chunks
↓
100 embeddings

Semantic search works against chunks, not entire documents.

---

### 5. OpenSearch Instead of pgvector

Project Decision:

We are using OpenSearch vector search.

Not:
- PostgreSQL pgvector

Architecture:

Document
↓
OCR
↓
Chunking
↓
Embedding Generation
↓
OpenSearch Index
↓
Semantic Search
↓
RAG

---

### 6. FileNet Architecture Analogy

FileNet:
System of Record

OpenSearch:
Search and Vector Layer

Future Django ECM:
Django Application = Repository
OpenSearch = Search Platform

---

### 7. Hybrid Search

Enterprise systems typically combine:

Keyword Search
+
Vector Search

Benefits:
- Exact matches
- Semantic matches
- Better ranking

---

## Architect Notes

Documents are permanent.
Embeddings are temporary.

Embedding models will change over time.

Design the platform so embeddings can be regenerated without affecting stored documents.

---

## Biggest Takeaway

Documents are not what we search.

Chunks are what we search.

This concept is the foundation for semantic search and RAG.

---

## Questions for Future Learning

1. How does OpenSearch store vectors?
2. What is k-NN search?
3. How is similarity score calculated?
4. How should chunk metadata be designed?
5. How should re-indexing work when embedding models change?
