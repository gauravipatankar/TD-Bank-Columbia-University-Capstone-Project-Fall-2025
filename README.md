# Forecasting Customer Financial Behavior
### A Two-Phase Framework Using Classical Time Series & Deep Learning

**Capstone Project – Columbia University (DSI) | Industry Partner: TD Bank**

---

## Project Overview
This project aims to forecast customer spending behavior to support **risk management, liquidity planning, and personalized financial services** for a retail bank.

We propose a **two-phase forecasting framework**:
1. **Cluster-level forecasting** using classical time series models to capture stable, aggregate spending patterns.
2. **Individual-level forecasting** using deep learning models (LSTM, Transformer) to model nuanced customer behavior.

This approach balances **interpretability, scalability, and predictive accuracy**.

---

## Dataset
- **Source:** Public bank transaction dataset  
- **Time span:** 2010–2020  
- **Granularity:** Transaction-level data aggregated to **monthly spending per customer**

Due to size constraints, raw data is hosted externally (see `data/README.md`).

---

## Preprocessing & Feature Engineering
- Aggregated transactions to monthly totals per customer
- Handled missing values and extreme outliers
- Engineered financial behavior features:
  - Income utilization ratio
  - Debt-to-income ratio
  - Credit utilization ratio
  - Multi-card usage indicator

EDA revealed strong **seasonality and behavioral heterogeneity**, motivating segmentation.

---

## Customer Segmentation
- Applied **PCA on 36 engineered features** (retained top 3 components)
- Clustered customers into **4 personas** using K-Means:
  1. Regular Spenders
  2. Conservative Budgeters
  3. Selective High-Value Purchasers
  4. Debt-Burdened Consistent Spenders

Segmentation enabled more stable cluster-level forecasting and targeted business insights.

---

## Phase 1: Cluster-Level Forecasting (Classical Models)
**Models evaluated:**
- SARIMA
- Prophet
- Holt-Winters

**Key result:**  
Holt-Winters achieved the **lowest MAPE across all clusters (≈1.1–1.5%)**, accurately capturing trend and seasonality.

Cluster-level models provide:
- Strong interpretability
- Low computational cost
- Reliable aggregate forecasts

---

## Phase 2: Individual-Level Forecasting (Deep Learning)

### LSTM
- 12-month rolling input windows
- Trained with MSE loss and early stopping
- Captures temporal dependencies but sensitive to outliers

### Transformer
- Encoder-only architecture
- 2 layers, 4 attention heads, positional embeddings
- More robust to irregular spending patterns

**Best performing model:** Transformer  
- MAE ≈ $606  
- MAPE ≈ 18–19%  
- Lightweight training (~3 minutes on minimal GPU)

---

## Evaluation Strategy
- Rolling-window cohort-based train/validation/test split
- Metrics used:
  - MAE
  - MSE
  - RMSE
  - MAPE

Classical models excelled at **segment-level stability**, while deep learning models improved **individual personalization**.

---

## Key Insights & Business Implications
- Classical models are effective for **segment trends** but limited by univariate assumptions
- Individual spending depends on **multiple behavioral and financial drivers**
- Deep learning models better capture this complexity
- The two-phase framework enables **scalable personalization without sacrificing interpretability**

---

## Future Work
- Robust outlier handling for extreme spending events
- Improved feature selection and multicollinearity checks
- Longer histories and additional behavioral signals
- Hybrid approaches combining classical + neural forecasts

---

## Attribution
This repository is a **fork of the original team capstone repository**.  
Original work completed collaboratively as part of a semester-long project.

Team members:  
**Gauravi Patankar**, Vi Mai, Zekai Su, Qinghui Zeng, Anouksha Rajesh

Faculty Mentor: Yining Liu  
Industry Mentors: Michael Borish, Sandeep Mandala
