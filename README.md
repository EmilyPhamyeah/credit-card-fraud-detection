Here is a **clean, professional `README.md`** you can use directly for GitHub:

---

# 💳 Credit Card Fraud Detection

## 📌 Project Overview

This project aims to build machine learning models to detect fraudulent credit card transactions using a highly imbalanced real-world dataset.

Fraud detection is a critical problem in fintech, where missing fraudulent transactions can lead to significant financial loss, while too many false alarms can negatively impact user experience.

---

## 🎯 Objectives

* Detect fraudulent transactions with **high recall**
* Maintain **reasonable precision** to reduce false alarms
* Compare multiple machine learning approaches
* Provide **business-oriented insights**

---

## ⚠️ Challenges

* Extreme class imbalance

  * Fraud: 492
  * Normal: 284,315
* Fraud patterns are subtle and overlap with normal behavior
* Trade-off between:

  * Detecting fraud (recall)
  * Avoiding false alerts (precision)

---

## 📊 Dataset

* Source: https://www.kaggle.com/datasets/mlg-ulb/creditcardfraud (Due to file size limitations, the dataset is not included)
* Features:

  * **V1–V28**: PCA-transformed features (anonymized)
  * **Time**: seconds since first transaction
  * **Amount**: transaction value
  * **Class**: target (0 = Normal, 1 = Fraud)

---

## 🔍 Exploratory Data Analysis (EDA)

Key findings:

* **Highly imbalanced dataset**
* Fraud transactions are often:

  * Smaller in median value
  * More concentrated in distribution
* Significant overlap between fraud and normal → no single feature is sufficient
* Time-based patterns show slightly higher fraud activity during early hours (weak signal)
* PCA features are mostly uncorrelated

---

## ⚙️ Methodology

### Data Preprocessing

* Train-test split with stratification
* Feature scaling (for Logistic Regression & Autoencoder)
* Handling imbalance:

  * **SMOTE** (Logistic Regression, Random Forest)
  * **Class weights** (LightGBM)
  * No resampling (XGBoost)

---

## 🤖 Models Used

* Logistic Regression
* Random Forest
* XGBoost
* LightGBM
* Autoencoder (unsupervised anomaly detection)

---

## 📈 Model Performance

| Model               | Precision | Recall    | F1-score  | ROC-AUC |
| ------------------- | --------- | --------- | --------- | ------- |
| Autoencoder         | 0.008     | **0.949** | 0.016     | —       |
| XGBoost             | 0.351     | 0.898     | 0.504     | 0.974   |
| LightGBM            | 0.633     | 0.898     | **0.743** | 0.976   |
| Logistic Regression | 0.648     | 0.847     | 0.735     | 0.976   |
| Random Forest       | **0.827** | 0.827     | **0.827** | 0.964   |

---

## 🔢 Confusion Matrix Summary

| Model               | TP | FN | FP    | TN    |
| ------------------- | -- | -- | ----- | ----- |
| Logistic Regression | 83 | 15 | 45    | 56819 |
| Random Forest       | 81 | 17 | 17    | 56847 |
| XGBoost             | 88 | 10 | 163   | 56701 |
| LightGBM            | 88 | 10 | 51    | 56813 |
| Autoencoder         | 93 | 5  | 11103 | 45761 |

---

## 🔍 Feature Importance Insights

Across all models, the most important features are:

* **V14**
* **V10**
* **V12**
* **V17**

These features consistently appear as top predictors, indicating strong fraud signals.

Secondary contributors:

* V4, V3, V11, V16

👉 Fraud detection relies on **multiple interacting features**, not a single variable.

---

## 💼 Business Insights

### 1. High fraud detection capability

* LightGBM and XGBoost detect ~90% of fraud cases

### 2. Trade-off: Recall vs Precision

* Higher recall → more false positives
* Example:

  * XGBoost: high recall but more false alarms
  * Autoencoder: unusable due to extremely high false positives

### 3. Best model for real-world use

* **LightGBM provides the best balance**

  * High recall
  * Reasonable precision
  * Strong overall performance

### 4. Autoencoder limitation

* High recall but extremely low precision
* Not suitable as a standalone solution
* Can be used as a **supporting anomaly signal**

---

## 🚀 Deployment Strategy (Recommended)

Instead of using a single model:

**Step 1:** Use LightGBM as primary model
**Step 2:** Apply risk thresholds:

* High risk → block / OTP verification
* Medium risk → manual review
* Low risk → allow transaction

---

## 🧠 Key Takeaways

* Tree-based models outperform linear models in fraud detection
* Feature interactions are critical
* Threshold tuning is essential
* Best system = balance between:

  * Fraud detection (recall)
  * Customer experience (precision)

---

## 🛠️ Tech Stack

* Python
* Pandas, NumPy
* Scikit-learn
* XGBoost
* LightGBM
* Matplotlib, Seaborn

---

## 📁 Project Structure

```
├── data/
│   └── creditcard.csv
├── notebooks/
│   └── fraud_detection.ipynb
├── README.md
```



