# 🎯 Uplift Modeling — Ad Campaign Optimization

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/uplift-modeling/uplift_modeling.ipynb)

## Overview
Causal ML system that identifies **persuadable users** in ad campaigns — users who will convert only if shown an ad. Built on Criteo's real ad exposure dataset (500K users) using scikit-uplift and LightGBM.

## The Problem
Showing ads to everyone wastes budget on:
- **Sure Things** — buy regardless (wasting ad spend)
- **Lost Causes** — won't buy regardless
- **Do Not Disturb** — less likely to buy if shown an ad

Only **Persuadables** should be targeted.

## Results
| Metric | Value |
|--------|-------|
| CVR — Untargeted | 0.26% |
| CVR — Targeted (top 25%) | 0.51% |
| CVR Improvement | +96% |
| Ad Spend Saved | 75% |
| Persuadables Identified | 25,001 / 100,000 |

## How It Works
1. **Data** — 500K users sampled from Criteo Uplift v2 dataset (real ad exposure data)
2. **Treatment** — 50% shown ad, 50% control group
3. **Models** — Solo Model (S-learner) and Two Models (T-learner) using LightGBM
4. **Scoring** — each user gets an uplift score = predicted causal effect of ad exposure
5. **Targeting** — only show ads to top 25% by uplift score

## User Segments
- **Persuadables (top 25%)** — target these
- **Neutral (middle 50%)** — optional
- **Do Not Disturb (bottom 25%)** — never target

## Tech Stack
Python, scikit-uplift, LightGBM, Criteo Uplift Dataset, Matplotlib, Google Colab

## Dataset
- **Criteo Uplift v2** — real anonymized ad exposure data from Criteo
- 500K users sampled from 13M total
- Features: 12 anonymized user behavior features (f0-f11)
- Labels: treatment (ad shown), conversion (purchase), visit
