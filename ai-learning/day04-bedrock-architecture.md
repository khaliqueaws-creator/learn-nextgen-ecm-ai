# Day 4 - AWS Bedrock Architecture

## Executive Summary

This session focused on understanding AWS Bedrock's role within an AI-powered Enterprise Content Management platform.

Key objective:

Understand how Django, OpenSearch, and Bedrock work together to deliver semantic search, metadata extraction, and Retrieval-Augmented Generation (RAG).

---

## Key Concepts Learned

### 1. What is AWS Bedrock?

AWS Bedrock is a managed AI platform.

Think of it as:

- EC2 = Compute Platform
- RDS = Database Platform
- Bedrock = AI Platform

Bedrock hosts multiple AI models while AWS manages scaling, security, monitoring, and API access.

---

### 2. Embedding Models vs Foundation Models

Embedding Models:

Purpose:

Text -> Vector

Example:

- Amazon Titan Embeddings

Used for:

- Semantic Search
- Vector Search
- RAG Retrieval

Foundation Models:

Purpose:

Question -> Answer

Examples:

- Amazon Nova
- Claude
- Llama

Used for:

- Summarization
- Reasoning
- Question Answering
- Metadata Extraction

---

### 3. System Responsibilities

Django Responsibilities:

- Authentication
- Authorization
- Upload
- OCR orchestration
- OpenSearch integration
- Bedrock integration
- User interface

OpenSearch Responsibilities:

- Store chunks
- Store vectors
- Hybrid search
- Similarity search
- Ranking

Bedrock Responsibilities:

- Embeddings
- Classification
- Metadata extraction
- Summarization
- Answer generation

---

### 4. Metadata Extraction

Example:

Invoice PDF

OCR Output:

Vendor: Microsoft
Amount: $12,000

Bedrock Output:

```json
{
  "document_type": "Invoice",
  "vendor": "Microsoft",
  "amount": 12000
}
```

---

### 5. Classification

Example:

Document:

Health Insurance Policy

Bedrock Classification:

- Policy
- HR
- Benefits

---

### 6. Security Architecture

Correct Flow:

User
↓
Security Validation
↓
OpenSearch
↓
Authorized Chunks
↓
Bedrock

Bedrock should never receive unauthorized content.

---

### 7. Cost Optimization

Avoid:

Every Search
↓
Bedrock

Prefer:

Search
↓
OpenSearch

Only use Bedrock when AI reasoning is required.

---

## Architecture Diagram

```text
                    Django
                       │
        ┌──────────────┼──────────────┐
        │              │              │
        ▼              ▼              ▼
  PostgreSQL     OpenSearch      Bedrock
        │              │              │
 Documents      Find Information  Understand
 Metadata       Search Chunks     Generate Answers
 Security       Vector Search     Extract Metadata
```

---

## Enterprise ECM Mapping

FileNet-style architecture:

```text
Repository of Record
        ↓
Search and Retrieval Layer
        ↓
AI Services
```

NextGen ECM architecture:

```text
Django Repository
        ↓
OpenSearch
        ↓
AWS Bedrock
```

---

## Biggest Takeaway

OpenSearch finds information.

Bedrock understands information.

Django orchestrates everything.

---

## Questions for Future Learning

1. Which Bedrock model should generate embeddings?
2. Which Bedrock model should answer questions?
3. What should run inside Django versus Bedrock?
4. How should IAM be handled for Bedrock access?
5. How can Bedrock costs be controlled in an enterprise ECM platform?
