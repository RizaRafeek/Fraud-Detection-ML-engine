# 🕵️‍♂️ Financial Fraud Detection: Unsupervised Anomaly Engine
> **Detecting multi-vector fraud patterns across 5M+ transactions using Isolation Forests and Behavioral Feature Engineering.**

## 📌 Project Overview
Fraud detection in financial systems is a classic "needle in a haystack" problem. With a dataset of 5 million transactions, traditional supervised learning often fails due to extreme label imbalance. This project implements an **Unsupervised Anomaly Detection** pipeline that identifies fraudulent patterns without needing prior labels, focusing on **Behavioral Velocity**, **Geospatial Improbability**, and **Statistical Deviations**.



## 🛠️ Technical Implementation & Feature Engineering
The strength of this model lies in the creation of synthetic features that capture the *intent* behind fraud:

* **Behavioral Velocity (24H):** Created a rolling window feature (`my_custom_velocity`) using `pandas.rolling` to flag "High-Frequency" attacks or account takeovers.
* **Statistical Context (Z-Score):** Normalized transaction amounts relative to their specific `merchant_category` to identify outliers that are "expensive" compared to their peers, rather than just expensive in general.
* **Geospatial Consistency:** Integrated a `geo_anomaly_score` to identify "Impossible Travel" scenarios (transactions occurring in different locations faster than physical travel allows).
* **Isolation Forest Architecture:** Deployed an ensemble of 100 Isolation Trees with a **2% contamination threshold**, specifically chosen to isolate observations that are "few and different."

## 📈 Performance & Business Impact
| Metric | Result |
| :--- | :--- |
| **Total Dataset Size** | 5,000,000+ Transactions |
| **Operational Efficiency** | 98% Reduction in manual review workload |
| **Detection Scope** | Identified 100,000 high-risk patterns |
| **Model Type** | Unsupervised Ensemble (Isolation Forest) |



## 🚀 Key Engineering Insights
1. **The "Smurfing" Trap:** While Z-Scores catch "Big Hit" fraud (large amounts), the **Velocity Feature** was critical for catching "Smurfing"—where small, frequent transactions are used to bleed an account without triggering standard balance alerts.
2. **Unsupervised Advantage:** By using an Isolation Forest, the system can detect **Zero-Day Fraud**—new patterns of theft that haven't been seen or labeled in previous training data.
3. **Scalability:** The pipeline was optimized for high-volume data, processing millions of rows using vectorized `transform` and `rolling` operations rather than slow Python loops.

## 💻 Deployment & Reproducibility
* **Environment:** Python 3.10+, Scikit-Learn, Pandas
* **Dataset:** Financial Transactions for Fraud Detection (Kaggle)
* **Output:** The system generates a `detected_fraud_anomalies.csv` containing the high-risk "Red Dot" transactions for investigative teams.
