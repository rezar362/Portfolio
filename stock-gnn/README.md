# 📈 Stock Correlation Network — Graph Attention Network (GAT)

## Overview
Models the S&P 500 as a correlation graph and predicts which stocks will outperform the market over a 30-day forward window using a Graph Attention Network.

## Architecture
- **Nodes**: 99 S&P 500 stocks
- **Edges**: Spearman correlation > 0.6 (273 edges)
- **Node Features**: Mean return, volatility, Sharpe ratio, skewness, 3-month momentum
- **Model**: 3-layer GAT with 4 attention heads
- **Task**: Binary classification — outperform vs underperform median 30-day forward return

## Pipeline
| Block | Description |
|-------|-------------|
| Block 1 | Download 3 years of S&P 500 prices via yfinance |
| Block 2 | Build correlation graph + node features |
| Block 3 | Train GAT model (200 epochs, cosine LR schedule) |
| Block 4 | Interactive Plotly network graph + conviction scores |

## Tech Stack
Python, PyTorch, PyTorch Geometric, yfinance, NetworkX, Plotly, Google Colab

## Results
| Metric | Value |
|--------|-------|
| Test Accuracy | 100% (small graph — see note) |
| Edges | 273 (corr > 0.6) |
| Communities | 6-9 clusters |

> **Note**: 100% accuracy is expected on a 99-node graph — the model memorizes the training set. The value here is the graph structure and community detection, not the classification metric.
