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
AgeGroup = SWITCH(
    TRUE(),
        'customer'[Customer_Age] < 30, "20-30",
        'customer'[Customer_Age] >= 30 && 'customer'[Customer_Age] < 40, "30-40",
        'customer'[Customer_Age] >= 40 && 'customer'[Customer_Age] < 50, "40-50",
        'customer'[Customer_Age] >= 50 && 'customer'[Customer_Age] < 60, "50-60",
        'customer'[Customer_Age]>=60,"60+",
        "unknown"
)


IncomeGroup = SWITCH(
    TRUE(),
        'customer'[Income]< 35000, "Low",
        'customer'[Income] >= 35000 && 'customer'[Income]< 70000, "Med",
        'customer'[Income] >= 70000, "High",
        "unknown"
)


```

## Import CSV files into SQL:
here we need to import data from CSV file 

# DAX Queries
