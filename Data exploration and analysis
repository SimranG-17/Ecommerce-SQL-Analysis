-- STEP 5 - DATA EXPLORATION  -KPIS 

--5.1 TOTAL REVENUE 
SELECT ROUND(SUM(quantity*unit_price),2) AS total_revenue from clean_orders;

-- 5.2  Total Customers 
SELECT COUNT(*) AS total_customers FROM clean_customers;

-- 5.3 Total Orders 
SELECT COUNT(*) AS total_orders FROM clean_orders;

-- 5.4 Total Order Value 
SELECT SUM(total_amount) AS total_sales
FROM clean_orders;

-- 5.5 Average Order value/AOV
SELECT AVG(total_amount) AS average_order_value
FROM clean_orders;

-- 5.6 Purchasing Customers
SELECT COUNT(DISTINCT customer_id) AS purchasing_customers
FROM clean_orders;

-- 5.7  Total delivered orders  
SELECT SUM(total_amount) AS delivered_sales
FROM clean_orders
WHERE order_status = 'Delivered';

--5.8 Average order value of delivered orders
SELECT AVG(total_amount) AS average_delivered_order_value
FROM clean_orders
WHERE order_status = 'Delivered';


-- STEP 6 DATA ANALYSIS 

--6.1  REVENUE BY STATE 
SELECT c.state, ROUND(SUM(o.quantity*o.unit_price),2) AS revenue
FROM clean_orders o
JOIN clean_customers c
ON o.customer_id = c.customer_id
GROUP BY state;

--6.2 TOP 10 PRODUCTS BY SALES
SELECT product_name, product_category,
SUM(total_amount) as total_sales
FROM clean_orders
GROUP BY product_name,product_category
ORDER BY total_sales DESC
LIMIT 10;

-- 6.3 Customer Ranking by Delivered Sales
SELECT
    c.customer_id,
    CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
    c.loyalty_tier,
    COUNT(o.order_id) AS total_orders,
    ROUND(SUM(o.total_amount), 2) AS total_spending,
    ROUND(AVG(o.total_amount), 2) AS average_order_value,
    DENSE_RANK() OVER (
        ORDER BY SUM(o.total_amount) DESC
    ) AS customer_rank
FROM customers c
JOIN orders o
    ON c.customer_id = o.customer_id
WHERE o.order_status = 'Delivered'
GROUP BY
    c.customer_id,
    c.first_name,
    c.last_name,
    c.loyalty_tier
ORDER BY customer_rank
LIMIT 10;

-- 6.4 Monthly Sales Trend
SELECT 
    TO_CHAR(order_date, 'YYYY-MM') AS month,
    ROUND(SUM(total_amount)::NUMERIC, 2) AS monthly_sales
FROM orders
WHERE order_status = 'Delivered'
GROUP BY TO_CHAR(order_date, 'YYYY-MM')
ORDER BY month;

-- 6.5 SALES BY CATEGORY AND PRODUCT 
SELECT product_category, prodUCt_name,
SUM(total_amount) AS total_sales
FROM clean_orders
WHERE order_status = 'Delivered'
GROUP BY product_category,product_name
ORDER BY total_sales DESC;

--6.6 REGION WISE SALES AND ORDER VALUE 
SELECT warehouse_region,
COUNT(order_id) AS total_sales,
ROUND(SUM(total_amount),2) AS total_amount,
ROUND(AVG(total_amount),2) AS avg_amount
FROM clean_orders
GROUP BY warehouse_region
ORDER BY total_amount DESC;

