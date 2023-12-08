# CreditCardChurning
The Churn Prediction Challenge involves data exploration and preparation, involving building a predictive model to classify users into active and inactive categories based on their activity and payment history.

:round_pushpin: **Objective:**
> Predict churn customers

**Code:** 
- [main](./main.ipynb)

**Dataset:**
- [Description](./Credit%20card%20churning.pdf)
- y_train.csv - Output for selected user IDs
- demo.csv - Personal information of customers
- card_info.csv - Credit card information
- cc_txn.csv - Credit card transaction log
- sa_bal.csv - Saving account balance aggregated by months
- dtxn.csv - Incoming and outgoing transactions aggregated by months (exclude credit card transactions) 

**Process:**
1. Clean and prepare data
2. Explore dataset
3. EDA
4. Model training
5. Model evaluation
6. Conclusion and recommendations


# Clean and prepare data

- Handle with a null value

### Personal information of customers dataset

![image](https://github.com/terjirapat/CreditCardChurning/assets/77285026/3364b9be-6348-4dc6-ae84-b52c682d63a6)

- Found null value on the Personal information of customers dataset
  - 23.30% of the total in column 'marital_status'
  - 12.93% of the total in column 'family_income_segment_code'
  - 6.06% of the total in column 'individual_income_segment_code'
  
**Solution**: replace null with 'unk' value

# Explore dataset

### Personal information of customers dataset
- Create an age of customers column (age) from > 2018 - birth_year column
- Create a customer duration column (cus_dur) from > 2018 - account_start_date column

<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/e91d172c-3bb6-4567-aa9d-9b47033d8d8a' width="720" height="280">

- Customer age range between 17-117 years
- Customer duration between 9-77 years

### Credit card information dataset
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/ffb3fd35-e3f0-4d58-8a93-1091cf9a4f6b' width="550" height="130">

### Credit card transaction log dataset

<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/9067ef9b-43cb-43d0-a383-6b07811d9548' width="720" height="220">

- The minimum per transaction is 1 and the maximum is 487,141
- Transaction log data starts from 2017-01-26 to 2017-12-31

### Saving account balance aggregated by months dataset
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/c3ef7ea8-a015-403f-b0f9-096185cdb601' width="550" height="110">

### Incoming and outgoing transactions aggregated by months (exclude credit card transactions) dataset
- Create net money inflow column (change) from > amt_in - amt_out column

<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/6bf7909f-7d75-40e2-bdd5-c666bdd67429' width="800" height="150">

# EDA

### Categorical data

<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/ad500b8a-f125-4101-9db2-377e9189579e' width="300" height="250">
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/bb4d42a8-2a86-43b6-b6af-d66db0e874aa' width="300" height="250">
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/38ec531b-c33b-4ea7-897f-3b6b3406d662' width="300" height="250">
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/f1d11b49-96c3-40e9-9cae-f0bea93bef61' width="300" height="250">

- Target does not seem to be related with any categorical in the personal information of customers' dataset

<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/68cef2c8-4b65-4ca9-bd55-a616c31049c0' width="500" height="280">
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/10ebc095-34fa-4c1b-92de-df9894f01d32' width="500" height="280">

- Target does not seem to be related to the total spending and transactions count of each merchant category

## Correlation plot
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/e6817eff-2cc5-473d-8b96-9c02d70640c4' width="700" height="700">

- Feature choosing from high correlation with the target
  - total_spend - Total spending of customer
  - total_spend_3m - Total spending of a customer last 3 months
  - total_spend_6m - Total spending of a customer last 6 months
  - avg_spend - Average spending of customer per transaction
  - avg_spend_3m - Average spending of a customer per transaction last 3 months
  - avg_spend_6m - Average spending of a customer per transaction last 3 months
  - avg_sabal_month - Average saving balance of customer
- Feature choosing from domain knowledge
  - count_txn - Count of transactions of a customer
  - count_txn_3m - Count of transactions of a customer last 3 months
  - count_txn_6m - Count of transactions of a customer last 6 months
  - count_day - Count of unique day transactions
  - count_day_3m - Count of unique day transactions last 3 months
  - count_day_6m - Count of unique day transactions last 6 months
  - count_month - Count of unique month transactions
  - count_month_3m - Count of unique month transactions last 3 months
  - count_month_6m - Count of unique month transactions last 6 months

## Cohort Analysis
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/ffb62019-902b-49a0-b091-7a3c61c1ccd0' width="700" height="300">

- There are no new customers after April 2007
- Customers have an extremely high retention rate 99%-100%

# Model Training
1. Prepare data
2. Train test split (70: 30)
3. Model training
4. Model evaluation

## Prepare data

### Standardize features

- Using StandardScaler
- Formular > z = (x - u) / s

### Handle imbalanced
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/a6248490-0158-46d0-9b7b-de92e6536f28' width="300" height="300">

- Target data are imbalanced 26.3% on the positive label
- Performed upsampling with SMOTE on the training dataset

## Model training
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/b14b3071-3ee8-4c1a-a46d-d3632a0463e7' width="600" height="300">

- Using pycaret to perform cross-validation
- The best model is **XGBoost** measured by F2 score = 0.991100
- Choosing the XGBoost model for classification

## Model evaluation

### Confusion matrix
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/7317ddb7-b50a-4c42-9f66-9733521da690' width="300" height="250">

### Evaluation Score: F2
- Inactive customers: 1
- Active customers: 1

### Feature Importance: XGBoost
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/d0bb23e5-9b2a-4639-ad28-ddcbf8ac5397' width="600" height="300">

- avg_spend is the highest important feature.

### Feature Importance: Random Forest
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/da6d1cb3-4085-41de-90cb-ff846fad3fd3' width="600" height="300">

- avg_spend is the highest important feature.
- Followed by avg_spend_6m, avg_sabal_month, avg_spend_3m and total_spend respectively.

### CHAP plot: Random Forest
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/21a49290-3d2b-41d9-904a-8a1d0fa3b305' width="400" height="450">

- The more value of avg_spend, total_spend and avg_sabal_month the more probability to churn

# Recommendations
- The F2 score is very high, It may be because the model is overfitted from the training data size is too small suggest collecting more data for better performance of the model
- After adding the training dataset the best performance model might be changed
- The transaction log date should start from 01/01/2017

