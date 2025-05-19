# Time-Series Analysis: Predicting Realized Volatility from VIX

This project explores how to forecast the **forward 1-year realized volatility** of the S&P 500 using a combination of implied volatility indices (VIX1Y) and trailing realized volatilities (EWMA-based). We evaluate and compare multiple statistical and time series models for their predictive accuracy.

## Repository Structure

- `RealizedVVIX.ipynb` – Main notebook with full analysis and modeling pipeline
- `data files/` – Contains VIX data (VIX1Y, VIX3M, VIX6M, VIX30D), SPY prices, and calculated trailing volatilities
- `*.png` – Generated plots for model performance and visualization
- `Project Write Up.pdf` – Summary of methods and project direction
- `predicting-vix-on-volatility/` – Prior modeling code and R-based exploration, reverse of the main project.

---

## Problem Overview

We aim to **predict the 1-year forward realized volatility** (computed from SPY returns) using:

- **Implied volatility** from VIX1Y (CBOE)
- **Realized volatilities** computed as exponentially weighted moving averages:
  - `EWMA21` (1 month)
  - `EWMA63` (3 months)
  - `EWMA252` (1 year)

---

## Models Used

### 1. Linear Regression
Basic benchmark to understand baseline fit between predictors and target.

### 2. Lasso Regression (with Time Series Cross-Validation)
Used to reduce overfitting and select only informative predictors. Applied with `TimeSeriesSplit` to preserve temporal order.

### 3. SARIMAX Model
A seasonal ARIMA model with exogenous regressors (`VIX1Y`, `EWMA21`, `EWMA63`, `EWMA252`). Captures both time-series dynamics and explanatory variable influence.

---

## Evaluation Metrics

- **RMSE / MAE**: Error metrics on test set
- **R² Score**: Goodness of fit
- **Bias**: Mean prediction error
- **Durbin-Watson**: Autocorrelation in residuals
- **Residual Plots**: Temporal patterns and variance check
- **Prediction vs Actual**: Visual comparison of model predictions

---

## Key Plots

- `actual_vs_predicted_volatility.png` – Ground truth vs predictions
- `residuals_over_time.png` – Residual diagnostics
- `error_distribution_histogram.png` – Model error spread
- `rmse_comparison_bar_chart.png` – Comparison of OLS, Lasso, and SARIMAX

---

## Methodology

- All models were trained using **time-aware train-test splits** to prevent data leakage
- Lasso regression used `TimeSeriesSplit` to ensure validation reflected real-world forecasting constraints
- Final performance was measured using holdout evaluation on the last year of data

---

## Takeaways

- **Lasso regression** significantly reduced prediction error compared to OLS by regularizing and shrinking noisy coefficients
- **SARIMAX** achieved the best overall fit by combining autoregressive structure with external volatility indicators
- Respecting the temporal structure using time series CV and carefully aligning dates was crucial for realistic forecasting

---

## Future Work

- Incorporate more macroeconomic indicators (e.g., rates, spreads)
- Explore machine learning models (e.g., XGBoost, LSTM)
- Extend to volatility forecasting for other asset classes

---

## Authors

- **Rohan Shukla**
- **Cindy Xu**
