# ESG-Driven Stock Value Prediction

Machine learning research project predicting stock intrinsic value using Environmental, Social, and Governance (ESG) factors. Conducted as undergraduate research (Nov 2023 -- Mar 2024).

Part of a broader [quantitative finance toolkit](https://github.com/YichengYang-Ethan) — this project explores the alpha signal in ESG data, complementing the technical/momentum indicators used in [clawdfolio](https://github.com/YichengYang-Ethan/clawdfolio) and [crypto-return-prediction](https://github.com/YichengYang-Ethan/crypto-return-prediction-kaggle).

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)

---

## Methodology

### 1. Data Processing

- **Source**: Stock price + ESG factor data for 500+ companies over 10 years
- **Cleaning**: Missing values handled via mean/median imputation
- **Transformation**: `StandardScaler` normalization for model convergence

### 2. Feature Engineering

| Category | Features | Signal Type |
|----------|----------|-------------|
| **ESG Composite** | Avg of environmental, social, governance ratings | Fundamental / alternative |
| **Momentum** | 5-day price percentage change (`momentum_5d`) | Technical |
| **Trend** | 10-day rolling mean of stock prices (`rolling_mean_10`) | Technical |

> The momentum and rolling mean features share the same conceptual framework as the SMA/RSI indicators used in [clawdfolio](https://github.com/YichengYang-Ethan/clawdfolio)'s technical analysis module.

### 3. Validation Strategy

- **Walk-forward backtesting** — 5 sequential time-ordered folds
- Always train on past, test on future (no data leakage)
- Same temporal-split philosophy used in [crypto-return-prediction](https://github.com/YichengYang-Ethan/crypto-return-prediction-kaggle) (TimeSeriesSplit)

### 4. Model Training

| Model | Role | Metric |
|-------|------|--------|
| Random Forest Regressor | Primary (regression -> classification) | RMSE / Accuracy |
| Logistic Regression | Baseline benchmark | Accuracy |

## Results

- Random Forest achieved **15% relative lift** in classification accuracy over Logistic Regression
- Walk-forward backtesting confirmed consistent outperformance across all folds

<p align="center">
  <img src="results/backtest_plot.png" width="600" alt="Backtest Results">
</p>

## Future Work

- Expanded feature engineering (volatility indicators, interaction terms)
- Hyperparameter optimization with Optuna
- Advanced models: XGBoost, LightGBM (as used in [crypto-return-prediction](https://github.com/YichengYang-Ethan/crypto-return-prediction-kaggle))
- Portfolio-level optimization with risk-adjusted metrics (Sharpe ratio — as computed by [clawdfolio](https://github.com/YichengYang-Ethan/clawdfolio))

## Related Projects

| Project | Role |
|---------|------|
| [clawdfolio](https://github.com/YichengYang-Ethan/clawdfolio) | Core engine — risk analytics, Sharpe ratio, technical indicators |
| [crypto-return-prediction](https://github.com/YichengYang-Ethan/crypto-return-prediction-kaggle) | LightGBM prediction with shared momentum/trend feature methodology |
| [investment-dashboard](https://github.com/YichengYang-Ethan/investment-dashboard) | Portfolio visualization frontend |

## License

MIT
