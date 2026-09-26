# Financial Performance Analysis

An end-to-end sales and profit analysis of order data using **Excel, SQL, and Power BI**. The project cleans raw order data, answers business questions with SQL, and presents the results in an interactive Power BI dashboard.

![Dashboard Preview](Dash%20Bord%20Image.png)

---

## Table of Contents

- [Project Overview](#project-overview)
- [Business Questions](#business-questions)
- [Dataset](#dataset)
- [Tools Used](#tools-used)
- [Project Workflow](#project-workflow)
- [Repository Structure](#repository-structure)
- [SQL Analysis](#sql-analysis)
- [Dashboard](#dashboard)
- [Key Insights](#key-insights)
- [How to Run](#how-to-run)
- [Future Improvements](#future-improvements)
- [Author](#author)

---

## Project Overview

Businesses need to know where money is made and where it is lost. This project looks at order-level data to find out:

- Which regions, categories, and customer segments drive sales and profit
- Which products and customers matter most
- Which products lose money
- How shipping modes and discounts affect performance

The final output is a set of SQL queries plus a Power BI dashboard that a manager can use to make decisions.

## Business Questions

1. What are the total sales, profit, quantity, and average discount?
2. Which regions and states perform best and worst?
3. Which categories and sub-categories are the most profitable?
4. Who are the top 10 customers and products by sales and profit?
5. Which products are loss-making?
6. Which customer segment generates the most revenue and profit?
7. Which shipping mode performs best?
8. How can customers, regions, and segments be classified by sales performance?

## Dataset

| Item | Detail |
|---|---|
| File | `order_cleaned.csv` (also `EXCEL CLEANED FINAL.xlsx`) |
| Size | ~2.2 MB |
| Records | 10194  |
| Period | 03/01/2023 - 30/12/2026 |

**Key columns used in analysis:** `row_id`, `order_id`, `customer_name`, `segment`, `region`, `state`, `category`, `sub_category`, `product_name`, `ship_mode`, `sales`, `quantity`, `discount`, `profit`

> Add or remove columns to match your file.

## Tools Used

- **Excel**: data cleaning and formatting
- **SQL** ([MySQL / PostgreSQL]): analysis and business queries
- **Power BI**: interactive dashboard and visuals

## Project Workflow

1. **Data cleaning (Excel):** removed duplicates and blanks, fixed data types, standardised columns. Result: `EXCEL CLEANED FINAL.xlsx` and `order_cleaned.csv`
2. **Database loading (SQL):** loaded the cleaned CSV into an `orders` table and removed rows with a null `row_id`
3. **Analysis (SQL):** wrote queries from basic aggregations to advanced ones
4. **Visualisation (Power BI):** built the dashboard for sales, profit, region, category, and customer views

## Repository Structure

```
financial-performance-analysis/
├── Dash Bord Image.png                            # Dashboard screenshot
├── EXCEL CLEANED FINAL.xlsx                       # Cleaned Excel data
├── order_cleaned.csv                              # Cleaned data used for SQL
├── sql project query.sql                          # All SQL queries
├── financial performance analysis dashboard.pbix  # Power BI dashboard
└── README.md
```

## SQL Analysis

The SQL file is organised into these sections:

| Section | What it covers |
|---|---|
| Basic checks | Row count, total sales, profit, quantity, average discount, min/max sales |
| Sales analysis | Sales by region, state, category; top 10 customers and products |
| Profit analysis | Profit by region, state, category, sub-category; top 10 customers and products; loss-making products |
| Customer segment analysis | Sales, profit, orders, average sales/profit, quantity, and discount by segment |
| Region analysis | Same metrics by region |
| Category and sub-category analysis | Profit classification, rankings, top 5 sub-categories |
| Customer analysis | Top customers, ranking, Premium / Regular / Standard classification |
| Shipping analysis | Sales and profit by ship mode, average sales ranking |

**SQL concepts used:** `GROUP BY`, `HAVING`, `ORDER BY`, `LIMIT`, aggregate functions, `CASE WHEN`, window function `RANK() OVER()`, CTEs, and subqueries.

**Example: rank regions by total sales**

```sql
SELECT region,
       SUM(sales) AS total_sales,
       RANK() OVER (ORDER BY SUM(sales) DESC) AS sales_rank
FROM orders
GROUP BY region
ORDER BY sales_rank;
```

**Example: find loss-making products**

```sql
SELECT product_name,
       SUM(profit) AS total_profit
FROM orders
GROUP BY product_name
HAVING SUM(profit) < 0
ORDER BY total_profit ASC;
```

## Dashboard

The Power BI dashboard (`financial performance analysis dashboard.pbix`) includes:

- [KPI cards: $2.33M, $292.30K, 39K]
- [Sales and profit by region]
- [Category and sub-category performance]
- [Top customers and products]
- [Filters / slicers: add what you used]

> Open the `.pbix` file in Power BI Desktop to explore it.

## Key Insights

> Replace the placeholders with real numbers from your analysis.

- **Total sales:** $2.33M | **Total profit:** $292.30K
- **Top region by sales:** West, and by profit: $0.74M
- **Most profitable category:** Technology. **Weakest:** Furniture
- **Loss-making products:** 302 products lose money, so pricing and discounts need a review
- **Best customer segment:** Consumer Segment
- **Best shipping mode by sales:** Standard Class shipping mode

## How to Run

**SQL**
1. Create a table named `orders` in your database.
2. Import `order_cleaned.csv` into it.
3. Run the queries in `sql project query.sql` section by section.

**Power BI**
1. Install [Power BI Desktop](https://powerbi.microsoft.com/desktop/).
2. Open `financial performance analysis dashboard.pbix`.
3. If it asks for the data source, point it to `order_cleaned.csv`.

## Future Improvements

- Add time-based analysis (monthly and yearly sales trends)
- Add profit margin % and year-over-year growth
- Study the effect of discount on profit
- Add a Python notebook for EDA and forecasting
- Publish the dashboard online

## Author

**Pratyush Jalkote**
Data Analyst | B.E. in AI & Data Science

- GitHub: [Pratyush Jalkote](https://github.com/PratyushJalkote)
- LinkedIn: [LinkedIn](https://www.linkedin.com/in/pratyushj07/)
- Email: [pratyushjalkote@gmail.com]
