# Custom Ensemble Models for Out-of-Hospital Cardiac Arrest Prediction

This directory implements **custom ensemble learning strategies** for the **prediction of Out-of-Hospital Cardiac Arrest (OHCA)** using features extracted from 12-lead ECGs. This codebase corresponds to the experiments described in **Chapter 2** of the thesis and evaluates multiple ensemble approaches, including **voting, stacking, bagging, and boosting**.

---

## 📊 Dataset

- **Subtyping Cardiac Arrest Dataset**
- ECGs recorded within 24 hours prior to OHCA or up to 7 days before a non-OHCA event
- Final dataset: 19 OHCA ECGs and 247 controls
- Each ECG has 52 features per lead (total: 624 features)
- Only leads II and V1 used for feature extraction (P, Q, R, S wave duration and amplitude), plus age and gender

---

## ⚙️ Preprocessing Steps

1. **Feature Selection**: Limited to wave durations, amplitudes, age, and gender
2. **Class Balancing**: Applied SMOTE to achieve a 1:4 OHCA-to-control ratio
3. **Encoding**: One-hot encoding for gender
4. **Scaling**: MaxAbsScaler for numeric features

---

## 🧠 Custom Ensemble Methods

### 🗳️ Voting
- Base models: DT, LR, KNN, SGDC, SVM-RBF
- Types:
  - Hard Voting
  - Soft Voting
- Weight optimization via:
  - Grid Search
  - Bayesian Optimization (real & integer weights)

> **Result**: No improvement over standalone SVM-RBF; grid search typically gave all weight to SVM-RBF.

---

### 🧱 Stacking
- Four base models per stack, varied meta-models: DT, LR, KNN, SGDC, SVM-linear, SVM-RBF
- Out-of-fold predictions used to train the meta-learner

> **Result**: SVM-RBF as meta-model performed best but showed no major improvement over SVM-RBF alone.

---

### 🧃 Bagging
- Algorithms: LR, KNN, SGDC, SVM-linear, SVM-RBF
- Uses bootstrap sampling

> **Result**: All bagging models underperformed compared to simpler models like SVM-RBF.

---

### ⚡ Boosting
- Implemented AdaBoost using custom base learners
- Best results achieved using **SVM-RBF as base learner**
- Outperformed standalone SVM-RBF in:
  - F1 Score: **0.977**
  - Accuracy: **0.977**
  - Sensitivity: **0.917**
  - Precision: **0.965**

> ✅ **Boosting + SVM-RBF is the best custom ensemble model for ECG-based OHCA prediction.**

---

## 🔁 Evaluation Methodology

- **Nested Cross-Validation**: 5 outer folds, 3 inner folds
- **Metric Optimization**: F1-score
- **Hyperparameter Tuning**: Manual bounds → Grid Search or Bayesian Optimization
- **Final Validation**: Separate 70/30 training/validation split confirms generalization

---

## 📈 Key Results Summary

| Model              | F1 Score | Precision | Sensitivity | Specificity | Accuracy |
|-------------------|----------|-----------|-------------|-------------|----------|
| Voting (best case)| 0.900    | 0.951     | 0.861       | 0.984       | 0.964    |
| Stacking (SVM-RBF)| 0.888    | 0.951     | 0.844       | 0.988       | 0.961    |
| **Boosting (SVM)**| **0.977**| **0.965** | **0.917**   | **0.988**   | **0.977**|

---

## 🧪 Validation

Boosting SVM-RBF was tested on a held-out 30% set:
- Accuracy: **0.98**
- F1 Score: **0.94**
- Precision: **0.94**
- Sensitivity: **0.94**
- Specificity: **0.99**
- NPV: **0.99**

---

## 🔬 Citation

If this code contributes to your work, please cite:
Castro Gutierrez, H. (2025). Intelligent Models for Selected Disease Prediction Using Health Electronic Records. Doctoral dissertation, Purdue University.

---

## 📬 Contact

For questions or collaboration, reach out at `hcastrog at purdue.edu` or create a GitHub issue.
