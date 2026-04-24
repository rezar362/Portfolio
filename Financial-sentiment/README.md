# 🏦 Financial Sentiment Analysis — DistilBERT Fine-Tuning

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/Financial-sentiment/FInancial_sentiment.ipynb)

## Overview
Fine-tuned DistilBERT on Financial PhraseBank for 3-class financial sentiment classification (negative, neutral, positive).

## Dataset
- **Financial PhraseBank** — 2,264 sentences from Reuters financial news
- Annotated by 16 financial analysts (AllAgree subset — highest quality)
- Labels: Negative (303) / Neutral (1,391) / Positive (570)

## Model
- **Base**: DistilBERT (66M parameters)
- **Task**: 3-class sequence classification
- **Fine-tuning**: 5 epochs, AdamW optimizer, linear warmup scheduler

## Results
| Metric | Value |
|--------|-------|
| Val Accuracy | 97.4% |
| Test Accuracy | 95.6% |

## Tech Stack
Python, PyTorch, HuggingFace Transformers, DistilBERT, Google Colab
