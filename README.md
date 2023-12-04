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

### Personal information of customers dataset





## Correlation plot
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/e6817eff-2cc5-473d-8b96-9c02d70640c4' width="700" height="700">

- Aggregate value and create a new dataframe to create a correlation plot for choosing low correlation features with target value out
- Decided to remove the feature
  - cus_dur - Customer duration
  - age - Customer age
  - card_count - Number of credit card of the customer
  - total_netinflow - Total net inflow of money in the customer's bank account

## Cohort Analysis
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/ffb62019-902b-49a0-b091-7a3c61c1ccd0' width="700" height="300">

- There are no new customers after April 2007
- Customers have an extremely high retention rate 99%-100%

## Customer Movement Analysis

<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/9fc7eda1-908c-422f-accb-3f2a91b62618' width="600" height="350">

# Model Training
1. Train test split (70: 30)
2. Model training
3. Scoring
4. Model evaluation

## Train test split
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/a6248490-0158-46d0-9b7b-de92e6536f28' width="300" height="300">
- Target data are imbalanced 26.3% on the positive label
- Split data the performed upsampling with SMOTE on the training dataset

## Model training

Model

## Model evaluation

### Confusion matrix
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/9baa8f73-e9d9-464e-9d13-8d27daccf227' width="300" height="250">

### Evaluation Score: F2
- Inactive customers: 0.9951
- Active customers: 0.9926

# Recommendations
- The F2 score is very high, It may be because the model is overfitted from the training data size is too small suggest collecting more data for better performance of the model
- The transaction log date should start from 01/01/2017

