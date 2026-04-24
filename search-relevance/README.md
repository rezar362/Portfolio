# 🔍 Search Relevance — NGD vs BM25 vs SBERT

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/search-relevance/search_relevance.ipynb)

## Overview
Comparison of three search relevance approaches on Amazon's ESCI dataset (50K query-product pairs): a corpus-adapted Normalized Google Distance (NGD), BM25, and SBERT transformer embeddings.

**Key finding:** Corpus-adapted NGD matches SBERT on NDCG@10 (0.9506 vs 0.9501) with zero training, outperforming BM25 on ranking correlation.

## The Problem
Given a search query like "ps4 controller charger", rank products by relevance:
- **Exact** — directly matches the query
- **Substitute** — different but could replace it
- **Complement** — related accessory
- **Irrelevant** — no relation

## Models Compared

| Model | Description |
|-------|-------------|
| NGD (corpus-adapted) | Co-occurrence statistics from product corpus — no training |
| BM25 | Industry standard keyword search (Elasticsearch, Solr) |
| SBERT | Transformer embeddings — semantic similarity |

## Results

| Model | Spearman | NDCG@10 |
|-------|----------|---------|
| NGD (corpus-adapted) | 0.193 | **0.9506** |
| BM25 | -0.271 | 0.9263 |
| SBERT | **0.345** | 0.9501 |

## Key Insights
- NGD beats SBERT on NDCG@10 with zero training
- BM25 negative Spearman — IDF penalizes frequent terms, inverting rankings for exact matches in focused product catalogs
- SBERT best for global ranking order (Spearman)
- NGD best for top-10 result quality (NDCG) — what users actually see

## NGD Formula
