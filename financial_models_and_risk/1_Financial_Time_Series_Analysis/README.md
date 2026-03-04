# Financial Time Series Analysis
## Market Efficiency and Volatility Modeling
Overview:

This project focuses on the econometric analysis of financial time series within the framework of Market Risk Management.

The objective is to evaluate whether selected financial assets satisfy the Efficient Market Hypothesis (EMH) and to determine the appropriate volatility model for risk measurement purposes.

The analysis includes:
- Data downloading and preprocessing
- Log-return computation
- Detection and treatment of missing values and outliers
- Stationarity testing
- Serial correlation analysis
- Long-memory analysis (Hurst exponent)
- IID testing (BDS test)
- Normality assessment
- Model selection (GARCH vs ARMA-GARCH)

## Data Description

- Market: Spanish equity market
- Index: IBEX-35
- Assets: Multiple constituents of the IBEX-35
- Frequency: Daily
- Source: Yahoo Finance (via quantmod in R)
- Start date: 1990-01-01

Prices are downloaded using adjusted closing prices unless data inconsistencies justify using closing prices.

## Phase 1 – Data Preparation
1. Data Download

All assets are downloaded automatically using quantmod.

2. Price Selection

Adjusted prices are used by default.
If anomalies are detected (e.g., excessive negative values), closing prices are selected instead.

3. Return Calculation

Daily log-returns are computed as:

                                 𝑟𝑡=log(𝑃𝑡)−log(𝑃𝑡−1)​
4. Data Cleaning

- Missing values are quantified.
- Outliers are identified using standardized returns (Z-scores).
- Observations exceeding |Z| > 5 are removed.

A summary table is generated including:

- Initial observations
- Percentage of missing values
- Outliers detected under different thresholds
- Final sample size

## Phase 2 – Efficient Market Hypothesis (EMH) Testing

The project evaluates the weak-form EMH through the following tests:

1. Stationarity Tests

Applied to both prices and returns:
- Augmented Dickey-Fuller (ADF)
- Phillips-Perron (PP)
- KPSS test

Expected result:
- Prices → non-stationary
- Returns → stationary

2️. Serial Correlation
- ACF and PACF analysis
- Ljung-Box test (lag = 5)

Tested for returns and squared returns

3️. Long Memory – Hurst Exponent

Estimated using R/S methodology.

Interpretation:
- H = 0.5 → Random Walk (EMH consistent)
- H ≠ 0.5 → Persistence or anti-persistence

4️. BDS Test

Tests the null hypothesis of IID behavior.

5️. Normality
- Jarque-Bera test applied to returns.

Expected stylized fact:
- Financial returns are not normally distributed
- Presence of fat tails and excess kurtosis


# Stylized Facts Investigated

The project evaluates the following well-known stylized facts of financial markets:
- Prices follow a random walk
- Returns are leptokurtic and heavy-tailed
- Volatility clustering exists

# Model Selection

Based on the empirical results:
- If returns are uncorrelated but squared returns are correlated → GARCH model
- If both returns and squared returns show serial correlation → ARMA-GARCH model
- If no dependence is detected → no volatility model required

This step prepares the ground for subsequent Value-at-Risk (VaR) estimation and risk forecasting.


# Output

For each asset, the project generates:
- ACF and PACF plots
- ACF/PACF of squared returns
- QQ-plot
- Time series with ±2σ bands
- Summary decision table (EMH and model selection)

All results are automatically exported to structured folders.

# R Packages Used
- quantmod
- dplyr
- PerformanceAnalytics
- tseries
- forecast
- tseriesChaos
- nortest
- ggplot2
- xts / zoo


