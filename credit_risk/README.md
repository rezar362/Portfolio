# Credit Risk ML Pipeline — Lending Club

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/rezar362/Portfolio/blob/main/credit_risk/credit_risk.ipynb)

End-to-end machine learning pipeline for credit default prediction on real Lending Club loan data — covering EDA, feature engineering, clustering, modeling, evaluation, and SHAP explainability.

---

## What it does

- Downloads and processes **115,979 real US loan applications** from Lending Club 2018 Q4
- Full feature engineering pipeline: imputation, Winsorization, scaling, encoding, feature selection
- Unsupervised borrower segmentation via KMeans and DBSCAN on PCA + UMAP projections
- LightGBM classifier with SMOTE balancing and 5-fold stratified cross-validation
- Comprehensive evaluation: ROC-AUC, gains chart, lift, calibration, risk bucketing
- SHAP explainability: beeswarm, waterfall, dependence plots, decile analysis

---

## Results

| Metric | Value |
|---|---|
| ROC-AUC | 0.709 |
| CV AUC | 0.710 ± 0.005 |
| F1 (default class) | 0.359 |
| Average Precision | 0.299 |
| Top 10% captures | 25% of defaults (lift 2.5x) |
| Top 30% captures | 55% of defaults (lift 1.8x) |
| D1 default rate | 3.0% |
| D10 default rate | 34.5% |

The model creates an **11.5x spread** between the safest and riskiest decile — D10 borrowers default at 34.5% vs 3.0% for D1.

---

## SHAP Findings

| Feature | Mean \|SHAP\| | Direction |
|---|---|---|
| int_rate | 0.303 | Higher → more risk |
| term | 0.205 | 60-month → more risk |
| sub_grade | 0.162 | Higher grade → more risk |
| loan_to_income | 0.105 | Higher → more risk |
| inq_last_6mths | 0.086 | More inquiries → more risk |
| num_actv_rev_tl | 0.085 | More active accounts → less risk |
| emp_length | 0.077 | Longer employment → less risk |

**Key insight:** Interest rate, loan term, and sub-grade together dominate the model — they capture Lending Club's own internal risk assessment. A 27% rate + 60-month term alone contributes +1.0 in log-odds before any borrower-level features are considered.

---

## Risk Segments

| Decile | Default Rate | Action |
|---|---|---|
| D1–D3 | 3–7% | Approve |
| D4–D6 | 9–18% | Review |
| D7–D8 | 15–24% | Caution |
| D9–D10 | 22–35% | Decline |

---

## Pipeline — 9 blocks

| Block | Description |
|---|---|
| 1 | Mount Google Drive, persistent storage, config |
| 2 | Install dependencies, imports, plot style |
| 3 | Download Lending Club 2018 Q4, target engineering, feature selection, cleaning |
| 4 | EDA — distributions, correlations, missing values, outliers, categorical analysis |
| 5 | Feature engineering — KNN imputation, Winsorization, scaling, encoding, MI selection, SMOTE |
| 6 | Clustering — PCA, UMAP, KMeans elbow, DBSCAN, borrower segmentation |
| 7 | Modeling — LightGBM (class_weight vs SMOTE), 5-fold CV, learning curves, threshold tuning |
| 8 | Evaluation — ROC, PR curve, calibration, gains chart, lift, risk bucketing |
| 9 | SHAP — beeswarm, bar, waterfall, dependence, group comparison, decile analysis |

---

## Dataset

- **Source:** Lending Club 2018 Q4 — publicly available US peer-to-peer lending data
- **Size:** 128,414 loans downloaded → 115,979 closed loans (Fully Paid or Charged Off)
- **Target:** Binary — Charged Off (default) = 1, Fully Paid = 0
- **Class imbalance:** 85.4% Fully Paid / 14.6% Charged Off
- **Features:** 35 engineered features covering loan terms, borrower profile, and credit history
- No login or Kaggle account required — downloads directly in Block 3

---

## Feature Engineering

- **Imputation:** Median for high-missingness (>30%), KNN (k=5) for low-missingness, mode for categoricals
- **Winsorization:** Clip at 1st–99th percentile — avg skew reduced significantly
- **Scaling:** RobustScaler (median/IQR based — better than StandardScaler for financial data)
- **Encoding:** Ordinal for grade/sub_grade, target encoding with smoothing for addr_state, one-hot for the rest
- **Selection:** Variance threshold + mutual information — top 30 features retained
- **Derived features:** loan_to_income, revol_to_total_bal, util_gap, open_acc_ratio, delinq_rate, inq_pressure

---

## Stack

| Component | Library |
|---|---|
| Modeling | LightGBM |
| Explainability | SHAP |
| Imbalance | imbalanced-learn (SMOTE) |
| Dimensionality reduction | PCA, UMAP |
| Clustering | KMeans, DBSCAN |
| Data | Pandas, NumPy, SciPy |
| Visualization | Matplotlib, Seaborn |
| Storage | Google Drive (persistent across sessions) |

---

## Quickstart

1. Click **Open in Colab** above
2. Set runtime to **GPU** (optional — CPU works fine for this pipeline)
3. Run blocks 1–9 in order
4. Mount Google Drive when prompted in Block 1

All data, models, SHAP values, and plots persist to Google Drive automatically. Rerunning any block after the first session loads from cache.

---

## License

MIT
