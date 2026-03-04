## BAYESIAN INFERENCE IN PRACTICE
This project applies Bayesian statistical modeling to analyze survey data from 4th-year Data Science students.

The objetcive is to combine:
- Prior belifs (elicited before observing the data)
- Observed survey responses
- Conjugate Bayesian models

To obtain posterior distributions, quantify uncertinity, and geenrate predictive insights about future students

The goal is to estimate the true proportion of students enrolled in a Bayesian elective, evaluate how many enrolled students chose it as a first option, measure overall interest in Bayesian analysis, model daily ChatGpt usage among students and predict future enrollment and behaviour under uncertainty.

Unlike a purely descriptive analysis, this approach explicity models uncertainity and updates belifs using Bayes' theorem.

# Survey description
1. Are you enrolled in the Bayesian Analysis elective? (Yes/No)
2. If enrolled, was it your first option? (Yes/No)
3. Interest in Bayesian data analysis (1-5 scale)
4. Average number of daily ChatGpt uses (0-10+)

A total of 31 respondes were collected (8 enrolled, 23 not enrolled)

# Libraries
dplyr

tidyverse

HDInterval

# Bayesian Models Applied:
- Beta-binomial for proportiosn
- Poisson -Gamma for count data

# QUESTIONS
1. Enrollement proportion
Prior --> based on prior belifs from three students, the average estimated proportion was p=0.2467.

The moderate-strength prior is p∼Beta(2.6,7.4)

Posterior results --> Posterior mean ≈ 0.25 and 95% Credible Interval [0.13,0.40], the distribution is fairly symmetric, indicating stability.

Predictive Simulation --> 13 will be the expected enrolled students, with a 95% predictive interval [5,23], uncertainity reduction compared to prior = 9%.

So enrollment is likely between 19% and 32% with moderte uncertainity due to small sample size.

2. First Option Choice
Prior --> No prior knowledge avaiable: non-informative prior  p∼Beta(1,1); Uniform over [0,1]

Posterior results --> Posterior mean ≈ 0.20 and 95% credible interval width reduced from:
- Prior: 0.95
- Posterior: 0.454

Strong uncertainty reduction due to data.

Predictive --> 
Expected first-option choices:
2–3 students
Plausible range: 0–6.
The elective is rarely selected as first preference.


3. Interest in Bayesian Analysis
The original scale (1-5) is ordinal and cannot be directly modeled with Beta, so we transfrom :

Interest High = 1 if interest >=3

Prior --> Non-informative  p∼Beta(1,1)
Posterior results --> Posterior mean ≈ 0.79. 95% credible interval: [0.64,0.91]

The posterior is highly concentrated and symmetric.

Predictive --> 
Expected high-interest students: ≈39
95% interval:
[32,46]
Uncertainty reduction: substantial (CI width drops from 0.95 to 0.27).
A strong majority shows high interest.


4. Daily ChatGPT usage
ChatGPT usages is count data so will be modeled with λ∼Gamma(α,β)

Prior --> 
Based in scaled prior belif:     λprior≈2.467         λ∼Gamma(2.467,1)

Posterior results -->
Posterior mean ≈ 5 uses per day
95% credible interval:
[4.3,5.8]

Posterior is nearly symmetric. Uncertainty reduction: 74%. Data is highly informative.

Predictive results --> 
- For one student:
Expected ≈ 5 uses/day
Likely range ≈ 2–8 uses

- For 50 students:
Expected ≈ 250 total daily uses
Plausible range ≈ 215–290












