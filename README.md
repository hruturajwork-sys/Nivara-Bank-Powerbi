# 🏦 Nivara Bank | Retail & SME Analytics

**Turning banking data into insights on credit risk, customer behaviour, fraud, and operational performance.**

![Power BI](https://img.shields.io/badge/Power_BI-Dashboard-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Measures-0F766E?style=for-the-badge)
![Power Query](https://img.shields.io/badge/Power_Query-Data_Cleaning-134E4A?style=for-the-badge)
![Data](https://img.shields.io/badge/Dataset-Synthetic-64748B?style=for-the-badge)

---

## 📊 Dashboard at a glance

![Nivara Bank Overview Dashboard](image%20of%20dashboard/page1.jpg)

> 💡 **The business problem:** How can a bank monitor loan quality, identify potential risk, understand customer behaviour, and improve operational performance using its data?

I built this Power BI project around that question. The report brings together lending, transactions, customer information, and complaints to explore the areas a banking analytics team might investigate before making business decisions.

📄 **[View / Download the Full Dashboard PDF](Nivara_Bank_Dashboard.pdf)**

⚠️ **Data disclaimer:** Nivara Bank is fictional. All data is synthetic and used only for learning and portfolio purposes.

---

## 📌 Project snapshot

| | |
|---|---|
| 🏦 Industry | Retail and SME Banking |
| 🎯 Focus | Credit Risk, Customer Analytics, Fraud & Service Quality |
| 🛠️ Tools | Power BI, Power Query (M), DAX |
| 📂 Data model | Customer, account, loan, transaction, branch, complaint and date tables |
| 📈 Deliverable | Three-page interactive dashboard |
| 🔍 Approach | Data cleaning → Data modelling → KPI development → Analysis → Recommendations |

## 🖥️ Explore the dashboard

### 01 — 📈 Banking Overview

![Banking Overview](image%20of%20dashboard/page1.jpg)

A high-level view of the loan portfolio and banking activity, designed to help users identify the areas that need a closer look.

**Questions explored**
- How is the loan book distributed across products?
- What is the overall Gross NPA rate?
- How does transaction activity vary across channels and time?

### 02 — 🛡️ Credit Risk Analysis

![Credit Risk](image%20of%20dashboard/page2.jpg)

This page focuses on loan quality and the factors associated with higher reported NPA rates in the synthetic dataset.

**Questions explored**
- Which loan products contribute disproportionately to NPA?
- How do credit score and EMI burden relate to loan performance?
- Which branches and regions need further investigation?
- How much exposure sits in overdue buckets?

### 03 — 👥 Customer Analytics & Fraud

![Customers and Fraud](image%20of%20dashboard/page3.jpg)

This page connects customer behaviour and transaction monitoring with operational service quality.

**Questions explored**
- Which customer segments contribute the most estimated value?
- Where might the bank have retention or cross-selling opportunities?
- Which transaction channels and time periods show higher fraud rates?
- Are complaints being resolved within the defined SLA?

---

## 🔎 Key findings

The following figures are reported from the synthetic dataset used in this project.

| 📍 Area | 📊 Finding | 💼 Why it matters |
|---|---|---|
| 🏠 Loan portfolio | Approximately ₹252 Cr in the reported live loan book | Helps establish portfolio concentration |
| ⚠️ Gross NPA | 4.15%, approximately ₹10.5 Cr | Provides a headline view of reported stressed assets |
| 💳 Personal loans | Reported NPA rate of approximately 11.8% | Highlights a product segment for deeper risk analysis |
| 📉 Credit score | Approximately 20.9% NPA below a score of 600, versus 1.0% at 750+ | Shows an association worth investigating in credit-risk analysis |
| 💰 EMI burden | Approximately 8.2% NPA when EMI exceeds 50% of income | Highlights the importance of assessing repayment affordability |
| ⏳ Early warning | Approximately ₹14.5 Cr in the 31–90 days-past-due bucket | Provides a starting point for collections prioritisation |
| 🔐 Fraud | Reported rate of 35 fraud cases per 10,000 debit transactions | Supports comparisons across channels with different transaction volumes |
| 🎧 Customer service | Approximately 37% of resolved complaints reportedly missed SLA | Identifies an operational performance issue to investigate |

*These are dataset-specific results, not actual bank performance figures. Associations do not establish causation.*

## 💡 Business recommendations

Based on the patterns observed, I identified five areas a banking team could investigate further:

1. **Credit risk:** Review higher-NPA loan products and assess borrower affordability alongside credit scores before changing lending policies.
2. **Collections:** Prioritise accounts showing early signs of delinquency and track whether overdue balances progress into more severe buckets.
3. **Fraud monitoring:** Investigate unusual overnight transactions and high-risk digital activity; validate whether additional controls would be effective.
4. **Customer growth:** Explore retention initiatives for customers showing dormancy signals and identify relevant cross-selling opportunities.
5. **Service quality:** Break down SLA breaches by complaint category and branch to identify where process improvements may have the greatest impact.

These are recommendations for further investigation, not validated interventions or live banking policies.

---

## 🧹 Data preparation & quality

Before building the visuals, I worked on common data quality issues that can distort reporting.

| Issue | Treatment |
|---|---|
| Duplicate customer records | Removed duplicates using the customer identifier |
| Inconsistent category labels | Standardised gender and other category values |
| Inconsistent city names | Trimmed spaces and standardised casing |
| Invalid age values | Replaced using occupation-level median age, where applicable |
| Missing income | Filled using occupation-level median values |
| Missing credit scores | Retained as a separate “No score” category |
| Duplicate transaction IDs | Removed duplicate records |
| Missing merchant categories | Labelled as “Unknown” |
| Missing interest rates | Filled using product-level median values |

🔑 **Important modelling decision:** I retained missing credit scores as a separate category rather than automatically imputing them. Missing information can have business meaning and should not always be treated as a data error.

## 🧱 Data model

The report uses related fact and dimension tables to organise the data for analysis.

| Table | Rows | Purpose |
|---|---:|---|
| `dim_customers` | 5,000 | Customer attributes and segmentation |
| `dim_accounts` | 6,742 | Account status and balances |
| `dim_branch` | 24 | Branch and regional attributes |
| `dim_complaints` | 1,800 | Complaint details and SLA tracking |
| `fact_loan` | 3,200 | Loan balances, status and days past due |
| `fact_transaction` | 166,559 | Transaction activity, channels and fraud flags |
| `dim_date` | 365 | Calendar-based reporting |

The model uses one-to-many relationships where appropriate, with a calendar table supporting date-based analysis.

## 🧮 DAX highlights

A few examples of the measures and conditional formatting logic used in the report:

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

### 🎨 Reporting decisions

- Gross NPA is measured using outstanding amounts rather than simply counting loans.
- Fraud rates are normalised by debit transaction volume to improve channel comparisons.
- Missing credit scores are retained as a separate category.
- Conditional colours help distinguish values above and below the bank-level reference rate.

---

## 🚀 What this project demonstrates

- 🧹 **Data preparation:** Cleaning inconsistent values, handling missing data and removing duplicates.
- 🧱 **Data modelling:** Working with related fact and dimension tables.
- 🧮 **DAX:** Creating measures for banking KPIs and conditional formatting.
- 📊 **Visualisation:** Organising a multi-page report around business questions.
- 🏦 **Banking analytics:** Analysing NPA, overdue exposure, transaction fraud and customer behaviour.
- 💼 **Business thinking:** Connecting findings with practical areas for further investigation.

## 🔭 What I would improve next

There are several areas I would like to develop further:

- Monthly NPA movement and roll-rate analysis.
- Provision coverage and cost-to-income metrics.
- SQL-based data preparation before Power BI.
- More detailed customer profitability analysis.
- Automated data refresh and reporting.

## ⚠️ Limitations

- The data is synthetic and may not reflect real banking distributions.
- The analysis uses a snapshot dated 30 September 2026 and does not establish NPA trends over time.
- Branch-level rates should be considered alongside portfolio size.
- Customer value is an estimate based on simplified assumptions rather than a full profitability model.

## ▶️ How to explore the project

1. 📄 Open the [dashboard PDF](Nivara_Bank_Dashboard.pdf) to review the three report pages.
2. 💻 Download the `.pbix` file from the repository and open it in Power BI Desktop.
3. 🔍 Explore the visuals, filters, and measures to understand the analysis.

## 👤 About me

**Hruturaj Sansare**  
Aspiring Data Analyst | Finance & Banking Analytics

I am building practical skills in data analysis, with a focus on applying Python, SQL, Excel and Power BI to business problems in banking and financial services.

🔗 [Connect with me on LinkedIn](https://www.linkedin.com/in/hruturaj-sansare-549b64350/) · [Email me](mailto:Hruturajwork@gmail.com)
