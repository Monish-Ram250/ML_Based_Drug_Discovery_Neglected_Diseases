# ML-Based Drug Discovery for Neglected Diseases

## Project Overview

A machine learning system that predicts the **biological activity (pIC50)** of chemical compounds against four diseases — **Cancer, Dengue, HIV, and Tuberculosis** — using molecular fingerprints extracted from SMILES structures. The system ranks candidate molecules by predicted activity to accelerate early-stage drug discovery.

---

## Dataset

**Source:** ChEMBL Database (European Bioinformatics Institute) — collected via ChEMBL API  
**Total Molecules:** 19,146  
**Features:** Morgan/ECFP molecular fingerprints (from SMILES)  
**Target:** pIC50 (continuous — higher = more biologically active)

### Disease Distribution

| Disease | Molecules |
|---|---|
| Cancer | 8,655 |
| HIV | 5,061 |
| Dengue | 4,254 |
| Tuberculosis | 1,306 |
| **Total** | **19,146** |

> Tuberculosis is significantly underrepresented (~6.8% of data), making it the hardest disease class for the model to generalize on.

---

## Pipeline

```
ChEMBL API
    → Extract bioactivity data (IC50 values) for 4 diseases
    → Standardize to pIC50 = -log10(IC50 × 10⁻⁹)
    → Remove missing/invalid values
    → Convert SMILES → Morgan Fingerprints (ECFP) via RDKit
    → Merge all 4 disease datasets (19,146 molecules)
    → RandomizedSearchCV (Random Forest)
    → Predict pIC50
    → Rank top candidate molecules
```

---

## Feature Engineering — Molecular Fingerprints

Raw chemical structures (SMILES strings) are converted into numerical feature vectors using **Morgan Fingerprints (ECFP)** via RDKit. This encodes the local chemical environment around each atom into a fixed-length binary vector, enabling standard ML models to process molecular data without requiring graph-based architectures.

---

## Model — Random Forest Regressor

Optimized using **RandomizedSearchCV** with cross-validation.

**Best Parameters:**

| Parameter | Value |
|---|---|
| n_estimators | 108 |
| max_depth | 40 |
| max_features | None |
| min_samples_leaf | 1 |
| min_samples_split | 2 |

---

## Results

| Metric | Train | Test |
|---|---|---|
| **R² Score** | 0.9559 | **0.7953** |
| RMSE | 0.3377 | 0.7254 |
| MAE | 0.2279 | 0.4822 |

**Test R² of 0.7953** means the model explains ~80% of variance in biological activity from molecular structure alone — strong performance for a noisy cheminformatics regression task.

### Overfitting Note

The gap between Train R² (0.9559) and Test R² (0.7953) indicates moderate overfitting, driven by the deep tree configuration (`max_depth=40`, `min_samples_split=2`). Future work includes stronger regularization or switching to XGBoost/LightGBM with depth constraints.

---

## Output

For a given SMILES input, the system:
- Predicts pIC50 value (biological activity score)
- Ranks molecules from most to least active
- Supports prediction across all 4 disease targets

---

## Tech Stack

| Tool | Purpose |
|---|---|
| Python | Core language |
| ChEMBL API | Bioactivity data collection |
| RDKit | SMILES → Morgan Fingerprint conversion |
| Pandas, NumPy | Data processing |
| Scikit-learn | Random Forest, RandomizedSearchCV |
| Matplotlib, Seaborn | Visualization |
| Jupyter Notebook | Development environment |

---

## Limitations

- Moderate overfitting due to deep tree configuration
- Tuberculosis class is underrepresented (1,306 molecules vs 8,655 for Cancer)
- Morgan fingerprints lose 3D structural information — graph-based models (GNNs) would capture this better
- Static dataset — not connected to live ChEMBL updates

---

## Future Enhancements

- Graph Neural Networks (GNNs) for direct molecular graph learning
- Disease-specific models to handle class imbalance
- Stronger regularization (XGBoost, LightGBM, depth constraints)
- Streamlit deployment for real-time molecule input and ranking

---

## Author

**Akula Monish Ram**  
B.Tech CSE — Lovely Professional University  
Minor in AI — IIT Ropar
