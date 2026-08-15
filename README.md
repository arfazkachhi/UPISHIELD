# UPISHIELD — Fraud Detection Using Liquid Neural Network

## Overview

UPISHIELD is a fraud detection system designed to identify potentially fraudulent financial transactions by analysing customer transaction behaviour over time.

The project uses a **Liquid Neural Network (LNN)** based on the **Closed-form Continuous-time (CfC)** architecture. Instead of analysing transactions only as individual records, the model processes transactions in chronological sequences to capture changes in customer behaviour.

## Project Architecture

```text
Dataset
   ↓
Preprocessing
   ↓
Feature Engineering
   ↓
Sequence Generation
   ↓
Data Splitting
   ↓
CfC-LNN
   ↓
Fraud Prediction
   ↓
Perform
Methodology
1. Dataset

The project uses the BankSim dataset containing simulated financial transaction records. The dataset contains transaction information such as customer details, transaction amount, time-related information, and fraud labels.

The original dataset contains 594,643 transactions.

2. Preprocessing

The transaction data is cleaned and prepared before being provided to the model. Relevant columns are selected, categorical information such as gender is encoded, and time-related information is processed while maintaining the chronological order of transactions.

3. Behavioural Feature Engineering

Additional behavioural features are generated to capture changes in customer transaction patterns. These include:

Previous transaction amount
Amount difference
Rolling average transaction amount
Rolling transaction standard deviation
Amount compared with recent average
Previous time difference
Average time difference
Transaction count
Maximum and minimum recent transaction amounts
Increasing transaction indicator
Transaction amount z-score

These features provide additional information about how customer behaviour changes over time.

4. Sequence Generation

Transactions are arranged chronologically and converted into sequences so that the model can learn from multiple consecutive transactions rather than treating every transaction independently.

The final LNN configuration uses a sequence length of 10 transactions.

5. Data Splitting

The data is divided chronologically into training, validation, and test sets. The training data is used to learn the model parameters, the validation data is used for threshold selection and model monitoring, and the unseen test data is used for the final evaluation.

6. CfC-LNN Model

The core of UPISHIELD is a Liquid Neural Network using the Closed-form Continuous-time (CfC) model.

The LNN processes the transaction sequences and learns temporal relationships in customer behaviour. Its continuous-time architecture allows the model to capture changes in transaction patterns and use this information when determining whether a transaction sequence is likely to contain fraudulent activity.

7. Fraud Prediction

The trained model produces a probability indicating the likelihood of fraud. An optimal classification threshold is selected using the validation data based on the F1-score. This threshold is then applied to the unseen test data to classify transactions as either Normal or Fraud.

8. Performance Evaluation

The models are evaluated using:

Accuracy
Precision
Recall
F1-Score
ROC-AUC
PR-AUC

A confusion matrix is also used to examine the number of correctly and incorrectly classified normal and fraudulent transactions.

Model Comparison

The proposed LNN was compared with several machine learning approaches using the test results.

Model	Accuracy	Precision	Recall	F1-Score	ROC-AUC
ABOD	98.77%	50.32%	49.95%	50.39%	98.52%
CBLOF	99.02%	60.69%	61.74%	65.72%	96.88%
Isolation Forest	98.51%	66.74%	58.67%	69.32%	96.47%
Proposed LNN	99.46%	81.00%	65.75%	72.55%	99.19%

The proposed LNN achieved the highest Accuracy, Precision, F1-Score, and ROC-AUC among the models shown in the comparison.

Final LNN Results
Accuracy  : 99.46%
Precision : 81.00%
Recall    : 65.75%
F1 Score  : 72.55%
ROC-AUC   : 99.19%
PR-AUC    : 77.66%

These results show that the proposed approach can identify fraudulent behaviour while maintaining a strong balance between precision and recall.

Technologies Used
Python
PyTorch
Liquid Neural Network
Closed-form Continuous-time (CfC)
Pandas
NumPy
Scikit-learn
Matplotlib
Project Structure
UPISHIELD/
│
├── lnn_fraud_detection.ipynb
├── README.md
└── .gitignore

The BankSim dataset is not included in this repository.

Future Scope

Future work can focus on improving fraud detection recall, testing the model on real-world transaction datasets, exploring additional behavioural features, and developing a real-time fraud detection system.

Authors

Arfaz Kachhi

BCA — Symbiosis Institute of Computer Studies and Research (SICSR), Pune



