# ESG-Driven Stock Value Prediction

![Python](https://img.shields.io/badge/Python-3776AB?style=flat&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-F7931E?style=flat&logo=scikit-learn&logoColor=white)

Machine learning research predicting stock value using ESG (Environmental, Social, Governance) factors. Random Forest with walk-forward backtesting achieves a **~15% relative accuracy lift** over a Logistic Regression baseline across 500+ companies over 10 years.

Conducted as undergraduate research (Nov 2023 – Mar 2024).

## Methodology

### Features

| Category | Features | Signal Type |
|----------|----------|-------------|
| **ESG Composite** | Average of environmental, social, governance ratings | Fundamental |
| **Momentum** | 5-day price percentage change | Technical |
| **Trend** | 10-day rolling mean of stock prices | Technical |

### Validation

- **Walk-forward backtesting** — 5 sequential time-ordered folds
- Always train on past, test on future (no data leakage)
- `StandardScaler` fit only on training fold, then applied to test fold

### Models

| Model | Role | Approach |
|-------|------|----------|
| **Random Forest** | Primary | Regression → classification (above/below median) |
| Logistic Regression | Baseline | Direct classification |

## Results

- Random Forest achieves **~15% relative lift** in classification accuracy over Logistic Regression
- Consistent outperformance across all 5 walk-forward folds
- Per-fold accuracy and RMSE values are generated at runtime (dataset is not redistributable)

> Run all cells in the notebook to reproduce the backtest accuracy chart and per-fold metrics.

## How to Run

1. **Data**: Place `my_esg_stock_data.csv` (stock price + ESG ratings, 500+ companies) in the repo root
2. **Dependencies**: `pip install -r requirements.txt`
3. **Execution**: Run all cells in `esg-driven-stock-value-prediction.ipynb`

> The dataset was sourced from a university research database and is not redistributable.

## License

MIT
