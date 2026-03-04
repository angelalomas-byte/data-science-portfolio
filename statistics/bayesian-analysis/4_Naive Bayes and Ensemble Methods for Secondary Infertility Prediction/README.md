## Machine Learning for Secondary Infertility Risk Prediction
# A Comparative Study of Naive Bayes, Random Forest and XGBoost

This project applies machine learning models to predict secondary infertility using reproductive and sociodemographic variables.

The objective is to evaluate how different modeling approaches — probabilistic and ensemble-based — perform in a moderately imbalanced clinical dataset, while prioritizing sensitivity due to the higher clinical cost of false negatives.


# Objective

To assess how reproductive history and sociodemographic characteristics influence the probability of secondary infertility (case = Yes) and compare the predictive performance of:

- Naive Bayes (probabilistic model)
- Random Forest (ensemble tree-based model)
- XGBoost (gradient boosting model)

Special attention is given to:

- Class imbalance
- Sensitivity vs specificity trade-offs
- The impact of SMOTE sampling
- Clinical interpretation of results


# Dataset Description
The target variable:

case
- 1 → Secondary infertility
- 0 → Control (no infertility)

Class distribution:
- 165 controls (66%)
- 83 cases (34%)

The dataset presents moderate class imbalance.

Predictors
- age → woman’s age (discretized into intervals)
- parity → number of previous pregnancies
- induced → number of induced abortions
- spontaneous → number of spontaneous abortions
- education → education level
- stratum / pooled.stratum → matching identifiers (excluded from modeling)
- Categorical variables were converted to factors for compatibility with Naive Bayes.


# Modeling Strategy
# Train/Test Split

The dataset was divided into training and test sets.

Cross-validation:
- 5-fold cross-validation
- twoClassSummary metrics
- Class probabilities computed
- Final predictions saved for comparison

The primary evaluation metric was Sensitivity, because:

Failing to detect a true infertility case (false negative) has greater clinical consequences than a false positive.


# MODELS
1. Naive Bayes Model
Hyperparameter Tuning

Grid search over:
- Laplace smoothing (0–2)
- Classic Naive Bayes (no kernel, no variance adjustment)

Best model:
- Classic Naive Bayes
- Laplace = 0.5

SMOTE Was Not Used because artificially alters class proportions.

Since Naive Bayes relies directly on:
                           P(Y) and   P(X∣Y)

balancing the dataset changes prior probabilities and leads to overestimation of the minority class.

When SMOTE was applied:
- Sensitivity ≈ 1
- Specificity ≈ 0

Performance: 

- Confusion Matrix (Test Set):

                            TN: 35; TP: 10; FN: 14; FP: 14

- Metrics:

                Accuracy: 0.616; Sensitivity: 0.714; Specificity: 0.417

Interpretation:

The model detects most infertility cases. It is biased toward the majority class. Moderate predictive performance.



2. Random Forest

Initially trained without class balancing, resulting in strong bias toward the majority class.

After applying SMOTE:

- Improved balance between sensitivity and specificity
- Optimal mtry = 4

Performance:

                        Sensitivity: 0.755; Specificity: 0.583

Random Forest achieved a better balance between detecting positive and negative cases.


3. XGBoost

Configuration:

- 5-fold cross-validation
- Hyperparameter grid search
- Optimization for Sensitivity

Best model:
- nrounds = 100
- max_depth = 2 (shallow trees)
- Conservative and regularized configuration

With SMOTE applied:

                  ROC: 0.616; Sensitivity: 0.694; Specificity: 0.625

XGBoost provided the most balanced specificity among models


# Model Comparison

Naive Bayes prioritizes sensitivity but lacks specificity. Random Forest achieves best sensitivity. XGBoost offers best balance overall. Ensemble methods outperform Naive Bayes in overall discrimination.

# Proposed Clinical Strategy

A hybrid approach may be optimal:
1. Use Naive Bayes as a screening model (maximize sensitivity).
2. Apply Random Forest or XGBoost to predicted positives for refinement.

This leverages high detection rate of Naive Bayes and stronger discrimination of ensemble models


