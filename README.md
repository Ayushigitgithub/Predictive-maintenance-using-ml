# Predictive Maintenance using Machine Learning (AI4I 2020 Dataset)

## 📌 Overview
This project builds a machine learning pipeline to **predict machine failures in advance** using the AI4I 2020 Predictive Maintenance dataset (UCI).  
The pipeline focuses on:
- Handling **class imbalance** (~3.4% failures) using SMOTE
- Comparing multiple ML models (Logistic Regression, Random Forest, HistGradientBoosting, XGBoost)
- Evaluating beyond accuracy (ROC-AUC, PR-AUC, Precision, Recall, F1)
- Using **SHAP explainability** for feature importance and interpretability

---

## 📊 Dataset
- **Source:** [AI4I 2020 UCI Repository](https://archive.ics.uci.edu/ml/datasets/ai4i+2020+predictive+maintenance+dataset)  
- **Size:** 10,000 records, 14 columns  
- **Features used:**  
  - Air Temperature (K)  
  - Process Temperature (K)  
  - Rotational Speed (rpm)  
  - Torque (Nm)  
  - Tool Wear (minutes)  
  - Product Type (Low/Medium/High → one-hot encoded)  
- **Target:** Binary machine failure (1 = failure, 0 = normal)  
- **Note:** Failure-mode flags were excluded to prevent leakage.

---

## ⚙️ Pipeline Steps
1. Data preprocessing  
   - Dropped IDs and leakage-prone failure mode flags  
   - One-hot encoded product type  
   - Standard scaling of numeric features  
   - Outlier capping  

2. Train-test split (stratified, to preserve imbalance)

3. Imbalance handling  
   - Applied **SMOTE** only on training data  

4. Models compared  
   - Logistic Regression (baseline, linear model)  
   - Random Forest (bagging, feature randomness)  
   - HistGradientBoosting (scalable gradient boosting)  
   - XGBoost (tuned boosting, selected as best)  

5. Evaluation metrics  
   - ROC-AUC and PR-AUC  
   - Precision, Recall, F1-score  
   - Confusion Matrix  

6. Explainability  
   - SHAP bar plot → global feature importance  
   - SHAP beeswarm → feature effect distribution  
   - SHAP dependence plot → feature interactions  

---

## ✅ Results
- **Best model:** XGBoost  
- **Performance (test set):**  
  - Recall ≈ **94%** (failures correctly caught)  
  - Precision ≈ **98%** (very few false alarms)  
  - ROC-AUC ≈ **0.994**  
  - PR-AUC ≈ **0.97**  

- **Key drivers (SHAP):**  
  - Tool Wear ↑ → higher failure risk  
  - Low Rotational Speed → higher failure risk  
  - Extreme Torque values → higher failure risk  
  - Temperatures → minor effect  

---


