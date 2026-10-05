# Normal Transformation — Parkinson's Disease Analysis

## Overview
Comparison of three data transformation techniques applied to the 
Parkinson's Telemonitoring dataset. Investigates how Z-score, Robust 
Scaling and Logarithmic transformations affect linear regression model 
performance in predicting disease severity (total_UPDRS score).

## Research Question
Does data transformation improve prediction of Parkinson's disease 
severity? Which transformation technique produces the most accurate 
regression model?

## Dataset
- Parkinson's Telemonitoring Dataset (UCI Machine Learning Repository)
- 5,875 observations of Parkinson's patients
- Target: total_UPDRS (disease severity score)
- Features: voice measurements — Jitter, Shimmer, HNR, RPDE, DFA, PPE

## Data Quality & Cleaning

### Issues Found and Fixed:
- Missing subject IDs — inferred from age and sex combinations
- Data entry errors — age=650 corrected to 65, age=749 corrected to 74
- Missing age values — filled from subject reference table
- Negative time values — converted to absolute values
- Negative Jitter.PPQ5 and Shimmer.APQ3 values — removed as invalid
- Outliers — Jitter.PPQ5 > 8 and Shimmer.APQ3 > 5 removed

## Exploratory Analysis

### Correlation Analysis (3 pairs):
1. **Jitter vs Shimmer** — 2D density, scatter and 3D surface plots
2. **Jitter vs PPE** — 2D density, scatter and 3D surface plots  
3. **Jitter vs NHR** — 2D density, scatter and 3D surface plots

## Four Models Compared

### Model 1 — No Transformation (Baseline)
- Raw features: Jitter.Abs, Shimmer.APQ5, HNR, RPDE, DFA, PPE, age
- Predicts total_UPDRS directly

### Model 2 — Z-Score Standardization
- Applied StandardScaler equivalent (scale() in R)
- All features normalized to mean=0, std=1
- Predicts total_UPDRS_Zscore

### Model 3 — Robust Scaling
- Applied median and IQR based scaling manually
- More resistant to outliers than Z-score
- Predicts total_UPDRS_robust

### Model 4 — Logarithmic Transformation
- Applied log10(x+1) to all skewed features
- Handles right-skewed distributions
- Predicts total_UPDRS_log

## Model Comparison

| Model | Transformation | R-squared | Key Insight |
|---|---|---|---|
| Model 1 | None | — | Baseline |
| Model 2 | Z-Score | — | Standardized |
| Model 3 | Robust Scaling | — | Outlier resistant |
| Model 4 | Log Transform | — | Handles skew |

## Key Findings
- Voice measurements (Jitter, Shimmer) are significant predictors
- Age contributes meaningfully to disease severity prediction
- Transformation technique affects model interpretability more than accuracy
- HNR (Harmonics to Noise Ratio) consistently selected as key predictor

## Connection to Variable Selection Project
This project complements the Variable Selection project on the same dataset:
- Variable Selection identifies WHICH features matter
- Normal Transformation explores HOW to best prepare those features
- Together they provide a complete analytical framework for the dataset

## Technologies
- R programming language
- RStudio
- ggpubr, cowplot (visualization)
- plotly (3D density plots)
- dlookr (outlier detection)
- Base R linear regression (lm)

## Dataset Source
UCI Machine Learning Repository — Parkinson's Telemonitoring Dataset
