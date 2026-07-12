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

## Project Workflow
### Data Preparation
- Date/time conversion: `order_date` and `order_time` were converted to SQLite-friendly formats, enabling STRFTIME-based weekly, weekday, and hourly aggregations.
- Null values: 137 null values were found in `order_details.item_id`; all other fields in affected rows were complete. Since `item_id` is the join key to the `menu_items` table, these rows cannot contribute to any item or revenue analysis and were removed, reducing the row count to 12,097 rows (~1.12% data loss). This is likely due to data entry or system logging issues rather than actual zero-item orders.
- Duplicates: No duplicate records were found in either table.

### Data Analysis Overview

## Recommendations

## Repository contents
- restaurant_orders_sql_analysis.ipynb | Main analysis notebook
- menu_items.csv | Menu data
- order_details.csv | Order transaction data
- restaurant_db_data_dictionary.csv | Column descriptions
- README.md
