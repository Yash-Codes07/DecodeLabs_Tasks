# 📊 Advanced EDA & Feature Engineering on an E-Commerce Order Dataset

> **Decode Labs — Data Science Internship, Project 1**

## 📌 Overview

This project focuses on exploring, cleaning, and preparing an e-commerce order dataset for further analysis and machine learning. The workflow includes data inspection, handling missing values, analyzing outliers, and creating new features to improve the dataset while preserving the meaning of the original data.

## 📂 Dataset

**Dataset:** `data/Dataset for Data Analytics.xlsx`

- **Rows:** 1,200
- **Columns:** 14

| Column | Description |
|---------|-------------|
| OrderID | Unique order identifier |
| Date | Order date |
| CustomerID | Customer identifier |
| Product | Product purchased |
| Quantity | Number of units ordered |
| UnitPrice | Price per unit |
| ShippingAddress | Shipping location |
| PaymentMethod | Payment method used |
| OrderStatus | Current order status |
| TrackingNumber | Shipment tracking number |
| ItemsInCart | Number of items added to the cart |
| CouponCode | Coupon code used (if any) |
| ReferralSource | Customer acquisition source |
| TotalPrice | Total order value |

---

## 📁 Project Structure

```text
TASK_1/
│
├── data/
│   ├── Dataset for Data Analytics.xlsx
│   └── Cleaned_Dataset.csv
│
├── notebooks/
│   └── Project1.ipynb
│
├── README.md
├── requirements.txt
└── .gitignore
```

---

## ✅ Project Workflow

### 1. Data Inspection

- Loaded the dataset
- Checked dataset shape and data types
- Generated descriptive statistics
- Identified missing values and duplicate records

### 2. Missing Value Handling

The `CouponCode` column contained missing values representing orders where no coupon was applied.

Instead of removing these records or filling them with statistical values, the missing entries were replaced with **"No Coupon"** to preserve their actual meaning.

### 3. Outlier Detection

The Interquartile Range (IQR) method was used to identify potential outliers in numerical columns.

Outliers detected in `TotalPrice` were investigated and found to represent legitimate high-value purchases rather than data entry errors, so they were retained.

### 4. Feature Engineering

Six new features were created to improve the dataset:

- **Year** – extracted from the `Date` column.
- **Month** – extracted from the `Date` column for time-based analysis.
- **MonthName** – extracted for easier interpretation in visualizations.
- **SpendingCategory** – categorizes customers based on their total purchase amount.
- **CouponUsed** – indicates whether a coupon was used.
- **CartAbandonmentGap** – represents the difference between the number of items added to the cart and the number of items purchased.

---

## 📊 Output

The cleaned dataset was exported as:

```text
data/Cleaned_Dataset.csv
```

---

## 🛠️ Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn
- Jupyter Notebook

---

## 📚 Key Learnings

Through this project, I learned how to:

- Inspect and understand a real-world dataset.
- Handle missing values based on business context.
- Detect and analyze outliers using the IQR method.
- Create meaningful features from existing data.
- Prepare a dataset for future machine learning projects.

---

## 👤 Author

**Yash Singh**

B.Sc. (Hons.) Computer Science  
Keshav Mahavidyalaya, University of Delhi

**Decode Labs – Data Science Internship**
