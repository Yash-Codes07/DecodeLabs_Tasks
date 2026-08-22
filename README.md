# 🧠 Data Science Internship — Decode Labs
> **Yash Singh** — B.Sc. (Hons.) Computer Science, Keshav Mahavidyalaya, University of Delhi

This repository contains the project work completed as part of the **Decode Labs Data Science Internship**. Each task lives in its own folder with a dedicated dataset, notebook, and README covering the objective, workflow,
and results in detail.

---
## 📁 Repository Structure
```text
.
│
├── TASK_1/                     # Advanced EDA & Feature Engineering
│   ├── data/
│   │   ├── Dataset for Data Analytics.xlsx
│   │   └── Cleaned_Dataset.csv
│   ├── notebooks/
│   │   └── Project1.ipynb
│   ├── README.md
│   ├── requirements.txt
│   └── .gitignore
│
├── TASK_2/                     # Supervised Learning — Fraud Detection
│   ├── notebooks/
│   │   └── Project2.ipynb
│   ├── README.md
│   ├── requirements.txt
│   └── .gitignore
│
└── README.md                   # you are here
```

---
## 📌 Projects

| # | Project | Task | Key Skills | Result |
|---|---------|------|------------|--------|
| 1 | [Advanced EDA & Feature Engineering](./TASK_1) | Clean a 1,200-row e-commerce order dataset and engineer new predictive features | Pandas, NumPy, IQR outlier detection, statistical imputation, feature extraction | Delivered a leak-free, ML-ready dataset with 6 engineered features, missing values handled by business logic rather than blind imputation |
| 2 | [Supervised Learning — Fraud Detection](./TASK_2) | Build a leak-free classification pipeline to detect fraudulent credit card transactions on a severely imbalanced (0.17%) dataset | Scikit-learn, imbalanced-learn (SMOTE), GridSearchCV, Precision/Recall/F1/ROC-AUC | Random Forest (tuned) achieved 0.781 Precision, 0.837 Recall, 0.977 ROC-AUC — chosen over Logistic Regression for its far lower false-positive rate |

Click into each folder's README for the full breakdown: dataset details, step-by-step workflow, evaluation metrics, and key learnings.

---
## 🧭 Recurring Principles Across Both Projects
A few practices were applied consistently across both tasks, regardless of the specific problem:
- **Handle missing/imbalanced data based on what it actually means**, not by default statistical rules — e.g. missing `CouponCode` values were labeled `"No Coupon"` rather than imputed, since the absence itself was
  meaningful information, not noise.
- **Prevent data leakage end-to-end** — any transformation that "learns" from data (scaling, resampling, imputation with fitted statistics) is scoped strictly to training data, never leaking test-set information into the modeling process.
- **Choose metrics that match the problem, not the easiest number to report** — accuracy was deliberately avoided in Task 2 given severe class imbalance, in favor of Precision, Recall, F1, and ROC-AUC read together.

---
## 🛠️ Technologies Used
- Python
- Pandas / NumPy
- Matplotlib / Seaborn
- Scikit-learn
- imbalanced-learn (SMOTE)
- Jupyter Notebook

---
## 👤 Author
**Yash Singh**

B.Sc. (Hons.) Computer Science
Keshav Mahavidyalaya, University of Delhi

**Decode Labs — Data Science Internship**