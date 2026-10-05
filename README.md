# Bitcoin Market Regime Classification & Return Prediction

## Overview

This project analyzes historical Bitcoin market data to identify distinct market regimes and evaluate whether incorporating regime information improves short-term return prediction.

The analysis uses historical BTC-USD data from Yahoo Finance and combines unsupervised learning with supervised machine learning.

## Objectives

The project addresses three main questions:

1. Are the available data sufficiently complete and consistent for the period analyzed?
2. Do the identified market regimes exhibit meaningful differences in returns and volatility?
3. Does incorporating market-regime information improve out-of-sample prediction of the next day's Bitcoin return?

## Methodology

The analysis follows these main steps:

1. **Data exploration and preparation**
   - Historical BTC-USD daily data was obtained from Yahoo Finance.
   - Data quality was assessed using missing-value, duplicate-date, OHLC consistency, and date-continuity checks.

2. **Feature engineering**
   - Daily Bitcoin returns were calculated.
   - 30-day average daily return and 30-day return volatility were calculated using rolling windows.

3. **Market regime identification**
   - The 30-day return and volatility features were standardized.
   - K-Means clustering was evaluated across different numbers of clusters.
   - Three regimes were selected based on clustering diagnostics.
   - Regime characteristics and persistence were then analyzed.

4. **Next-day return prediction**
   - The target was defined as the next day's Bitcoin return.
   - A chronological train/test split was used.
   - A Random Forest regression model was established as a baseline.
   - A second Random Forest model incorporated one-hot encoded market-regime indicators.
   - Both models were evaluated on the unseen test period using MAE and RMSE.

## Key Results

Three distinct market regimes were identified:

- **Regime 0:** Positive 30-day average returns and relatively high volatility.
- **Regime 1:** Negative 30-day average returns and the highest volatility.
- **Regime 2:** Near-zero 30-day average returns and comparatively low volatility.

Regime 2 was the most frequent regime and also showed greater persistence than the other regimes.

For next-day return prediction:

| Model | MAE | RMSE |
| --- | ---: | ---: |
| Baseline | 0.018949 | 0.025829 |
| Regime-Enhanced | 0.019014 | 0.025972 |

Adding regime information increased MAE by approximately 0.34% and RMSE by approximately 0.55%.

Therefore, the regime-enhanced model did **not** improve out-of-sample prediction performance in this modeling setup.

## Conclusion

The identified market regimes provided useful descriptive information about historical Bitcoin market conditions, including differences in return, volatility, and persistence.

However, incorporating the regimes into the Random Forest prediction model did not provide additional predictive value for next-day Bitcoin returns beyond the return and volatility features already used by the baseline model.

Future work could investigate additional market features, alternative regime-detection methods, different prediction horizons, and alternative predictive models.

## Data Source

Historical Bitcoin data was obtained from Yahoo Finance using the BTC-USD ticker.

## Technologies

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Scikit-learn
- yfinance

## Project Structure

```text
.
├── .gitignore
├── bitcoin_market_regime_analysis.ipynb
├── PROJECT.md
├── README.md
└── requirements.txt
```

## Reproducibility

Install the required dependencies with:

```bash
pip install -r requirements.txt
```

The analysis is contained in `bitcoin_market_regime_analysis.ipynb`.