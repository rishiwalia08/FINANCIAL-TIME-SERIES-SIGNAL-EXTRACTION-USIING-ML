# FINANCIAL-TIME-SERIES-SIGNAL-EXTRACTION-USIING-ML

# 📈 Financial Time Series Signal Extraction and Backtesting using Machine Learning

## 📌 Overview

This project implements an **end-to-end machine learning pipeline** for extracting **trading signals** from financial time series data and evaluating them using **walk-forward backtesting**.

Instead of predicting exact prices, the project frames the problem as a **signal classification task (BUY / SELL / HOLD)** using technical indicators, volatility measures, and market context features.
The approach is validated on **NIFTY 50 daily data**.

---

## 🎯 Objectives

* Extract meaningful trading signals from noisy financial time series
* Avoid data leakage using proper time-series validation
* Compare linear and non-linear ML models
* Evaluate strategies using **risk-adjusted metrics** rather than accuracy alone

---

## 🧠 Key Concepts Used

* Financial time series analysis
* Technical indicators (momentum, trend, volatility)
* Supervised classification for trading signals
* Time-based train/test split
* Walk-forward backtesting
* Sharpe ratio evaluation

---

## 📂 Project Structure

```
.
├── data/                 # Raw or downloaded market data (optional)
├── notebooks/            # Jupyter notebooks for experiments
├── src/                  # Feature engineering & modeling code (optional)
├── README.md             # Project documentation
└── requirements.txt      # Python dependencies
```

---

## 📊 Data

* **Instrument**: NIFTY 50 Index
* **Frequency**: Daily
* **Source**: Yahoo Finance (`yfinance`)
* **Period**: 2013 – Present

A separate raw copy of the data is maintained for visualization and analysis to avoid accidental data loss during preprocessing.

---

## ⚙️ Feature Engineering

### Price-Based Features

* Log returns
* Rolling mean and rolling standard deviation
* Rolling normalized returns

### Technical Indicators

* **RSI (14)** – momentum indicator
* **MACD (12, 26, 9)** – trend indicator
* **Bollinger Bands (20)** – volatility regime
* **ATR (14)** – market volatility

### Market Context

* Volume percentage change
* Volatility regime via India VIX (when available)

All features use **only past information**, ensuring **no look-ahead bias**.

---

## 🏷️ Signal Labeling

The task is formulated as a **3-class classification problem**:

| Label | Meaning |
| ----- | ------- |
| `1`   | BUY     |
| `0`   | HOLD    |
| `-1`  | SELL    |

Signals are generated using **future log returns**:

[
r_{t+h} = \log\left(\frac{P_{t+h}}{P_t}\right)
]

Where:

* `h` = holding period (e.g. 1-day or 5-day)

Thresholds are applied to filter out noisy price movements.

---

## ⏱️ Train–Test Split

* **Time-based split (80% / 20%)**
* Training data strictly precedes test data
* Prevents data leakage and simulates real trading conditions

---

## 🤖 Models Used

### 1️⃣ Logistic Regression (Baseline)

* Provides interpretability
* Used to validate existence of predictive signal
* Features scaled using `StandardScaler`

### 2️⃣ Random Forest Classifier

* Captures non-linear feature interactions
* No feature scaling required
* Used as the primary ML model

---

## 🔍 Feature Importance

Random Forest feature importance is used to analyze which indicators contribute most to the model’s decisions.
This improves interpretability and validates feature engineering choices.

---

## 📈 Backtesting Methodology

* Signals are applied only on the **test period**
* Strategy returns are computed as:

[
\text{strategy return} = \text{signal} \times \text{market return}
]

### Evaluation Metrics

* Cumulative returns (strategy vs market)
* Sharpe ratio (risk-adjusted performance)

This ensures the model is evaluated on **economic usefulness**, not just classification accuracy.

---

## 📊 Results (High-Level)

* Strategy performance varies across market regimes
* Non-linear models outperform linear baseline in signal quality
* Risk-adjusted evaluation highlights strengths and limitations clearly

*(Exact results may vary depending on threshold and holding period.)*

---

## ⚠️ Limitations

* No transaction costs included (can be added)
* Strategy assumes instant execution at close prices
* Signals are evaluated on index data, not individual stocks
* Not intended for live trading without further validation

---

## 🚀 Future Improvements

* Add transaction cost and slippage modeling
* Regime-aware models (bull / bear / sideways markets)
* Gradient boosting models (XGBoost, LightGBM)
* Multi-horizon signal comparison
* Portfolio-level backtesting

---

## 🛠️ Tech Stack

* Python
* pandas, numpy
* scikit-learn
* pandas-ta
* matplotlib
* yfinance

---

## 📜 Disclaimer

This project is **for educational and research purposes only**.
It does **not** constitute financial advice or a production-ready trading system.

---

## 🙌 Author

Built as a learning-focused quant ML project to understand **financial time series modeling, signal extraction, and backtesting**.

