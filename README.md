# Profitability and Risk Segmentation in Retail

## Overview

This project analyzes orders from a retail dataset. The goal is to understand what drives profit margin and to separate high-risk orders from stable ones.

## Why it matters

Retail businesses lose money when they apply discounts or shipping policies without knowing the impact. This project shows patterns that help reduce losses and improve margin.

## What was done

- Cleaned and structured the dataset
- Created features related to location, category, shipping, and discounts
- Tested multiple models:
  - Lasso/Ridge (baseline, poor fit)
  - GAMLSS with t-distribution (better fit, but bimodal residuals)
  - XGBoost / LightGBM (high accuracy, low interpretability)
  - Final model: Mixture of Gaussian Linear Regressions with a concomitant model

## Key findings

- Two clear groups of orders:
  - **Cluster 1 (High Risk)**: Low margins, frequent losses  
    - Share of orders: 31,4%
    - Share of negative margin: 40%
    - Average margin: -13,2%
  - **Cluster 2 (Stable)**: Higher, more consistent margins  
    - Share of orders: 68,6%
    - Average margin: 23,5%

These groups help the business know where it’s losing money and where it's performing well.

## Business impact 

- Orders in Cluster 1 generate $677 of total loss over the period.
- A policy change targeting this group could reduce losses by approximately 67,86%.
- The main cost drivers in Cluster 1 are:
<img width="647" height="408" alt="image" src="https://github.com/user-attachments/assets/77b90099-1e1a-48c0-b982-cf5410c14274" />


## What to do with this

- Review all discount rules 
- Review Tables, Bookcases, Supplies and Machines pricing strategy
- Flag risky orders early using model probabilities

## Model validation

- The EM algorithm was stable after about 10 random restarts
- Bootstrap validation used 1000 resamples
- Performance metrics:
  - RMSE (out-of-sample): 0.06713472
  - R² (out-of-sample): 0.9786957

## Tools used

- Language: R
- Modeling: flexmix, gamlss, xgboost, lightgbm, glmnet
- Visualization: ggplot2
- Parallel computing: foreach, doParallel

## Visuals

**1. Risk-return tradeoff between clusters**  
Shows the difference in expected profit margin and loss probability between the two clusters.  
![Risk vs Margin](https://github.com/user-attachments/assets/a5e49e1f-9626-4335-a656-da1c601d3495)

**2. Operational drivers of high performance**  
Shows the variables most associated with being in the stable, high-margin cluster.  
![Variable Importance](https://github.com/user-attachments/assets/d2cfe6df-1e74-463e-9f5a-f202b0a6645b)

**3. Top 10 most impactful levels per cluster**
Shows variable levels with most impact into margin performance per cluster
<img width="1726" height="1104" alt="image" src="https://github.com/user-attachments/assets/8c4b4905-fea5-45c6-8ab4-57ea3ef7bd52" />

**4. Residual comparison between models**  
Shows how the mixture model handles distribution tails better than a standard linear model.  
![Residuals](https://github.com/user-attachments/assets/d7c83df4-82e9-4a70-8e0d-146c371fc4f6)

**5. Bootstrap validation**  
Shows model stability across resampled datasets.  
![Bootstrap RMSE](https://github.com/user-attachments/assets/9dfbd59b-5bec-4e46-861d-c75ad4a9ab53)

## Final note

This project shows how statistical modeling can support real business decisions. The focus is on clarity, reliability, and action.




