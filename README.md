# Intelligent Models for Sudden Cardiac Arrest Prediction

This repository contains the implementation of the machine learning models developed for the doctoral research project: **"Intelligent Models for Selected Disease Prediction Using Health Electronic Records"**. The project focuses on predicting **Out-of-Hospital Cardiac Arrest (OHCA)** using **electrocardiogram (ECG)** data and applies a variety of machine learning strategies from simple models to deep neural networks.

The codebase is organized by methodology chapters corresponding to the dissertation structure:

---

## 📁 `simple_models/` (Chapter 2)
This folder contains classical **shallow machine learning models** trained on ECG features extracted from the Subtyping Cardiac Arrest dataset.

### Implemented Models:
- Logistic Regression (LR)
- Decision Tree (DT)
- K-Nearest Neighbors (KNN)
- Stochastic Gradient Descent Classifier (SGDC)
- Support Vector Machines (SVM - linear and RBF)

### Features:
- Nested Cross-Validation for Model Selection
- SMOTE for data imbalance
- Preprocessing using MaxAbsScaler
- F1-score focused optimization

---

## 📁 `standard_ensemble_models/` (Chapter 2)
This subdirectory extends shallow models using **standard ensemble techniques**.

### Implemented Models:
- Random Forest (RF)
- AdaBoost
- Gradient Boosting
- LightGBM
- XGBoost

These models are compared against each other using nested cross-validation, and performance is evaluated using multiple metrics (F1-score, precision, sensitivity, specificity, accuracy, and NPV).

---

## 📁 `Custom_ensemble_models/` (Chapter 3)
Custom ensemble strategies are tested and evaluated in this section.

### Implemented Strategies:
- Hard Voting & Soft Voting (weighted and unweighted)
- Stacking with different meta-models
- Bagging with various base learners
- Boosting using SVM-RBF as base learner in AdaBoost

Bayesian optimization and grid search are used to tune voting weights. The best performance was obtained with a boosting ensemble using SVM-RBF as base learner, surpassing traditional ensemble methods.

---

## 📁 `Neural_Networks/` (Chapter 4)
This section explores **deep learning models** for predicting OHCA from raw ECG signals.

### Implemented Architectures:
- Recurrent Neural Networks (RNN)
- Long Short-Term Memory (LSTM)
- Gated Recurrent Units (GRU)
- Radial Basis Function Networks (RBFN)

### Signal Processing Techniques:
- Signal resampling and decimation
- Wavelet decomposition (e.g., Daubechies db2-level 4)
- Data augmentation and segmentation
- TimeSHAP for explainability of RNN predictions

The top-performing deep learning model was an LSTM using 12-lead ECG signals and wavelet transformation, achieving outstanding accuracy and generalization.

---

## 🧪 Dataset
The models were primarily trained and evaluated on the **Subtyping Cardiac Arrest dataset** provided by Nightingale Open Science. This dataset contains ECGs recorded before OHCA and from control patients.

---

## 📊 Performance Highlights
| Model                          | Accuracy | F1 Score | Precision | Sensitivity | Specificity |
|-------------------------------|----------|----------|-----------|-------------|-------------|
| SVM-RBF (Shallow)             | 0.964    | 0.900    | 0.951     | 0.861       | 0.984       |
| Boosting SVM-RBF (Custom)     | 0.977    | 0.977    | 0.965     | 0.917       | 0.988       |
| LSTM + resampling             | 0.988    | 0.988    | 0.989     | 0.986       | 0.989       |

---

## 📄 License
 GPL-3.0 license
---

## 🧠 Citation
If you use this repository in your work, please cite:
Castro Gutierrez, H. (2025). Intelligent Models for Selected Disease Prediction Using Health Electronic Records. Doctoral dissertation, Purdue University.

---

## 📬 Contact
For questions or contributions, please reach out via GitHub issues or email `hcastrog at purdue.edu`.
