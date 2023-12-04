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
1. Explore dataset
2. Clean and prepare data
3. Model training
4. Model evaluation
5. Conclusion and recommendations


# Data Exploration & Preparation

![image](https://github.com/terjirapat/CreditCardChurning/assets/77285026/3364b9be-6348-4dc6-ae84-b52c682d63a6)

- Found null value on the 'demo' dataset
  - 23.30% of the total in column 'marital_status'
  - 12.93% of the total in column 'family_income_segment_code'
  - 6.06% of the total in column 'individual_income_segment_code'
  - Solution: replace null with 'unk' value

Credit card transaction log

Start date: 2017-01-26

End date: 2017-12-31

## Cohort Analysis
<img src='https://github.com/terjirapat/CreditCardChurning/assets/77285026/ffb62019-902b-49a0-b091-7a3c61c1ccd0' width="700" height="300">

# Model Training
1. Train test split (70: 30)
2. Model training
3. Scoring
4. Model evaluation

