## Breast Cancer Classification Using Machine Learning and Bayesian Inference

# Project Overview

This project combines Machine Learning classification models with a Bayesian statistical framework to estimate and analyze the probability of malignant breast cancer diagnosis.

The objective is twofold:

Build and compare predictive models to detect malignant tumors.

Estimate the true probability of malignancy (θ) using a Beta-Binomial Bayesian approach, incorporating prior information and uncertainty quantification.

This work integrates classical predictive modeling with Bayesian inference in a coherent statistical framework.

# Dataset Description

- Number of observations: 568
- Number of variables: 32
- Dependent variable: diagnosis.
     M → Malignant
     B → Benign

The dataset contains clinical measurements extracted from digitized breast mass images.

There are no missing values, only numeric predictors and a slightly imbalanced target variable (more benign than malignant cases).

The response variable was encoded as:
- 0 → Benign (reference level)
- 1 → Malignant (event of interest)

# Libraries used
readr

corrplot

ggplot2

caret

tidyr

xgboost

LearnBayes

HDInterval

# Exploratory Data Analysis

- Verified absence of missing values.
- Visualized class distribution (moderately imbalanced).
- Examined correlation matrix.
- Multicollinearity was not addressed since tree-based models are robust to correlated predictors.

# Dataset Split

The dataset was divided using stratified sampling to preserve class proportions:
- Train (70%) → 398 observations
- Test_1 (15%) → 85 observations
- Test_2 (15%) → 85 observations

Test_1 is used for model evaluation.
Test_2 is reserved for Bayesian validation.

# Machine Learning Models

Four models were trained using 5-fold cross-validation with hyperparameter tuning:
- Random Forest
- XGBoost
- Support Vector Machine (SVM)
- K-Nearest Neighbors (KNN)

Evaluation:
- RF, XGB and SVM achieved perfect sensitivity.
- KNN showed poor sensitivity (misses many malignant cases).
- XGBoost achieved the highest Positive Predictive Value (≈ 0.97).

# Ensemble Analysis
Assuming conditional independence of errors:
- Joint Sensitivity = 0.46875
- Joint Specificity = 0.85706
- Posterior P(M | all models positive) ≈ 0.99999

Model Selection

If the objective is:
- Minimize false positives → keep all models
- Minimize false negatives → remove KNN

Given the medical context, KNN was discarded due to its low sensitivity.

# Best Individual Model

Using the Positive Predictive Value formula:
XGBoost was selected as the optimal individual classifier because it achieves perfect sensitivity, highest specificity and the highest PPV

## Bayesian Approach
Global Probability Construction

A new variable pred_prob_global was created as a weighted average of model probabilities, where weights were proportional to each model's sensitivity contribution.

# Bayesian Model: Beta-Binomial

We model:
                   θ=P(Malignant)

Using:
                  θ∼Beta(α,β)

Data from Test_1:
- n = 85
- x = 32 predicted malignant cases


1. Prior Elicitation Methods

Two approaches were used:
- Quantile Method, using median and 90th percentile.

Resulting prior:
                     Beta(0.14,0.33)
- Mean-Variance Method
                     Beta(0.085,0.149)

Both priors were weakly informative. The quantile-based prior showed slightly lower error when validated against Test_2.


2. Posterior Distribution

Using quantile-based prior:
                        θ∣data∼Beta(32.14,53.33)
The posterior is highly concentrated and nearly symmetric.



95% Credible Intervals
- Equal-Tailed Interval:
                       (0.277 , 0.481)

- HPD Interval:
                        (0.275 , 0.479)
Both intervals are nearly identical, indicating posterior symmetry.


## Simulation Approach

1,000,000 posterior samples were generated:
- Mean ≈ 0.3760
- Variance ≈ 0.0027
Simulation results match analytical results, confirming stability.


## Overfitting Analysis (Bayesian Test)

We tested:
               𝐻0:𝑝𝑡𝑟𝑎𝑖𝑛=𝑝𝑡𝑒𝑠𝑡
​
- Model 1: SVM
           Train accuracy: 0.987; Test accuracy: 0.976; Bayes Factor B₁₀ = 0.056

- Model 2: KNN
           Train accuracy: 0.827; Test accuracy: 0.776; Bayes Factor B₁₀ = 0.047

Since B₁₀ < 1 in both cases, evidence favors H₀.There is no significant overfitting.



