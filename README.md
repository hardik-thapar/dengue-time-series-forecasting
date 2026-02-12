Good.
We’ll write this like a serious ML engineer — minimal, precise, no fluff, no emojis, no hype.

This is what should sit in your root README.md:

⸻


# Dengue Time-Series Forecasting

This repository contains a structured machine learning pipeline for forecasting weekly dengue cases in San Juan (Puerto Rico) and Iquitos (Peru) using environmental and temporal features.

The project is based on the DrivenData “DengAI: Predicting Disease Spread” dataset and focuses on disciplined time-series modeling, proper validation strategy, and reproducible experimentation.

---

## Problem

Given weekly climate observations indexed by:

(city, year, weekofyear)

the objective is to predict the number of reported dengue cases (`total_cases`) for future weeks.

Evaluation metric: Mean Absolute Error (MAE).

The test data represents a pure future hold-out set. Therefore, chronological validation is required during model development.

---

## Approach

The modeling workflow follows a structured progression:

1. Exploratory Data Analysis (EDA)
2. Baseline regression models (Linear Regression, Random Forest)
3. Temporal feature engineering:
   - Autoregressive lags (1–4 weeks)
   - Rolling statistics (4 and 8 weeks)
   - Rolling standard deviation
4. Log transformation of the target variable
5. Chronological cross-validation using `TimeSeriesSplit`
6. Final model using CatBoost Regressor (MAE loss)

All experiments were conducted with strict temporal ordering and without shuffling.

---

## Results (Cross-Validated)

| City       | Baseline MAE | Final MAE |
|------------|-------------|-----------|
| San Juan  | ~30        | 11.8      |
| Iquitos   | ~31        | 4.7       |

Performance gains were primarily driven by autoregressive features and disciplined validation rather than complex model architecture changes.

---

## Repository Structure

dengue-time-series-forecasting/
│
├── data/              # Dataset instructions (data not redistributed)
├── notebooks/         # Full modeling workflow
├── reports/           # Technical project report (LaTeX + PDF)
├── images/            # Figures used in report
├── requirements.txt
└── LICENSE

---

## Reproducibility

Install dependencies:

pip install -r requirements.txt

Download dataset from the official competition page and place it inside the `data/` directory (see `data/README.md`).

Run notebooks in order:

1. 01_eda.ipynb  
2. 02_baseline_models.ipynb  
3. 03_feature_engineering.ipynb  
4. 04_final_model.ipynb  

---

## Dataset Source

DrivenData – DengAI: Predicting Disease Spread  
https://www.drivendata.org/competitions/44/dengai-predicting-disease-spread/

The dataset is not included in this repository. All rights belong to DrivenData and associated agencies.

---

## Author

Hardik Thapar  
Independent Machine Learning Project

