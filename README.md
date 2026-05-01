# 🛰️ AstroGuard: High-Recall Machine Learning for Asteroid Classification

> A machine learning framework for detecting Potentially Hazardous Asteroids (PHAs) — built for planetary defense.

---

## 📌 Overview

AstroGuard is an AI-powered classification system that identifies **Potentially Hazardous Asteroids (PHAs)** from NASA/JPL survey data. Using physical and orbital features of 132,046 asteroids, the framework prioritizes **Recall** over accuracy — ensuring that no genuine threat is missed.

The system is designed as a high-sensitivity "first pass" filter that astronomers can use to triage newly discovered near-Earth objects (NEOs) before deeper observational follow-up.

---

## 🚀 Key Features

- **High-Recall Detection** — XGBoost model achieves a Recall of **0.86**, minimizing dangerous false negatives
- **Class Imbalance Handling** — SMOTE (Synthetic Minority Oversampling Technique) applied to address the severe ~1.35% minority class
- **Comparative Benchmarking** — Logistic Regression, Random Forest, SVM, and XGBoost evaluated side by side
- **Feature Importance Analysis** — Validates that orbital geometry (especially perihelion distance) dominates hazard prediction
- **Leakage-Free Pipeline** — Data splitting, transformation, and resampling applied in strict order

---

## 📊 Model Performance

| Model | Precision | Recall | F1-Score |
|---|---|---|---|
| Logistic Regression | 0.22 | 0.77 | 0.34 |
| Random Forest | 0.38 | 0.64 | 0.48 |
| SVM (RBF Kernel) | 0.31 | 0.59 | 0.41 |
| **XGBoost (AstroGuard)** | **0.47** | **0.86** | **0.61** |

---

## 🗂️ Dataset

- **Source:** [NASA/JPL Center for Near Earth Object Studies (CNEOS)](https://cneos.jpl.nasa.gov/)
- **Size:** 132,046 asteroid observations
- **Class distribution:** ~1.35% hazardous (PHAs), ~98.65% non-hazardous
- **Features used:**
  - *Physical:* Absolute magnitude (H), diameter
  - *Orbital:* Eccentricity (e), perihelion distance (q), inclination (i), MOID, mean motion (n), orbital period (per)

---

## 🔬 Methodology

```
Data Acquisition (NASA/JPL)
        ↓
Data Cleaning & Feature Selection
        ↓
Train/Test Split (80/20, stratified)
        ↓
Feature Engineering (log-normalization + z-score scaling)
        ↓
SMOTE Oversampling (on training set only)
        ↓
Model Training (GridSearchCV + 3-fold CV)
        ↓
Evaluation on held-out test set
```

---

## 🧠 Top Predictive Features

1. **Perihelion Distance (q)** — >60% of model gain; directly determines if an asteroid can cross Earth's orbital path
2. **Asteroid Diameter** — Physical size contributes to hazard classification
3. **Eccentricity (e)** — Orbital shape influences Earth-crossing potential

---

## 🛠️ Tech Stack

- Python
- scikit-learn
- XGBoost
- imbalanced-learn (SMOTE)
- pandas / NumPy
- matplotlib / seaborn

---

## 📁 Project Structure

```
AstroGuard/
├── data/               # Raw and processed dataset
├── notebooks/          # Exploratory data analysis & experiments
├── src/
│   ├── preprocessing.py
│   ├── train.py
│   └── evaluate.py
├── models/             # Saved model files
├── results/            # Confusion matrices, feature importance plots
└── README.md
```

---

## 📄 Paper

This project was presented at **WiDS 2026** (Women in Data Science).

> *AstroGuard: Boosting Planetary Defense through High-Recall Machine Learning for Asteroid Classification*
> Areeshah Nadeem, Norah Alarifi, Abrar Wafa — Prince Sultan University, Riyadh, Saudi Arabia

---

## 🔭 Future Work

- **Hybrid CNN-XGBoost model** incorporating raw telescope images (FITS format)
- **Real-time pipeline** integration with Pan-STARRS and Vera C. Rubin Observatory data streams
- **Model drift detection** using Population Stability Index (PSI) for long-term robustness

---

## 📬 Contact

For questions or collaboration, reach out via [Prince Sultan University](https://www.psu.edu.sa).
