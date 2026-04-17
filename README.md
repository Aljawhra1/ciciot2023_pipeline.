# ciciot2023_pipeline.
ML-based IoT intrusion detection system using CICIoT2023 dataset with ensemble learning, SMOTE balancing, and hyperparameter tuning to detect malicious network traffic.
# 🛡️ ML-Based Anomaly Detection for IoT Network Security

<div align="center">

![Python](https://img.shields.io/badge/Python-3.10%2B-3776AB?style=for-the-badge&logo=python&logoColor=white)
![scikit-learn](https://img.shields.io/badge/scikit--learn-1.3-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=white)
![XGBoost](https://img.shields.io/badge/XGBoost-1.7-FF6600?style=for-the-badge)
![LightGBM](https://img.shields.io/badge/LightGBM-4.0-02A9FF?style=for-the-badge)
![Colab](https://img.shields.io/badge/Google%20Colab-Ready-F9AB00?style=for-the-badge&logo=googlecolab&logoColor=white)

**Graduation Project — Bachelor of Computer Science**  
Imam Mohammed Ibn Saud Islamic University · Riyadh, Saudi Arabia

</div>

---

## 📌 Overview

This project addresses a critical challenge in modern cybersecurity: **detecting malicious traffic in IoT networks** using supervised machine learning.

IoT devices are inherently resource-constrained and often lack built-in security mechanisms, making them prime targets for network attacks. This work trains, tunes, and evaluates multiple ML classifiers on the **CICIoT2023 dataset** — a large, realistic benchmark of IoT network traffic — and compares their ability to distinguish between **benign** and **attack** traffic.

---

## 🎯 Objectives

- Train and evaluate **5 ML classifiers**: KNN, Decision Tree, Random Forest, XGBoost, LightGBM
- Address class imbalance using **SMOTE** (Synthetic Minority Oversampling Technique)
- Perform **Hyperparameter Tuning** with RandomizedSearchCV + Stratified K-Fold CV
- Build **Ensemble models**: Soft Voting, Hard Voting, and Stacking (with Logistic Regression meta-learner)
- Report detailed metrics: Accuracy, Precision, Recall, F1 (per class + Macro average)

---

## 🗂️ Project Structure

```
iot-anomaly-detection/
│
├── 📓 FinalCopy.ipynb          # Main Colab notebook (full pipeline)
├── 📄 README.md                # You are here
│
├── 📁 results/                 # Auto-generated after running
│   ├── baseline_results_*.csv
│   ├── smote_results_*.csv
│   ├── tuned_results_*.csv
│   ├── ensemble_results_*.csv
│   └── *.png                   # Confusion matrix images
│
└── 📁 docs/                    # (Optional) Report / presentation
```

---

## 🔬 Methodology

### Pipeline Overview

```
Raw Data (CICIoT2023)
        │
        ▼
  Data Loading & EDA
        │
        ▼
  StandardScaler (Normalization)
        │
        ├──────────────────────────┐
        ▼                          ▼
  Baseline Training          SMOTE Resampling
  (5 classifiers)            (5 classifiers)
        │                          │
        └──────────┬───────────────┘
                   ▼
        Hyperparameter Tuning
        (RandomizedSearchCV, 5-Fold CV)
                   │
                   ▼
         Ensemble Methods
    (Soft Voting / Hard Voting / Stacking)
                   │
                   ▼
        Evaluation & Results
```

### Models Used

| Model | Type | Key Strength |
|-------|------|-------------|
| **KNN** | Instance-based | Simple, non-parametric |
| **Decision Tree** | Tree-based | Interpretable |
| **Random Forest** | Ensemble (Bagging) | Robust to overfitting |
| **XGBoost** | Ensemble (Boosting) | High accuracy, fast |
| **LightGBM** | Ensemble (Boosting) | Memory efficient |

### Ensemble Strategies

| Strategy | Description |
|----------|-------------|
| **Soft Voting** | Averages class probabilities across top-3 models |
| **Hard Voting** | Majority vote across top-3 models |
| **Stacking** | Top-3 models as base; Logistic Regression as meta-learner |

---

## 📊 Evaluation Metrics

Each model is evaluated on:

- **Accuracy**
- **Precision / Recall / F1** — for Benign class (0)
- **Precision / Recall / F1** — for Attack class (1)
- **Macro-averaged** Precision, Recall, F1
- **Confusion Matrix** (saved as PNG)

---

## 🗃️ Dataset

**CICIoT2023** — Canadian Institute for Cybersecurity

| Property | Value |
|----------|-------|
| Source | Kaggle (`gp1f9imamu/ciciot2023-samblef`) |
| Classes | Benign (0), Attack (1) |
| Format | CSV (train / test split) |
| Features | Network flow statistics |

> **Note:** The dataset is downloaded automatically from Kaggle inside the notebook. You only need a `kaggle.json` API key.

---

## 🚀 Getting Started

### Prerequisites

- Google Account (to run on Colab)
- Kaggle account + API token (`kaggle.json`)

### Steps

**1. Open the notebook in Google Colab**

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1s1ZQBfgNq6qoo2JtubaXIf_CyRNu76vY)

**2. Upload your `kaggle.json`**

When prompted in the first cell, upload your Kaggle API key. The notebook will handle dataset download automatically.

**3. Run all cells**

`Runtime → Run all` — the full pipeline runs end-to-end.

**4. Download results**

At the end, a `results_backup.zip` is generated and downloaded automatically containing all CSVs and confusion matrix PNGs.

---

## 📦 Dependencies

```python
# Automatically installed in the notebook
pip install lightgbm xgboost imbalanced-learn
```

| Library | Purpose |
|---------|---------|
| `scikit-learn` | ML models, preprocessing, CV |
| `xgboost` | XGBoost classifier |
| `lightgbm` | LightGBM classifier |
| `imbalanced-learn` | SMOTE oversampling |
| `pandas / numpy` | Data manipulation |
| `matplotlib / seaborn` | Visualization |

---

## 🔍 Key Design Decisions

**Why SMOTE?**  
IoT attack datasets are typically imbalanced. SMOTE generates synthetic samples for the minority class in feature space, preventing the model from being biased toward benign traffic.

**Why RandomizedSearchCV over GridSearch?**  
With large parameter spaces and multiple models, exhaustive grid search is computationally prohibitive. Randomized search achieves comparable results in a fraction of the time.

**Why Stacking?**  
Stacking allows a meta-learner to learn how to optimally combine base model predictions, often outperforming individual models or simple voting schemes.

---

## 🔒 Security Context

This project is grounded in real-world IoT security challenges:

- IoT devices often run on embedded systems with no endpoint protection
- Anomaly detection at the **network level** is one of the most practical defenses
- The OWASP IoT Top 10 lists insecure network services as a primary attack vector
- This work contributes toward **lightweight, software-based intrusion detection** for IoT environments

---

## 👩‍💻 Author

**Aljawhra Aldosari**  
Bachelor of Computer Science — Imam Mohammed Ibn Saud Islamic University  
📧 aljohrhali99@gmail.com  
🔗 [LinkedIn](https://linkedin.com/in/aljawhra-aldosari-616b28215) · [GitHub](https://github.com/Aljawhra1)

---

## 📄 License

This project is for academic purposes. Dataset usage follows CICIoT2023 terms and Kaggle's terms of service.

---

<div align="center">
  <sub>Graduation Project · 2024–2025 · Riyadh, Saudi Arabia</sub>
</div>
