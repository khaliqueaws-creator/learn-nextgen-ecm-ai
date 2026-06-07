# Day 6 - Intelligent Metadata Extraction

## Executive Summary

This session focused on how AI can automatically classify documents, extract metadata, generate summaries, and improve enterprise search.

Key objective:

Understand how Bedrock-powered metadata extraction fits into a modern Enterprise Content Management platform.

---

## The Traditional ECM Problem

Historically, document metadata was entered manually.

Example:

Document: Microsoft Invoice

Manual Entry:
- Document Type = Invoice
- Vendor = Microsoft
- Amount = $12,000
- Department = IT

This process becomes expensive and error-prone at scale.

---

## Traditional vs Modern ECM

Traditional:

Document
↓
Human Indexing
↓
Repository

Modern:

Document
↓
OCR
↓
AI Classification
↓
AI Metadata Extraction
↓
Repository

---

## What is Metadata Extraction?

AI reads document content and extracts structured information.

Example OCR Text:

Invoice Number: INV-12345
Vendor: Microsoft
Amount: $12,450
Due Date: June 30, 2026

AI Output:

```json
{
  "document_type": "Invoice",
  "invoice_number": "INV-12345",
  "vendor": "Microsoft",
  "amount": 12450,
  "due_date": "2026-06-30"
}
```

---

## What is Classification?

Classification determines the type of document.

Examples:

- Invoice
- Contract
- Policy
- Resume
- Employee Record
- Purchase Order

Example:

Document:
Employee Benefits Handbook

Classification:

```json
{
  "document_type": "Policy",
  "department": "HR",
  "subcategory": "Benefits"
}
```

---

## Classification vs Metadata Extraction

Classification answers:

"What is this document?"

Metadata Extraction answers:

"What important information is inside this document?"

---

## Workflow Architecture

```text
PDF Upload
      │
      ▼
 OCR Extraction
      │
      ▼
 Bedrock
      │
      ├── Classification
      │
      └── Metadata Extraction
      │
      ▼
 PostgreSQL
      │
      ▼
 OpenSearch
```

---

## Django ECM Upload Flow

```text
User Upload
      │
      ▼
 Django
      │
      ▼
 OCR
      │
      ▼
 Bedrock
      │
      ▼
 JSON Metadata
      │
      ▼
 PostgreSQL
      │
      ▼
 OpenSearch
```

---

## Example Metadata Extraction

### Invoice

```json
{
  "document_type": "Invoice",
  "vendor": "Microsoft",
  "amount": 12000,
  "invoice_date": "2026-05-31",
  "department": "IT"
}
```

### Contract

```json
{
  "document_type": "Contract",
  "vendor": "AWS",
  "effective_date": "2026-01-01",
  "expiration_date": "2027-01-01"
}
```

### HR Policy

```json
{
  "document_type": "Policy",
  "department": "HR",
  "policy_type": "Benefits"
}
```

---

## Prompt Design

Bad Prompt:

Read this document.

Better Prompt:

Return JSON and extract:

- document_type
- vendor
- invoice_number
- amount
- effective_date
- expiration_date

Structured prompts create structured outputs.

---

## Confidence Scores

Enterprise systems often evaluate confidence.

Example:

```json
{
  "document_type": "Invoice",
  "confidence": 0.97
}
```

---

## Human Review Workflow

If confidence > 90%

Auto Approve

If confidence < 90%

Human Review Queue

Workflow:

Document
↓
AI Extraction
↓
Confidence Check
↓
Auto Approve OR Human Review

---

## Storage Strategy

Store in PostgreSQL:

- document_type
- document_subtype
- department
- vendor
- effective_date
- expiration_date
- summary
- tags
- ai_confidence
- ai_model
- ai_processed_date

Index into OpenSearch:

- Metadata
- OCR text
- Summary
- Tags
- Chunks
- Embeddings

Architect Principle:

PostgreSQL = Source of Truth
OpenSearch = Search Layer

---

## Realistic Phase 1 AI Features

- Auto Document Type Detection
- Auto Vendor Detection
- Auto Date Extraction
- AI Generated Summary
- Auto Tagging
- Contract Expiration Detection
- Policy Categorization

---

## Architecture Diagram

```text
                 Upload
                    │
                    ▼
              Django Portal
                    │
                    ▼
                  OCR
                    │
                    ▼
             AWS Bedrock
            ┌────────────┐
            │Classify    │
            │Extract     │
            └─────┬──────┘
                  │
                  ▼
            PostgreSQL
                  │
                  ▼
             OpenSearch
```

---

## Biggest Takeaway

RAG helps users find answers.

Metadata Extraction helps users find documents.

In many ECM implementations, metadata extraction delivers business value before RAG because it immediately improves indexing, search, routing, and compliance.