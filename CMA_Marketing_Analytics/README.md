# Customer Marketing Analytics — Social Media Influencer Campaign Analysis

**Program:** MSc Data Science & Business Analytics — Bologna Business School  
**Course:** Customer Marketing Analytics (CMA) — Assignment 1, 2026  
**Dataset:** Social Media Influencer Campaign Data (Team Assignment 1 Data 2026)

---

## Overview

This project analyses social media influencer marketing campaign data to understand what drives audience engagement, click-through behaviour, and comment volume. Using a multi-model regression approach, the analysis answers four business-critical questions for a marketing analytics team — each requiring a different statistical model suited to the outcome variable's distribution.

---

## Business Questions

| # | Question | Outcome Variable | Method |
|---|---|---|---|
| Q1 | What predicts Engagement Rate? | `Engagement_Rate` (continuous) | OLS Linear Regression |
| Q2 | What predicts Click-Through? | `Click_Through` (binary 0/1) | Binary Logistic Regression |
| Q3 | What predicts Comment Count? | `Comment_Count` (count) | Negative Binomial Regression |
| Q4 | Do interactions improve the Engagement model? | `Engagement_Rate` | OLS + Interaction Terms |

---

## Dataset

**Source:** Team Assignment 1 Data 2026 (`Team Assignment 1 Data 2026.csv`)  
**Format:** Semicolon-delimited CSV  
**Domain:** Social media influencer campaign performance records

### Key Variables

| Variable | Type | Description |
|---|---|---|
| `Engagement_Rate` | Continuous | % of audience that engaged with post |
| `Click_Through` | Binary | Whether post generated a click (0/1) |
| `Comment_Count` | Count | Number of comments on post |
| `Platform` | Categorical | Social media platform (Instagram, TikTok, YouTube, etc.) |
| `Post_Type` | Categorical | Content format (video, image, carousel, story) |
| `Influencer_Tier` | Categorical | Nano / Micro / Macro / Mega |
| `Caption_Sentiment` | Categorical | Sentiment of post caption (positive/neutral/negative) |
| `Topic_CTA_Positive` | Binary | Whether post includes a positive call-to-action |

---

## Methodology

### Q0 — Data Overview & Variable Preparation
Descriptive statistics computed for all key metrics (`Engagement_Rate`, `Click_Through`, `Comment_Count`). Variables encoded for regression modelling — categorical variables converted to dummy/indicator format, reference categories established.

### Q1 — OLS Linear Regression (Engagement Rate)
- **Predictors:** Platform, Post_Type, Influencer_Tier, Caption_Sentiment, Topic_CTA_Positive
- **Model:** Ordinary Least Squares via `statsmodels.formula.api`
- **Interpretation:** β coefficients — marginal effect of each predictor on engagement rate, holding others constant
- **Diagnostics:** R², F-statistic, residual analysis

### Q2 — Binary Logistic Regression (Click-Through)
- **Predictors:** Platform, Post_Type, Topic_CTA_Positive, Caption_Sentiment
- **Model:** `smf.logit()` — binary outcome (0/1)
- **Interpretation:** Log-odds ratios converted to odds ratios (exp(β)) for business interpretation
- **Evaluation:** Pseudo-R², likelihood ratio test, classification accuracy

### Q3 — Negative Binomial Regression (Comment Count)
- **Predictors:** Platform, Influencer_Tier, Post_Type
- **Why Negative Binomial?** Count outcome with overdispersion (variance >> mean in `Comment_Count`). Poisson vs Negative Binomial comparison performed first — AIC comparison used to justify model selection
- **Interpretation:** Incidence Rate Ratios (IRR = exp(β)) — multiplicative effect on expected comment count
- **Output:** AIC, N, IRR table with confidence intervals

### Q4 — OLS with Interaction Terms
- **Extension of Q1** with two interaction terms added:
  - `Topic_CTA_Positive × Platform` — Does CTA effectiveness vary by platform?
  - Additional interaction explored for model improvement
- **Evaluation:** Compared AIC/R² against base Q1 model to test whether interactions significantly improve fit

---

## Key Results

A cross-model summary table was produced comparing predictor effects across all three regression frameworks:

| Variable | Q1 OLS β | Q2 Log Odds Ratio | Q3 IRR |
|---|---|---|---|
| Platform (vs baseline) | Varies | Varies | Varies |
| Topic_CTA_Positive | + | + | + |
| Influencer_Tier (Macro/Mega) | + | — | + |
| Caption_Sentiment (Positive) | + | + | — |
| Post_Type (Video) | + | + | + |

*Full coefficient tables, p-values, and confidence intervals available in the notebook and presentation.*

---

## Presentation

The full analysis and findings are summarised in `BBS_CMA_Assignment1_2026_MODERN_v6.pptx` — a slide deck prepared for the course assignment submission covering methodology, model outputs, and marketing recommendations.

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.x (Google Colab) |
| Statistical Modelling | statsmodels (OLS, Logit, Negative Binomial) |
| Data Processing | Pandas, NumPy |
| Visualization | Matplotlib, Seaborn |
| Presentation | PowerPoint (PPTX) |

---

## Files

```
CMA_Marketing_Analytics/
├── BBS_CMA_Analysis_Colab.ipynb              # Full analysis notebook (4 regression models)
├── BBS_CMA_Assignment1_2026_MODERN_v6.pptx   # Presentation deck with results & recommendations
└── README.md
```

---

## Academic Context

**Course:** Customer Marketing Analytics (CMA)  
**Assignment:** Team Assignment 1 — 2026  
**School:** Bologna Business School — MSc Data Science & Business Analytics
