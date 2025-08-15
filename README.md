# Fraud Detection Model

## Project Overview

This project aims to detect fraudulent transactions in a financial dataset using machine learning techniques.  
The model analyzes transaction patterns and identifies suspicious activities to help prevent financial losses.

## Dataset

The dataset contains transaction details such as:

- Transaction type (e.g., payment, transfer, cash-out)
- Transaction amount
- Old and new balances for sender and receiver
- Fraud flag (`isFraud`)

### Source:

- https://drive.usercontent.google.com/download?id=1VNpyNkGxHdskfdTNRSjjyNa5qC9u0JyV&export=download&authuser=0

## Data Cleaning & Processing

1. **Missing Values**

   - Checked for missing values — none were found.

2. **Outlier Analysis**

   - Transaction amount distribution examined using log scale.
   - Outliers were not removed blindly, as some fraud cases can be high-value transactions.

3. **Multicollinearity Check**

   - Used Pearson correlation heatmap.
   - Found high correlation between:
     - `amount` and `amount_scaled`
     - `oldbalanceOrg` and derived balance features
   - For XGBoost, retained features; for regression-based models, would drop one of the correlated features.

4. **Feature Encoding & Scaling**
   - One-hot encoded categorical features like `type_payment`.
   - Scaled numerical features where required.

## Exploratory Data Analysis (EDA)

- Visualized fraud vs. non-fraud transactions.
- Observed that most fraudulent transactions occur in `TRANSFER` and `CASH_OUT` types.
- Fraud cases often have `oldbalanceDest` and `newbalanceOrig` inconsistencies.

## Model Development

- **Algorithm Used:** XGBoost Classifier
- **Evaluation Metrics:** Accuracy, Precision, Recall, F1-Score, ROC-AUC
- **Feature Selection:** Based on feature importance from the model and domain knowledge.
