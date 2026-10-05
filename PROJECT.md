# Technology Project — Bitcoin Market Regime Classification & Return Prediction

## 1. GENERAL INFORMATION

- Project name: Bitcoin Market Regime Classification & Return Prediction
- Specialization: DS
- Project source: Public financial market dataset
- Original source link: [Yahoo Finance - BTC-USD Historical Data](https://finance.yahoo.com/quote/BTC-USD/history/)
- Published project link: https://github.com/laperezortiz/bitcoin-market-regime-classification

## 2. OBJECTIVE

Analyze historical Bitcoin market data to identify distinct market regimes and evaluate whether incorporating regime information improves short-term return prediction. The analysis aims to provide information that can support the evaluation of Bitcoin market conditions and short-term exposure.

## 3. WORK PLAN

1. Initial exploration — Explore the structure, quality, and behavior of the historical Bitcoin data.
2. Data preparation — Clean the data and engineer features related to returns and volatility.
3. Model development — Identify market regimes and develop models to predict short-term Bitcoin returns.
4. Evaluation — Compare models using time-based validation and appropriate performance metrics.
5. Conclusions and next steps — Interpret the results, document limitations, and identify potential improvements.

## 4. KEY QUESTIONS

1. Are the available data sufficiently complete and consistent for the period being analyzed?
2. Do the identified market regimes exhibit meaningful differences in returns and volatility?
3. Does incorporating market-regime information improve out-of-sample return prediction?

## 5. WHAT WAS DONE AND HOW

The historical Bitcoin dataset was obtained from Yahoo Finance using the BTC-USD ticker. The data was inspected for missing values, duplicate dates, OHLC consistency, and date continuity.

Daily returns were calculated from the closing price. Two rolling 30-day features were then created: 30-day average daily return and return volatility. These features were used to characterize different market conditions.

K-Means clustering was applied to the 30-day return and volatility features. The features were standardized before clustering, and several values of k were evaluated using silhouette scores and inertia. Three clusters were selected because the silhouette score was highest at k=3, while the inertia results showed diminishing improvement as the number of clusters increased.

The resulting clusters were analyzed according to their return, volatility, frequency, and persistence. Regime durations were calculated by identifying consecutive observations belonging to the same regime.

For the prediction component, the target variable was defined as the next day's Bitcoin return. The data was divided chronologically into training and test periods to preserve the time ordering of the observations.

For the prediction component, the regime-identification process was fitted using only the training data. The same scaler and K-Means model were then applied to the test data to avoid data leakage.

A Random Forest regression model was first trained using daily return, 30-day average return, and 30-day volatility as baseline features. A second Random Forest model was then trained using the same features together with one-hot encoded market-regime indicators.

Both models were evaluated on the unseen test period using Mean Absolute Error (MAE) and Root Mean Squared Error (RMSE).

## 6. RESULTS

The analysis identified three distinct market regimes.

- Regime 0 was characterized by positive 30-day average returns and relatively high volatility.
- Regime 1 was characterized by negative 30-day average returns and the highest volatility.
- Regime 2 was characterized by near-zero 30-day average returns and comparatively low volatility.

Regime 2 was the most frequent regime, representing approximately 63.8% of the observations. It also showed greater persistence, with an average duration of approximately 36 days. Regimes 0 and 1 had average durations of approximately 13 and 14 days, respectively.

For next-day return prediction, the baseline Random Forest model achieved:

- MAE: 0.018949
- RMSE: 0.025829

The regime-enhanced model achieved:

- MAE: 0.019014
- RMSE: 0.025972

Adding regime information therefore did not improve out-of-sample predictive performance. MAE increased by approximately 0.34% and RMSE increased by approximately 0.55% compared with the baseline model.

The results indicate that the identified regimes provide descriptive information about Bitcoin market conditions but did not provide meaningful additional predictive information for next-day returns beyond the return and volatility features already used by the baseline model.

## 7. CONCLUSIONS

The analysis successfully identified three distinct Bitcoin market regimes based on 30-day average returns and volatility. The regimes exhibited meaningful differences in their return, volatility, frequency, and persistence characteristics.

However, incorporating the identified regimes into a Random Forest model did not improve next-day Bitcoin return prediction. The regime-enhanced model produced slightly higher MAE and RMSE than the baseline model on the out-of-sample test period.

Therefore, within the modeling approach used in this project, market-regime information was useful for describing historical Bitcoin market conditions but did not provide additional predictive value for short-term return prediction.

The results are subject to several limitations. The regimes were identified using only 30-day average return and volatility, prediction was performed using a Random Forest model, and evaluation used a single chronological train/test split. Different features, regime-detection methods, prediction horizons, validation approaches, or predictive models could produce different results.

Future work could investigate additional market features, alternative regime-detection techniques, and longer prediction horizons to determine whether market-regime information becomes more useful under different modeling conditions.

## 8. PRE-PUBLICATION CHECKLIST

- [x] README explains the project without requiring the reader to inspect all the details
- [x] Files are organized, with no stray tests or outdated versions
- [x] No credentials or sensitive data are included in the repository
- [x] Original data source link is included and working
- [x] Project is published and accessible
- [ ] Project link has been shared with the coach
