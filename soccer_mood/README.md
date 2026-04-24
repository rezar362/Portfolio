# ⚽ SoccerMood — Real-time Player Emotion Analysis

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/soccer-mood/soccer_mood.ipynb)

## Overview
Computer vision pipeline that analyzes soccer player emotions from match footage in real-time. Extracts frames from video, detects faces, classifies emotions, and generates an emotion timeline across the match.

## Demo
UEFA Euro 2024 — Portugal vs France Penalty Shootout
- 92 frames extracted from 3-minute clip
- 94 faces detected
- Dominant emotion: **SAD** (penalty pressure)
- Average sentiment score: **-0.178** (high-stress match)

## Key Moments Detected
| Moment | Timestamp | Emotion |
|--------|-----------|---------|
| Happiest | t=47s | HAPPY |
| Saddest | t=93s | SAD |
| Angriest | t=31s | ANGRY |
| Most Fearful | t=108s | FEAR (Mbappé before penalty) |

## Pipeline
1. **Video Download** — yt-dlp downloads YouTube match footage
2. **Frame Extraction** — OpenCV extracts 1 frame every 2 seconds
3. **Face Detection** — OpenCV detector locates faces in each frame
4. **Emotion Recognition** — DeepFace classifies 7 emotions per face
5. **Sentiment Scoring** — Maps emotions to sentiment score (-1 to +1)
6. **Dashboard** — Timeline, distribution, and key moment visualization

## Emotions Detected
- 😊 Happy — goal celebrations, saves
- 😢 Sad — missed penalties, defeats
- 😡 Angry — frustration, disputes
- 😨 Fear — pressure moments before penalty
- 😮 Surprise — unexpected events
- 😐 Neutral — focused, composed
- 🤢 Disgust — disagreement with referee

## Real Product Applications
- **Broadcast analytics** — overlay emotion data on live TV
- **Team psychology** — coaches monitor player mental state
- **Player scouting** — identify composure under pressure
- **Fantasy sports** — emotion as performance signal

## Tech Stack
Python, DeepFace, OpenCV, yt-dlp, Matplotlib, Google Colab

## Results
| Metric | Value |
|--------|-------|
| Frames processed | 92 |
| Faces detected | 94 |
| Emotions classified | 7 |
| Processing time | ~5 min on CPU |
| Avg sentiment | -0.178 (high pressure match) |
