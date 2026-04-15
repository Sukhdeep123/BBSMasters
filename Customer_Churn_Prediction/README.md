# Customer Churn Prediction — LightGBM & XGBoost

**Program:** MSc Data Science & Business Analytics — Bologna Business School  
**Team:** Individual Project  
**Dataset:** 1.4M-record Italian Auto-Insurance Dataset (2015–2020)

---

## Overview

This project tackles customer churn prediction for an Italian auto-insurance company using a real-world dataset spanning six years of policy data. The goal was to build a production-ready binary classification pipeline capable of identifying at-risk policyholders before renewal, enabling targeted retention interventions.

The dataset was assembled from four relational sources:

| Table | Description |
|---|---|
| `CLIENT` | Policyholder demographics & customer attributes |
| `CONTRACT` | Policy terms, coverage type, premium data |
| `CONTRACT_DATES` | Renewal and cancellation event timestamps |
| `INFOMOTOR` | Vehicle metadata (make, model, year, engine) |

---

## Business Problem

Insurance churn is costly — acquiring a new customer costs 5–7× more than retaining an existing one. The challenge was predicting which policyholders would **not renew** their contract, using historical behavior and contract features, so the business could intervene with targeted offers.

Key constraints:
- Severe class imbalance (churned customers are the minority class)
- Need for high **recall** (missing a churner is worse than a false positive)
- Model must be **interpretable** to business stakeholders

---

## Data Engineering & Feature Engineering

- Merged four source tables on `client_id` and `contract_id` keys
- Engineered **14 final features** including:
  - `Total_Warranties` — aggregated coverage count per policy (custom engineered feature)
  - Policy tenure, payment method, vehicle age, premium amount
  - Renewal history indicators, contract type flags
- Applied label encoding for categorical features
- Handled missing values with median/mode imputation per feature group

---

## Class Imbalance — SMOTE

The dataset had significant class imbalance (churners ~15–20% of total). Applied **SMOTE (Synthetic Minority Over-sampling Technique)** on the training set only (after train/test split) to prevent data leakage while generating synthetic minority samples for balanced training.

---

## Models Trained

Four classifiers were benchmarked with full hyperparameter tuning:

| Model | Configuration |
|---|---|
| **LightGBM** | `num_leaves`, `learning_rate`, `n_estimators`, `min_child_samples` grid search |
| **XGBoost** | `max_depth`, `eta`, `subsample`, `colsample_bytree` grid search |
| **Logistic Regression** | L2 regularization, baseline benchmark |
| **Random Forest** | `n_estimators`, `max_depth`, `min_samples_split` |

All experiments tracked with **Weights & Biases (WandB)** — full run history, hyperparameter logs, and metric comparisons available in the WandB project dashboard.

---

## Results

**Winner: LightGBM**

| Metric | LightGBM | XGBoost |
|---|---|---|
| AUC-ROC | **0.884** | 0.871 |
| Recall | **93.6%** | 89.2% |
| Precision | ~72% | ~74% |
| F1 Score | ~0.816 | ~0.808 |

LightGBM outperformed on both AUC and recall. Given the business objective (minimize missed churners), recall was the primary optimization metric.

---

## Model Interpretability — SHAP

Applied **SHAP (SHapley Additive exPlanations)** on the final LightGBM model:
- Generated global feature importance summary plots
- Produced individual SHAP waterfall plots for local explanations
- Key drivers: `Total_Warranties`, policy tenure, premium level, vehicle age
- SHAP values used to communicate model decisions to non-technical stakeholders

---

## Interactive Dashboard

An interactive churn analytics dashboard (`churn_dashboard_v6.html`) was built to visualize:
- Churn rate by customer segment
- Feature distribution comparisons (churned vs retained)
- Model performance metrics and confusion matrix
- SHAP importance rankings

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.x |
| ML Models | LightGBM, XGBoost, Scikit-learn |
| Imbalance Handling | imbalanced-learn (SMOTE) |
| Interpretability | SHAP |
| Experiment Tracking | Weights & Biases (WandB) |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn, Plotly |

---

## Files

```
Customer_Churn_Prediction/
├── S_LightGBM_XGBoost_ML_Churn.ipynb    # Main analysis notebook
├── churn_dashboard_v6.html               # Interactive dashboard
└── README.md
```

---

## Academic Context

**Course:** Machine Learning for Business Analytics  
**School:** Bologna Business School — MSc Data Science & Business Analytics  
**Dataset Source:** Real Italian insurance company data (anonymized), provided via academic collaboration
