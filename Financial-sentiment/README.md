# 🏦 Financial Sentiment Analysis — DistilBERT Fine-Tuning

## What is Fine-Tuning?
Pre-trained language models like DistilBERT are trained on massive general text (Wikipedia, books).
Fine-tuning adapts the model to a specific task by continuing training on domain-specific labeled data.

## Architecture
```
Input Text
    ↓
DistilBERT Tokenizer (WordPiece, max 128 tokens)
    ↓
DistilBERT Encoder (6 transformer layers, 66M parameters)
    ↓
[CLS] token embedding
    ↓
Pre-classifier (Linear + ReLU)
    ↓
Classifier (Linear → 3 classes)
    ↓
Output: Negative / Neutral / Positive
```

## What Changed During Fine-Tuning
| Layer | Pretrained | Fine-Tuned |
|-------|-----------|------------|
| DistilBERT encoder | General language understanding | Adapted to financial text |
| Pre-classifier | Random init | Learned financial sentiment features |
| Classifier | Random init | Maps to 3 sentiment classes |

## Dataset
- **Financial PhraseBank** — 2,264 sentences from Reuters financial news
- Annotated by 16 financial analysts (AllAgree subset — highest quality)
- Labels: Negative (303) / Neutral (1,391) / Positive (570)

## Training
- **Optimizer**: AdamW (lr=2e-5, weight decay=0.01)
- **Scheduler**: Linear warmup then decay
- **Epochs**: 5 with best model saved by val accuracy
- **Batch size**: 16

## Results
| Metric | Value |
|--------|-------|
| Val Accuracy | 97.4% |
| Test Accuracy | 95.6% |
