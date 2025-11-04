project_name: "Depi Graduation Project — Group 79"

about_project: "This Stock Analysis Data Science Project analyzes five years of historical data for all companies in the S&P 500 index to uncover patterns and predict market movements. Stock data is volatile, yet it contains valuable insights. This project demonstrates how data science and machine learning can be applied to analyze, visualize, and predict trends."

dataset_overview:
  source: "https://www.kaggle.com/datasets/camnugent/sandp500"
  size: "~619,000 rows × 7 columns"
  data_range: "5 years of daily prices (Open, High, Low, Close, Volume)"
  tools: "Python, Pandas, NumPy, Matplotlib, Seaborn, Scikit-learn, XGBoost, LightGBM"
  cleaning_summary:
    - "Missing values and duplicates removed"
    - "Dates standardized and sorted chronologically"
    - "Final dataset size: ~593,000 clean records"

objectives:
  - "Analyze large-scale stock market data efficiently"
  - "Generate technical and temporal indicators to capture trends"
  - "Build classification models to predict next-day stock movement (Up/Down)"
  - "Evaluate models and interpret feature importance"

workflow_summary:
  data_loading_cleaning:
    - "Imported using kagglehub"
    - "Dropped missing values and converted date to datetime objects"
    - "Sorted by stock symbol and date"
  exploratory_data_analysis:
    - "Line charts for top 5 traded stocks"
    - "Bar charts for total trading volume"
    - "Observation: Tech stocks (AAPL, FB) outperformed industrial/financial sectors"
  feature_engineering:
    technical_indicators: ["SMA_20", "SMA_50", "RSI_14", "volatility_20", "volatility_50"]
    temporal_features: ["day_of_week", "is_month_end", "is_quarter_end"]
    target_features: ["Next_Day_Return", "Target_UpDown (Up=1, Down=0)"]
  key_observations:
    - "SMA crossovers indicate bullish/bearish trends"
    - "RSI peaks/troughs highlight overbought/oversold conditions"
    - "Volatility spikes show high-risk periods"
    - "Mild day-of-week and month-end effects observed"

machine_learning_models:
  features_used: ["volatility_20", "volatility_50", "SMA_20", "SMA_50", "RSI_14", "day_of_week", "is_month_end", "is_quarter_end", "daily_return"]
  target: "Target_UpDown = 1 if Next_Day_Return > 0, else 0"
  models:
    - name: "LightGBM"
      accuracy: "53.6%"
      notes: "Best balance between speed and performance after tuning"
    - name: "XGBoost"
      accuracy: "53.5%"
      notes: "Reliable, interpretable, good generalization"
    - name: "Random Forest"
      accuracy: "52.8%"
      notes: "Stable ensemble, simple baseline"
  top_features: ["RSI_14", "volatility_20", "SMA_20", "daily_return", "day_of_week"]
  final_model: "LightGBM"

hyperparameter_tuning:
  description: "Optimized the LightGBM classifier using GridSearchCV, slightly improving accuracy (0.535 → 0.536) and achieving balanced prediction performance for both upward and downward stock movements."
  method:
    - "Preserved chronological order using TimeSeriesSplit"
    - "Explored combinations of n_estimators, max_depth, learning_rate, and class_weight"
  best_configuration:
    max_depth: 7
    learning_rate: 0.05
    n_estimators: 200
    class_weight: "balanced"

flask_api_deployment:
  status: "Planned/Experimental"
  overview: "The trained LightGBM model is prepared for potential integration into a web API, allowing predictions from external requests."
  planned_steps:
    - "Serialize the trained model using joblib or pickle"
    - "Develop a Flask app with a /predict endpoint for real-time prediction"
    - "Conduct local tests using Postman or curl to ensure reliability"
    - "Explore hosting options on platforms like Render, Railway, or Heroku"
  goal: "Enable smooth transition from local model to interactive API, providing stock movement predictions in a structured format."
  alternatives: ["Plan A: Flask API", "Plan B: Streamlit"]
