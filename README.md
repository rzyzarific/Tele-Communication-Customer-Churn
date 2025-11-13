# Tele-Communication-Customer-Churn
I worked on a Kaggle Dataset which was Customer Churn Prediction for a Telecom Company. 

This project focuses on **exploring, cleaning, and preparing** a telecom customer dataset for churn prediction.  
You’ll go from **raw business data → SQL insights → a clean ML-ready dataset**.

---

## 📊 Tasks Overview

### 1. Data Exploration

Use **Pandas** & **SQL** to answer:

- 🔹 How many customers **churned**?
- 🔹 What’s the **average tenure** of churn vs non-churn customers?
- 🔹 Which **contract type** has the highest churn?

---

### 2. Data Cleaning & Preprocessing

Steps:

- 🧹 Handle **missing values** in `TotalCharges`
- 🔢 Convert **categorical variables** (`gender`, `Contract`, etc.) into numeric  
  (via **Label Encoding** or **One-Hot Encoding**)
- 📏 **Standardize** numeric features: `MonthlyCharges`, `TotalCharges`, `tenure` using `StandardScaler`
- 🚫 Remove duplicate `customerID` entries (if any)

---

### 3. Feature Engineering

Create useful new features:

| Feature Name | Formula / Logic | Description |
|---------------|----------------|--------------|
| `AvgChargesPerMonth` | `TotalCharges / (tenure + 1)` | Average charge per customer per month |
| `IsSenior` | `(SeniorCitizen == 1)` | Binary flag for senior citizens |
| `HasPartnerAndDependents` | `(Partner == "Yes" and Dependents == "Yes")` | Flag for customers with both partner and dependents |

---

### 4. SQL Reporting

Generate reports for management using SQL queries:

-- 1. Customers who churned but had tenure > 2 years
SELECT * 
FROM customers
WHERE Churn = 'Yes' AND tenure > 24;

-- 2. Churn rate by payment method
SELECT PaymentMethod, 
       ROUND(SUM(CASE WHEN Churn = 'Yes' THEN 1 ELSE 0 END)*100.0/COUNT(*), 2) AS ChurnRate
FROM customers
GROUP BY PaymentMethod;

-- 3. Average monthly charges by internet service type
SELECT InternetService, 
       ROUND(AVG(MonthlyCharges), 2) AS AvgMonthlyCharges
FROM customers
GROUP BY InternetService;

What I learned --
1. How industry datasets are messy (missing values, categorical encoding, scaling)
2. How SQL fits into analytics pipelines.
3. How to bridge raw business problem → clean dataset → ready for modeling.
