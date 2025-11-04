# Fourth Place Solution

**10 Oct 2025, 20:03 · 05 min read**

---

## 1. Overview and Objectives

**Purpose:** This document describes a winning solution for the _RAIL: Indigenous Weather Forecasting Challenge_ on Zindi. The goal is to build a classification model that predicts the type of rainfall (HEAVYRAIN, MEDIUMRAIN, SMALLRAIN, or NORAIN) expected in the next 12 to 24 hours, based on indigenous ecological indicators submitted by trained farmers in Ghana.

**Objectives and Expected Outcomes:**

1. **Accurate Rainfall Predictions**: Achieve high Macro F1 for classifying rainfall intensity.
2. **Feature Integration**: Incorporate confidence, predicted intensity, community, district, and ecological indicators.
3. **Robustness**: Handle missing values, class imbalance, and categorical features effectively.
4. **Efficient Inference Pipeline**: Offer a systematic approach from raw data transformation to final predictions.

---

## 🔥 Summary

This repository contains the winning solution for the RAIL: Indigenous Weather Forecasting Challenge. It provides a complete end-to-end pipeline—from data loading and feature engineering, through model training and ensemble optimization, to inference and submission file generation.

**Key Results**

- **Public Leaderboard F1:** 0.968444344
- **Private Leaderboard F1:** ---
- **Final Rank:** 🥉 4th Place

---

## 🧹 Data Preprocessing & Cleaning

- **Forecast Length Extraction:** Parsed IDs to extract forecast_length (12 or 24 hours) as a numeric feature.
- **Missing Value Handling:** Used imputation (median for numerics, most_frequent for categoricals) in the pipeline.
- **Class Balance Check:** Visualized and analyzed target distribution to identify potential imbalance.
- **Final Dataset:** Prepared train/test splits with features like user_id, confidence, predicted_intensity, community, district, and indicators.

---

## 🌦️ Feature Engineering

- **Numeric Features:** user_id, confidence, predicted_intensity, forecast_length.
- **Categorical Features:** community, district, prediction_time, indicator, indicator_description, time_observed.
- **Encoding and Imputation:** Applied OneHotEncoding for categoricals and handled missing values via pipeline.
- **No Advanced Interactions:** Focused on core features; potential for time-based derivations from prediction_time in future iterations.

---

## 🧪 Strategic Data Segmentation

No explicit temporal segmentation was used, as the dataset focuses on ecological indicators rather than seasonal patterns. Instead:

- **Stratified Splitting:** Employed StratifiedKFold for cross-validation to preserve class distribution.
- **Full Dataset Usage:** Trained on the entire dataset for a global model capturing all patterns.

---

## 🧠 Advanced Ensemble Modeling

1. **Model Configurations:**
   - **ExtraTreesClassifier:** Tuned with n_estimators=248 for robust feature handling.
   - **RandomForestClassifier:** Tuned with n_estimators=300 for balanced performance.
   - **Voting Ensemble:** Soft voting combiner for improved generalization.
2. **Cross-Validation:** 5-fold Stratified CV to evaluate Macro F1 and accuracy.
3. **Optuna Optimization:** Bayesian-inspired search for optimal hyperparameters (e.g., n_estimators).
4. **Pipeline Integration:** Combined preprocessing (imputation + OHE) with models for seamless training/inference.

---

## 🔗 Dataset Access via Zindi

Due to file size limits, raw CSV files are **not** included here. Please download from Zindi:

1. Visit:  
   👉 [RAIL: Indigenous Weather Forecasting Challenge](https://zindi.africa/competitions/rail-indigenous-weather-forecasting-challenge)
2. Download the train.csv, test.csv, and SampleSubmission.csv from the Data tab.
3. Place into this repo under:
   ```
   data/raw/
   ├── train.csv
   ├── test.csv
   └── SampleSubmission.csv
   ```

---

## 📂 Repository Structure

```
.
├── data/                               # Zindi data (not committed)
│   └── raw/
├── output/                             # Generated submissions, plots
├── 4TH_PLACE_SOLUTION.ipynb            # Full notebook with code & docs
├── submission.csv                      # Submission file matching leaderboard
├── requirements.txt                    # Python dependencies
└── README.md                           # This documentation
```

---

## 🛠️ How to Run

1. Clone the repo
2. Download & place the dataset as described above
3. Create and activate a Conda/Python environment:
   ```bash
   pip install -r requirements.txt
   ```
4. Open `4TH_PLACE_SOLUTION.ipynb` in Jupyter/Colab
5. Run cells top to bottom—full training takes ~5–10 minutes (including Optuna)

---

## 📈 Performance Metrics

- **CV Macro F1:** 0.9798 ± 0.0050
- **CV Accuracy:** 0.9951 ± 0.0017
- **Ensemble Improvement:** Voting improved F1 by ~0.5% over single models

---

## 🕒 Run Time

- **Data preprocessing & feature engineering:** <1 minute
- **Model training (5-fold CV + Optuna):** ~5–10 minutes
- **Inference & submission export:** <1 minute

---

## ❓ Additional Notes

- **Reproducibility:** `seed_everything(42)` ensures consistent results.
- **Logging:** Basic logging for key stages (data loading, CV).
- **Error Handling:** Pipeline handles unknown categories and NaNs robustly.

---

## 📞 Contact

[Your Name]  
✉️ [your.email@example.com]  
🔗 [LinkedIn/GitHub Profile]

---

_Thank you for reviewing this solution!_
