# Data Mining — California Housing Case Study

**Program:** MSc Data Science & Business Analytics — Bologna Business School  
**Course:** Data Mining & Machine Learning (Lab 02)  
**Reference:** [Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow](https://www.oreilly.com/library/view/hands-on-machine-learning/9781492032632/) — Aurélien Géron  
**Dataset:** California Housing Census Data (20,640 blocks, 10 attributes)

---

## Overview

End-to-end data mining workflow on California census housing data — from raw data profiling through geospatial visualisation, feature engineering, Pareto frontier analysis, and a full supervised ML prediction pipeline. The notebook follows the canonical Géron case study extended with advanced data analysis techniques including the **Skyline operator** and multi-dimensional Pareto optimisation.

---

## Dataset

**Source:** California Housing dataset via `w4bo/handsOnDataPipelines`  
**Granularity:** One row = one census block group  
**Size:** ~20,640 records

| Variable | Type | Description |
|---|---|---|
| `longitude` / `latitude` | Float | Geographic coordinates of block |
| `housing_median_age` | Float | Median age of houses in block |
| `total_rooms` | Float | Total rooms across all households |
| `total_bedrooms` | Float | Total bedrooms (has missing values) |
| `population` | Float | Block population |
| `households` | Float | Number of households |
| `median_income` | Float | Scaled & capped median income (max 15.0001) |
| `median_house_value` | Float | Target variable — median house value |
| `ocean_proximity` | Categorical | Location relative to ocean (INLAND, NEAR BAY, etc.) |

---

## Analysis Workflow

### 1 — Data Profiling
- `df.info()` and `df.describe()` for schema and statistical overview
- Identified missing values in `total_bedrooms` — handled via imputation strategy
- Explored skewed distributions (median income capped at 15.0001, house values capped at $500K)

### 2 — Geospatial Visualisation
- Scatter plot of latitude vs longitude with:
  - Point size proportional to `population`
  - Colour mapped to `median_house_value` (jet colormap)
- Revealed clear coastal premium — highest values concentrated in Bay Area and LA coast
- Integrated open data context for enriched geographic interpretation

### 3 — Categorical Analysis — Ocean Proximity
- `value_counts()` and histogram for `ocean_proximity` distribution
- Seaborn scatterplot coloured by ocean proximity to show geographic clustering of categories
- Computed mean values per `ocean_proximity` for all numerical features

### 4 — Memory Optimisation
- Demonstrated dtype downcasting: `float64 → float32` across all numeric columns
- Measured memory reduction — practical technique for large-scale datasets

### 5 — Correlation Analysis
- Pearson correlation matrix filtered to strong relationships
- Pairplot on key variables: `median_income`, `housing_median_age`, `median_house_value`, `households`, `population`, `total_rooms`
- Identified `median_income` as strongest predictor of `median_house_value` (r ≈ 0.69)

### 6 — Feature Engineering
Three derived features engineered:
- `rooms_per_household = total_rooms / households`
- `population_per_household = population / households`
- `bedrooms_per_room = total_bedrooms / total_rooms`

These per-household ratios proved more predictive than raw totals.

### 7 — Pareto Frontier & Skyline Operator
Advanced multi-objective optimisation analysis:

**2D Pareto Frontier** — *price vs rooms_per_household*:
```python
from paretoset import paretoset
mask = paretoset(df[["median_house_value", "room_per_household"]], sense=["min", "max"])
```
Identifies blocks with the best trade-off between low cost and high room density.

**3D Skyline** — *age, rooms_per_household, price*:
Extended to three dimensions — youngest housing, most rooms, lowest price. The Skyline operator computes the Pareto optimum across all three objectives simultaneously, surfacing blocks that are non-dominated across all dimensions.

### 8 — ML Prediction Pipeline (Exercise 3)
Full supervised learning pipeline for `median_house_value` prediction:
- Random seed set for reproducibility (`RANDOM_SEED = 42`)
- Missing value imputation (`total_bedrooms`)
- One-hot encoding for `ocean_proximity`
- Feature scaling and train/test split
- Model training, evaluation, and comparison

---

## Key Concepts Demonstrated

| Concept | Technique |
|---|---|
| Exploratory Data Analysis | Profiling, distributions, correlation |
| Geospatial Analysis | Lat/lon scatter, population-weighted maps |
| Multi-objective Optimisation | Pareto frontier, Skyline operator |
| Feature Engineering | Per-household ratio features |
| Missing Data | Imputation strategies |
| ML Pipeline | End-to-end prediction workflow |

---

## Tech Stack

| Category | Tools |
|---|---|
| Language | Python 3.x (Google Colab) |
| Data Processing | Pandas, NumPy |
| Visualisation | Matplotlib, Seaborn |
| Optimisation | paretoset |
| Machine Learning | Scikit-learn |
| Environment | Jupyter / Google Colab |

---

## Files

```
Data_Mining/
├── lab_02_housing.ipynb    # Full data mining notebook
└── README.md
```

---

## Academic Context

**Course:** Data Mining & Machine Learning  
**Lab:** Lab 02 — California Housing Case Study  
**School:** Bologna Business School — MSc Data Science & Business Analytics  
**Reference:** Géron, A. (2019). *Hands-On Machine Learning with Scikit-Learn, Keras & TensorFlow* (2nd ed.). O'Reilly Media.
