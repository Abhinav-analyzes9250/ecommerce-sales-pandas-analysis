# Business Insights

## Quick summary

Out of 1,000 orders placed by 300 customers across 5 countries, 695 (80.5%) completed, bringing
in $311,111.00 at an average order value of $447.64. The customer base is a genuine strength here
— a 73.41% repeat rate, and revenue isn't propped up by a small group of big spenders. Below is
what stood out once I actually dug into the numbers.

## 1. Hair is carrying the category mix

Hair pulled in $101,637 — about a third of all revenue (32.67%), clearly ahead of Makeup
(26.06%), Body (24.43%), and Skin (16.84%). If I had to pick one place to focus inventory or
marketing budget, this is it.

## 2. "Best seller" isn't one thing

Product_45 sold the most units (154), but Product_16 made the most money ($9,732). Two different
products. This only becomes obvious once you look at Q18 and Q19 side by side — a product can
move a lot of volume at a lower price and still lose out on total revenue to something that
sells less but costs more per unit. Worth remembering before calling anything a "top product"
without specifying by what measure.

## 3. Revenue bounces around more than it trends

Monthly revenue swings between roughly $22.8K and $30.9K, and month-over-month growth goes from
about +32% to -25% across the year — no clean upward or downward line. January was the strongest
revenue month ($30,948), October had the most orders (70). I'd hold off calling this a "trend" —
it reads more like normal fluctuation, possibly seasonal, but one year of data isn't enough to
say for sure.

## 4. Repeat customers, and no single group dominating revenue

73.41% of active customers (196 of 267) placed more than one completed order — a solid signal
that people are coming back. At the same time, the top 10 customers only account for 11.34% of
revenue, and the top 20% get you to 42.31%. So this isn't a "handful of whales" situation —
revenue is spread fairly broadly across the customer base.

## 5. Country performance splits depending on what you measure

Italy has the highest total revenue ($70,719, 22.73% share). Morocco has the highest average
order value ($486.30) despite not leading on total revenue. So "best market" really depends on
whether the question is about scale or about order size — they point to different countries here.

## Things I'd want to check next

- What actually happened in January 2024 that pushed revenue up (promo? seasonal demand?).
- Why October had the most orders but not the most revenue — smaller basket sizes that month?
- Whether Morocco's higher AOV is a product-mix thing or genuinely fewer-but-bigger orders.
- The 9.2% return rate — worth breaking down by category/product to see if it's concentrated
  anywhere.

## One honest caveat

All of the above describes patterns that are actually in the data — I recalculated every number
from the raw tables and cross-checked the totals against `sales_cleaned.csv` (all 4 checks
passed). But none of it explains *why* those patterns exist. I don't have marketing spend,
pricing history, or stock-level data, so causal claims would be a stretch beyond what these 5
files can support.
