# 🏦 Nivara Bank | Retail & SME Analytics

**Exploring credit risk, customer behaviour, fraud patterns, and banking performance with Power BI.**
---

## 📊 Dashboard Preview

![Nivara Bank Overview Dashboard](image%20of%20dashboard/page1.jpg)

📄 **[View or download the complete 3-page dashboard PDF](https://github.com/hruturajwork-sys/Nivara-Bank-Powerbi/blob/main/Nivara_Bank_Dashboard.pdf)**

The report covers three areas: banking performance, credit risk, and customer analytics & fraud. The PDF contains all three dashboard pages.

> ⚠️ **Data disclaimer:** Nivara Bank is fictional. All data is synthetic and intended for learning and portfolio purposes. No real customer or bank data is used.

---

## 📌 About the Project

I built this project to practise the full analytics workflow, from cleaning raw data and modelling relationships to creating a dashboard that answers business questions.

The scenario is a fictional Indian bank looking to understand its loan portfolio, investigate potential credit risk, monitor transaction fraud, and improve customer service.

I wanted to go beyond displaying KPIs and use the data to identify patterns that a banking team could investigate further.

| | Details |
|---|---|
| 🏦 Industry | Retail and SME Banking |
| 🛠️ Tools | Power BI, Power Query (M), DAX |
| 📂 Data | Customer, account, loan, transaction, branch and complaint records |
| 📈 Output | Three-page interactive dashboard |
| 🎯 Focus | Credit risk, customer analytics, fraud and service quality |

## ❓ Business Questions

| Area | Question |
|---|---|
| 📈 Lending | How is the loan book distributed across products? |
| ⚠️ Credit risk | What is the Gross NPA rate, and which products contribute most to it? |
| ⏳ Early warning | How much outstanding exposure is already overdue? |
| 💳 Borrower analysis | How do credit scores and EMI burden relate to NPA? |
| 🏢 Branch performance | Which branches and regions have relatively high NPA rates? |
| 👥 Customer analytics | Which customer segments contribute the most estimated value? |
| 🔄 Retention | Which customers may be becoming dormant or leaving? |
| 💡 Cross-selling | Where could product penetration improve? |
| 🔐 Fraud | Which channels and time periods show higher fraud rates? |
| 🎧 Service quality | Are complaints being resolved within the defined SLA? |

## 🔎 Key Findings

These figures are from the synthetic dataset used in the project.

| Area | Finding | Why it matters |
|---|---|---|
| 🏠 Loan portfolio | Approximately ₹252 Cr in the reported live loan book | Shows the scale and concentration of lending |
| ⚠️ Gross NPA | 4.15%, or approximately ₹10.5 Cr | Provides a headline measure of stressed assets |
| 💳 Personal loans | Reported NPA rate of approximately 11.8% | Highlights a product segment for further investigation |
| 📉 Credit score | Approximately 20.9% NPA below a score of 600, versus around 1.0% at 750+ | Shows an association worth investigating |
| 💰 EMI burden | Approximately 8.2% NPA when EMI exceeds 50% of income | Highlights repayment affordability as an area to examine |
| ⏳ Overdue exposure | Approximately ₹14.5 Cr in the 31–90 days-past-due bucket | Provides a starting point for collections review |
| 🔐 Fraud | Reported rate of 35 cases per 10,000 debit transactions | Helps compare channels with different transaction volumes |
| 🎧 Complaints | Approximately 37% of resolved complaints reportedly missed SLA | Highlights an operational issue to investigate |

*These figures describe the synthetic dataset, not actual banking performance. Observed associations do not establish causation.*

## 💡 Recommendations

Based on the patterns in the report, I identified five areas a banking team could investigate further.

1. **Credit risk:** Review higher-NPA loan products and borrower affordability before changing lending policies.
2. **Collections:** Prioritise accounts showing early signs of delinquency and monitor whether overdue balances progress into more severe buckets.
3. **Fraud monitoring:** Investigate unusual overnight and high-value digital transactions to assess whether additional monitoring is justified.
4. **Customer retention:** Explore dormancy patterns and identify relevant cross-selling opportunities for suitable customer segments.
5. **Service quality:** Review SLA breaches by complaint category and branch to identify where process improvements may have the greatest impact.

These are recommendations for further investigation, not validated interventions or live banking policies.

## 🧹 Data Cleaning & Preparation

I used Power Query to address data quality issues before building the report.

| Issue | Treatment |
|---|---|
| Duplicate customer records | Removed duplicates using the customer identifier |
| Inconsistent category labels | Standardised gender and other category values |
| Inconsistent city names | Trimmed spaces and standardised casing |
| Invalid ages | Replaced using occupation-level median age, where applicable |
| Missing income | Filled using occupation-level median values |
| Missing credit scores | Retained as a separate “No score” category |
| Duplicate transaction IDs | Removed duplicate records |
| Missing merchant categories | Labelled as “Unknown” |
| Missing interest rates | Filled using product-level median values |

🔑 **One modelling decision:** Missing credit scores were kept separate rather than automatically imputed. Missing information can carry meaning and should not always be treated as a data error.

## 🧱 Data Model

The report uses related fact and dimension tables to organise the data for analysis.

| Table | Rows | Purpose |
|---|---:|---|
| `dim_customers` | 5,000 | Customer profile, segment and credit score |
| `dim_accounts` | 6,742 | Account status and balances |
| `dim_branch` | 24 | Branch, city and region |
| `dim_complaints` | 1,800 | Complaint details and SLA tracking |
| `fact_loan` | 3,200 | Loans, outstanding amounts and days past due |
| `fact_transaction` | 166,559 | Transactions, channels and fraud flags |
| `dim_date` | 365 | Calendar-based reporting |

The model uses one-to-many relationships where appropriate. The date table supports date-based analysis.

## 🧮 DAX Highlights

Here are a few examples of the measures and conditional formatting logic used in the report.

**1. Gross NPA percentage**

```DAX
Gross NPA % =
DIVIDE ( [NPA Cr], [Loan Book Cr] )
```

**2. Fraud cases per 10,000 debit transactions**

```DAX
Fraud per 10K =
DIVIDE ( [Fraud Cases], [Debit Txns] ) * 10000
```

**3. Conditional risk colour**

```DAX
Risk Colour =
IF (
    [Gross NPA %] > [Bank GNPA %],
    "#FF6B6B",
    "#14B8A6"
)
```

### 🎨 Reporting Decisions

- Gross NPA is measured using outstanding amounts rather than simply counting loans.
- Fraud rates are normalised by debit transaction volume to make channel comparisons more meaningful.
- Missing credit scores are retained as a separate category.
- Conditional colours distinguish values above and below the bank-level reference rate.

## 🚀 Skills Demonstrated

- 🧹 **Data cleaning:** Handling duplicates, missing values and inconsistent categories.
- 🧱 **Data modelling:** Working with related fact and dimension tables.
- 🧮 **DAX:** Creating measures for banking KPIs and conditional formatting.
- 📊 **Dashboard design:** Organising a multi-page report around business questions.
- 🏦 **Banking analytics:** Analysing NPA, overdue exposure, fraud and customer behaviour.
- 💼 **Business thinking:** Connecting findings with recommendations for further investigation.

## 🔭 What I Would Improve Next

There are a few areas I would like to explore in a future version:

- Monthly NPA movement and roll-rate analysis.
- Provision coverage ratio and cost-to-income ratio.
- SQL-based data preparation before Power BI.
- More detailed customer profitability analysis.
- Automated data refresh and reporting.

## ⚠️ Limitations

- The dataset is synthetic and may not reflect real banking behaviour.
- The analysis uses a snapshot dated 30 September 2026 and does not establish NPA trends over time.
- Branch-level rates should be considered alongside portfolio size.
- Customer value is an estimate based on simplified assumptions rather than a full profitability model.

## ▶️ How to Explore the Project

1. 📄 Open the [full dashboard PDF](https://github.com/hruturajwork-sys/Nivara-Bank-Powerbi/blob/main/Nivara_Bank_Dashboard.pdf) to review all three pages.
2. 💻 Download the `.pbix` file from the repository.
3. 🔍 Open it in Power BI Desktop to explore the interactive report.

## 👤 About Me

**Hruturaj Sansare**  
Aspiring Data Analyst | Finance & Banking Analytics

I am building practical data analysis skills, with a focus on applying Python, SQL, Excel and Power BI to business problems in banking and financial services.

🔗 [Connect with me on LinkedIn](https://www.linkedin.com/in/hruturaj-sansare-549b64350/) · [Email me](mailto:Hruturajwork@gmail.com)
