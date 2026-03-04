## Bayesian Networks for Sales Prediction
Inference, Simulation and Structure Learning

This project develops a Bayesian Network model to analyze how promotions, weekend/holiday effects, demand, and stock availability influence the probability of high sales.

The goal is to model causal relationships, perform probabilistic inference, compare exact vs Monte Carlo methods, and evaluate structure and parameter learning from simulated data.

# Objective

We model how:
- Promotion (P)
- Weekend/Holiday (f)
- Demand (D)
- Stock Availability (S)
- High Sales (V)

affect the probability of observing high sales.

# Bayesian Network Structure

We define a Directed Acyclic Graph (DAG): [P][f][D|P:f][V|D:S][S]
Dependencies:
- P (Promotion) → independent
- f (Weekend/Holiday) → independent
- S (Stock) → independent
- D (High Demand) depends on P and f
- V (High Sales) depends on D and S

Interpretation:

Promotions and weekends influence demand. Sales depend on both demand and stock availability. Without stock, high sales are impossible.Demand acts as a mediator between promotions and sales.

# Libraries Used
bnlearn

gRain

knitr

# Conditional Probability Tables (CPTs)

We manually define prior probabilities based on domain knowledge.

Examples:
- High demand is very likely when both promotion and weekend occur:

                                    P(D=1∣P=1,f=1)=0.95
- High sales are almost certain when demand and stock are both high:

                                     P(V=1∣D=1,S=1)=0.98

These probabilities reflect reasonable business assumptions before observing real data.


# Markov Blanket Analysis

For each node, we compute its Markov Blanket — the minimal set of variables required for optimal prediction.

Key insights:
- Demand is fully determined by promotion and weekend.
- Sales are directly influenced only by demand and stock.
- Promotion and weekend are independent unless conditioning on downstream variables.

This confirms the causal structure encoded in the DAG.

# Conditional Independence (d-Separation)

We verify independence relationships:
- Promotion and weekend are independent.
- Demand is not independent of promotion.
- Sales are not independent of demand.
- Conditioning on common effects introduces dependencies (explaining-away phenomenon).

This validates the causal logic of the network.


# Synthetic Data Generation

We simulate:
- 1,000 observations (initial validation)
- 2,000 observations (structure learning phase)

using forward sampling from the defined Bayesian Network.

This allows controlled testing of inference and learning algorithms.


# Exact inference vs Monte Carlo

For example:
      P(D=1∣P=0,f=1)

Exact: 0.706
Monte Carlo: 0.754

Differences are small and mainly occur for rare events due to sampling variability. So the network behaves consistently under both inference methods.


# Structure Learning

Using simulated data (n = 2000), we test three algorithms:
- Hill-Climbing (HC)
- Grow-Shrink (GS)
- MMHC (Hybrid)

We evaluate:
- Hamming Distance (difference from original DAG)
- BIC Score (model fit)

Results:

Grow-Shrink and MMHC perfectly recover the original structure. Hill-Climbing introduces a minor structural difference. MMHC achieves the best BIC score.

So MMHC performs best overall.


# Parameter Learning

We estimate parameters using:
- Maximum Likelihood Estimation (MLE)
- Bayesian estimation

Key results confirm expected relationships:

Very high probability of sales when demand and stock are high. Sales probability decreases significantly when demand is low. Promotions strongly increase demand, especially during weekends.






