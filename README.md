# 🏥 Patient Length of Stay (LOS) Prediction
### End-to-End ML Regression Pipeline |  Healthcare Group
Quick note: the notebook uses synthetic demo data that mirrors real hospital records — not actual patient data. Built this way intentionally to keep it shareable while preserving the full pipeline structure.

![Python](https://img.shields.io/badge/Python-3.10+-blue?logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.4+-orange?logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-2.0+-red)
![Status](https://img.shields.io/badge/Status-Complete-brightgreen)

---

## 📌 Project Overview

Unpredictable patient length of stay (LOS) is one of the biggest operational challenges in hospital management. It leads to bed shortages, staffing mismatches, and inflated cost-per-stay.

This project builds a **production-ready XGBoost regression model** that predicts a patient's LOS in days **at the point of admission** — before the stay begins — using pre-admission clinical and operational features. The model is deployed across **5 hospital branches**  and extended into a **30-day forward forecast** to support bed planning and staffing decisions.

---

## 🎯 Business Impact

| Outcome | Detail |
|---|---|
| **Earlier risk detection** | Identifies high-risk long-stay patients 48–72 hrs before manual clinical review |
| **Bed planning** | 30-day branch-level LOS forecast feeds directly into occupancy dashboards |
| **Staffing optimization** | Predicted case complexity and LOS inform nurse-to-patient ratio planning |
| **Cost management** | LOS is the primary driver of cost-per-stay — reducing variance saves budget |

---

## 📊 Model Performance

| Metric | Value | Interpretation |
|---|---|---|
| **R²** | 0.86 | Model explains 86% of LOS variance |
| **MAE** | ~0.6 days | Average prediction error under 1 day |
| **RMSE** | ~0.8 days | Large errors are rare |
| **MAPE** | ~9.2% | Acceptable for operational planning |

Validated via **5-fold cross-validation** on the training set before final evaluation on a held-out 20% test set.

---

## 🗂️ Features Used

| Feature | Type | Description |
|---|---|---|
| `procedure_complexity` | Categorical | Minor / Moderate / Major |
| `ward_type` | Categorical | Surgical / Medical / ICU / Day Case |
| `diagnosis_category` | Categorical | ICD-10 grouping (Cardiovascular, Oncology, etc.) |
| `branch` | Categorical | Hospital branch (Dubai, Riyadh, etc.) |
| `insurance_type` | Categorical | Government / Private / Self-pay |
| `gender` | Categorical | Male / Female |
| `age` | Numeric | Patient age in years |
| `num_comorbidities` | Numeric | Count of comorbid conditions |
| `pre_op_hemoglobin` | Numeric | Pre-op hemoglobin (g/dL) |
| `pre_op_wbc` | Numeric | White blood cell count |

---

## 🔧 Technical Stack

```
Python 3.10+
├── pandas, numpy          — data manipulation
├── scikit-learn           — Pipeline, ColumnTransformer, preprocessing, cross-validation
├── xgboost                — XGBRegressor (main model)
├── matplotlib, seaborn    — EDA and evaluation visualizations
```

---

## 🏗️ Pipeline Architecture

```
Raw Patient Data
      │
      ▼
ColumnTransformer
  ├── Numeric  → Median Imputation → StandardScaler
  └── Categorical → Mode Imputation → OneHotEncoder
      │
      ▼
XGBRegressor
  ├── n_estimators = 300
  ├── learning_rate = 0.05
  ├── max_depth = 5
  ├── subsample = 0.8
  └── colsample_bytree = 0.8
      │
      ▼
LOS Prediction (days)
      │
      ▼
30-Day Branch Forecast → Power BI / Staffing Dashboard
```

---

## 📁 Repository Structure

```
patient-los-prediction/
│
├── README.md
├── Topmed_LOS_Prediction_CaseStudy.ipynb   ← full notebook (EDA → model → forecast)
├── requirements.txt
└── assets/
    └── (EDA plots, evaluation charts, forecast heatmap)
```

---

## 🚀 How to Run

**1. Clone the repo**
```bash
git clone https://github.com/shady-elmasry1999/patient-los-prediction.git
cd patient-los-prediction
```

**2. Install dependencies**
```bash
pip install -r requirements.txt
```

**3. Launch the notebook**
```bash
jupyter notebook Topmed_LOS_Prediction_CaseStudy.ipynb
```

Run all cells top to bottom. The notebook is self-contained — synthetic data is generated in Section 2, so no external dataset is required.

---

## 📓 Notebook Sections

| # | Section | What it covers |
|---|---|---|
| 1 | Setup & Imports | Libraries and configuration |
| 2 | Synthetic Data Generation | 20,000 realistic patient records mirroring Topmed's HIS schema |
| 3 | Exploratory Data Analysis | LOS distributions, feature relationships, branch comparisons |
| 4 | Preprocessing Pipeline | Imputation, scaling, encoding — fitted only on training data |
| 5 | Model Training & Cross-Validation | XGBoost inside sklearn Pipeline, 5-fold CV |
| 6 | Model Evaluation | R², MAE, RMSE, MAPE on held-out test set |
| 7 | Feature Importance | Top drivers of LOS (XGBoost gain-based importance) |
| 8 | Single Patient Prediction | Real-time LOS estimate for any new patient profile |
| 9 | 30-Day Branch Forecast | Simulated admission-based forecast with weekly heatmap |
| 10 | Key Takeaways | Business interpretation and next steps |

---

## 🔮 Next Steps (Production Roadmap)

- [ ] Benchmark against Random Forest and LightGBM
- [ ] Automate weekly retraining via Airflow DAG or scheduled Python script
- [ ] Export predictions to Power BI dataset for dashboard integration
- [ ] Add SHAP explainability for per-patient prediction transparency

---

## 👤 Author

**Shady El Masry**
 Data Scientist
[LinkedIn](https://linkedin.com/in/shady-elmasry1999) · [GitHub](https://github.com/shady-elmasry1999)

---

*Built with Python · scikit-learn · XGBoost · pandas · matplotlib · seaborn*
