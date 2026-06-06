# Day 3 - OpenSearch Vector Architecture

## Executive Summary

This session focused on how OpenSearch enables semantic search and Retrieval-Augmented Generation (RAG) for Enterprise Content Management systems.

Key learning objective:
Understand how document chunks, vectors, OpenSearch indexes, and similarity search work together.

---

## Key Concepts Learned

### 1. OpenSearch Stores Chunks, Not Documents

A large document is split into smaller chunks before indexing.

Example:

Employee Handbook
↓
100 Chunks
↓
100 OpenSearch Records

Each chunk becomes independently searchable.

Architect Takeaway:

Documents are stored.
Chunks are searched.

---

### 2. OpenSearch Record Design

Recommended structure:

- document_id
- chunk_id
- title
- document_type
- department
- chunk_text
- vector
- security_group
- created_date

This allows:
- Semantic Search
- Metadata Filtering
- Security Filtering
- Hybrid Search

---

### 3. k-NN Search

k-NN = k Nearest Neighbors.

OpenSearch compares the query vector against stored vectors and returns the closest matches.

Example:

Query:
cloud billing records

Results:
- Azure Invoice
- AWS Monthly Bill
- Vendor Payment Request

The top matching chunks are returned.

---

### 4. Similarity Scoring

Semantic search relies on vector similarity rather than keyword matching.

Common approach:
- Cosine Similarity

Concept:
Higher score = more similar meaning.

Example:
Invoice vs Bill
= High Similarity

Invoice vs Bicycle
= Low Similarity

---

### 5. Hybrid Search

Enterprise systems rarely rely on a single search method.

Recommended approach:

Keyword Search
+
Vector Search

Benefits:
- Exact matching
- Meaning matching
- Better ranking
- Better user experience

---

### 6. Security Filtering

Semantic search results must respect repository permissions.

Retrieval Flow:

Query
↓
Vector Search
↓
Security Filter
↓
Return Results

OpenSearch should never bypass content repository security.

---

### 7. Re-indexing Strategy

Documents are permanent.
Indexes are rebuildable.

When embedding models change:

Document
↓
Chunking
↓
New Embeddings
↓
Re-index OpenSearch

The original content remains unchanged.

---

## ECM Architecture Mapping

Current Vision:

Document Upload
↓
OCR
↓
Chunking
↓
Bedrock Embeddings
↓
OpenSearch Vector Index
↓
Hybrid Search
↓
RAG

---

## FileNet Analogy

FileNet:
System of Record

OpenSearch:
Search and Retrieval Layer

Future Django ECM:
Django Repository
+
OpenSearch Search Platform
+
Bedrock AI Services

---

## Architect Notes

1. OpenSearch is not the source of truth.
2. OpenSearch is a search optimization layer.
3. Chunk design is more important than document design for AI search.
4. Security filtering must always be enforced.
5. Hybrid search is generally preferred over pure vector search.

---

## Biggest Takeaway

OpenSearch does not search documents.

OpenSearch searches indexed chunks and returns the most semantically relevant content for retrieval and RAG workflows.

---

## Questions for Day 4

1. Which Bedrock model should generate embeddings?
2. Which Bedrock model should answer questions?
3. How does Bedrock interact with OpenSearch?
4. What should run in Django versus Bedrock?
5. How should Bedrock be integrated into an Enterprise Content Management platform?