## Bayesian Networks and Naive Bayes for Breast Cancer Diagnosis
# Project Overview

This project presents a comprehensive Bayesian analysis applied to a breast cancer dataset where the target variable is:

diagnosis → Malignant (M) or Benign (B)

The objective is to:
- Transform continuous medical variables into categorical variables for Bayesian Networks.
- Build and compare different Bayesian Network structures.
- Train and optimize a Naive Bayes classifier.
- Extract interpretability and clinical insights from the models.

The project combines probabilistic graphical models and machine learning classification, emphasizing both predictive performance and interpretability.

# Dataset Description
Binary dependent variable: diagnosis
- Malignant
- Benign

30 numeric predictors describing tumor characteristics:
- Radius
- Perimeter
- Area
- Texture
- Smoothness
- Compactness
- Concavity
- Concave points
- Symmetry
- Fractal dimension

Each variable is available in three versions:
- mean
- standard deviation
- worst

For modeling purposes, only the “worst” variables were selected because they represent extreme tumor values, which are clinically more relevant for malignancy detection.


1. Data Preprocessing
Creation of a Parallel Dataset (datos_redes)

Bayesian Networks require categorical variables. Therefore:
- Continuous variables were discretized into 3 or 4 categories.
- Discretization was justified using class-conditional histograms.
- Categories were defined using quantiles:
      A.Highly discriminative variables → 4 levels
         (Low, Medium-Low, Medium-High, High)
      B.Moderately discriminative variables → 3 levels
         (Low, Medium, High)

This approach:
- Reduces dimensionality
- Avoids redundancy
- Improves interpretability
- Preserves discriminative power


2. Bayesian Networks
Six predictive variables were selected:
- radius_worst
- perimeter_worst
- area_worst
- concavity_worst
- concave_points_worst
- compactness_worst

These capture both tumor size and morphological irregularity.

A) Fully Manual Bayesian Network (Structure + Probabilities)
*Structure*

Size chain:
radius → perimeter → area

Morphology chain:
area → concavity → concave_points → compactness

Diagnosis depends on:
- area
- concavity
- compactness

Probabilities were manually assigned based on:
- Clinical intuition
- Logical tumor progression patterns

*Markov Blanket*

For diagnosis, the Markov Blanket contains:
- area_worst
- concavity_worst
- compactness_worst

Meaning:

Once these three variables are known, all other variables become irrelevant for predicting diagnosis.

Example Inference

If area = High and concavity = High, then the P(Malignant) ≈ 84%

B) Manual Structure with Data-Driven Probabilities
- DAG defined manually based on medical reasoning.
- Conditional probability tables estimated from data.
- Laplace smoothing applied to avoid zero probabilities.

Here diagnosis depends on all six predictors this produces high interpretability, clinically coherent relationships and slightly more complex structure

C) Automatic Bayesian Network (Hill-Climbing Algorithm)

Structure learned using:
- Hill-Climbing search
- BIC score optimization

Key Findings

The automatic model identified concave_points_worst and radius_worst as the main parents of diagnosis. This suggests tumor size and extreme concave points concentrate most predictive information.

Some relationships differ from manual models, but reflect statistical dependencies found in data rather than causal assumptions.


FINAL SELECTION: 
The automatic network was selected because It reduces redundancY, Concentrates predictive information, Maintains clinical plausibility and likely generalizes better


3. Naive Bayes Classifier
Train/Test Split with 70% Training and 30% Testing, using stratified sampling to preserve class proportions

Model Training
- Categorical Naive Bayes
- Laplace smoothing
- 5-fold cross-validation
- Sensitivity prioritized (clinical importance of detecting malignancy)

Optimal Hyperparameters
- Laplace = 0
- Kernel = FALSE
- Adjust = 1

Cross-validation confirmed the baseline model was already optimal.

When evaluating Malignant as the positive class, sensitivity (Recall for Malignant) ≈ 98.4% and specificity ≈ 90.6%. This is clinically desirable because missing a malignant tumor (false negative) is more dangerous than a false positive.




# Clinical interpretation
- Size variables show progressive malignancy risk.
- Shape irregularity variables (concavity, concave points, compactness) are extremely discriminative.
- Extreme morphological irregularity is highly indicative of malignancy.
Both Bayesian Networks and Naive Bayes provide:
- Strong predictive performance
- Clear probabilistic interpretation
- Clinically meaningful insights


This project demonstrates how:
- Bayesian Networks provide structural interpretability and dependency analysis.
- Naive Bayes offers strong predictive power with transparent probabilistic reasoning.
- Automatic structure learning can outperform manual modeling in predictive focus while maintaining coherence.

The combination of probabilistic modeling and clinical reasoning makes this approach powerful for medical decision support systems.









