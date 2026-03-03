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
