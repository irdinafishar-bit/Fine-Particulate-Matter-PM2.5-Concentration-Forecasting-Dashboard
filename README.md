# Fine-Particulate-Matter-PM2.5-Concentration-Forecasting-Dashboard
Currently refactoring the preprocessing pipeline to integrate chronological splitting and hybrid gap-length imputation ahead of Streamlit deployment.

# Fine Particulate Matter (PM2.5) Concentration Forecasting Dashboard

![Status](https://img.shields.io/badge/Status-In%20Progress-yellow)
![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Framework](https://img.shields.io/badge/Frontend-Streamlit-red)

## Overview
An end-to-end environmental data science project that predicts hourly fine particulate matter ($PM_{2.5}$) concentrations using meteorological parameters and translates predictions into actionable US EPA Air Quality Index (AQI) health advisories via an interactive Streamlit web dashboard.

## Project Roadmap
- [x] **Phase 1: Problem Formulation & Literature Review** (CRISP-DM framework)
- [x] **Phase 2: Data Preparation & Leakage-Free Preprocessing** (Chronological split & hybrid imputation)
- [ ] **Phase 3: Feature Engineering & Baseline Modeling** (Ridge, Random Forest, XGBoost, LightGBM)
- [ ] **Phase 4: Hyperparameter Optimization & Evaluation** (10-fold CV via `RandomizedSearchCV`)
- [ ] **Phase 5: Deployment** (Streamlit UI + live OpenWeather REST API integration)

## Technical Methodology
* **Dataset:** UCI / Beijing $PM_{2.5}$ Hourly Dataset (43,800 hourly observations across 5 years).
* **Leakage Prevention:** Strict chronological 80/20 train-test split applied prior to imputation, scaling, and lag generation].
* **Hybrid Missing Value Imputation:**
  * Short sensor outages ($\le 5$ hours): Temporal linear interpolation.
  * Extended outages ($> 5$ hours): Multivariate Random Forest Regressor trained exclusively on non-missing training records.
* **Feature Engineering (17 Features):**
  * Cyclical trigonometric encoding (`sin`/`cos`) for hour of day and month.
  * Autoregressive target lags ($PM_{2.5, t-1}$, $PM_{2.5, t-2}$, $PM_{2.5, t-24}$).
  * 1-hour lagged meteorological drivers (temperature, dew point, pressure, wind speed).
* **Model Benchmarking:** Comparing regularized linear baselines (Ridge with polynomial interaction features) against tree ensembles (Random Forest, XGBoost, LightGBM) using RMSE, MAE, $R^2$, and inference latency.

## Benchmark Results *(Updating Soon)*
| Model | Tuned RMSE ($\mu g/m^3$) | Tuned MAE ($\mu g/m^3$) | $R^2$ Score | Inference Time |
| :--- | :---: | :---: | :---: | :---: |
| Ridge Regression | *TBD* | *TBD* | *TBD* | *TBD* |
| Random Forest | *TBD* | *TBD* | *TBD* | *TBD* |
| XGBoost | *TBD* | *TBD* | *TBD* | *TBD* |
| LightGBM | *TBD* | *TBD* | *TBD* | *TBD* |

## Tech Stack
* **Data Processing & ML:** `pandas`, `numpy`, `scikit-learn`, `xgboost`, `lightgbm`
* **Deployment & APIs:** `streamlit`, `requests`, OpenWeather API
