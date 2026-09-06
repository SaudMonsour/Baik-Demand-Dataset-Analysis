---

### 3. Bike Demand Analysis (`Baik-Demand-Dataset-Analysis`)

```markdown
# Daily Bike Demand Time-Series Regression

**Time-Series Regression · Demand Forecasting**

Predicting aggregate daily shared bike rental demand using calendar schedules and observed meteorological conditions evaluated on a strict chronological split.

---

## Overview

* **Objective:** Forecast daily rental demand (`cnt`) conditionally using calendar flags and weather features.
* **Dataset:** 731 daily records (UCI Bike Sharing Dataset).
* **Selected Model:** **Ridge Regression** (Holdout $RMSE = 1165.65$, $R^2 = 0.6134$).
* **Top Feature:** Feeling temperature (`atemp`) yielded the highest permutation importance drop (326.69).

---

## Evaluation Design & Results

* **Split Strategy:** Expanding-window CV with a 7-row gap; final chronological holdout of 147 days.
* **Leakage Guard:** `casual` and `registered` columns strictly excluded (direct sums of target).

### Final Chronological Holdout

| Model | RMSE | MAE | $R^2$ |
| :--- | :--- | :--- | :--- |
| **Ridge Regression** | **1165.65** | **870.67** | **0.6134** |
| Random Forest (CV Candidate) | 1465.81 | — | — |
| Dummy Baseline | 2560.56 | 2290.41 | -0.8657 |

---

## Visualizations

| Feature Distributions | Model CV Comparison |
| :---: | :---: |
| ![Distributions](figures/distributions.png) | ![Model Comparison](figures/model-comparison.png) |

| Chronological Demand Forecast | Permutation Importance |
| :---: | :---: |
| ![Time Series](figures/time-series.png) | ![Feature Importance](figures/feature-importance.png) |

---

## Repository Structure

```text
├── figures/                   # Chronological tracking, residuals, and importance plots
├── analysis.ipynb             # Notebook detailing chronological cross-validation
├── audit.json                 # Data integrity record and configuration run trace
├── data_dictionary.csv        # Column dictionary and temporal coverage details
├── descriptive_statistics.csv # Parametric and non-parametric distribution metrics
├── error_analysis.csv         # Chronological residual analysis and max error points
├── feature_importance.csv     # Permutation score drops across candidate predictors
├── metrics.json               # Final validation and holdout performance values
└── README.md
