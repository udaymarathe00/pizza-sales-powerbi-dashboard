# Pizza Sales Dashboard (Power BI)

An interactive 3-page Power BI dashboard that analyses one year of pizza sales: revenue, orders, busiest times, best and worst sellers, and sales by category and size. Built with a star schema, DAX measures and a dark, restaurant-style theme (tomato red, cheese yellow, basil green).

<img width="1304" height="728" alt="page1-home" src="https://github.com/user-attachments/assets/0bfecead-82d7-40a3-9ff3-9b0ec682948b" />


# Business questions
- How much revenue, how many orders, and how many pizzas did the year bring in?
- When do customers order: which day, month and hour are busiest?
- Which pizzas sell best, and which earn the most (or the least)?
- How do the four categories and five sizes share the sales?

## Dataset
| Item | Detail |
|------|--------|
| Source | `pizza_sales.csv` (one row per pizza line in an order) |
| Size | 48,620 rows, 12 columns |
| Period | 1 January 2015 to 31 December 2015 |
| Content | 21,350 orders, 32 pizza types, 4 categories (Classic, Chicken, Supreme, Veggie), 5 sizes (S, M, L, XL, XXL) |

Columns: pizza_id, order_id, pizza_name_id, quantity, order_date, order_time, unit_price, total_price, pizza_size, pizza_category, pizza_ingredients, pizza_name.

## Data preparation (Power Query)
- Set the correct data types for dates, times, numbers and text.
- Split the raw file into a fact table and dimension tables, and renamed them as `Fact_` and `Dim_` tables.
- Added helper columns for day of week, month and hour to power the time analysis.

## Data model
A star schema: one fact table of order lines connected to dimension tables, plus a separate table that holds only the DAX measures.

## Key DAX measures
``` DAX
Total Revenue = SUM(Fact_Sales[total_price])
Total Orders = DISTINCTCOUNT(Fact_Sales[order_id])
Pizzas Sold = SUM(Fact_Sales[quantity])
Avg Order Value = DIVIDE([Total Revenue], [Total Orders])
Pizzas per Order = DIVIDE([Pizzas Sold], [Total Orders])
```

## Dashboard pages

### 1. Home
Five KPI cards (total revenue, total orders, pizzas sold, average order value, pizzas per order), monthly orders trend, orders by day of week, pizzas sold by category, a day-and-hour heatmap of when customers order, the top 5 best sellers, and revenue by pizza size.

<img width="1304" height="728" alt="page1-home" src="https://github.com/user-attachments/assets/36dcd56a-891d-461f-81f7-deeeff03a590" />

### 2. Best and worst sellers
Top 5 and bottom 5 pizzas by quantity sold, and top 5 and bottom 5 by revenue.

<img width="1304" height="728" alt="page2-best-worst-sellers" src="https://github.com/user-attachments/assets/7dcf2bb9-a956-4b64-ad84-ce51d88e4d39" />

### 3. Summary
One-glance cards for the busiest day, month and hour, the top category and top size, and the best, worst, highest-revenue and lowest-revenue pizzas.

<img width="1304" height="728" alt="page3-summary" src="https://github.com/user-attachments/assets/857cfeec-a90f-417f-b010-c19adc87645e" />

## Interactivity
- Category buttons (Chicken, Classic, Supreme, Veggie) filter every page.
- A date range slicer narrows the period.
- Navigation buttons at the top move between the three pages.

## Key insights (full year, no filters)
- The year brought in **$817,860** from **21,350 orders** and **49,574 pizzas**, with an average order value of **$38.31** (2.32 pizzas per order).
- **Friday** is the busiest day (3,538 orders), **July** the busiest month (1,935 orders), and **12 PM** the busiest hour (2,520 orders), with a second peak around 6 PM.
- **The Classic Deluxe Pizza** sells the most (2,453 pizzas), while **The Thai Chicken Pizza** earns the most revenue ($43,434).
- **The Brie Carre Pizza** is the weakest on both counts (490 pizzas, $11,589).
- **Classic** is the top category by revenue ($220,053), and **large (L)** pizzas bring in the most revenue (45.9% of the total).

## Files
- `report/`: the `.pbix` file and a PDF export
- `screenshots/`: images of each dashboard page
- `data/`: the `pizza_sales.csv` file

## Tools
Power BI Desktop, DAX, Power Query.

## Author
**Uday Marathe**: [LinkedIn](https://linkedin.com/in/uday-marathe)

