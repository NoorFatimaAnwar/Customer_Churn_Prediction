# 🛒 Customer Churn Prediction for E-commerce Using Machine Learning

This project builds a machine-learning based **Customer Churn Prediction System** for an e-commerce platform.  
The dataset initially **did not contain any churn label**, so churn was derived using a realistic industry-standard definition based on **180 days of inactivity**.

The main strength of this project is **rich feature engineering**, including RFM, interpurchase gap analysis, temporal behavior tracking, 30-day rolling features, and customer trend decline detection.

---

## 📌 Project Highlights

- ✔ Created a realistic churn label (no label originally present)
- ✔ Engineered **30+ advanced features** describing customer behavior
- ✔ Cleaned & transformed date + time data
- ✔ Built multiple ML models (RF, XGBoost, GBC, Logistic Regression)
- ✔ Evaluated using Accuracy, Precision, Recall, F1, and ROC-AUC
- ✔ Explained **why ROC-AUC is high but accuracy is lower**
- ✔ Delivered insights close to real-world churn prediction challenges

---

# 📂 Dataset Overview

The dataset consists of **51,290 e-commerce order records**, including:

- Customer ID  
- Order Date + Time  
- Product Category  
- Quantity, Sales, Discount, Shipping Cost  
- Payment Information  
- Login Device  
- Customer Location  

### **Churn Definition (Important)**  
Since no churn label existed:

> **A customer is considered “churned” if they have not placed any order in the last 180 days from the reference date.**

This makes the dataset realistic and usable for predicting future inactivity.

---

# 🧹 Data Cleaning & Preprocessing

### Key steps performed:

- Filled missing numeric values using **median**
- Filled `Quantity` with **1**, and `Discount` with **0**
- Filled categorical missing values using **mode**
- Fixed invalid time formats (e.g., entries like `1`)
- Combined `Order_Date` and `Time` into a single **Order_Datetime**
- Ensured data consistency for temporal calculations

This enabled reliable time-based feature engineering.

---

# 🧠 Feature Engineering (Core Contribution)

The heart of this project is **behavior-driven features** that detect subtle churn patterns.

## **1️⃣ RFM Features**
- Recency (days since last purchase)
- Frequency (total orders)
- Monetary value (total spend)
- Average order value
- Customer lifetime

## **2️⃣ Order Behavior**
- Total quantity purchased
- Favorite product category
- Product diversity
- Percentage of weekend orders
- Discount usage rate
- Most preferred hour of purchase

## **3️⃣ Shipping & Cost Patterns**
- Average shipping cost per customer

## **4️⃣ Interpurchase Gap Features**
- Mean interpurchase days  
- Standard deviation of gaps  
- Maximum purchase gap  
- Recent gap (last 2 orders)  
- Gap trend (increasing or decreasing)  
- **Gap-increase flag** (binary)

## **5️⃣ 30-Day Rolling Window**
For each customer:

- Orders in last 30 days  
- Spend in last 30 days  
- Orders in previous 30 days  
- Spend in previous 30 days  
- **Orders trend (current vs previous 30 days)**  
- **Spend trend**  
- Decline flags (binary)

## **6️⃣ Rate & Trend Features**
- Purchase rate per day
- Recent frequency per day
- Long-term vs short-term frequency ratio
- Frequency decline flag  
- Spend decline flag

These engineered features mimic **real business intelligence KPIs** used by large e-commerce companies.

---

# 🤖 Machine Learning Models Used

- **Random Forest**
- **Gradient Boosting Classifier**
- **XGBoost**
- **Logistic Regression**

### Evaluation Metrics
- Accuracy  
- Precision  
- Recall  
- F1-score  
- ROC-AUC  
- Confusion Matrix  

Models were trained after:

✔ SMOTE applied only to training set (correct)  
✔ Standard scaling  
✔ Train-test split using stratification  

---

# 📊 Results

| Model | Accuracy | F1 Score | ROC-AUC |
|-------|----------|----------|---------|
| Random Forest | ~0.68 | ~0.68 | ~0.76 |
| Gradient Boosting | ~0.68 | ~0.68 | ~0.764 |
| XGBoost | ~0.68 | ~0.67 | ~0.766 |

### Interpretation

Even with extensive feature engineering:

- Accuracy stays around **66–70%**
- ROC-AUC is **strong (~0.76)**

This is **normal** because:

- Churn label is derived, not directly observed  
- Customer behavior patterns are noisy and overlapping  
- Purchase churn is harder than subscription churn  
- Real-world churn datasets commonly achieve **60–75% accuracy**

---

# ⚠️ Why Accuracy Is Lower but ROC-AUC Is Higher?

Accuracy/F1 measure **hard classification** at threshold 0.5.  
ROC-AUC measures **how well the model ranks churners higher than non-churners**.

My model ranks correctly → **high ROC-AUC**  
But thresholding at 0.5 → **moderate accuracy**  

which is expected and perfectly valid for churn problems.

---

