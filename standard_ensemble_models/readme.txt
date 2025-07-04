# Standard Ensemble Models for OHCA Prediction

This folder contains implementations of standard ensemble machine learning models for the prediction of **Out-of-Hospital Cardiac Arrest (OHCA)** based on ECG features. This work corresponds to **Chapter 1** of the thesis, which evaluates and compares ensemble methods against traditional shallow learning models using rigorous nested cross-validation and class balancing techniques.

---

## 📊 Dataset

- **Nightingale Subtyping Cardiac Arrest Dataset**
- 19 OHCA ECGs and 247 control ECGs were used
- ECGs collected within:
  - 24 hours before OHCA for cases
  - 7 days before non-OHCA visits for controls
- Features extracted:
  - P, Q, R, S wave amplitude and duration (leads II and V1)
  - Age and gender
- Total of 26 selected features

---

## ⚙️ Preprocessing Steps

- **Feature selection** from leads II and V1
- **Class balancing** using SMOTE to adjust positive class to negative class ratio from 1:13 to 1:4
- **Encoding**: One-hot for gender
- **Scaling**: MaxAbsScaler for all numeric features

---

## 🧠 Ensemble Methods Implemented

All models use decision trees as base estimators and are evaluated using nested cross-validation (5-fold outer, 3-fold inner). Grid search was used to optimize the F1-score.

### 🌳 Random Forest (RF)
- Combines multiple decision trees using bagging
- Key parameters: `n_estimators`, `max_depth`, `min_samples_split`, `max_features`

### ⚡ AdaBoost
- Boosts the performance of weak learners using weighted samples
- Weights updated based on misclassification

### 📈 Gradient Boosting Classifier (GBC)
- Sequential learners trained on residuals
- Loss minimized using the additive model

### 🌟 LightGBM (LGBC)
- Optimized for large datasets
- Leaf-wise tree growth
- Uses histogram-based training

### 🚀 XGBoost (XGBC)
- Level-wise tree growth
- Regularized to reduce overfitting
- Supports parallel training

---

## 🧪 Evaluation Methodology

- **Nested Cross-Validation** with grid search on the inner loop
- **Metric Optimized**: F1-score (to handle class imbalance)
- **Comparison**: Accuracy, Precision, Sensitivity, Specificity, NPV

---

## 📈 Performance Summary

| Model     | F1 Score      | Precision (PPV) | Sensitivity | Specificity | Accuracy |
|-----------|---------------|----------------|-------------|-------------|----------|
| RF        | 0.747 ± 0.142 | 0.874 ± 0.074  | 0.667       | 0.980       | 0.921    |
| AdaBoost  | 0.658 ± 0.165 | 0.695 ± 0.105  | 0.655       | 0.935       | 0.888    |
| GBC       | 0.621 ± 0.174 | 0.902 ± 0.084  | 0.508       | 0.984       | 0.882    |
| LGBC      | 0.678 ± 0.058 | 0.873 ± 0.068  | 0.561       | 0.980       | 0.895    |
| **XGBC**  | **0.755 ± 0.083** | 0.743 ± 0.061 | **0.773**   | 0.939       | 0.908    |

> ✅ **Best Performing Ensemble Model:** XGBoost Classifier

---

## 🎯 Conclusion

While ensemble models like XGBoost and Random Forest performed well, **Support Vector Machines with RBF kernel** (in `simple_models/`) still provided the best overall metrics, highlighting the effectiveness of simpler models under well-tuned conditions. However, ensemble methods offer robustness and are promising when working with high-dimensional or larger datasets.

---

## 🔬 Citation

If this work helps your research, please cite: Castro Gutierrez, H. (2025). Intelligent Models for Selected Disease Prediction Using Health Electronic Records. Doctoral dissertation, Purdue University.

---

## 📬 Contact

For questions, contributions, or feedback, please contact `hcastrog at purdue.edu` or submit an issue on [GitHub](https://github.com/heinercg/OHCA_prediction).
