# Predicting Churn in Italian Motor Insurance — End-to-End ML Project

**Program:** MSc Data Science & Business Analytics — Bologna Business School  
**Course:** Machine Learning for Business Analytics  
**Dataset:** Italian Motor Insurance — Customer-Year Panel (2015–2020)  
**Unit of Analysis:** Customer-Year | ~908,000 observations · 43 variables

---

## 📊 Live Dashboard

> ### 👉 [View Interactive Churn Dashboard](https://strong-dolphin-66a5cd.netlify.app/)
> Explore the full model results, customer segmentation, churn risk scores, and business insights interactively.

---

## Authors

**Machine Learning Fieldwork 2026 | DSBA – Group 5**

| Name |
|---|
| Federico Zabeo |
| Hanna Kassahun Yihunie |
| Francesco Gambera |
| Akosua Ayewa Ofori-Karikari |
| Sukhdeep Singh Saini |
| Sofia Silingardi |
| Maria Alejandra Zapata Gil |

---

## Project Overview

An end-to-end machine learning project focused on predicting customer churn for an Italian motor insurance company, with the goal of enabling targeted retention campaigns and improving customer retention.

The project combines:
- Business understanding
- Data cleaning and preparation
- Churn target definition
- Exploratory data analysis
- Feature engineering
- Predictive modeling
- Business interpretation of model outputs

---

## Business Problem

Customer churn is a major business issue in the insurance industry, especially in highly competitive markets where policyholders can easily switch providers. In this project, we developed a predictive model to identify customers who are most likely to **not renew** their motor insurance policy, so the company can intervene before renewal with personalised retention actions.

The churn rate observed in the dataset is approximately **21.5%** — about 1 in 5 customers does not renew their policy.

---

## Project Objective

Develop a predictive model that estimates the probability of churn within one year, so the business can:
- Prioritise high-risk customers
- Optimise retention campaigns
- Allocate CRM resources more efficiently
- Maximise customer lifetime value

---

## Dataset Description

The project integrates **four sources** of insurance-related data at the customer level:

### Client Data
Demographic and behavioural information:
- Age, seniority, number of accidents
- App usage, risk rating, province of residence

### Contract Data
- Premium amounts, discounts, payment method
- Number of installments, product and risk type
- Warranty indicators / optional coverages

### Contract Dates
- Contract effective date, closing date, expiration date

### Vehicle Data
- Commercial value, vehicle type, power, yearly mileage
- ABS presence, airbag presence, anti-theft presence

---

## Churn Definition

A customer is classified as **churned** when their policy expires and they do **not renew within 366 days** of expiration. This definition reflects the real business meaning of churn. The project distinguishes between:
- Early termination without renewal
- Early termination followed by renewal
- Normal expiration followed by renewal or non-renewal

---

## Data Preparation

Main preprocessing steps:
- Converting date columns into proper datetime format
- Removing columns with too many missing values
- Converting Yes/No fields into binary variables
- Aggregating contract-level data into one row per customer per year
- Restricting data to contracts expiring between 2015 and mid-2020
- Handling multicollinearity and removing leakage-prone features

---

## Exploratory Data Analysis

Key findings from the exploratory analysis:
- Churn remained relatively stable over time, around **21%**
- **New customers** and **mid-tenure customers** (4–7 years) were more likely to churn
- Customers with **no optional coverages** had significantly higher churn rates
- Customers with a **previous churn event** were more likely to churn again
- **Low-premium customers** churned regardless of discount — discount alone is not always an effective retention tool

---

## Feature Engineering

**Final dataset:** ~908,000 observations · 43 variables

Feature selection focused on keeping the most informative predictors while reducing redundancy and leakage. Strongest signals retained:
- **Seniority** — customer tenure
- **Discount** — premium discount level
- **Previous churn** — historical churn indicator
- **Selected coverages** — optional warranty flags

> Expiry-year-related information was removed as it was too strongly correlated with the target and created data leakage.

---

## Modeling Approach

Three models compared using an **out-of-time split** (train on past, test on future — for realistic evaluation):

| Model | Accuracy | ROC-AUC | Recall | Precision |
|---|---|---|---|---|
| Logistic Regression (baseline) | 62.01% | 74.40% | 76.60% | 33.33% |
| XGBoost | 71.90% | **92.80%** | 88.50% | 43.10% |
| **LightGBM** | 71.50% | **93.40%** | 88.40% | 42.60% |

**Evaluation priority:** Recall was the primary metric — in a churn setting, missing a customer who is about to leave is more costly than contacting one who would have stayed.

### Key Results

- The best models catch **~88 out of 100 customers** who would have churned
- Around **43 out of 100** contacted customers are truly at risk
- Even with moderate precision, the model is highly valuable — preventing churn typically justifies the cost of contacting false positives

---

## Business Insights

**High-risk customer segments identified:**
- New clients in their first year
- Mid-tenure clients with 4–7 years of seniority
- Customers with no optional coverages
- Customers with low premium and no discount
- Customers with previous churn history

---

## Recommended Retention Strategy

| Action | Target Segment |
|---|---|
| Contact 60–90 days before renewal | All high-priority predicted churners |
| Reward loyalty programmes | Mid-tenure customers (4–7 years) |
| Demonstrate value / onboarding | New customers (Year 1) |
| Propose add-on coverages | Low-coverage clients |
| Integrate churn scores into CRM | All segments — automated workflow |

---

## Limitations & Next Steps

**Current limitations:**
- Missing behavioural signals (call centre interactions, digital engagement)
- Limited predictive depth due to unavailable CRM and telematics data

**Suggested next steps:**
- Integrate model outputs into CRM systems
- Monitor campaign outcomes and model performance over time
- Retrain the model every 6–12 months
- Enrich the dataset with call centre, digital, and telematics signals

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.x (Jupyter Notebook) |
| Data Processing | Pandas, NumPy |
| Machine Learning | Scikit-learn, XGBoost, LightGBM |
| Visualisation | Matplotlib, Seaborn |
| Evaluation | ROC-AUC, Recall, Precision, Accuracy |

---

## Files

```
ML_Churn_Prediction_Italian_Insurance/
├── DSBA_ML_Churn_prediction.ipynb                    # Full ML notebook
├── Predicting Churn in Italian Motor Insurance.pdf   # Project report
└── README.md
```

---

## Academic Context

**Course:** Machine Learning for Business Analytics  
**School:** Bologna Business School — MSc Data Science & Business Analytics  
**Dataset:** Italian motor insurance company data (anonymised), 2015–2020
