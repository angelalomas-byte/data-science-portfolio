## Volatility Modeling and ARMA–GARCH Model Selection
# Financial Risk Management

# Project Overview

This project develops a complete econometric analysis of a financial asset within the framework of market risk management.

The study covers:
- Data cleaning and preprocessing
- Stylized facts verification
- Stationarity and dependence testing
- Volatility clustering analysis
- ARMA–GARCH model specification
- Model selection using information criteria
- Residual diagnostics
- Marginal vs conditional moments comparison

The objective is to determine whether financial returns are predictable and to identify the most appropriate conditional volatility model.

# Objectives

The main goals of this project are:
- To verify whether asset prices follow a random walk.
- To test if returns exhibit stylized financial properties.
- To assess the presence of heteroskedasticity.
- To determine whether an ARMA–GARCH specification improves modeling.
- To select the optimal in-sample model.
- To evaluate model adequacy through statistical diagnostics.

# Data Description
- In-sample period: Up to August 31, 2025
- Frequency: Daily data
- Variables:
  
Closing price

Adjusted closing price

Log-returns

Price Selection

Adjusted closing prices were used to ensure consistency in the presence of:

Dividends

Stock splits

Corporate actions

Raw closing prices may be preferred only for short-term microstructure analysis.

# Step 1: Data Cleaning and Descriptive Analysis
1. Return Computation

Logarithmic returns were computed as:
                       
                       𝑟𝑡=ln(𝑃𝑡/𝑃𝑡−1)
​

2. Data Cleaning

- Missing values identification
- Outlier detection using thresholds:

                  𝜇±𝐶⋅𝜎           𝐶=3 and 𝐶=5

3. Descriptive Statistics
- Mean
- Standard deviation
- Skewness
- Kurtosis

Results confirm excess kurtosis and potential asymmetry.

# Step 2: Stylized Facts of Financial Markets

Stylized Fact 1 – Random Walk in Prices

A. Stationarity Tests
- Augmented Dickey–Fuller (ADF)
- Phillips–Perron (PP)
- KPSS

Prices → non-stationary; Returns → stationary

B. Serial Correlation
- ACF and PACF
- Ljung–Box test (lags 1, 5, 10, 20, 30)

Weak linear dependence in returns.

C. Long Memory
- Hurst exponent (R/S methodology)

D. BDS Test
- Test for IID structure.

Stylized Fact 2 – Fat Tails and Leptokurtosis
- Histogram and empirical density
- Normal density comparison
- Q-Q plot
- ±2σ graphical bands

Results confirm are heavy tails, excess kurtosis, non-normality


Stylized Fact 3 – Volatility Clustering
- ACF and PACF of squared returns
- Ljung–Box test on squared returns

Strong evidence of ARCH effects.

# Step 3: Model Specification

Two alternative models were evaluated:

- Model 1: GARCH(m,r)
  
                                    𝑟𝑡 = 𝜇 + 𝜖𝑡
​
                            𝜎𝑡2 = 𝜔 + ∑𝛼𝑖𝜖−𝑖2 + ∑𝛽𝑗𝜎𝑡−𝑗2

	​- Model 2: ARMA(p,q)–GARCH(m,r)

Includes conditional mean dynamics:

                              𝑟𝑡=𝜇𝑡+𝜖𝑡
	​
Mean modeled via ARMA(p,q).



# Model Selection

Model selection was performed using:
- AIC
- BIC
- HQC


Final Model is selected following goodness-of-fit, parsimony, residual diagnostics and stability conditions

# Model Diagnostics

Residual analysis includes:
- Ljung–Box test (residuals)
- Ljung–Box test (squared residuals)
- ARCH LM test
- Standardized residual distribution analysis

Conclusion:

No remaining autocorrelation

No remaining ARCH effects

Model adequately captures volatility dynamics



# Libraries used
- rugarch
- tseries
- forecast
- FinTS
- PerformanceAnalytics



# Key Findings

Prices follow a random walk, returns are stationary but non-normal. Strong volatility clustering is present. GARCH-type models are necessary. RMA structure may improve mean specification ans selected model passes diagnostic checks.


