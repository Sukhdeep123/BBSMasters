# BBS Masters — Data Science & Business Analytics Projects

Projects completed during the **MSc in Data Science & Business Analytics** at **Bologna Business School** (University of Bologna).

---

## Projects

| Project | Domain | Key Techniques | Folder |
|---|---|---|---|
| [Customer Churn Prediction](./Customer_Churn_Prediction/) | Machine Learning | LightGBM, XGBoost, SMOTE, SHAP, WandB | `Customer_Churn_Prediction/` |
| [Cross-Domain Opinion Mining](./NLP_Opinion_Mining/) | NLP / Deep Learning | BERT Fine-Tuning, HuggingFace, TF-IDF, WandB | `NLP_Opinion_Mining/` |
| [Customer Marketing Analytics](./CMA_Marketing_Analytics/) | Marketing Analytics | OLS, Logistic Regression, Negative Binomial, statsmodels | `CMA_Marketing_Analytics/` |
| [Data Mining — California Housing](./Data_Mining/) | Data Mining / ML | EDA, Pareto Frontier, Skyline Operator, Scikit-learn | `Data_Mining/` |

---

## Customer Churn Prediction

**Dataset:** 1.4M-record Italian auto-insurance dataset (2015–2020) across 4 relational sources  
**Objective:** Binary classification — predict policy non-renewal for targeted retention  
**Best Model:** LightGBM — **AUC 0.884 | Recall 93.6%**  
**Highlights:** SMOTE for class imbalance, SHAP interpretability, WandB experiment tracking, interactive churn dashboard  

→ [View Project](./Customer_Churn_Prediction/)

---

## Cross-Domain Opinion Mining — BERT & NLP

**Dataset:** ~150K Amazon reviews across Gift Cards & Magazine Subscription domains  
**Objective:** Train sentiment classifier in one domain, evaluate cross-domain transfer robustness  
**Best Model:** Fine-Tuned BERT — **92.15% accuracy**  
**Highlights:** TF-IDF+LR vs frozen BERT vs fine-tuned BERT benchmarking, WandB hyperparameter sweeps, supervised by Prof. Gianluca Moro & Dr. Giacomo Frisoni (DISI, University of Bologna)  

→ [View Project](./NLP_Opinion_Mining/)

---

## Customer Marketing Analytics — Influencer Campaign Analysis

**Dataset:** Social media influencer campaign data — engagement, click-through, comment metrics  
**Objective:** Multi-model regression analysis to identify drivers of campaign performance  
**Models:** OLS Linear Regression, Binary Logistic Regression, Negative Binomial Regression, OLS + Interaction Terms  
**Highlights:** Full model comparison across Q1–Q4, statsmodels pipeline, PowerPoint presentation deck included  

→ [View Project](./CMA_Marketing_Analytics/)

---

## Data Mining — California Housing Case Study

**Dataset:** California census housing data (20,640 blocks, 10 attributes)  
**Objective:** End-to-end data mining workflow — profiling, geospatial visualisation, Pareto frontier analysis, and ML prediction pipeline  
**Highlights:** Skyline operator (multi-objective optimisation), feature engineering, Pareto frontier (2D & 3D), full supervised learning pipeline  

→ [View Project](./Data_Mining/)

---

## Program

**Degree:** MSc Data Science & Business Analytics  
**Institution:** Bologna Business School — University of Bologna  
**Location:** Bologna, Italy
