# Detecting When Customers Stop Buying Using Linear Regression

This project demonstrates a **simple, interpretable approach to detecting declining customer purchase behavior** using time series aggregation and linear regression.  
Instead of relying on complex churn models, we analyze **purchase trends over time** to identify when customers are slowly disengaging.

## 📌 Problem Statement

Customer churn rarely happens overnight.  
In many cases, customers gradually reduce their purchasing frequency before stopping completely. Such a phenomenon is often referred to as **silent churn**.

Traditional churn models:
- Require labeled churn data
- Are complex and hard to explain
- Detect churn **after** it already happened

This project answers a simpler question:

> **“Is this customer slowing down?”**

## 💡 Solution Overview

We use **monthly purchase trends** and **linear regression** to measure customer momentum over time.

The core idea:
1. Aggregate customer transactions by month
2. Create a continuous time index
3. Fill missing months with zero purchases
4. Fit a linear regression line
5. Use the **slope (converted to degrees)** to quantify buying behavior

A **negative slope** indicates declining engagement.

## 🧠 Why Linear Regression?

- Extremely fast to compute
- Highly interpretable
- Works well with sparse transaction data
- Easy to explain to business stakeholders

Instead of predicting churn, we **measure trend direction**.

## 🛠️ Methodology

### 1. Filter Customer Transactions
We isolate transactions for a single customer.

### 2. Group by Month
Transactions are aggregated monthly to reduce noise and standardize time intervals.

### 3. Create a Continuous Time Index
Each month becomes a numeric index (0, 1, 2, ...), allowing flexible time windows beyond fixed calendar years.

### 4. Handle Missing Months
Months without purchases are explicitly filled with `0` to preserve trend continuity.

### 5. Apply Linear Regression
We apply `scipy.stats.linregress` to calculate:
- Slope
- Intercept
- Trend direction

### 6. Convert Slope to Degrees
The slope is converted to degrees using `arctan` for better interpretability:

- Positive angle → Increasing purchases
- Near zero → Stable behavior
- Negative angle → Declining purchases

## 📈 Example Interpretation

| Slope Angle | Interpretation |
|------------|----------------|
| > +5° | Growing customer |
| -5° to +5° | Stable customer |
| < -5° | Declining / At-risk |

> These thresholds are adjustable depending on business context.

## 🧪 Notebook Highlights

- Quick experimentation with `linregress`
- Step-by-step trend calculation
- Explicit handling of zero-purchase months
- Business-friendly interpretation of mathematical results

## 🚀 Use Cases

- Early churn detection
- Customer health scoring
- Retention analytics
- Feature engineering for churn models
- CRM prioritization

## 🔍 Limitations

- Not a probabilistic churn prediction
- Sensitive to very short time windows
- Works best when combined with other behavioral signals

## 🧰 Tech Stack

- Python
- Pandas
- NumPy
- SciPy
- Jupyter Notebook

## 📖 Next Steps

Possible extensions:
- Apply the logic at scale for all customers
- Combine slope with recency and frequency metrics
- Feed trend features into a churn classification model
- Automate monitoring with scheduled jobs

## ✍️ Author

Created by **Gustavo Santos**  
Data Scientist | Educator | Author  

If you find this useful, feel free to ⭐ the repository or adapt it to your own retention problems.


