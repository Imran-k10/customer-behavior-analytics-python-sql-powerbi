# 🛍️ Customer Behavior Analytics: Python, MySQL & Power BI

An end-to-end analytics project on 3,900 retail customer transactions: cleaned in **Python**, queried in **MySQL**, and presented in an interactive **Power BI** dashboard.

![Dashboard](./dashboard_screenshot.png)

---

## Overview

Retail teams want to know who their customers are, what they buy, and what drives spending. This project answers 10 business questions, such as:

- Do subscribers spend more than non-subscribers?
- Which products sell best in each category?
- Does shipping type or a discount change how much customers spend?
- Which age groups bring in the most revenue?

## Dataset

| | |
|---|---|
| File | `customer_shopping_behavior.csv` |
| Size | 3,900 rows × 18 columns |
| Customer | ID, age, gender, location |
| Purchase | item, category, amount (USD), size, color, season |
| Behavior | review rating, subscription status, shipping type, discount / promo code, previous purchases, payment method, purchase frequency |
| Data quality | 37 missing review ratings; no other missing values |

## Tools

| Tool | Used for |
|---|---|
| Python (pandas) | Loading, exploring and cleaning the data |
| SQLAlchemy + PyMySQL | Loading the cleaned table into MySQL |
| MySQL Server | 10 analysis queries (aggregations, subqueries, CTEs, `CASE`, window functions) |
| Power BI | Interactive dashboard and DAX measures |

## Steps

1. **Load and explore (Python):** read the CSV, checked structure, data types, summary statistics and missing values.
2. **Clean (Python):**
   - filled 37 missing review ratings with the median rating of each product category
   - standardised column names (lowercase, underscores)
   - dropped `promo_code_used`, which was identical to `discount_applied` in all 3,900 rows
3. **Feature engineering (Python):** created `age_group` (four quartile-based groups) and `purchase_frequency_days` (e.g. Weekly = 7, Quarterly = 90).
4. **Load into MySQL:** wrote the cleaned data to a `customer` table in the `customer_behavior` database.
5. **Analyse with SQL:** ran 10 business-question queries ([`customer_behavior_queries.sql`](./customer_behavior_queries.sql)).
6. **Visualise in Power BI:** built the dashboard below.

## Dashboard

[`customer_behavior_dashboard.pbix`](./customer_behavior_dashboard.pbix)

- **KPI cards:** number of customers, average purchase amount, average review rating
- **Charts:** customers by subscription status, revenue and customers by category, revenue and customers by age group
- **Slicers:** subscription status, gender, category, shipping type

## Results

**Overall:** 3,900 customers · **$233,081** total revenue · **$59.76** average purchase · **3.75** average review rating

- **Clothing leads revenue:** $104,264 (about 45%), ahead of Accessories ($74,200), Footwear ($36,093) and Outerwear ($18,524).
- **Subscribers don't spend more:** average spend is $59.49 for subscribers vs $59.87 for non-subscribers, even though subscribers are 27% of customers.
- **Repeat buyers aren't more likely to subscribe:** 27.5% of customers with 5+ previous purchases subscribe, vs 27.0% overall.
- **Men generate about 68% of revenue ($157,890 vs $75,191),** but only because they are 68% of customers. Average spend is nearly identical ($59.54 vs $60.25).
- **Shipping type barely matters:** Express averages $60.48 vs $58.46 for Standard.
- **Discounts don't stop big spenders:** 839 customers (50% of discounted purchases) used a discount and still spent above the average.
- **Most discounted products:** Hat (50.0%), Sneakers (49.7%), Coat (49.1%), Sweater (48.2%), Pants (47.4%).
- **Top-rated products:** Gloves (3.86), Sandals (3.84), Boots (3.82), Hat (3.80), Skirt (3.78). Ratings are tightly clustered.
- **Customer base is mature:** 80% are Loyal (over 10 previous purchases), 18% Returning, 2% New.
- **Revenue is spread evenly across ages,** from $55.8K to $62.1K per age group, with young adults (18–31) highest.

**Takeaways:** the subscription program isn't lifting spend and may need a stronger offer; Clothing is the revenue driver; and with a large loyal base, retention matters more than acquisition.

## How to Run

**Requirements:** Python 3.9+, MySQL Server, Power BI Desktop (Windows).

```bash
# 1. Clone and install
git clone https://github.com/Imran-k10/customer-behavior-analytics-python-sql-powerbi.git
cd customer-behavior-analytics-python-sql-powerbi
pip install -r requirements.txt
```

2. In MySQL, create the database: `CREATE DATABASE customer_behavior;`
3. Open `customer_behavior_analysis.ipynb` in Jupyter and run all cells. Enter your MySQL password when prompted (or set the `MYSQL_PASSWORD` environment variable). This cleans the data and creates the `customer` table.
4. Run `customer_behavior_queries.sql` in MySQL Workbench to reproduce the SQL results.
5. Open `customer_behavior_dashboard.pbix` in Power BI Desktop. The data is already embedded, so it opens without a database connection.

## Project Structure

```
├── README.md
├── customer_behavior_analysis.ipynb     # Python: load, EDA, clean, load to MySQL
├── customer_behavior_queries.sql        # 10 MySQL queries
├── customer_behavior_dashboard.pbix     # Power BI dashboard
├── customer_shopping_behavior.csv       # Dataset
├── dashboard_screenshot.png
└── requirements.txt
```

## Author

**Muhammed Imran K** · Data Analyst · [LinkedIn](https://www.linkedin.com/in/muhammedimrank/)
