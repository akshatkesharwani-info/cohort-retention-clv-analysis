# Cohort Retention and Customer Lifetime Value (CLV) Analysis

![Python](https://img.shields.io/badge/Python-3.10+-blue)
![Status](https://img.shields.io/badge/Status-Completed-brightgreen)
![Cost](https://img.shields.io/badge/Cost-Free%20(Google%20Colab)-orange)
![Data](https://img.shields.io/badge/Data-Real%20(Online%20Retail%20%2F%20Kaggle)-lightgrey)

Monthly cohort retention and cumulative revenue per customer, built on the real Online Retail transactions dataset.

## Table of Contents
1. [Problem Statement](#problem-statement)
2. [STAR Summary](#star-summary)
3. [Dataset](#dataset)
4. [What the Notebook Does](#what-the-notebook-does)
5. [Key Results (from the executed run)](#key-results-from-the-executed-run)
6. [Sample Output](#sample-output)
7. [Checks and Fallbacks](#checks-and-fallbacks)
8. [Limitations](#limitations)
9. [Tech Stack](#tech-stack)
10. [How to Run](#how-to-run)
11. [Files](#files)
12. [About Me](#about-me)

## Problem Statement
An online retailer wants to know how many customers come back after their first purchase, which signup months bring the most valuable customers, and how much of the revenue depends on a small group of buyers. This project builds a monthly cohort retention table and a cumulative CLV view to answer that.

## STAR Summary
- **Situation:** An online retail business had thousands of transactions but no view of whether customers returned after their first order.
- **Task:** Measure retention by signup month and estimate customer lifetime value so retention spend can be targeted.
- **Action:** Cleaned 541,909 transaction rows, assigned each customer to the month of their first purchase, built a retention heatmap and a cumulative revenue-per-customer table, and split customers into value segments (top 20%, middle 40%, bottom 40%).
- **Result:** Average retention is 20.6% at month 1 and stays between about 20% and 31% afterwards. The top 20% of customers (867 of 4,338) bring 74.6% of revenue and 34.4% of customers bought only once.

## Dataset
- **Source:** Online Retail dataset on Kaggle (`carrie1/ecommerce-data`), downloaded inside the notebook with `kagglehub`.
- **Size:** 541,909 rows before cleaning, 397,884 after cleaning, 4,338 customers.
- **Date range:** 2010-12-01 to 2011-12-09.
- **Total revenue (cleaned data):** 8,911,407.9 (the retailer sells in GBP).
- **Cleaning:** dropped rows without a CustomerID, rows with negative quantity (returns) and rows with zero price.

## What the Notebook Does
1. Loads the real Online Retail data (falls back to a sample with the same columns if the Kaggle download fails).
2. Cleans the data and creates a Revenue column.
3. Builds monthly cohorts (month of first purchase) and a cohort index (months since first purchase).
4. Draws the cohort retention heatmap and the average retention curve.
5. Builds cumulative revenue per customer by cohort (historical CLV) and a 3-month / 6-month CLV summary.
6. Splits customers into Top 20% / Middle 40% / Bottom 40% by revenue.
7. Prints key insights and saves charts and CSV files.

## Key Results (from the executed run)
| Metric | Value |
|---|---|
| Customers analysed | 4,338 |
| Average retention, month 1 / month 3 / month 6 | 20.6% / 23.2% / 24.4% |
| Average revenue per customer | 2,054.27 |
| Average orders per customer | 4.27 |
| Average order value | 419.17 |
| Top 20% customers' share of revenue | 74.6% (867 customers) |
| Middle 40% / Bottom 40% share of revenue | 20.4% / 5.0% |
| One-time customers | 1,493 (34.4%) |
| Best cohort by 3-month CLV | 2010-12 (1,566.01) |
| Weakest cohort by 3-month CLV | 2011-07 (632.36) |

The 2011-08 cohort had the second highest 3-month CLV (1,069.61) even though it was one of the smallest cohorts (169 customers).

## Sample Output
```
KEY INSIGHTS
--------------------------------------------------
1. Data used: Real Online Retail dataset (Kaggle)
2. Customers analysed: 4338 | Total revenue: 8911408.0
3. Average retention -> Month 1: 20.6 % | Month 3: 23.2 % | Month 6: 24.4 %
4. Biggest drop is between month 0 and month 1 (100% -> 20.6 %), so the first 30 days decide retention
5. Best cohort by 3 month CLV: 2010-12 | Weakest: 2011-07
6. Top 20% customers bring 74.6 % of revenue
7. One-time customers are 34.4 % of all customers
```

## Checks and Fallbacks
- Row counts are printed before and after cleaning (541,909 to 397,884) so the filtering is visible.
- Cohort sizes are printed next to the retention table so small cohorts are easy to spot.
- If the Kaggle download fails, the notebook switches to a generated sample with the same columns and prints which data source was used. The executed run used the real dataset.
- No LLM or paid API is used, so there is no cost or latency to track.

## Limitations
- The dataset starts in December 2010, so the 2010-12 cohort also contains customers who may have bought before the data begins. Its high CLV should be read with that in mind.
- The 2011-12 cohort has only 41 customers because the data ends on 9 December 2011.
- Month 12 retention comes from a single cohort (2010-12).
- CLV here is historical cumulative revenue, not a predictive model.

## Tech Stack
| Area | Tools |
|---|---|
| Language | Python |
| Data handling | pandas, numpy |
| Charts | matplotlib, seaborn |
| Data download | kagglehub |
| Environment | Google Colab |

## How to Run
1. Open `cohort_retention_clv.ipynb` in Google Colab.
2. Click Runtime > Run all.
3. The notebook installs its libraries in the first cell and downloads the dataset by itself.
4. Charts and CSV files are saved in the Colab file panel.

## Files
- `cohort_retention_clv.ipynb` (executed notebook with outputs)
- `requirements.txt`
- Generated by the notebook: `cohort_retention_heatmap.png`, `average_retention_curve.png`, `clv_by_cohort_heatmap.png`, `revenue_share_by_segment.png`, `cohort_retention_table.csv`, `clv_summary_by_cohort.csv`, `customer_level_data.csv`

## About Me
**Akshat Kesharwani** | Data Analyst and Data Scientist (fresher) | Sagar, Madhya Pradesh
- Portfolio: https://akshatkesharwani-info.github.io/
- GitHub: https://github.com/akshatkesharwani-info
- Email: akshatkesharwani12345@gmail.com
