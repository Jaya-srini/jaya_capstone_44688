
# Business Data Quality Scoring
### Capstone Project | MS Analytics

A machine learning pipeline to automatically score the quality of business license records using the City of Chicago Business Licenses dataset.

---

## Project Overview

This project builds an end-to-end data quality scoring system that identifies poor quality business records before they reach downstream systems or customers. Since no prior quality labels existed, a binary quality label was engineered from `LICENSE_STATUS` and three classification models were trained and compared.

---

##  Dataset

- **Source:** [City of Chicago Business Licenses](https://catalog.data.gov/dataset/business-licenses)
- **Records:** 1,173,151 (after cleaning)
- **Features:** 18 (after feature engineering)
- **Target:** `QUALITY_LABEL` (0 = Good Quality, 1 = Poor Quality)
- **Class Split:** 93.38% Good / 6.62% Poor

---

## 🔧Project Structure


##  Pipeline

```
Raw Data → Cleaning → Feature Engineering → Label Generation → Model Training → SHAP Explainability
```

1. **Data Cleaning** — dropped irrelevant columns, standardized text fields, fixed date/numeric types, filtered to IL records with valid ZIP codes
2. **Feature Engineering** — created binary missing indicator flags, term length validity flags, one hot encoded `APPLICATION_TYPE`
3. **Label Generation** — engineered `QUALITY_LABEL` from `LICENSE_STATUS` (AAI = 0, all others = 1)
4. **Model Training** — trained and compared Logistic Regression, Random Forest, and XGBoost
5. **Explainability** — computed SHAP values to explain feature importance

---

## 🤖 Models and Results

| Model | Accuracy | Precision (Poor) | Recall (Poor) | F1 (Poor) |
|---|---|---|---|---|
| Logistic Regression | 51% | 0.09 | 0.70 | 0.16 |
| Random Forest | 65% | 0.10 | 0.55 | 0.17 |
| **XGBoost** | **67%** | **0.11** | **0.56** | **0.18** |

**XGBoost** was selected as the final model for its best overall performance and fastest training time (1.7 seconds).

---

## Key Findings

- **TERM_LENGTH** was the most influential feature — despite appearing unremarkable in EDA
- **Geography matters** — `POLICE_DISTRICT` and `WARD` were top 3 predictors, suggesting certain Chicago areas have systematically incomplete records
- **Application type** is a quality signal — liquor license expansions (`C_EXPA`) had the highest poor quality rate at 7.43%
- **Class imbalance** (93/7) was the biggest modeling challenge

---

## Tech Stack

- **Language:** Python 3.12
- **Libraries:** pandas, numpy, scikit-learn, xgboost, shap, matplotlib, seaborn
- **Environment:** Jupyter Notebook
- **Version Control:** Git / GitHub

---

##Setup


## 📁 Data

The dataset is not included in this repository due to file size. Download it directly from:
[https://catalog.data.gov/dataset/business-licenses](https://catalog.data.gov/dataset/business-licenses)

---

## Author

