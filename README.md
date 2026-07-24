# New Menu Performance Analysis — Taste of the World Café (Q1 2023)
A SQL portfolio project analysing the first-quarter performance of a newly launched restaurant menu, using order and menu data to identify what's selling, when demand peaks, and which cuisines to prioritise for further development.

Note: Taste of the World Café is a fictitious restaurant used for analytical practice. The dataset and findings are illustrative rather than from an actual business. The data is sourced from Maven Analytics.

## Business Question
How did the new menu perform across items and cuisines over its first quarter, and which cuisines should the café prioritise for further development?

## Dataset
Two tables covering January to March 2023 — the menu's first full quarter:
- `order_details`(12,234 order lines across 5,370 distinct orders): order_details_id, order_id, order_date, order_time, **item_id**
- `menu_items`(32 rows for 32 menu items): **menu_item_id**, item_name, category, price

## Tools
- Python (pandas) — data loading, cleaning, and preparation
- SQLite — all analysis queries
- Google Colab — notebook environment

## Key Insights
**Revenue is stable but not growing.** 
Weekly revenue holds between $11,200 and $13,600 for 12 of 14 weeks with no upward trend. The new menu has generated consistent demand but not organic growth across its first quarter.
 
**Lunch is the highest-value period, not just the busiest.** 
The 12–1 pm window carries an AOV of ~$34, roughly 20% above dinner (5–7 pm). Customers at lunch tend to place more complete meal orders, making this the most profitable and highest-risk service window of the day.
 
**Monday outperforms the weekend on revenue, driven entirely by volume.**
Average order value is consistent across all seven days (~$29–31), meaning weekday revenue differences reflect footfall, not spend per customer. Monday leading the weekend is unusual for a restaurant and warrants local context investigation before acting on it.
 
**Italian earns the most revenue from fewer sales, pricing is the driver.** 
Italian generates 31% of total revenue from just 24% of items sold, with the highest average item price of any category. Asian leads on volume but earns proportionally less. American  underperforms on both volume and revenue, which is the weakest category across every dimension.
 
**A small number of dishes drive a disproportionate share of revenue.**
The top five dishes by revenue account for 27% of total revenue. Korean Beef Bowl leads at $10,555; Chicken Tacos is last with $1,470 from just 123 units sold over the quarter.
 
**High-spending orders skew heavily Italian.** 
Across the top 10 highest-spending orders, Italian dishes dominate in both frequency and revenue contribution. Eggplant Parmesan averages one appearance per order, indicating consistent preference among high-spending tables rather than a pricing effect.

## Project Workflow
### Data Preparation
- Date/time conversion: `order_date` and `order_time` were converted to SQLite-friendly formats, enabling STRFTIME-based weekly, weekday, and hourly aggregations.
- Null values: 137 null values were found in `order_details.item_id`; all other fields in affected rows were complete. Since `item_id` is the join key to the `menu_items` table, these rows cannot contribute to any item or revenue analysis and were removed, reducing the row count to 12,097 rows (~1.12% data loss). This is likely due to data entry or system logging issues rather than actual zero-item orders.
- Duplicates: No duplicate records were found in either table.

### Data Analysis Overview
#### 1. Demand and Timing Patterns
*When does the restaurant generate the most orders and revenue, and is demand growing across the quarter?*
- Overall revenue, order volume, and average order value (AOV)
- Weekly revenue trend assessing whether the new menu generated growth momentum across the quarter
- Revenue and AOV by weekday identifying the strongest and weakest trading days
- Revenue and AOV by hour pinpointing peak value periods, not just peak volume periods
  
#### 2. Menu and Cuisine Performance
*Which menu items and cuisine categories are driving revenue, and which are underperforming?*
- Item-level revenue and volume across all 32 dishes
- Category-level breakdown: revenue share, volume share, and average  price per cuisine, identifying where pricing, not just popularity, drives results

#### 3. Highest-Spend Orders
*What do the highest-spend orders tell about top customers' preferences?*
- Top 10 orders ranked by total spend
- Item and category composition of high-value orders

## Recommendations
**Expand Italian and Asian menus** - add 2–3 new items each in the next refresh; Italian leads on revenue per item, Asian on total volume 
**Protect the 12–1 pm service window** - ensure full stock and adequate staffing from 11:30 am; a lunch gap costs ~20% more per lost order than dinner
**Review Mexican pricing** - volume is comparable to Italian, but revenue is limited by low average item price; test higher-priced mains in Q2 
**Investigate American before developing it further** - low volume and low revenue point to a demand issue, not a pricing fix 
**Replace Chicken Tacos** - 123 units over a full quarter is the lowest of any dish; the menu slot is better used by a higher-priced item
**Understand weekday patterns before acting** -  Monday's lead and Wednesday's weakness are both volume-driven; verify local context before adjusting staffing or promotions 

## Limitations
- No pre-launch menu data — performance cannot be benchmarked against the previous menu
- Revenue figures only — no cost data to assess margin or profitability
- No customer ID — order patterns cannot be linked to individual or repeat customers

## Repository contents
- restaurant_orders_sql_analysis.ipynb | Main analysis notebook
- menu_items.csv | Menu data
- order_details.csv | Order transaction data
- restaurant_db_data_dictionary.csv | Column descriptions
- README.md
