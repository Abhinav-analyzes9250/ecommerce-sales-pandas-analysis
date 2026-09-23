# Data Dictionary

Notes on each file and column, mostly so I (or anyone else) can come back to this in six months
and still know what everything means.

## `customers.csv` — 300 rows

| Column | Type | Notes |
|---|---|---|
| `customer_id` | int | primary key |
| `country` | string | Spain, Italy, France, Morocco, or Germany |
| `signup_date` | date | when the account was created |

## `orders.csv` — 1,000 rows

| Column | Type | Notes |
|---|---|---|
| `order_id` | int | primary key |
| `customer_id` | int | -> `customers.customer_id` |
| `order_date` | date | when the order was placed |
| `status` | string | `Completed`, `Cancelled`, or `Returned` |

## `order_items.csv` — 2,000 rows

| Column | Type | Notes |
|---|---|---|
| `order_id` | int | -> `orders.order_id` (one order can have multiple line items) |
| `product_id` | int | -> `products.product_id` |
| `quantity` | int | units in this line item (1–5) |
| `price` | int | unit price for this line item (10–119) |

No single-column primary key here — I'm treating `(order_id, product_id)` as the effective key,
with 33 legitimate cases of the same product appearing twice in one order.

## `products.csv` — 50 rows

| Column | Type | Notes |
|---|---|---|
| `product_id` | int | primary key |
| `product_name` | string | display name |
| `category` | string | `Body`, `Skin`, `Hair`, or `Makeup` |

## `sales_cleaned.csv` — 1,625 rows

This is a pre-cleaned version of just the Completed-order line items, already merged and with
`Revenue`/`year`/`month` added. I only used it at the end, to check that my own pipeline (built
from the 4 raw tables above) lands on the exact same numbers.

## Fields I created during the analysis

| Field | How it's calculated |
|---|---|
| `Revenue` | `quantity * price` |
| `year`, `month`, `month_name`, `year_month` | pulled out of `order_date` |
| `AOV` | `Total Revenue / Completed Orders` |
| repeat customer | anyone with more than one completed `order_id` |
| repeat purchase rate | `repeat customers / active customers * 100` |
| revenue share % | `group revenue / total revenue * 100` (used for category, country) |

## How the tables relate

```
customers (1) --< orders (1) --< order_items (N) >-- (1) products
```

One customer -> many orders. One order -> many line items. One product can appear across many
line items.

## Scope

Revenue/AOV/customer KPIs use Completed orders only — Cancelled and Returned orders are real
rows in the data and get tracked in status metrics, but they're not counted as sales.
