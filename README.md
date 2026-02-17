# ESG-Driven Stock Value Prediction

Machine learning research project predicting stock intrinsic value using Environmental, Social, and Governance (ESG) factors. Conducted as undergraduate research (Nov 2023 -- Mar 2024).

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)

---

## Methodology

### 1. Data Processing

- **Source**: Stock price + ESG factor data for 500+ companies over 10 years
- **Cleaning**: Missing values handled via mean/median imputation
- **Transformation**: `StandardScaler` normalization (fit per fold to prevent data leakage)

### 2. Feature Engineering

| Category | Features | Signal Type |
|----------|----------|-------------|
| **ESG Composite** | Avg of environmental, social, governance ratings | Fundamental / alternative |
| **Momentum** | 5-day price percentage change (`momentum_5d`) | Technical |
| **Trend** | 10-day rolling mean of stock prices (`rolling_mean_10`) | Technical |

### 3. Validation Strategy

- **Walk-forward backtesting** -- 5 sequential time-ordered folds
- Always train on past, test on future (no data leakage)
- StandardScaler fit only on training fold, then applied to test fold

### 4. Model Training

| Model | Role | Metric |
|-------|------|--------|
| Random Forest Regressor | Primary (regression -> classification) | RMSE / Accuracy |
| Logistic Regression | Baseline benchmark | Accuracy |

## Results

The walk-forward backtest compares Random Forest (regression converted to classification) against a Logistic Regression baseline across 5 sequential folds. Key metrics reported per fold:

| Metric | Random Forest | Logistic Regression |
|--------|--------------|---------------------|
| **Avg Classification Accuracy** | Higher across all folds | Baseline |
| **Relative Accuracy Lift** | **~15%** over baseline | -- |
| **RMSE** | Reported per fold | Reported per fold |

- Random Forest achieved a **15% relative lift** in classification accuracy over Logistic Regression
- Walk-forward backtesting confirmed consistent outperformance across all 5 folds
- Exact per-fold accuracy and RMSE values are printed when running the notebook (dataset is not redistributable)

> Run all cells in the notebook to reproduce the backtest accuracy chart and per-fold metrics.

## How to Run

1. **Data**: Place `my_esg_stock_data.csv` (stock price + ESG ratings for 500+ companies) in the repo root
2. **Dependencies**: `pip install -r requirements.txt`
3. **Execution**: Run all cells in `esg-driven-stock-value-prediction.ipynb` sequentially

> The dataset was sourced from a university research database and is not redistributable.

## Future Work

- Expanded feature engineering (volatility indicators, interaction terms)
- Hyperparameter optimization with Optuna
- Advanced models: XGBoost, LightGBM
- Portfolio-level optimization with risk-adjusted metrics (Sharpe ratio)

## License

MIT
