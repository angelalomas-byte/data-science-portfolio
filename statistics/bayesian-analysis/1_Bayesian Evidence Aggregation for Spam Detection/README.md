## Bayesian Evidence Aggregation for Spam Detection

An advanced Spam / Ham classification system combining:
- Support Vector Machines (SVM)
- LASSO Logistic Regression (GLMNET)
- Bayesian lexical evidence
- Probabilistic calibration analysis

This project integrates machine learning with Bayesian inference to build a highly accurate and interpretable spam detection framework.

## Dataset
The project uses the classic SMS Spam Collection Dataset (spam.csv), containing:
- ham --> tegitimate message
- spam --> unwanted message

Observed class distribution:

𝑃(𝑆𝑝𝑎𝑚)=0.134

Approximately 13.4% of messages are spam (class imbalance present).

## Libraries Used
e1071
quanteda
tidymodels
textrecipes
readr
caret
glmnet
Matrix
pROC
dplyr
ggplot2
ggpubr
here
stopwords

## Project Pipeline
1. Text Preprocessing
Tokenization using quanteda
Removal of:
- punctuation
- numbers
- symbols
- stopwords
Lowercasing
Construction of Document-Term Matrix (DFM)

Output: Clean numerical matrix suitable for modeling.

2. Train/Test Split
80% training
20% testing
Stratified sampling (createDataPartition)
Reproducibility ensured (set.seed)

## IMPLEMENTED METHODS:
MODEL 1: Support Vector Machine (SVM)
Sensitivity ≈ 0.899       Specificity ≈ ~1           AUC ≈ 0.9972        Brier Score ≈ 0.0033

MODEL 2: LASSO Logistic Regression (GLMNET)
L1 regularization
Automatic feature selection
Hyperparameter tuned via CV (cross-validation)
Sensitivity ≈ 0.8725             AUC ≈ 0.9939                      Brier Score ≈ 0.0046

## EXERCISES
1. Bayesian Model Aggregation
Combies SVM predictions & LASSO predictions
The joint probabilities for Spam is 0.784 and for ham 0.0001
The posterior probability of spam is 0.9998, the model agreement drematically increases posterior confidence

2. Bayesian Calibration Analysis
The models used were evaluated using:
- AUC
- Brier Score
- ECE
- MCE

SVM shows slightly better average calibration (lower ECE). Logistic regression is marginally more stable in extreme bins. Both models exhibit near-perfect probabilistic behavior.

3. Bayesian Lexial Analysis
Estimated P(Word∣Spam) & P(Word∣Ham) using Laplace smoothing. The words that strongly increase Spam Probability are 'claim', 'prize', 'won', 'guaranteed', 'awarded'...The words that reduce Spam Probability are 'it', 'gt', 'lor', 'later', 'morning'... more typical conversational tokens from legitimate SMS messages

