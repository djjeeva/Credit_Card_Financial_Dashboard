# Credit_Card_Financial_Dashboard-Public

## Challenge:

The challenge was to develop a robust dashboard that could provide real-time insights into credit card transactions and customer profiles. The system needed to handle and process large volumes of data efficiently, ensure accurate reporting, and present information in a user-friendly manner. Key difficulties included integrating data from multiple sources, maintaining real-time updates, and deriving meaningful insights from complex metrics.

## Objectives:

- Create a Dynamic Dashboard: Develop a Power BI dashboard to visualize credit card transaction data and customer demographics in an interactive format.
- Enable Real-Time Data Processing: Implement features for real-time updates to ensure the dashboard reflects the most current information available.
- Generate Actionable Insights: Offer insights into customer spending patterns, revenue trends, and overall credit card performance to support strategic decision-making.
- Ensure Seamless Data Integration: Integrate data from various sources and maintain consistency across the dashboard.


## Data Sources
We are using an MSSQL database that  contains transaction and customer data.


## My work 

### 1. Data Preparation and Import

**Data Files:**
- `customer_data.csv`: Contains customer demographics (age and income).
- `crdite transactions.csv`: Includes transaction details (annual fees, amounts, and interest).
- `add_cust.csv`: This is for testing real-time updates.
- `add_trans.csv`: To verify real-time functionality.

**Database Schema Creation:**

## Create tables in SQL:
```sql
-- 1. Create a database 
CREATE DATABASE ccdb;

-- 2. Create cc_detail table

CREATE TABLE cc_detail (
    Client_Num INT,
    Card_Category VARCHAR(20),
    Annual_Fees INT,
    Activation_30_Days INT,
    Customer_Acq_Cost INT,
    Week_Start_Date DATE,
    Week_Num VARCHAR(20),
    Qtr VARCHAR(10),
    current_year INT,
    Credit_Limit DECIMAL(10,2),
    Total_Revolving_Bal INT,
    Total_Trans_Amt INT,
    Total_Trans_Ct INT,
    Avg_Utilization_Ratio DECIMAL(10,3),
    Use_Chip VARCHAR(10),
    Exp_Type VARCHAR(50),
    Interest_Earned DECIMAL(10,3),
    Delinquent_Acc VARCHAR(5)
);


-- 3. Create cc_detail table

CREATE TABLE cust_detail (
    Client_Num INT,
    Customer_Age INT,
    Gender VARCHAR(5),
    Dependent_Count INT,
    Education_Level VARCHAR(50),
    Marital_Status VARCHAR(20),
    State_cd VARCHAR(50),
    Zipcode VARCHAR(20),
    Car_Owner VARCHAR(5),
    House_Owner VARCHAR(5),
    Personal_Loan VARCHAR(5),
    Contact VARCHAR(50),
    Customer_Job VARCHAR(50),
    Income INT,
    Cust_Satisfaction_Score INT
);


```

## Import CSV files into SQL:
here we need to import data from CSV file 

# DAX Queries

```DAX
AgeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[customer_age] < 30, "20-30",
    'public cust_detail'[customer_age] >= 30 && 'public cust_detail'[customer_age] < 40, "30-40",
    'public cust_detail'[customer_age] >= 40 && 'public cust_detail'[customer_age] < 50, "40-50",
    'public cust_detail'[customer_age] >= 50 && 'public cust_detail'[customer_age] < 60, "50-60",
    'public cust_detail'[customer_age] >= 60, "60+",
    "unknown"
)
IncomeGroup = SWITCH(
    TRUE(),
    'public cust_detail'[income] < 35000, "Low",
    'public cust_detail'[income] >= 35000 && 'public cust_detail'[income] < 70000, "Med",
    'public cust_detail'[income] >= 70000, "High",
    "unknown"
)
week_num2 = WEEKNUM('public cc_detail'[week_start_date])
Revenue = 'public cc_detail'[annual_fees] + 'public cc_detail'[total_trans_amt] + 'public cc_detail'[interest_earned]
Current_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])
    )
)
Previous_week_Reveneue = CALCULATE(
    SUM('public cc_detail'[Revenue]),
    FILTER(
        ALL('public cc_detail'),
        'public cc_detail'[week_num2] = MAX('public cc_detail'[week_num2])-1
    )
)

```
#Project Insights

##Week over Week (WoW) Change
- Revenue increased by 28.8%
- Total Transaction Amount & Count increased by xx% & xx%
- Customer count increased by xx%

  ## Overview Year-to-Date (YTD)
- Overall revenue is 57M
- Total interest is 8M
- Total transaction amount is 46M
- Male customers are contributing more in revenue 31M, female 26M
- Blue & Silver credit cards are contributing to 93% of overall transactions
- TX, NY & CA are contributing to 68%
- Overall Activation rate is 57.5%
- Overall Delinquent rate is 6.06%

##  Analytics Report





## How to Run the Project

 - Clone the repository:
```
https://github.com/djjeeva/Credit_Card_Financial_Dashboard-Public.git
```
- Set up the MSSQL database and import the data using the provided SQL scripts.
- Open the Power BI dashboard file and connect it to the MSSQL database.
- To test the real-time functionality, add data to the cust_add.csv and cc_add.csv files  
- import them into the database. Refresh the Power BI dashboard to see the updates.

### Dashboard Link
If you're interested in exploring and interacting with the dashboard,[click here](https://app.powerbi.com/view?r=eyJrIjoiYTAyMWY5NzktNjAzZi00MjNiLTgwZWMtZDY5ZGM1ZWVlN2U2IiwidCI6Ijc1NWUxZmNkLWY3YzAtNDBmNi1iMWRhLTg5NjkyNDVkNjg1ZCJ9)

## Contact
For any questions or further information, please contact    [Jeevitha D J](http://jeevithadj1999@gmail.com#fragment)

