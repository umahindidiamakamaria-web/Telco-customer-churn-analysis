#  Telco Customer Churn Analysis — ABC Communications Ltd

## Project Overview
This project presents a Customer Churn Analysis for ABC Communications Ltd, a telecom company, using the Telco Customer Churn dataset. The analysis investigates why customers leave, which segments carry the highest churn risk, and what business actions can improve retention — covering contract structure, tenure, service usage, payment behavior, and demographics.

**Track:** Data Analytics Internship — Week 1 Business Analytics Case Study | AnalystLab Africa Consulting
**Prepared by:** Ndidiamaka Umahi
**Tools Used:** Microsoft Excel | Power Query | PivotTables | Dashboard Design | Microsoft Word | Microsoft PowerPoint

## Files in This Repository
| File | Description |
|---|---|
| `WA_Fn-UseC_-Telco-Customer-Churn.xlsx` | Raw dataset — 7,043 customer records |
| `telco_churn_dashboard.xlsx` | Cleaned data, pivot tables, and interactive dashboard |
| `DASHBOARD.png` | Screenshot of the final dashboard |
| `ABC_Communications_Churn_Analysis_Report.pdf` | Full Business Analytics Report (Understanding, Inspection, Analysis, Insights, Recommendations) |
| `ABC_Communications_Dataset_Inspection_Report.pdf` | Standalone Dataset Inspection Report |
| `ABC_Communications_Churn_Presentation.pptx` | Business Presentation slide deck |

## Dataset Description
| Column | Description |
|---|---|
| `customerID` | Unique customer identifier |
| `gender`, `SeniorCitizen`, `Partner`, `Dependents` | Customer demographics |
| `tenure` | Number of months customer has stayed with the company |
| `Contract` | Month-to-month, One year, or Two year |
| `PaymentMethod` | How the customer pays their bill |
| `MonthlyCharges`, `TotalCharges` | Billing amounts |
| `PhoneService`, `InternetService`, `OnlineSecurity`, `OnlineBackup`, `DeviceProtection`, `TechSupport`, `StreamingTV`, `StreamingMovies` | Subscribed services |
| `Churn` | Whether the customer left (Yes/No) — target variable |

##  Data Cleaning Steps (Power Query)
- Converted `TotalCharges` from text to Decimal Number
- Identified 11 blank `TotalCharges` rows, all belonging to customers with `tenure = 0`; filled with 0 as the logically correct value (MonthlyCharges × 0 tenure), not an average or dropped row
- Converted `SeniorCitizen` from 0/1 to Yes/No for consistency with other binary fields
- Verified 0 duplicate rows and confirmed all other column types matched expected format
- Added **Tenure Group** column — bucketed into 0-12, 13-24, 25-48, 49-60, 61-72 month ranges
- Added **Churn Flag** column — numeric 1/0 version of Churn, enabling churn-rate averaging in pivots
- Added **Service Count** column — count of add-on services (0-6) per customer
- Added **Avg Monthly Spend** column — TotalCharges ÷ tenure, guarded against divide-by-zero for new customers
- Added **CLTV Estimate** column — MonthlyCharges × tenure, an estimated customer lifetime value

## Business Questions & Key Findings

### Q1 — What Does the Customer Base Look Like?
| Metric | Value |
|---|---|
| Total Customers | 7,043 |
| Gender Split | 50% Female / 50% Male |
| Contract Split | 55% Month-to-month / 21% One year / 24% Two year |
| Average Tenure | 32.4 months |
| Average Monthly Charges | $64.76 |
> Gender is evenly split and not a differentiating factor, but the customer base is heavily weighted toward month-to-month contracts — the exact segment that proves to carry the highest churn risk.

### Q2 — Which Segments Have the Highest Churn?
| Segment | Churn Rate |
|---|---|
| Senior Citizens | 41.7% |
| Non-Senior Citizens | 23.6% |
| No Partner | 33.0% |
| Has Partner | 19.7% |
| No Dependents | 31.3% |
| Has Dependents | 15.5% |
> Customers with fewer household ties — no partner, no dependents, and particularly senior citizens — show markedly higher churn. Gender shows almost no relationship (26.9% vs 26.2%).

### Q3 — Does Contract Type Influence Retention?
| Contract Type | Churn Rate |
|---|---|
| Month-to-month | 42.7% |
| One year | 11.3% |
| Two year | 2.8% |
> The single strongest churn driver in the dataset — a ~15x gap between month-to-month and two-year contracts.

### Q4 — Does Tenure Affect Loyalty?
| Tenure Group | Churn Rate |
|---|---|
| 0-12 months | 47.4% |
| 13-24 months | 28.7% |
| 25-48 months | 20.4% |
| 49-60 months | 14.4% |
| 61-72 months | 6.6% |
> Churn declines steadily and consistently with tenure. The customer base itself is bimodal — a large cluster of new customers and a second cluster of long-term loyalists, with fewer in between.

### Q5 — Which Services Influence Churn?
| Service Factor | Churn Rate |
|---|---|
| Fiber Optic Internet | 41.9% |
| DSL Internet | 19.0% |
| No Online Security | 41.8% |
| Has Online Security | 14.6% |
> Fiber optic customers churn more than double DSL customers despite being the premium tier. Churn peaks among customers with exactly 1 add-on service (45.8%) — higher than customers with none (21.4%) — before dropping steadily as service count rises to 6 (5.3%).

### Q6 — Which Payment Methods Have Higher Churn?
| Payment Method | Churn Rate |
|---|---|
| Electronic Check | 45.3% |
| Mailed Check | 19.1% |
| Bank Transfer (Automatic) | 16.7% |
| Credit Card (Automatic) | 15.2% |
> Electronic check users churn nearly 3x more than automatic payment methods — and it's the largest payment segment in the base (2,365 customers).

### Cross-Factor Analysis — Correlation & Spend
| Variable | Correlation with Churn |
|---|---|
| Tenure | -0.35 |
| Monthly Charges | +0.19 |
| Total Charges | -0.20 |
| Service Count | -0.09 |
> Tenure is the strongest linear predictor of churn. Churned customers also show a higher median monthly spend, reinforcing the fiber optic and premium-pricing churn pattern.

## 📊 Dashboard Features

- **6 KPI Cards** — Total Customers, Churn Rate, Total Revenue (CLTV), Retained Customers, Avg Monthly Charges, Average Tenure
- **9 Interactive Charts:**
  - Churn Rate by Contract Type (Bar Chart)
  - Churn Rate by Tenure Group (Bar Chart)
  - Churn Rate by Payment Method (Bar Chart)
  - Customer Base by Gender (Donut Chart)
  - Customer Base by Contract Type (Donut Chart)
  - Distribution of Customer Tenure (Histogram)
  - Distribution of Monthly Charges (Histogram)
  - Monthly Charges Distribution by Churn Status (Box Plot)
  - Correlation Heatmap — Key Metrics
- **3 Dynamic Slicers** — Contract, Internet Service, Payment Method
- **Colour Theme** — Teal `#1A6B6B` and Navy Blue accents

## Recommendations

1. **Incentivize contract upgrades** — offer discounts or free add-ons to convert month-to-month customers (55% of the base) to annual contracts
2. **Launch a first-year retention program** — proactive check-ins at 30/90/180 days to address the 47.4% first-year churn spike
3. **Investigate electronic check churn** — determine whether it's a billing friction issue or a customer profile issue, and incentivize migration to autopay
4. **Review the fiber optic customer experience** — survey premium-tier customers to identify the root cause of their elevated churn
5. **Bundle add-on services** — restructure single-service upsells into 2-3 service packages to avoid the "partial adoption" churn spike

## Key Takeaways

- Overall churn rate stands at **26.5%**, with **73.5%** of customers retained
- Contract type is the **single strongest churn driver** — a ~15x gap between month-to-month and two-year holders
- **47.4%** of first-year customers churn — loyalty builds sharply after year one
- Electronic check payment is linked to **45.3%** churn, nearly 3x automatic payment methods
- Total estimated customer lifetime value across the base: **$16,055,091**
