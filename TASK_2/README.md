# 💳 Supervised Learning — Credit Card Fraud Detection Pipeline
> **Decode Labs — Data Science Internship, Project 2**

## 📌 Overview
This project builds a leak-free, imbalance-aware supervised classificationpipeline to detect fraudulent credit card transactions. The workflow covers EDA, a stratified train/test split, SMOTE-based class balancing, and
training/evaluation of two classifiers — Logistic Regression and Random Forest — using metrics appropriate for severe class imbalance (Precision, Recall, F1, ROC-AUC) rather than raw accuracy.

**Key result:** the pipeline is methodologically leak-free (stratified split before any scaling or resampling, SMOTE isolated to the training folds via an `imblearn` pipeline), and the features carry a strong,
genuine signal — both models substantially outperform random guessing (ROC-AUC 0.97+). Random Forest is the stronger model overall: it trades a small amount of Recall for a dramatic improvement in Precision, making it
the more deployable choice for a real fraud system.

## 📂 Dataset
**Dataset:** `creditcard.csv` [(Kaggle "Credit Card Fraud Detection" dataset — European cardholder transactions, September 2013)](https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud)
- **Rows:** 284,807
- **Columns:** 31
- **Class balance:** 492 fraud / 284,315 legitimate (0.17% positive class)

| Column | Description |
|---------|-------------|
| Time | Seconds elapsed between this transaction and the first in the dataset |
| V1–V28 | Anonymized features from a PCA transformation (original features not disclosed) |
| Amount | Transaction amount |
| Class | Target label — 1 = fraudulent, 0 = legitimate |

No missing values, no duplicate records.

---
## 📁 Project Structure
```text
TASK_2/
│
├── notebooks/
│   └── Project2.ipynb
|
├──visuals/
|   └──(images)
|
├── README.md
├── requirements.txt
└── .gitignore
```
---
## ✅ Project Workflow

### 1. Exploratory Data Analysis
- Checked shape, dtypes, missing values, and duplicates - Plotted class distribution and computed the exact fraud rate (0.17%) - Compared transaction `Amount` distribution between fraud and legitimate classes (boxplot + density histogram)

### 2. Preprocessing
- Features used: `Time`, `V1`–`V28`, `Amount` (all numeric, no categorical encoding needed since `V1`–`V28` are already PCA-transformed) - No feature dropping — since `V1`–`V28` are anonymized principal components, there are no interpretable identifier-like columns to remove

### 3. Stratified Train/Test Split
Split 80/20 using `stratify=y`, so both sets preserve the true 99.83%/0.17%
class ratio: - Train: 227,845 rows (227,451 legitimate / 394 fraud)- Test: 56,962 rows (56,864 legitimate / 98 fraud)
This keeps the test set representative of the real deployment distribution.

### 4. Leak-Free Scaling & SMOTE
- `StandardScaler` and `SMOTE` are both placed **inside** an `imblearn.pipeline.Pipeline`, fit only on training folds during `GridSearchCV` — never on the held-out test set - The train/test split happens **before** either step touches the data
  
This order matters: applying scaling or SMOTE before the split lets information from the test set leak into training, producing evaluation numbers that look better than the model will actually perform in production.

### 5. Hyperparameter Tuning
`GridSearchCV` (3-fold, scored on ROC-AUC) tuned both pipelines end-to-end, including the SMOTE neighbor count:
- **Logistic Regression:** best params `C=0.1`, `smote__k_neighbors=5` (CV ROC-AUC 0.981)
- **Random Forest:** best params `max_depth=20`, `n_estimators=100`,  `smote__k_neighbors=5` (CV ROC-AUC 0.969)

### 6. Model Evaluation
Both tuned models were evaluated on the **original, untouched, imbalanced** test set using Precision, Recall, F1, and ROC-AUC. Accuracy was excluded — a model predicting "legitimate" for every transaction scores 99.8% accuracy while catching zero fraud.

---
## 📊 Results

| Model | Precision | Recall | F1-Score | ROC-AUC |
|---|---|---|---|---|
| Logistic Regression | 0.058 | 0.918 | 0.109 | 0.971 |
| Random Forest | 0.781 | 0.837 | 0.808 | 0.977 |

Confusion matrices (test set, 56,864 legitimate / 98 fraud):

| Model | True Negative | False Positive | False Negative | True Positive |
|---|---|---|---|---|
| Logistic Regression | 55,407 | 1,457 | 8 | 90 |
| Random Forest | 56,841 | 23 | 16 | 82 |

---
## 🔍 Key Finding: Precision vs. Recall Trade-off

Logistic Regression catches slightly more fraud in absolute terms (90 vs.82 true positives), but at a steep cost: it misflags 1,457 legitimatetransactions to get there, a precision of just 5.8%. In a live payment system that translates to over a thousand real customers being blocked or flagged for every extra fraud case caught — an unacceptable customer-experience and operational cost.

Random Forest gives up 8 true positives but cuts false positives by over 98% (1,457 → 23), yielding a far more balanced and deployable model (F1 0.808 vs. 0.109).

**Conclusion:** Random Forest is the stronger model for this task.
Recall in isolation is a misleading measure of model quality on severely imbalanced data — Precision, Recall, F1, and ROC-AUC need to be read together against the real-world cost of false positives vs. false negatives before declaring a "better" model.

---
## 📚 Key Learnings
Through this project, I learned how to:
- Build a fully leak-free pipeline for imbalanced classification (correct order of split → scale → SMOTE, resampling isolated to training data only, via `imblearn.pipeline.Pipeline`) - Tune resampling and model hyperparameters jointly and safely with `GridSearchCV`, without leaking synthetic samples into validation folds - Choose and interpret metrics appropriate for severe class imbalance (Precision, Recall, F1, ROC-AUC) instead of accuracy - Read a confusion matrix in terms of real-world cost, not just headline  metrics — recognizing when high Recall hides an unusable false-positive rate - Compare two tuned models honestly and justify a final choice based on
  deployment trade-offs, not just the single highest number

---
## 🛠️ Technologies Used
- Python
- Pandas
- Matplotlib
- Seaborn
- Scikit-learn
- imbalanced-learn (SMOTE)
- Jupyter Notebook

---
## 👤 Author
**Yash Singh**
B.Sc. (Hons.) Computer Science
Keshav Mahavidyalaya, University of Delhi
**Decode Labs – Data Science Internship**