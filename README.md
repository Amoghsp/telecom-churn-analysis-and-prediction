# telecom-churn-analysis-and-prediction

## **⭐ Key Highlights**

| | |
|---|---|
| **Dataset** | 7,032 telecom customers, 26.6% churn rate |
| **Biggest churn driver** | Month-to-month contract: 42.7% churn vs 2.9% for two-year |
| **Highest-risk segment** | Month-to-month fiber-optic users: 54.6% churn |
| **Models compared** | Logistic Regression, Decision Tree, Random Forest, XGBoost |
| **Final model** | Tuned XGBoost (GridSearchCV, class weighting) |
| **Final performance** | 84.02% ROC-AUC, 80.48% recall, 60.99% F1 |
| **Tools** | Python, Pandas, NumPy, Seaborn, Scikit-learn, XGBoost |

## **📌 Project Overview**
Customer churn is a major business problem for telecom companies because losing existing customers affects revenue and growth.

This project combines **Exploratory Data Analysis (EDA)** and **Machine Learning** to understand customer churn patterns and predict which customers are likely to churn. It analyzes 7,032 telecom customer records and compares Logistic Regression, Decision Tree, Random Forest and XGBoost models.

## **🎯 Project Objectives**
- Understand key factors associated with customer churn
- Clean and prepare telecom customer data
- Perform exploratory data analysis
- Engineer tenure and monthly-charge groups
- Compare multiple classification models
- Tune XGBoost using GridSearchCV
- Evaluate models using Accuracy, Precision, Recall, F1 Score and ROC-AUC
- Generate churn probability and risk levels for new customers

## **📊 Dataset**
Telco Customer Churn dataset (IBM sample data, publicly available on Kaggle).

- Raw data: 7,043 customers and 21 columns
- Cleaning: converted `TotalCharges` to numeric and removed 11 rows with missing values (customers with 0 months of tenure, not yet billed), leaving **7,032 customers**
- Churn rate: **26.6%** (1,869 churned, 5,163 stayed)
- Target: `Churn` (Yes = churned, No = stayed)
- Feature categories: demographics, tenure, phone and internet services, online security and backup, device protection, tech support, streaming, contract type, paperless billing, payment method, monthly and total charges

## **🔎 Exploratory Data Analysis**
Churn was examined across demographics, tenure, contracts, services and billing behavior.

### **Feature Engineering**
**TenureGroup**

| Tenure | Group |
|---|---|
| 0–12 months | 0-12 Months |
| 13–24 months | 13-24 Months |
| 25–36 months | 25-36 Months |
| 37–48 months | 37-48 Months |
| 49–60 months | 49-60 Months |
| 61–72 months | 61-72 Months |

**MonthlyChargeGroup**

| Monthly Charges | Group |
|---|---|
| Up to 30 | Low |
| Above 30 to 60 | Medium |
| Above 60 to 90 | High |
| Above 90 to 120 | Very High |

### **Key Findings**
- About 1 in 4 customers churned (26.6%)
- **Contract type matters most:** month-to-month customers churn at **42.7%**, one-year at 11.3% and two-year at only **2.9%**
- **Highest-risk segment:** month-to-month fiber-optic users at **54.6%**
- **New customers leave most:** 47.7% churn in the first 12 months versus 6.6% for customers with 61-72 months
- Churned customers paid more per month on average (about $74 vs $61); high and very high charge groups churn at roughly 33-34%
- Customers without tech support, those paying by electronic check, senior citizens, and those without a partner or dependents also showed higher churn

## **🤖 Machine Learning Workflow**
```
Cleaned Data
    ↓
Train-Test Split
    ↓
Feature Preprocessing
    ↓
Model Training
    ↓
Model Comparison
    ↓
XGBoost Hyperparameter Tuning
    ↓
Model Evaluation
    ↓
Feature Importance
    ↓
New Customer Prediction
```

### **Data Preprocessing**
- Scikit-learn `ColumnTransformer`: `StandardScaler` for numeric features, `OneHotEncoder` for categorical features
- Scikit-learn `Pipeline` combining preprocessing and model training (preprocessing is fitted on training data only)
- Stratified 80/20 train-test split

### **Models Compared**
Logistic Regression, Decision Tree, Random Forest, XGBoost, and a tuned XGBoost.

### **⚙️ XGBoost Hyperparameter Tuning**
Tuned with `GridSearchCV` (3-fold, F1 scoring) over `n_estimators`, `max_depth` and `learning_rate`. Class weighting (`scale_pos_weight`) was used to address class imbalance.

## **📈 Model Results (Test Set)**

| Model | Accuracy | Precision | Recall | F1 | ROC-AUC |
|---|---|---|---|---|---|
| Logistic Regression | 0.8038 | 0.6612 | 0.5374 | 0.5929 | 0.8359 |
| Decision Tree | 0.7783 | 0.5807 | 0.5963 | 0.5884 | 0.8195 |
| Random Forest | 0.7889 | 0.6323 | 0.4920 | 0.5534 | 0.8340 |
| XGBoost | 0.7946 | 0.6341 | 0.5374 | 0.5818 | 0.8399 |
| **Tuned XGBoost** | 0.7264 | 0.4910 | **0.8048** | **0.6099** | **0.8402** |

### **Final Model: Tuned XGBoost**
| Metric | Score |
|---|---|
| Accuracy | 72.64% |
| Precision | 49.10% |
| Recall | 80.48% |
| F1 Score | 60.99% |
| ROC-AUC | 84.02% |

### **Why Recall Matters**
For churn prediction, missing a customer who is likely to leave is costly. The final model therefore emphasizes recall and identifies about 80% of customers who actually churn.

The trade-off is lower precision (49%), meaning more false alarms. This is usually acceptable when a retention offer costs less than losing a customer.

## **🔮 Customer Churn Prediction**
For a new customer, the workflow produces a churn prediction, churn probability and risk level.

```
Prediction: Customer is likely to CHURN
Churn Probability: 83.71 %
Risk Level: High
```
> Because class weighting inflates predicted probabilities, treat the probability as a risk score rather than an exact likelihood.

## **🛠️ Technologies Used**
- **Programming & analysis:** Python, Pandas, NumPy
- **Visualization:** Matplotlib, Seaborn
- **Machine learning:** Scikit-learn, XGBoost
- **Techniques:** Data cleaning, EDA, feature engineering, one-hot encoding, feature scaling, classification, GridSearchCV, model evaluation, feature importance

## **📂 Project Structure**
```
telecom-churn-analysis-and-prediction/
│
├── Customer_churn_analysis.ipynb      # cleaning, feature engineering, EDA
├── Customer_churn_prediction.ipynb    # modelling, tuning, prediction
├── Telco Customer Churn.csv           # raw dataset
├── Customer churn analysis.csv        # cleaned dataset
├── requirements.txt
├── .gitignore
└── README.md
```

## **💡 Business Value**
- Identify customer segments with higher churn risk
- Understand relationships between contracts, tenure, services and billing
- Prioritize customers who may need retention efforts
- Provide probability-based churn predictions

This is a portfolio-level analytical and predictive workflow rather than a production deployment.

## **⚠️ Limitations**
- The analysis shows relationships, not causes
- The final model was selected using test-set results; cross-validated comparison would be more rigorous

## **🔭 Future Improvements**
- Test additional classification algorithms
- Calibrate predicted probabilities
- Optimize the classification threshold based on business costs
- Expand hyperparameter search and cross-validation
- Deploy the model through a Streamlit application

## **📚 Dataset Credit**
Telco Customer Churn dataset (IBM sample data), available on Kaggle.
