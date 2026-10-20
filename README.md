# 🏦 Nivara Bank | Credit Risk & Customer Analytics (Power BI)

**A 3-page Power BI report on a fictional Indian bank's ₹252 Cr loan book.**

🏠 Home loans are **64% of the book but only 2.4% NPA**. 💳 Personal loans are **6% of the book but 11.8% NPA**. Gross NPA is **4.15% (₹10.5 Cr)**, and it rises sharply for borrowers with a **credit score below 600 (20.9% NPA, vs 1.0% at 750+)**.

🛠️ **Built with:** Power Query (M), DAX, 166,559 transactions (161K successful).

📄 [Full dashboard PDF](https://github.com/hruturajwork-sys/Nivara-Bank-Powerbi/blob/main/Nivara_Bank_Dashboard.pdf) | 💻 [Download the .pbix](https://github.com/hruturajwork-sys/Nivara-Bank-Powerbi/blob/main/Nivara_BankLTD_dashboard.pbix)

> ⚠️ **Data disclaimer:** Nivara Bank is fictional. All data is synthetic and used for learning and portfolio purposes. No real customer or bank data is used.

---

## 📊 Dashboard Preview

**Page 1: Overview**
![Overview](image%20of%20dashboard/page1.jpg)

<!-- After you upload page2.jpg and page3.jpg to "image of dashboard", remove the comment markers around the next two blocks.

**Page 2: Credit Risk**
![Credit risk](image%20of%20dashboard/page2.jpg)

**Page 3: Customers & Fraud**
![Customers and fraud](image%20of%20dashboard/page3.jpg)
-->

---

## 📌 About the Project

I built this project to practise the full analytics workflow: cleaning raw data, modelling relationships, writing DAX, and designing a dashboard that answers business questions.

The scenario is a fictional Indian bank that wants to understand its loan portfolio, find credit risk, monitor transaction fraud and improve customer service. The goal was not just to display KPIs, but to find patterns a banking team could act on.

| | Details |
|---|---|
| 🏦 Industry | Retail and SME banking |
| 🛠️ Tools | Power BI, Power Query (M), DAX |
| 📂 Data | Customer, account, loan, transaction, branch and complaint records (synthetic) |
| 🗂️ Data source | Synthetic dataset generated using Claude for learning and portfolio purposes. All entities, including Nivara Bank, are fictional. | 
| 📈 Output | Three-page interactive dashboard |
| 🎯 Focus | Credit risk, customer analytics, fraud, service quality |

---

## ❓ Business Questions

| Area | Question |
|---|---|
| 📈 Lending | How is the loan book distributed across products? |
| ⚠️ Credit risk | What is the Gross NPA rate, and which products contribute most? |
| ⏳ Early warning | How much outstanding exposure is already overdue? |
| 💳 Borrower analysis | How do credit score and EMI burden relate to NPA? |
| 🏢 Branch performance | Which branches and regions have relatively high NPA? |
| 👥 Customer analytics | Which customer segments contribute the most estimated value? |
| 🔄 Retention | Which customers may be becoming dormant or leaving? |
| 💡 Cross-selling | Where could product penetration improve? |
| 🔐 Fraud | Which channels and time periods have higher fraud rates? |
| 🎧 Service quality | Are complaints resolved within the defined SLA? |

---

## 🔎 Key Findings

| Area | Finding |
|---|---|
| 🏠 Loan portfolio | ₹252 Cr live loan book |
| 🏦 Deposits | **₹331 Cr** across open accounts |
| 👥 Active customers | **4,869** of 5,000 |
| ⚠️ Gross NPA | **4.15% (₹10.5 Cr)** |
| 🏠 Home vs personal loans | Home loans are **64% of the book but only 2.4% NPA**. Personal loans are **6% of the book but 11.8% NPA** |
| 📉 Credit score | **20.9% NPA** below a score of 600, vs **1.0%** at 750+ |
| 💰 EMI burden | **8.2% NPA** when EMI is more than 50% of income |
| ⏳ Overdue exposure | **₹14.5 Cr** in the 31 to 90 days-past-due bucket |
| 💸 Channel mix | UPI carries **39% of transactions**, but NEFT/RTGS carries **54% of the money** |
| 🔐 Fraud | **35 cases per 10,000** debit transactions, **₹91 L** fraud loss in the last 12 months |
| 🎧 Complaints | **37%** of resolved complaints missed the SLA |

*These figures describe the synthetic dataset, not real banking performance. The patterns are associations, not proof of cause.*

---

## 💡 Recommendations

Each recommendation is a starting point for investigation, not a validated policy.

1. 💳 **Credit risk:** Personal loans carry the highest NPA (11.8%). Review approval rules for borrowers with a credit score below 600 (20.9% NPA) or an EMI above 50% of income (8.2% NPA).
2. ⏳ **Collections:** ₹14.5 Cr sits in the 31 to 90 DPD bucket. Prioritise these accounts for follow-up before they roll into NPA.
3. 🔐 **Fraud monitoring:** Fraud runs at 35 cases per 10,000 debit transactions. Investigate the channels, overnight periods and high-value digital transactions with the highest rates.
4. 💸 **Channel strategy:** NEFT/RTGS carries 54% of the money from a small share of transactions. Monitor large-value transfers closely, and grow low-cost digital channels for everyday payments.
5. 👥 **Retention and cross-sell:** Study dormancy patterns, then target suitable customer segments with relevant products.
6. 🎧 **Service quality:** 37% of resolved complaints missed the SLA. Review SLA breaches by complaint category and branch to find the biggest process gaps.

---

## 🧹 Data Cleaning & Preparation

I used Power Query to fix data quality issues before building the report.

| Issue | Treatment |
|---|---|
| Duplicate customer records | Removed using the customer identifier |
| Inconsistent category labels | Standardised gender and other categories |
| Inconsistent city names | Trimmed spaces and standardised casing |
| Invalid ages | Replaced with the occupation-level median age |
| Missing income | Filled with the occupation-level median |
| Missing credit scores | Kept as a separate "No score" category |
| Duplicate transaction IDs | Removed |
| Missing merchant categories | Labelled "Unknown" |
| Missing interest rates | Filled with the product-level median |

🔑 **One modelling decision:** missing credit scores were kept as their own category instead of being imputed. A missing score can carry meaning (no credit history), so it should not automatically be treated as an error.

---

## 🧮 DAX Highlights

**1. Gross NPA percentage**

```DAX
Gross NPA % = DIVIDE ( [Npa Cr], [Loan Book Cr] )
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

- Gross NPA is measured on outstanding amounts, not on loan counts.
- Fraud is normalised by debit transaction volume, so channels with different volumes can be compared fairly.
- Missing credit scores stay as a separate category.
- Colours show whether a value is above or below the bank-level reference rate.

---

## 🚀 Skills Demonstrated

- 🧹 **Data cleaning:** duplicates, missing values and inconsistent categories in Power Query.
- 🧱 **Data modelling:** related fact and dimension tables.
- 🧮 **DAX:** banking KPIs (NPA, fraud rate) and conditional formatting.
- 📊 **Dashboard design:** a three-page report built around business questions.
- 🏦 **Banking analytics:** NPA, overdue exposure, fraud and customer behaviour.
- 💼 **Business thinking:** turning findings into recommendations.

---

## ⚠️ Limitations

- The dataset is synthetic and may not reflect real banking behaviour.
- The report is a snapshot dated 30 September 2026. It does not show NPA trends over time.
- Branch-level rates should be read alongside portfolio size.
- Median imputation for income and age can understate real variation.
- Customer value is an estimate based on simplified assumptions, not a full profitability model.

## 🔭 What I Would Improve Next

- Monthly NPA movement and roll-rate analysis.
- Provision coverage ratio and cost-to-income ratio.
- SQL-based data preparation before Power BI.
- Customer profitability analysis.
- Automated data refresh.

---

## 📁 Repository Contents

| File / Folder | What it is |
|---|---|
| `Nivara_BankLTD_dashboard.pbix` | The interactive Power BI report |
| `Nivara_BankLTD.pbit` | Power BI template (model and queries, no data) |
| `Nivara_Bank_Dashboard.pdf` | 3-page PDF export of the dashboard |
| `data/` | Synthetic source data files |
| `image of dashboard/` | Dashboard screenshots used in this README |

---

## ▶️ How to Explore the Project

1. 📄 Open the [full dashboard PDF](https://github.com/hruturajwork-sys/Nivara-Bank-Powerbi/blob/main/Nivara_Bank_Dashboard.pdf) to see all three pages.
2. 💻 Download the [`.pbix` file](https://github.com/hruturajwork-sys/Nivara-Bank-Powerbi/blob/main/Nivara_BankLTD_dashboard.pbix) from this repository.
3. 🔍 Open it in Power BI Desktop to explore the interactive report.

---

## 👤 About Me

**Hruturaj Sansare**
Aspiring Data Analyst | Banking & Finance Analytics

I build practical data skills with Python, SQL, Excel and Power BI, applied to business problems in banking and financial services.

🔗 [LinkedIn](https://www.linkedin.com/in/hruturaj-sansare-549b64350/) · 📧 [Email](mailto:Hruturajwork@gmail.com)
