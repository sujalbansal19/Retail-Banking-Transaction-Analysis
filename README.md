# Retail Banking Transaction Analysis — Python + Power BI

> **End-to-end Data Analytics & Business Intelligence portfolio project**  
> Python data preparation and analysis combined with a Power BI semantic model and executive dashboard.

## 1. Project Overview

This project analyses retail-banking data across **customers, accounts and high-volume transactions**.

The solution combines:

- Python for data understanding, cleaning and feature engineering
- Exploratory analysis for business-oriented investigation
- Power BI for semantic modelling, KPI development and interactive reporting
- GitHub for reproducible project presentation and portfolio documentation

The project contains four Power BI report experiences:

**Customer → Account → Transaction → Final Executive Dashboard**

---

## 2. Dataset Scale

The central transaction fact table has:

**2,377,169 rows × 8 columns**

### Transaction table

`account_transactions_cleaned`

| Column | Purpose |
|---|---|
| `transaction_id` | Transaction identifier |
| `account_id` | Associated bank account |
| `linked_transaction_id` | Optional linked transaction |
| `created_time` | Transaction timestamp |
| `transaction_type` | Credit / Debit |
| `transaction_code` | Transaction classification |
| `amount` | Transaction value |
| `channel` | Transaction channel |

### Supporting tables

| Table | Role | Supplied size |
|---|---|---:|
| `bank_accounts_cleaned` | Account / portfolio layer | 3,553 × 9 |
| `customer_profiles_cleaned` | Customer dimension | 1,000 × 7 |
| `customer_names_mapping` | Customer-name mapping | 1,000 × 2 |
| `transaction_codes_cleaned` | Transaction reference | 15 × 5 |
| `DateTable` | Power BI date dimension | Used for fiscal/calendar analysis |

---

## 3. Business Problem

Banking data is distributed across multiple business domains. A management user needs a unified view of:

- Customer relationships
- Customer value
- Account/product mix
- Savings and fixed-deposit balances
- Loan exposure
- Transaction volume
- Transaction value
- Transaction channels
- Transaction trends

The objective is to convert these operational datasets into an interactive business-intelligence solution.

---

## 4. Business Questions

### Customer

1. How many customers are in the portfolio?
2. Which age groups contain the largest customer base?
3. Which states and cities have the highest customer concentration?
4. Which customers have the highest net balance?
5. How is net balance distributed across customer segments?

### Account

1. How are accounts distributed by account type?
2. What is the account-status mix?
3. What are the Savings/CASA and Fixed Deposit/TD balances?
4. What is the loan-disbursement and outstanding-loan position?
5. How does loan amount vary by age group?
6. How does balance vary by account type?
7. How do interest rate and loan amount relate?
8. How are accounts distributed across interest-rate bands and loan terms?

### Transaction

1. What is the transaction count?
2. How is transaction value split between Credit and Debit?
3. Which channels contribute the most transaction value?
4. How does transaction volume change over time?
5. Which transaction codes generate the highest volume?
6. How does transaction value change by fiscal quarter?
7. How are transactions distributed across amount bands?
8. Which weekdays have the highest transaction volume?

---

## 5. Python Workflow

```text
Data Understanding
       ↓
Data Profiling
       ↓
Missing / Duplicate Checks
       ↓
Business Rule Validation
       ↓
Data Cleaning
       ↓
Feature Engineering
       ↓
Exploratory Analysis
       ↓
Power BI Semantic Model
       ↓
Dashboard & Business Insights
```

### Data preparation

The supplied notebooks cover:

- Shape and structure checks
- Data-type inspection
- Missing-value analysis
- Duplicate checks
- Date conversion
- Reference-value validation
- Negative-value checks
- Outlier investigation
- Skewness and percentile analysis

### Feature engineering

The project creates / uses analytical fields such as:

- Customer age
- Customer age group
- Customer-level net balance
- Transaction amount bands
- Date / Fiscal Year / Fiscal Quarter / Weekday

A key financial-data principle followed in the analysis is that **large transaction values should not automatically be deleted as outliers**. A large payment can be legitimate.

---

# 6. Power BI Dashboard

The Power BI dashboard is the main business-facing output of this project.

The supplied PBIX contains four pages:

1. **Customer**
2. **Account**
3. **Transaction**
4. **Final**

---

## 6.1 Customer Page

### Purpose

The Customer page focuses on customer segmentation, geography and relationship value.

### Visuals identified in the supplied PBIX

- **Count of Customers** — card
- Customer count by **Age Group** — column chart
- **Top 10 States** — clustered bar chart
- Top cities — clustered bar chart
- **Top 10 Customers** by net balance
- **Net Balance by Age Group** — pie chart
- Net Balance by State — clustered bar chart
- Total Net Balance — card
- Average Net Balance — card

### Business use

This page can be used to identify:

- Customer concentration
- High-value customer relationships
- Age-based portfolio composition
- Geographic concentration
- Net-balance concentration

---

## 6.2 Account Page

### Purpose

The Account page focuses on account mix, portfolio balances and credit exposure.

### KPI cards identified

- Savings Balance / CASA Balance
- FD Balance / TD Balance
- Outstanding Loan Amount
- Loan Amount / Loan Disbursements
- Net Balance
- Transaction-linked account count

### Visuals identified

- Account type distribution
- Account status distribution
- Loan amount by customer age group
- Balance by account type
- Loan amount vs interest rate
- Account count by interest-rate band
- Account count by term months

### Business use

This page provides a portfolio view of:

**Deposits + Account Mix + Credit Exposure + Interest Rate + Tenure**

---

## 6.3 Transaction Page

### Purpose

The Transaction page is the primary analytical layer for the **2,377,169-row transaction fact table**.

### Visuals identified

#### 1. Transaction Count

A card using:

`account_transactions_cleaned → transaction_id`

#### 2. Transaction Value by Credit / Debit

Donut chart using:

- `transaction_type`
- `amount`

#### 3. Transaction Value by Channel

Clustered column chart using:

- `channel`
- `amount`

#### 4. Transaction Count over Time

Line chart using:

- Date
- Transaction Count

#### 5. Transaction Volume by Transaction Code

Clustered bar chart using:

- `transaction_code`
- Transaction Count

#### 6. Quarter-Wise Trend of Transaction Amount

Column chart using:

- Fiscal Year
- Fiscal Quarter
- Sum of transaction amount

#### 7. Transaction Amount Distribution

Clustered bar chart using:

- `Transaction_Amt_Band`
- Transaction Count

#### 8. Transaction Volume by Weekday

Clustered bar chart using:

- Weekday
- Transaction Count

### Business use

The Transaction page separates **volume** from **value**, which is important in banking analytics.

For example:

> A channel can have high transaction volume without having the highest monetary value.

This page therefore supports behavioural, channel and transaction-value analysis.

---

# 7. Final Executive Dashboard

The Final page is the management-facing dashboard.

## KPI cards

The supplied PBIX contains these eight cards:

| KPI | PBIX source |
|---|---|
| **CUSTOMER COUNT** | `customer_profiles_cleaned` → Count of `customer_id` |
| **NO OF ACCOUNTS** | `account_transactions_cleaned` → Count of `account_id` |
| **NET BALANCE** | `bank_accounts_cleaned` → `net_balance_measure` |
| **TRANSACTION COUNT** | `account_transactions_cleaned` → Count of `transaction_id` |
| **CASA BALANCE** | `bank_accounts_cleaned` → `savings_balance` |
| **TD BALANCE** | `bank_accounts_cleaned` → `fd_balance` |
| **LOAN DISBURSEMENTS** | `bank_accounts_cleaned` → Sum of `loan_amount` |
| **OUTSTANDING LOANS** | `bank_accounts_cleaned` → `outstanding_loan_amt` |

## Interactive slicers

The Final dashboard contains slicers for:

- Channel
- Account Type
- Customer Name
- State / City
- Age Group
- Date
- Transaction Type

## Executive visuals

The page also contains:

- **Top 10 Customers**
- **Net Balance** by Age Group
- **Count of Accounts** by Account Status
- **Quarterly Transaction Value Trend**
- **Transaction Volume** by Amount Band
- State / City / Customer summary table

---

# 8. Important Power BI KPI Observation

There is one modelling point worth fixing before publishing this project as an industry-level portfolio.

The Final page's **"NO OF ACCOUNTS"** card is currently configured as:

```text
account_transactions_cleaned
        ↓
Count of account_id
```

This counts non-null `account_id` values in the transaction fact table.

It is **not equivalent to the number of distinct bank accounts**.

### Recommended industry-standard implementation

For a true account count, use:

```DAX
No of Accounts =
DISTINCTCOUNT(bank_accounts_cleaned[account_id])
```

Then, if the current transaction-level metric is useful, rename it something like:

```text
Transaction-Linked Account Records
```

This distinction is important because KPI names should accurately reflect their aggregation logic.

---

# 9. Dashboard-Led Insights

The following insights are based specifically on the Power BI dashboard structure:

### Customer insights

The dashboard treats customer value as more than customer count. It ranks the Top 10 Customers by net balance and analyses net balance across age groups and states.

### Account insights

The Account page combines account-type distribution with Savings, FD, Loan and Net Balance measures, allowing deposit and credit-side analysis in the same analytical layer.

### Transaction insights

The Transaction page separates:

**Transaction Volume**  
from  
**Transaction Value**

and analyses both across channel, transaction type, transaction code, amount band, weekday and fiscal quarter.

### Executive insight

The Final dashboard combines the three business domains into one management view:

**Customer + Account + Transaction**

with interactive filtering.

---

# 10. Data Governance Recommendations

Before publishing the project:

- Validate uniqueness of `transaction_id`.
- Validate account references.
- Validate transaction-code references.
- Validate permitted transaction types.
- Validate permitted channels.
- Validate date ranges.
- Validate monetary-value rules.
- Use explicit DAX measure names.
- Document the definition of Net Balance.
- Change the misleading "NO OF ACCOUNTS" KPI to a distinct account count.

---

# 11. Repository Structure

```text
Retail-Banking-Python-PowerBI/
│
├── README.md
│
├── dataset/
│   ├── account_transactions_cleaned.csv
│   ├── bank_accounts_cleaned.csv
│   ├── customer_profiles_cleaned.csv
│   ├── customer_names_mapping.csv
│   └── transaction_codes_cleaned.csv
│
├── python/
│   ├── 01_Cleaning.ipynb
│   └── 02_Analysis.ipynb
│
├── powerbi/
│   └── Retail_Banking_Analysis.pbix
│
├── documentation/
│   └── Project_Documentation.pdf
│
├── presentation/
│   └── Project_Presentation.pptx
│
└── screenshots/
    └── dashboard.png
```

---

# 12. Large Dataset Recommendation

The transaction table contains:

**2,377,169 records**

Therefore, for GitHub publication, consider:

- Git LFS
- GitHub Releases
- External dataset storage
- A documented sample dataset

Do not compromise the reproducibility of the project by silently excluding the main transaction fact table.

---

# 13. Technology Stack

| Technology | Purpose |
|---|---|
| Python | Data cleaning and analysis |
| Pandas | Data manipulation |
| NumPy | Numerical analysis |
| Matplotlib | Visualisation |
| Seaborn | Exploratory visualisation |
| Jupyter Notebook | Analytical workflow |
| Power BI | Data modelling and dashboard |
| DAX | KPI / measure logic |
| GitHub | Version control and portfolio presentation |

---

# 14. Portfolio Skills Demonstrated

**Data Analytics**

- Data Cleaning
- Data Validation
- Feature Engineering
- Exploratory Data Analysis
- Financial Data Analysis

**Business Intelligence**

- Data Modelling
- DAX Measures
- KPI Development
- Slicers
- Dashboard Design
- Executive Reporting

**Business Understanding**

- Customer Analytics
- Account Analytics
- Deposit Analysis
- Loan Analytics
- Transaction Analytics
- Channel Analysis
- Trend Analysis

---

# 15. Conclusion

This project demonstrates a complete analytics workflow:

**Python → Clean Data → Analysis → Power BI Model → KPI Layer → Executive Dashboard → Business Insights**

The high-volume transaction fact table, with **2.37 million records**, gives the project realistic scale.

The four Power BI pages provide distinct analytical purposes:

| Page | Business focus |
|---|---|
| Customer | Customer segmentation and relationship value |
| Account | Portfolio and credit analysis |
| Transaction | High-volume transaction behaviour |
| Final | Executive decision support |

The project is therefore suitable for demonstrating practical skills relevant to:

- Data Analyst
- Business Analyst
- BI Analyst
- Reporting / MIS Analyst
- Junior Business Intelligence roles

---

## Author

**Sujal Bansal**

Data Analytics | Python | SQL | Power BI | Business Intelligence
