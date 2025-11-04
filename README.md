<span style="font-family:Arial, sans-serif;">Depi Graduation Project — Group 79</span>
<span style="font-family:Arial, sans-serif;">About the Project</span>

This <strong>Stock Analysis Data Science Project</strong> analyzes <em>five years of historical data</em> for all companies in the <strong>S&P 500 index</strong> to uncover patterns and predict market movements.

Stock data is volatile, yet it contains valuable insights. This project demonstrates how <strong>data science and machine learning</strong> can be applied to analyze, visualize, and predict trends.

<span style="font-family:Arial, sans-serif;">Dataset Overview</span>

Source: <a href="https://www.kaggle.com/datasets/camnugent/sandp500">Kaggle – camnugent/sandp500</a>

Size: ~619,000 rows × 7 columns

Data Range: 5 years of daily prices (Open, High, Low, Close, Volume)

Tools: Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM

After cleaning and preprocessing:

Missing values and duplicates removed

Dates standardized and sorted chronologically

Final dataset size: ~593,000 clean records

<span style="font-family:Arial, sans-serif;">Objectives</span>

Analyze large-scale stock market data efficiently

Generate <em>technical</em> and <em>temporal</em> indicators to capture trends

Build <strong>classification models</strong> to predict next-day stock movement (Up/Down)

Evaluate models and interpret feature importance

<span style="font-family:Arial, sans-serif;">Workflow Summary</span>
1. Data Loading & Cleaning

Imported using kagglehub

Dropped missing values and converted date to datetime objects

Sorted by stock symbol and date

2. Exploratory Data Analysis

Line charts for top 5 traded stocks

Bar charts for total trading volume

Observation: Tech stocks (AAPL, FB) outperformed industrial/financial sectors

3. Feature Engineering

Technical Indicators: SMA_20, SMA_50, RSI_14, volatility_20, volatility_50

Temporal Features: day_of_week, is_month_end, is_quarter_end

Target Features: Next_Day_Return, Target_UpDown (Up=1, Down=0)

4. Key Observations

SMA crossovers indicate bullish/bearish trends

RSI peaks/troughs highlight overbought/oversold conditions

Volatility spikes show high-risk periods

Mild day-of-week and month-end effects observed

<span style="font-family:Arial, sans-serif;">Machine Learning Models</span>

Features Used: volatility_20, volatility_50, SMA_20, SMA_50, RSI_14, day_of_week, is_month_end, is_quarter_end, daily_return
Target: Target_UpDown = 1 if Next_Day_Return > 0, else 0

Model	Accuracy	Notes
LightGBM	53.6%	Best balance between speed and performance after tuning
XGBoost	53.5%	Reliable, interpretable, good generalization
Random Forest	52.8%	Stable ensemble, simple baseline

Top Features: RSI_14, volatility_20, SMA_20, daily_return, day_of_week

LightGBM selected as the final model for deployment

<span style="font-family:Arial, sans-serif;">Hyperparameter Tuning</span>

Hyperparameter Tuning: Optimized the LightGBM classifier using GridSearchCV, slightly improving accuracy (0.535 → 0.536) and achieving balanced prediction performance for both upward and downward stock movements.

Method:

Preserved chronological order using TimeSeriesSplit

Explored combinations of n_estimators, max_depth, learning_rate, and class_weight

Best Configuration:

max_depth=7

learning_rate=0.05

n_estimators=200

class_weight='balanced'

<span style="font-family:Arial, sans-serif; color:#2F4F4F;">Flask API Deployment (Planned/Experimental)</span>

Overview:
The trained LightGBM model is prepared for potential integration into a web API, allowing predictions from external requests.

Planned Steps :

Serialize the trained model using joblib or pickle

Develop a Flask app with a /predict endpoint for real-time prediction

Conduct local tests using Postman or curl to ensure reliability

Explore hosting options on platforms like Render, Railway, or Heroku

Goal:
Enable smooth transition from local model to interactive API, providing stock movement predictions in a structured format.
plan A FlaskAPI 
Plan B Steamlit

