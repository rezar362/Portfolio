# 🎙️ EarningsMood — CEO Voice Mood Analysis on Earnings Calls

[Open in Colab](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/earnings-mood/earnings_mood.ipynb)

## Overview
Audio analysis pipeline that extracts acoustic features from FAANG Q4 2025 earnings calls and correlates CEO vocal mood with next-day stock price reaction. Achieves Spearman r=0.866 between voice confidence score and stock return.

## Key Finding
**Confident vocal tone → positive stock return. Hesitant vocal tone → negative stock return.**

| Company | Mood | Stock Return |
|---------|------|-------------|
| Apple (AAPL) | Confident | -0.38% |
| Amazon (AMZN) | Confident | **+4.00%** |
| Alphabet (GOOGL) | Confident | -0.54% |
| Meta (META) | Hesitant | -2.95% |
| Netflix (NFLX) | Hesitant | -2.13% |

## Correlation
| Metric | Value |
|--------|-------|
| Spearman r | **+0.866** |
| p-value | 0.058 |
| Pearson r | +0.727 |

## Pipeline
1. **Download** — yt-dlp downloads first 5 minutes of each earnings call from YouTube
2. **Extract** — librosa extracts acoustic features per 30-second segment
3. **Cluster** — KMeans (k=4) clusters segments into mood states
4. **Score** — mood score per company (Confident=+1, Hesitant=-0.5)
5. **Correlate** — mood score vs next-day stock return via yfinance

## Acoustic Features Extracted
- **Pitch (F0)** — mean and variance of fundamental frequency
- **Energy (RMS)** — vocal loudness and confidence
- **Pause ratio** — proportion of silence (hesitation indicator)
- **Voiced ratio** — proportion of speech vs silence
- **MFCCs** — 13 mel-frequency cepstral coefficients (timbre/vocal quality)
- **Spectral centroid & rolloff** — brightness and frequency distribution
- **Zero crossing rate** — speech rate proxy

## Mood States
- 😊 **Confident** — high energy, low pause ratio
- ⚡ **Energetic** — high energy, higher pauses
- 😟 **Hesitant** — low energy, high pause ratio
- 😰 **Stressed** — low energy, low voiced ratio

## Acoustic Insights
| Company | Pitch | Energy | Pause Ratio | Mood |
|---------|-------|--------|-------------|------|
| AAPL | 176Hz | 0.076 | 20.1% | Confident |
| AMZN | 119Hz | 0.069 | 11.6% | Confident |
| GOOGL | 137Hz | 0.053 | 21.0% | Confident |
| META | 189Hz | 0.035 | 31.4% | Hesitant |
| NFLX | 114Hz | 0.017 | 40.0% | Hesitant |

## Real Product Applications
- **Quant signal** — voice mood as alpha factor in earnings trading strategy
- **Risk management** — flag hesitant management tone before position sizing
- **IR analytics** — help companies improve executive communication
- **Real-time alerts** — live mood scoring during earnings calls

## Tech Stack
Python, librosa, KMeans, PCA, yfinance, yt-dlp, Matplotlib, Google Colab

## Dataset
- FAANG Q4 2025 earnings calls from YouTube
- 5 companies × 9 segments × 30 seconds = 45 total segments
- Features: 15 acoustic features per segment
