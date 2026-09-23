# E-Commerce Sales & Customer Analytics (Pandas)

A year of order data from a small e-commerce store selling beauty/personal-care products across
5 countries. I started with 5 raw CSV files and built this out into a full analysis: cleaning,
merging, 30 business questions, a KPI dashboard, and a set of insights I could actually defend
with numbers.

## The problem I was trying to answer

Given the raw order data, what's actually driving revenue — which products/categories, which
customers, which months — and how healthy does the customer base look (are people coming back,
or is revenue riding on a few big spenders)?

## Data

| File | Rows | What's in it |
|---|---|---|
| `customers.csv` | 300 | customer_id, country, signup_date |
| `orders.csv` | 1,000 | order_id, customer_id, order_date, status |
| `order_items.csv` | 2,000 | order_id, product_id, quantity, price |
| `products.csv` | 50 | product_id, product_name, category |
| `sales_cleaned.csv` | 1,625 | pre-cleaned reference version, used at the end to sanity-check my results |

Column-by-column notes are in [`DATA_DICTIONARY.md`](DATA_DICTIONARY.md).

## How the tables connect

```
customers -> orders -> order_items <- products
```
One customer, many orders. One order, many line items. One product can show up in many line items.

## Scope note

Revenue/AOV/customer KPIs only count **Completed** orders. Cancelled and Returned orders are
tracked separately (order-status rates) but I didn't count them as sales — they aren't.

## Tools

Python, Pandas, NumPy, Matplotlib, Seaborn, Google Colab.

## What I checked before trusting the data

- No missing values anywhere across the 5 files.
- No fully duplicated rows. There are 33 repeated `order_id + product_id` combos in
  `order_items` — checked these and they're legit (same product ordered twice in one order),
  not junk to drop.
- Dates parsed cleanly with `pd.to_datetime(errors="coerce")`, nothing failed.
- No negative/zero prices or quantities.
- IDs (`customer_id`, `order_id`, `product_id`) are all unique, no orphaned foreign keys.
- After merging, row count matched `order_items` exactly (2,000 rows) — no accidental
  many-to-many blow-up.

## The 30 questions

All answered in the notebook, results also summarized in
[`30_question_results.csv`](30_question_results.csv). A few numbers that stood out:

- Total revenue (completed orders): **$311,111.00**
- Completed orders: **695**, AOV: **$447.64**
- Leading category: **Hair** (32.67% of revenue)
- Top product by revenue: **Product_16** ($9,732) — not the same product as the top seller by
  volume (**Product_45**, 154 units)
- Best revenue month: **Jan 2024** ($30,948); most orders: **Oct 2024** (70)
- Repeat purchase rate: **73.41%**
- Top 10 customers = **11.34%** of revenue

## KPI dashboard

Full table with definitions in [`KPI_summary.csv`](KPI_summary.csv):

| KPI | Value |
|---|---|
| Total Revenue | $311,111.00 |
| Completed Orders | 695 |
| Average Order Value | $447.64 |
| Active Customers | 267 |
| Repeat Purchase Rate | 73.41% |
| Top 10 Customer Revenue Share | 11.34% |
| Top 20% Customer Revenue Share | 42.31% |
| Completed / Cancelled / Returned Rate | 80.50% / 10.30% / 9.20% |

## What I found

Longer version with evidence and caveats in [`BUSINESS_INSIGHTS.md`](BUSINESS_INSIGHTS.md) — short version:

- Hair is the clear revenue leader among the 4 categories.
- The top seller by volume and the top earner by revenue are two different products — worth
  keeping those metrics separate.
- Monthly revenue bounces around rather than trending up or down.
- Repeat purchasing is strong and revenue isn't concentrated in a handful of customers.
- Italy leads on total revenue, Morocco on average order value — not the same country.

## Charts

In [`charts/`](charts/): monthly revenue, revenue by category, top 10 products, top 10 customers,
monthly order count, repeat vs one-time customers, and revenue by country.

## Folder layout

```
ecommerce-sales-pandas-analysis/
├── data/                 the 5 source CSVs
├── notebook/              the full analysis notebook
├── charts/                exported PNGs
├── KPI_summary.csv
├── 30_question_results.csv
├── dataset_overview.csv
├── category_analysis.csv
├── monthly_analysis.csv
├── country_analysis.csv
├── top_products_by_revenue.csv
├── top_products_by_quantity.csv
├── top_customers_by_revenue.csv
├── BUSINESS_INSIGHTS.md
├── DATA_DICTIONARY.md
├── requirements.txt
└── README.md
```

## Running it

Open `notebook/Ecommerce_Sales_Customer_Analytics_Final.ipynb` in Colab and run top to bottom.
It'll ask you to upload the 5 CSVs if they're not already sitting next to it.

## Validation

At the end, I recompute the completed-sales dataset from the 4 raw tables and compare it against
`sales_cleaned.csv` on row count, revenue, unique orders, and unique customers. All 4 checks pass
exactly — same numbers either way.

## Limitations

- One year of data, 5 countries — wouldn't extrapolate this to a different year or market without
  more data.
- No pricing history or marketing calendar, so I can say *what* happened (e.g. the January
  revenue spike) but not confidently say *why*.
- `order_items` doesn't have a clean single-column primary key — I treated `(order_id,
  product_id)` as the effective key.

## Conclusion

$311,111 in revenue across 695 completed orders, led by the Hair category, with a broad and
frequently-returning customer base (73.41% repeat rate) and revenue that isn't riding on a few
big spenders. Monthly performance moves around rather than trending, and revenue/AOV both differ
by country. Everything above checks out exactly against the provided reference file.
