Depi Graduation Project — Group 79
About the Project

This Stock Analysis Data Science Project analyzes five years of historical data for all companies in the S&P 500 index to uncover patterns and predict market movements.

Despite market volatility, stock data contains valuable insights that can be extracted using data science and machine learning. This project demonstrates how to analyze, visualize, and predict market trends using advanced models.

Dataset Overview

Source: Kaggle – camnugent/sandp500

Size: ~619,000 rows × 7 columns

Data Range: 5 years of daily prices (Open, High, Low, Close, Volume)

Tools: Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM

After cleaning and preprocessing:

Missing values and duplicates were removed.

Dates were standardized and sorted chronologically.

Final dataset size: ~593,000 clean records.

Objectives

Analyze large-scale stock market data efficiently.

Generate technical and temporal indicators to capture trends.

Build classification models to predict next-day stock movement (Up/Down).

Evaluate models and interpret feature importance.

Workflow Summary
1. Data Loading & Cleaning

Imported using kagglehub.

Dropped missing values and converted date to datetime objects.

Sorted by stock symbol and date.

2. Exploratory Data Analysis

Line charts for top 5 traded stocks.

Bar charts for total trading volume.

Observations: Tech stocks (AAPL, FB) outperformed industrial and financial sectors.

3. Feature Engineering

Technical Indicators:

SMA_20, SMA_50 (trends)

RSI_14 (momentum)

volatility_20, volatility_50 (risk)

Temporal Features: day_of_week, is_month_end, is_quarter_end

Target Features: Next_Day_Return, Target_UpDown (binary: Up=1, Down=0)

4. Key Observations

SMA crossovers indicate bullish/bearish trends.

RSI peaks/troughs show overbought/oversold conditions.

Volatility spikes highlight high-risk periods.

Day-of-week and month-end effects reveal mild cyclical behavior.

Machine Learning Models

Features Used: volatility_20, volatility_50, SMA_20, SMA_50, RSI_14, day_of_week, is_month_end, is_quarter_end, daily_return
Target: Target_UpDown = 1 if Next_Day_Return > 0, else 0

Model	Accuracy	Notes
LightGBM	53.6%	Best balance between speed and performance after tuning
XGBoost	53.5%	Reliable, interpretable, good generalization
Random Forest	52.8%	Stable ensemble, simple baseline

Top Features: RSI_14, volatility_20, SMA_20, daily_return, day_of_week

Slight accuracy improvement after tuning LightGBM (0.535 → 0.536).

LightGBM chosen as the final model for deployment.

Flask API Deployment Plan

Main Steps:

Save the trained LightGBM model using joblib or pickle.

Create a Flask app with a /predict endpoint to receive inputs and return predictions.

Test locally using Postman or curl.

Deploy online on platforms like Render, Railway, or Heroku for public API access.
