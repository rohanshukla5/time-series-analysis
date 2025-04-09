# time-series-analysis

We aim to predict volatility of the market through backtesting and applying time series models. Specifically SARIMA and GARCH models. 

We will do this by comparing two of the main volatility market indicators, VIX(Volatility Index) and the actual implied volatility of the market. 

The actual implied volatility will be calculated, for the next month worth of data, the next 3 months, and the next year worth of data. We will do this on the S&P500(SPY), since this holds the most information regarding the markets.  To do this we will fit the data onto linear regression models and compare the VIX with the actual implied volatility. We will then simply use the predicted VIX, and implied volatility from the models to generate a volatility assumption.
