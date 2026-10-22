# Daily Bike Demand Time-Series Regression

Predicting aggregate daily shared bike rental demand from calendar and meteorological features using chronological validation.

---

## Overview

* **Task:** Retrospective conditional demand regression on the UCI Bike Sharing dataset.
* **Selected Model:** Ridge Regression ($RMSE = 1165.65$, $R^2 = 0.6134$).
* **Baseline:** Dummy Baseline ($RMSE = 2560.56$, $R^2 = -0.8657$).
* **Primary Predictor:** Feeling temperature (`atemp`) yielded the highest permutation importance drop (326.69).

---

## Evaluation & Results

Evaluation uses expanding-window cross-validation with a 7-row gap on 584 training records, followed by a final chronological holdout of 147 rows. Direct target components (`casual`, `registered`) were excluded to prevent target leakage.

### Final Chronological Holdout

| Model | Metric | Value |
| :--- | :--- | :--- |
| **Ridge Regression** | **RMSE** | **1165.65** |
| Ridge Regression | MAE | 870.67 |
| Ridge Regression | $R^2$ | 0.6134 |
| Dummy Baseline | RMSE | 2560.56 |
| Dummy Baseline | MAE | 2290.41 |
| Dummy Baseline | $R^2$ | -0.8657 |

---

## Data Summary

* **Source:** [UCI Bike Sharing Dataset](https://archive.ics.uci.edu/dataset/275/bike+sharing+dataset) (CC BY 4.0)
* **Quality:** 731 rows, 0 missing cells, 0 duplicates removed.
* **Collinearity:** Strong correlation observed between `temp` and `atemp` ($\vert{}r\vert{} = 0.997$).

---

## Visualizations

| Demand Distributions | CV Model Comparison |
| :---: | :---: |
| ![Distributions](figures/distributions.png) | ![Model Comparison](figures/model-comparison.png) |

| Chronological Predictions | Permutation Importance |
| :---: | :---: |
| ![Time Series](figures/time-series.png) | ![Feature Importance](figures/feature-importance.png) |

---

## Repository Structure

```text
├── figures/                 # Diagnostic, time-series, and residual plots
├── analysis.ipynb           # Interactive workflow and cross-validation walkthrough
├── audit.json               # Environment hashes and pipeline reproducibility data
├── data_dictionary.csv      # Column schemas and data types
├── descriptive_statistics.csv # Parametric summary stats
├── error_analysis.csv       # Holdout residuals and largest error logs
├── feature_importance.csv   # Model-level permutation importance scores
├── metrics.json             # CV and final holdout scores
└── README.md
