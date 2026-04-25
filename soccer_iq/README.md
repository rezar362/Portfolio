# 🧠 SoccerIQ — Reinforcement Learning for Pass Strategy Optimization

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/soccer-iq/soccer_iq.ipynb)

## Overview
Deep Q-Network (DQN) agent that learns optimal passing strategies against specific opponents using StatsBomb World Cup 2022 data. The agent learns to avoid high-pressure zones where interception probability is high and find the most efficient path to goal.

## Key Results

| Opponent | Goal Rate | Difficulty |
|----------|-----------|------------|
| Argentina | 75% | ⭐⭐⭐⭐⭐ Hardest |
| Brazil | 78.5% | ⭐⭐⭐⭐ |
| England | 83% | ⭐⭐⭐ |
| Morocco | 85% | ⭐⭐⭐ |
| France | 87% | ⭐⭐ |
| USA | 95% | ⭐ Easiest |

**Argentina hardest to break down — matches real World Cup 2022 result (Argentina won)**

## Environment
- **State**: current zone (one-hot) + opponent pressure per zone (12 features total)
- **Actions**: pass to any of 6 zones or shoot at goal (7 actions)
- **Reward**: +10 goal, -5 interception, +1 progressive pass, -1 backward pass, -0.5 per step
- **Interception**: probability = opponent pressure × 0.8 — high pressure zones are genuinely dangerous

## Zones
