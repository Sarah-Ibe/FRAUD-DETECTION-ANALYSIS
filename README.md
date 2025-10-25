# FRAUD-DETECTION-ANALYSIS


<img width="1178" height="653" alt="Fraud2" src="https://github.com/user-attachments/assets/2014f465-750c-49b6-8b37-5fabaaa87dc2" />
![User details](https://github.com/user-attachments/assets/8a67ed48-628c-4890-93a8-9df594c5dbd6)


This dashboard provides a comprehensive overview of fraudulent activity across financial transactions. It combines real-time metrics, behavioral patterns, and user-level drilldowns to help analysts detect, monitor, and respond to fraud with precision.
# Data Source
https://www.kaggle.com/datasets/ranjitmandal/fraud-detection-dataset-csv

# Data Cleaning & Preparation
Before building any visuals or writing DAX, I performed a thorough data cleaning process to ensure accuracy and consistency:
# Steps Taken:

# Handled Missing Values:
For numerical columns (e.g. Transaction_Amount, Account_Age), I filled missing values using the mean.
For categorical columns (e.g. Device, Location, Payment_Method), I used the mode to fill blanks.

# Removed Duplicates:
Identified and dropped duplicate rows to prevent skewed metrics.

#Corrected Data Types:
Converted Time_of_Transaction to proper datetime format.
Ensured that Fraudulent was treated as a binary flag (0 or 1).
Verified that Transaction_Amount was numeric and properly scaled.

# Validated Column Consistency:
Checked for outliers in transaction amounts and account ages.
Ensured all user IDs were unique and consistently formatted.
This cleaning process ensured that all downstream calculations, especially fraud rates and behavioral flags, were based on reliable data.

# Key Metrics & DAX Measures
Each KPI card is powered by a custom DAX measure designed to surface critical fraud indicators. Below are the core metrics and their logic:

| Metric | DAX Logic | Purpose |
| :------ | :---------- | :----: |
| Total Transactions | COUNTROWS('Fraud Detection Dataset') | Total number of transactions |
| Total Transaction Amount |COALESCE(SUM('Fraud Detection Dataset'[Transaction_Amount]), 0) | Sum of all transaction values |
| Average Transaction Amount | AVERAGE('Fraud Detection Dataset'[Transaction_Amount]Another description. | Mean value of all transactions |
| Total Fraudulent Transactions | COALESCE(CALCULATE(COUNTROWS('Fraud Detection Dataset'), 'Fraudulent' = 1), 0) | Count of transactions flagged as fraud |
| Total Fraudulent Transaction Amount | COALESCE(CALCULATE(SUM('Transaction_Amount'), 'Fraudulent' = 1), 0) | Total value of fraudulent transactions |
| Average Fraudulent Transaction Amount | DIVIDE([TotalFraudulentTransactionAmount], [TotalFraudulentTransactions], 0) | Mean value of fraudulent transactions |
| Fraudulent Transaction Rate |DIVIDE([TotalFraudulentTransactions], [Total Transactions], 0)) | % of transactions that are fraudulent |
| Fraudulent Amount Rate | DIVIDE([TotalFraudulentTransactionAmount], [TotalTransactionAmount], 0) |% of transaction value lost to fraud |
| Total Gain (Non-Fraud)| [TotalTransactionAmount] - [TotalFraudulentTransactionAmount] | Value of legitimate transactions |
| Fraud Count This Hour| CALCULATE(COUNTROWS('Fraud Detection Dataset'), 'Fraudulent' = 1, HOUR('Time_of_Transaction') = HOUR(NOW()))) | Number of frauds in the current hour |
| Fraud Count Previous Hour| CALCULATE(COUNTROWS('Fraud Detection Dataset'),'Fraud Detection Dataset'[Fraudulent] = 1,'Fraud Detection Dataset'[Time_of_Transaction] = HOUR(NOW()) - 1) | Number of frauds in the previous hour |
| Hour-over-Hour Change| DIVIDE([FraudCountThisHour] - [FraudCountPreviousHour], [FraudCountPreviousHour], 0) | % change in fraud count compared to previous hour |

# Visual Components
# Fraud Overview Panel
A set of KPI cards displaying:
Total transactions and amounts
Fraud counts and rates
Hourly fraud activity vs goal
Financial impact of fraud

# Fraudulent Transaction Amount Over Time
Line chart showing how fraudulent transaction values trend hourly
Helps detect spikes or seasonal patterns.

# Fraudulent Transaction Count by User
Bar chart ranking users by the number of transactions and frauds.
Useful for identifying repeat offenders or suspicious profiles.

# Fraudulent Transaction Count by Payment Method
Pie chart showing fraud distribution across:
UPI (24.38%)
Credit Card (22.87%)
Debit Card (22.79%)
Net Banking (27.05%)
Invalid Method (2.91%)
Reveals which payment channels are most vulnerable.

# User details report
Shows granular details about specific users, including devices, location etc

# Behavioral Insights
Complex Behavior Isn’t Always Fraud
Some users with no fraudulent activity still transacted across multiple locations and devices. This highlights the need for contextual analysis — not all anomalies are malicious.

# Key Patterns Identified
High-risk users often show:
High transaction volume in short timeframes
Device switching
Geographic inconsistency
Fraud spikes occur at specific hours, making hourly monitoring essential.
Net Banking-based methods are more prone to fraud than direct debit or credit banking

The Hourly Fraud Count represents the number of fraudulent transactions detected within the current hour. It’s a real-time metric that helps you monitor spikes or patterns in fraudulent activity as they happen.
# Why It Matters:
It shows how active fraud is right now, not just historically.
You can compare it against a goal or threshold to see if fraud is increasing or decreasing.
It’s useful for alerting, response planning, and resource allocation, especially in high-risk time windows.

# What This Dashboard Enables
Real-time fraud monitoring
Behavioral pattern recognition
Financial impact analysis
User-level investigation
Strategic fraud prevention

# Acknowledgments
Inspired by the clean design principles of Emeka Nweke, this dashboard balances clarity with depth — making complex fraud data intuitive and actionable.


