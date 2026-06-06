# Day 5 - RAG Implementation

## Executive Summary

This session focused on Retrieval-Augmented Generation (RAG) and how enterprise AI assistants are built.

Key objective:

Understand how OpenSearch retrieval and Bedrock reasoning combine to create accurate AI answers.

---

## What is RAG?

RAG stands for:

Retrieval
Augmented
Generation

---

## The Problem

Question:

"What is our PTO policy?"

Without RAG:

User
↓
Bedrock
↓
Answer

Risk:

Hallucination.

The model may not know the organization's actual policy and may produce an incorrect answer.

---

## The RAG Solution

User
↓
Search Repository
↓
Retrieve Content
↓
Provide Context
↓
Generate Answer

Now the answer is based on enterprise content instead of only model memory.

---

## RAG Components

### Retrieval

OpenSearch finds relevant chunks.

### Augmentation

Retrieved chunks are added to the prompt.

### Generation

Bedrock generates the answer using the supplied context.

---

## Complete RAG Flow

```text
User Question
       │
       ▼
Django
       │
       ▼
Bedrock Embedding Model
       │
       ▼
OpenSearch Vector Search
       │
       ▼
Relevant Chunks
       │
       ▼
Prompt Builder
       │
       ▼
Bedrock Foundation Model
       │
       ▼
Generated Answer
```

---

## Prompt Builder

The prompt builder combines the user's question with retrieved context.

Example:

```text
Context:
Employees receive 20 PTO days annually.

Question:
How many PTO days do employees receive?
```

This grounding significantly improves answer quality.

---

## Chunk-Based Retrieval

Best Practice:

Documents
↓
Chunks
↓
Embeddings
↓
OpenSearch

Search should target chunks rather than entire documents.

Reasons:

- Better accuracy
- Lower token cost
- Faster responses
- More precise citations

---

## Top-K Retrieval

Typical values:

- k = 3
- k = 5
- k = 10

Goal:

Retrieve enough context without overwhelming the model.

Too few chunks may miss context.
Too many chunks may increase cost and reduce answer quality.

---

## Security Filtering

Correct Flow:

Search
↓
Permission Check
↓
Bedrock

Only authorized chunks should be included in prompts.

Bedrock should never receive content the user is not allowed to view.

---

## Enterprise AI Assistants

RAG enables:

- Policy Assistant
- Contract Assistant
- HR Assistant
- Enterprise Search Copilot
- Document Summarization Assistant

---

## Architecture Diagram

```text
User Question
       │
       ▼
Django Portal
       │
       ▼
Bedrock Embedding Model
       │
       ▼
OpenSearch Vector Search
       │
       ▼
Relevant Chunks
       │
       ▼
Prompt Builder
       │
       ▼
Bedrock Foundation Model
       │
       ▼
Generated Answer
       │
       ▼
Django Portal
```

---

## ECM Architecture Mapping

Django:

- Receives user question
- Checks authentication and authorization
- Calls Bedrock for query embeddings
- Calls OpenSearch for retrieval
- Builds prompt
- Calls Bedrock foundation model
- Displays answer

OpenSearch:

- Stores chunks
- Stores vectors
- Performs vector search
- Supports hybrid search

Bedrock:

- Generates embeddings
- Generates final answer
- Performs reasoning over retrieved context

---

## Biggest Takeaway

OpenSearch retrieves.

Bedrock reasons.

Django orchestrates.

RAG connects them.

---

## Questions for Future Learning

1. How should prompts be structured for reliable RAG?
2. How should citations be included in answers?
3. How should failed retrieval be handled?
4. How should user permissions be enforced before Bedrock calls?
5. How should RAG answers be logged for audit purposes?
