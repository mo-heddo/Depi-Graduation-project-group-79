# Depi-Graduation-project-group-79

## About the Project

This **Stock Analysis Data Science Project** explores **five years of historical stock data** for all companies in the **S&P 500 index** to uncover market patterns and build predictive models for stock price movement.

Stock market data is inherently noisy, yet it holds valuable insights that can guide investment decisions when analyzed systematically. This project demonstrates how **data science and machine learning** techniques can be applied to financial datasets to analyze, visualize, and predict market trends.

---

### 🧩 Project Overview

* **Dataset:** S&P 500 companies’ daily stock prices (Open, High, Low, Close, Volume) from the past 5 years.

  * Source: [Kaggle – camnugent/sandp500](https://www.kaggle.com/datasets/camnugent/sandp500)
* **Size:** 619,040 rows × 7 columns
* **Tools Used:** Python (NumPy, Pandas, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM)

The dataset is cleaned, analyzed, and transformed to generate powerful technical indicators and temporal features. The processed data is then used to train several machine learning classifiers to predict whether a stock’s **next-day return** will be positive (Up) or negative (Down).

---

###  Objectives

1. Analyze large-scale stock market data efficiently.
2. Generate technical and time-based indicators to capture market behavior.
3. Build classification models to predict the **next-day stock direction**.
4. Evaluate models and interpret feature importance.

---

###  Workflow Summary

#### 1. **Data Loading & Cleaning**

* The dataset was imported using `kagglehub` and cleaned by:

  * Dropping missing values (≈11 NaNs in OHLC columns)
  * Converting dates to `datetime` objects
  * Sorting chronologically by stock symbol and date
* No duplicates found; resulting clean dataset contained **~593,000 rows**.

#### 2. **Exploratory Data Analysis (EDA)**

* **Line charts** showed the performance of the top 5 traded companies (AAPL, FB, BAC, GE, F).
* **Bar charts** of total trading volume highlighted the most active stocks.
* Insights revealed tech companies outperformed industrial and financial sectors.

#### 3. **Feature Engineering**

New features were derived to improve predictive performance:

* **Technical Indicators:**

  * `SMA_20`, `SMA_50`: Capture short- and medium-term trends.
  * `RSI_14`: Measures momentum to identify overbought (>70) or oversold (<30) conditions.
  * `volatility_20`, `volatility_50`: Reflect market stability and risk.
* **Temporal Features:**

  * `day_of_week`, `is_month_end`, `is_quarter_end`
    Capture cyclical behavior and end-of-period market effects.
* **Target Features:**

  * `Next_Day_Return`: Percentage change of next day’s closing price.
  * `Target_UpDown`: Binary label → 1 if return > 0, else 0.

---

###  Key Observations

* **SMA crossovers** (SMA20 > SMA50) indicate bullish trends; cross-downs signal bearishness.
* **RSI peaks and troughs** align with market overreaction and recovery points.
* **Volatility spikes** highlight periods of instability and higher risk exposure.
* **Day-of-week and month-end effects** show mild cyclic behavior — markets tend to dip on Mondays and recover midweek.

---

### 🤖 Machine Learning Models

The project tested three major classification models:

| Model             | Accuracy | Key Traits                                                   |
| ----------------- | -------- | ------------------------------------------------------------ |
| **LightGBM**      | 53.5%    | Fastest and most balanced performance.                       |
| **XGBoost**       | 53.4%    | Strong generalization, interpretable via feature importance. |
| **Random Forest** | 52.8%    | Reliable benchmark model with stable performance.            |

**Top Features by Importance:**

* `RSI_14`
* `volatility_20`
* `SMA_20`
* `daily_return`
* `day_of_week`

Although the accuracy hovers around 53–54%, this is **statistically meaningful** in stock prediction tasks, where random guessing yields 50%. Such a margin can be significant when applied to trading strategies.

---

### 📈 Insights & Conclusions

* Technical indicators (SMA, RSI, Volatility) significantly help models detect price direction trends.
* Time-based features contribute modestly but improve stability.
* Ensemble models like **LightGBM** and **XGBoost** perform best for large, noisy financial datasets.
* Even small accuracy improvements beyond random performance can yield measurable gains in algorithmic trading scenarios.

---

** Machine Learning Model Development and Optimization

This section focuses on predicting the next-day stock movement (Up/Down) using ensemble-based classifiers trained on technical and temporal indicators.

 Objective

Build and optimize machine learning models to identify directional stock trends using features like SMA, RSI, volatility, and time-based patterns.

 Features Used

volatility_20, volatility_50, SMA_20, SMA_50, RSI_14,
day_of_week, is_month_end, is_quarter_end, daily_return

Target:
Target_UpDown = 1 (Up) if Next_Day_Return > 0, else 0 (Down)

 Models Compared
Model	Description	Accuracy
🥇 LightGBM	Fast, accurate, handles imbalance well	0.535 → 0.536 (tuned)
🥈 XGBoost	Reliable, interpretable gradient booster	0.5349
🥉 Random Forest	Stable ensemble baseline	0.5279
⚙️ Tuning & Evaluation

Used TimeSeriesSplit + GridSearchCV for LightGBM optimization.

Best Parameters: max_depth=7, learning_rate=0.05, n_estimators=200, class_weight='balanced'

Slight accuracy gain (0.535 → 0.536).

Evaluation metrics: Accuracy, F1-score, Confusion Matrix.

🔍 Key Insights

Top Features: RSI_14, volatility_20, SMA_20, SMA_50, daily_return

Model performs slightly better at predicting upward days.

Consistent accuracy (~53–54%) indicates weak but meaningful predictive power in noisy financial data.

✅ Final Outcome

LightGBM Classifier selected as the final model for deployment — offering the best tradeoff between speed, accuracy, and interpretability for stock direction prediction.

** Flask API Deployment Plan

Main Steps:

Save the trained model using joblib or pickle.

Create a Flask app with a /predict endpoint to receive input and return predictions.

Test locally using Postman or curl to ensure correct responses.

Deploy online on platforms like Render, Railway, or Heroku for public API access
---

