# Impact of Missing Data Mechanisms and Imputation Strategies on Machine-Learning-Based ICU Mortality Prediction

## Repository Overview

This repository hosts the experimental pipeline and analysis code for investigating how missing-data mechanisms, missingness levels, and imputation strategies influence downstream machine-learning models for intensive-care-unit (ICU) mortality prediction. Because measurements in electronic health records (EHRs) are collected at irregular intervals and depend on clinical workflows, patient conditions, and test availabilities, how missing values are handled significantly affects both dataset properties and model performance.

---

## Key Objectives & Research Questions

* **Primary Aim:** Determine how the interaction between missingness mechanisms, missingness levels, imputation methods, and classification models affects the reliability of ICU mortality prediction.


* **Core Research Inquiries:**
* How increasing missingness affects ICU mortality-prediction performance.


* How classifier performance differs under MCAR, MAR, and MNAR missingness scenarios.


* Which imputation method performs best across different mechanisms and levels.


* Whether better imputation accuracy automatically translates to superior downstream mortality-prediction performance.


* How imputation methods interact with various classification models.





---

## Experimental Methodology

### 1. Dataset & Prediction Task

* **Primary Dataset:** MIMIC-IV, a widely used critical-care EHR database.


* **Prediction Task:** Binary ICU mortality prediction.


* **Optional Extension:** eICU-CRD may be considered for external validation if time permits.



### 2. Missingness Mechanisms

Controlled masking and simulation are used to represent missingness scenarios across levels from 10% to 70% (in steps of 10%):

* **MCAR (Missing Completely At Random):** Randomly masks observed values independently of patient characteristics.


* **MAR (Missing At Random):** Makes missingness depend on observed variables such as age or other recorded clinical features.


* **MNAR (Missing Not At Random):** Uses a documented sensitivity-analysis rule where missingness depends on the masked value or an unobserved factor.



### 3. Imputation Methods

* **Median Imputation:** Serves as a simple and transparent baseline.


* **KNN Imputation:** Estimates missing values using similar observations.


* **MICE (Multiple Imputation by Chained Equations):** Iterative model-based imputation.


* **MissForest:** Iterative random-forest-based imputation and an important nonlinear baseline.



### 4. Classification Models

* **Logistic Regression:** Interpretable baseline model.


* **XGBoost:** Primary gradient-boosting model.


* **CatBoost:** Comparative gradient-boosting model.


* **LightGBM:** Comparative gradient-boosting model.



---

## Evaluation Framework

* **Imputation Quality Metrics:** Evaluated using MAE, RMSE, $R^{2}$, and adjusted $R^{2}$ computed strictly on masked entries where original values are known.


* **Classification Discrimination & Quality Metrics:** Evaluated using AUROC, AUPRC, F1-Score, Precision, Log Loss, and Brier Score.



---

## Reproducibility & Version Control

* Every experiment is executed using **at least three random seeds** (e.g., 0, 1, and 2) to control data splits, masking, imputers, and classifiers.


* Results rely on fixed seeds, saved configuration files, and pinned library versions to ensure full reproducibility.


* Patient-level MIMIC-IV data is excluded from version control for privacy compliance.
