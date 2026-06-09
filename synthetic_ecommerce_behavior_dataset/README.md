# Synthetic E-commerce User Behavior Dataset

This dataset is 100% synthetic and generated locally for a data-analysis portfolio project. It does not use APIs, scraping, real customers, or real transactions.

## Size
- customers.csv: 20,000 rows
- products.csv: 500 rows
- orders.csv: 100,000 rows
- order_items.csv: 166,207 rows

## Recommended joins
- orders.customer_id -> customers.customer_id
- order_items.order_id -> orders.order_id
- order_items.product_id -> products.product_id

## Suggested analyses
1. Average order value / average check
   - Filter to completed orders for a clean business metric.
   - Use `order_total` or `net_revenue_for_analysis` depending on whether you want returns included.

2. Top customers
   - Aggregate completed orders by customer_id.
   - Calculate revenue, number of orders, first order date, last order date, average order value.

3. Cohort analysis
   - For every customer, define cohort_month as the month of their first completed order.
   - For every later order, calculate months since cohort_month.
   - Build a retention matrix: cohort_month x month_number.

4. RFM analysis
   - Recency: days since last completed order, using max order date in the dataset as the analysis date.
   - Frequency: number of completed orders.
   - Monetary: total completed order revenue.
   - Score each metric into quantiles from 1 to 5.

5. Seasonality
   - Aggregate revenue/orders by month, weekday, category, promo_code.
   - There are stronger patterns around November/December and smaller summer uplift.

## Intentional realistic features
- Some customer city and birth_year values are missing.
- Orders include completed, returned, and cancelled statuses.
- Revenue fields are separated so you can practice choosing the right metric.
- Order line prices vary slightly from product list prices.
- Customers have unequal activity levels, so top-customer and RFM analysis are meaningful.
- Promo codes and seasonal effects influence discounts and order volume.

## Main metric recommendation
For most beginner analyses, start with completed orders only:
`orders[orders['order_status'] == 'completed']`

For net business impact including returns and cancellations, use `net_revenue_for_analysis`.