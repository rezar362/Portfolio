# 📊 10-K RAG System — Nasdaq 100

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/10k-rag/RAG_10K.ipynb)

## Overview
Retrieval-Augmented Generation system over SEC 10-K annual filings for the top 20 Nasdaq 100 companies. Ask natural language questions and get grounded answers sourced directly from official filings.

## Example Queries
- "What are the main risk factors for NVIDIA?"
- "How does Apple describe its competition?"
- "Compare AI strategy across NVIDIA, Microsoft and Google"
- "Which companies mention supply chain risks?"
- "Compare revenue growth across Apple, Amazon and Meta"

## How It Works
1. **Ingest** — Downloads 10-K filings from SEC EDGAR for top 20 Nasdaq 100 companies
2. **Chunk** — Splits filings into 150-word overlapping chunks
3. **Embed** — Encodes chunks using `all-MiniLM-L6-v2` sentence embeddings
4. **Store** — Persists 3,334 chunks in ChromaDB vector database
5. **Retrieve** — Finds most relevant chunks via cosine similarity search
6. **Generate** — Passes retrieved context to Llama 3.1 via Groq API for grounded answers

## Companies Covered
AAPL, MSFT, NVDA, GOOGL, AMZN, META, TSLA, AVGO, COST, AMD,
NFLX, ADBE, QCOM, INTU, TXN, ISRG, BKNG, AMAT, MU, LRCX

## Tech Stack
Python, ChromaDB, sentence-transformers, Groq API (Llama 3.1), SEC EDGAR, LangChain, Google Colab

## Results
| Metric | Value |
|--------|-------|
| Companies | 20 Nasdaq 100 |
| Total chunks | 3,334 |
| Avg chunks/company | 166 |
| Embedding model | all-MiniLM-L6-v2 (384 dims) |
| LLM | Llama 3.1 8B via Groq |

## Setup
1. Get a free Groq API key at [console.groq.com](https://console.groq.com/keys)
2. Add it to Colab Secrets as `10K_Grok`
3. Run blocks 1 → 2 → 3 → 4 in order
4. All data persists to Google Drive automatically
