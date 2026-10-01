# UPI Fraud Detection Model

## Overview
This project analyzes UPI transactions and builds fraud detection models using a Jupyter notebook workflow.

## Repository Contents
- `/home/runner/work/upi-fraud-model/upi-fraud-model/upi-transactions-2024-analysis-and-fraud-detection.ipynb` — EDA, preprocessing, modeling, and evaluation
- `/home/runner/work/upi-fraud-model/upi-fraud-model/upi_transactions_2024.csv` — transaction dataset used by the notebook

## Problem Statement
UPI adoption has grown rapidly, and so have fraudulent transactions. The goal is to classify transactions as fraud (`1`) or non-fraud (`0`) and improve detection quality beyond raw accuracy.

## Setup
```bash
python -m venv venv
source venv/bin/activate   # On Windows: venv\Scripts\activate
pip install pandas numpy scikit-learn matplotlib seaborn jupyter
```

## How to Run
1. Open the notebook:
   ```bash
   jupyter notebook /home/runner/work/upi-fraud-model/upi-fraud-model/upi-transactions-2024-analysis-and-fraud-detection.ipynb
   ```
2. Update the dataset path in the notebook to:
   `/home/runner/work/upi-fraud-model/upi-fraud-model/upi_transactions_2024.csv`
3. Run all cells.

## Modeling Approach
- Data cleaning and categorical encoding
- Stratified train/test split
- Models:
  - Logistic Regression (`class_weight='balanced'`)
  - Random Forest (`class_weight='balanced_subsample'`)
- Threshold tuning for Logistic Regression using ROC (`argmax(tpr - fpr)`)

## Latest Evaluation Snapshot
Using the current notebook pipeline:

### Logistic Regression (tuned threshold)
- Threshold: `0.633122`
- Confusion Matrix `[[TN, FP], [FN, TP]]`: `[[74003, 853], [141, 3]]`
- Accuracy: `0.986747`
- Precision: `0.003504`
- Recall: `0.020833`
- F1-score: `0.006000`
- ROC-AUC: `0.441349`

### Random Forest (class-weighted)
- Confusion Matrix `[[TN, FP], [FN, TP]]`: `[[74856, 0], [144, 0]]`

## Key Takeaway
The dataset is highly imbalanced, so high accuracy alone is misleading. Fraud-focused metrics (precision, recall, F1, confusion matrix) should be used as primary evaluation criteria.

## Future Improvements
- Try resampling methods (SMOTE / undersampling)
- Add cost-sensitive learning and better threshold optimization targets
- Improve feature engineering with temporal and behavioral fraud signals
- Evaluate with PR-AUC and cross-validation
