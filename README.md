## Project Overview

This project focuses on predicting and ranking potential drug molecules for multiple diseases using Machine Learning. The system analyzes chemical compounds and estimates their biological activity (pIC50), helping identify promising candidates for further research.

The goal is to accelerate drug discovery by leveraging data-driven approaches instead of traditional trial-and-error methods.

---

## What This Project Does

* Collects bioactivity data of chemical compounds
* Converts molecular structures (SMILES) into numerical features using fingerprints
* Trains ML models to predict pIC50 (drug effectiveness)
* Ranks molecules based on predicted activity
* Supports multi-disease prediction system

---

## Dataset Information

* Data is collected from the ChEMBL database
* ChEMBL is maintained by the European Bioinformatics Institute
* It is a trusted and certified bioactivity database used globally in drug discovery research

---

## Dataset Details

* Data collected for 4 different diseases
* Each dataset contains:

  * Molecule ID (molecule_chembl_id)
  * SMILES (chemical structure)
  * Bioactivity values (IC50/pIC50)
* All 4 datasets are:

  * Cleaned
  * Preprocessed
  * Merged into a single unified dataset for training

---

## Workflow

1. Data Collection

   * Extracted using ChEMBL API

2. Data Preprocessing

   * Removed missing/invalid values
   * Standardized bioactivity values

3. Feature Engineering

   * Converted SMILES to molecular fingerprints (ECFP/Morgan)

4. Model Training

   * Applied ML models such as:

     * Random Forest
     * Gradient Boosting
     * SVM (optional)

5. Evaluation

   * Metrics used:

     * R² Score
     * RMSE
     * MAE

6. Prediction

   * Predict pIC50 values
   * Rank top molecules for each disease

---

## Key Concepts Used

* Machine Learning (Regression Models)
* Feature Engineering (Molecular Fingerprints)
* Bioinformatics Data Processing
* Model Optimization (RandomizedSearchCV)

---

## Output

* Predicted pIC50 values for molecules
* Ranking of top potential drug candidates
* Model performance metrics

---

## Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* RDKit
* Matplotlib, Seaborn

---

## Real-World Impact

* Helps in early-stage drug discovery
* Reduces time and cost of research
* Supports research in neglected diseases
* Can be extended to a multi-disease recommendation system

---

## Future Enhancements

* Deep Learning models (Graph Neural Networks)
* Integration with a chatbot interface
* Real-time molecule input and prediction
* Deployment using Streamlit or a web application

---


