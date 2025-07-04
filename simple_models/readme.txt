# Simple Machine Learning Models for OHCA Prediction

This folder contains the implementation of **shallow (non-ensemble) machine learning models** used for predicting **Out-of-Hospital Cardiac Arrest (OHCA)** based on ECG features. These models are fundamental to understanding baseline performance before exploring ensemble and deep learning alternatives.

This work is part of **Chapter 1** of the thesis titled *"Intelligent Models for Selected Disease Prediction Using Health Electronic Records."*

---

## 📊 Dataset

- Source: **Nightingale Subtyping Cardiac Arrest Dataset**
- Positive cases: 23 ECGs recorded ≤ 24 hours before OHCA
- Control group: 247 ECGs recorded ≤ 7 days before a non-OHCA event
- Selected features:
  - P, Q, R, S wave **amplitudes and durations** from leads II and V1
  - Patient **age** and **gender**
  - Total: **26 features**

---

## ⚙️ Preprocessing Steps

1. **Feature Selection**:
   - Only wave features from leads II and V1 were selected due to their orthogonal representation of heart activity

2. **Class Imbalance Handling**:
   - **SMOTE** used to rebalance OHCA-to-control ratio from 1:13 to **1:4**

3. **Categorical Encoding**:
   - One-hot encoding for gender

4. **Feature Scaling**:
   - Applied `MaxAbsScaler` to preserve sparsity and scale all numeric variables

---

## 🧠 Implemented Shallow Models

### ✅ Logistic Regression (LR)
- Estimates the probability of OHCA based on a logistic function
- Optimized using maximum likelihood
- Tested with various solvers and penalties (`l1`, `l2`, `elasticnet`)

### 🌲 Decision Tree (DT)
- Constructs hierarchical splits based on Gini or entropy
- Prone to overfitting; used as a baseline for ensemble models

### 📐 Support Vector Machine (SVM)
- Both **Linear** and **RBF kernels**
- Finds optimal hyperplane using margin maximization
- **Best-performing model** overall

### 📏 K-Nearest Neighbors (KNN)
- Classifies based on the `k` closest neighbors
- Tested with various distance metrics and weights

### ⚙️ Stochastic Gradient Descent Classifier (SGDC)
- Efficient linear model using mini-batch updates
- Tuned with `alpha`, `l1_ratio`, and loss functions

---

## 🧪 Evaluation Methodology

- **Nested Cross-Validation** (5-fold outer, 3-fold inner)
- **Hyperparameter tuning** with grid search
- **Primary metric optimized**: F1-score (ideal for imbalanced data)

---

## 📈 Performance Summary

| Model        | F1 Score       | Precision | Sensitivity | Specificity | Accuracy |
|--------------|----------------|-----------|-------------|-------------|----------|
| Decision Tree| 0.603 ± 0.105  | 0.649     | 0.614       | 0.911       | 0.855    |
| Logistic Reg.| 0.627 ± 0.052  | 0.555     | 0.733       | 0.862       | 0.839    |
| KNN          | 0.684 ± 0.057  | 0.662     | 0.721       | 0.911       | 0.875    |
| SGDC         | 0.585 ± 0.091  | 0.544     | 0.697       | 0.837       | 0.812    |
| SVM Linear   | 0.612 ± 0.047  | 0.541     | 0.733       | 0.846       | 0.826    |
| **SVM RBF**  | **0.900 ± 0.032** | **0.951** | **0.861**   | **0.984**   | **0.964** |

> ✅ **Best Shallow Model**: SVM with RBF kernel

---

## 🎯 Conclusion

SVM with RBF kernel significantly outperformed all other shallow models in terms of F1-score, precision, and overall consistency. This model also achieved a performance comparable to deep learning methods used in other OHCA prediction studies, making it a strong candidate for clinical application where interpretability and generalization are critical.

---

## 🔬 Citation

If this work contributed to your research, please cite:
Castro Gutierrez, H. (2025). Intelligent Models for Selected Disease Prediction Using Health Electronic Records. Doctoral dissertation, Purdue University.

---

## 📬 Contact

For questions or contributions, please contact `hcastrog at purdue.edu` or open an issue on [GitHub](https://github.com/heinercg/OHCA_prediction).
