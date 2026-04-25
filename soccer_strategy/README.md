# ⚽ Soccer Pass Optimization — Dijkstra + XGBoost

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/soccer-strategy/soccer_strategy.ipynb)

## Overview
Two-stage soccer passing strategy system built on StatsBomb World Cup 2022 data. First uses Dijkstra pathfinding to find optimal passing routes, then upgrades to XGBoost to learn opponent-specific strategies from successful attacking sequences.

## Key Results
- **68,515 passes** across 64 World Cup 2022 matches
- **32 teams** with individual passing profiles
- **Opponent-aware routing** — genuinely different paths vs different opponents
- **XGBoost accuracy** — predicts next optimal zone from current position + opponent pressure

## Example: Iran vs Argentina vs USA
| Starting Zone | vs Argentina | vs USA |
|--------------|-------------|--------|
| Mid (Right) | Mid Right → Mid Left → Att Left → GOAL | Mid Right → Att Left → GOAL |
| Def (Right) | Def Right → Mid Right → Att Left → GOAL | Def Right → Att Left → GOAL |

**Key insight:** vs Argentina, Iran should build slower through midfield (Argentina pressure 0.154 in Mid Left). vs USA, Iran can attack more directly (USA weaker in
