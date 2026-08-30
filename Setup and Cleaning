-- 	STEP 1 DATA CREATION 
-- CREATING TABLES
CREATE TABLE Customers (
    customer_id INTEGER PRIMARY KEY,
    first_name VARCHAR(100),
    last_name VARCHAR(100),
    age INTEGER,
    gender VARCHAR(20),
    signup_date DATE,
    loyalty_tier VARCHAR(50),
    city VARCHAR(100),
    state VARCHAR(100),
    country VARCHAR(100),
    annual_income_inr NUMERIC(15,2),
    acquisition_channel VARCHAR(50),
    is_inactive BOOLEAN
);

CREATE TABLE Orders (
    order_id INTEGER PRIMARY KEY,
    customer_id INTEGER,
    order_date DATE,
    product_category VARCHAR(100),
    product_name VARCHAR(200),
    quantity INTEGER,
    unit_price NUMERIC(12,2),
    discount_percent NUMERIC(5,2),
    subtotal NUMERIC(15,2),
    shipping_cost NUMERIC(12,2),
    tax_amount NUMERIC(12,2),
    total_amount NUMERIC(15,2),
    payment_method VARCHAR(50),
    order_status VARCHAR(50),
    shipping_method VARCHAR(50),
    sales_channel VARCHAR(50),
    coupon_code VARCHAR(50),
    warehouse_region VARCHAR(100),
    delivery_days NUMERIC(5,1)
);
-- 1.1 ALTER TABLE 
ALTER TABLE orders
ALTER COLUMN delivery_days TYPE INT;

--IMPORT THE CSV FILES 

-- STEP 2 - DATA QUALITY CHECK 
--2.1 TOP 10 ROWS FROM CUSTOMERS TABLE 
SELECT * FROM Customers
LIMIT 10;

--2.2 TOP 10 ROWS FROM ORDERS TABLE 
SELECT * FROM Orders 
LIMIT 10;

--2.3 COUNT THE ROWS IN CUSTOMERS TABLE 
SELECT COUNT(*) FROM customers; 

--2.4 COUNT THE ROWS IN ORDERS TABLE 
SELECT COUNT(*) FROM orders;

--STEP 3 - CHECKING THE NULL VALUE 
--3.1 CHECK NULL VALUE IN CUSTOMERS TABLE 
SELECT 
  SUM(CASE WHEN customer_id IS NULL THEN 1 ELSE 0 END) AS null_customer_id,
  SUM(CASE WHEN first_name IS NULL THEN 1 ELSE 0 END) AS null_first_name,
  SUM(CASE WHEN last_name IS NULL THEN 1 ELSE 0 END) AS null_last_name,
  SUM(CASE WHEN age IS NULL THEN 1 ELSE 0 END) AS null_age,
  SUM(CASE WHEN gender IS NULL THEN 1 ELSE 0 END) AS null_gender,
  SUM(CASE WHEN signup_date IS NULL THEN 1 ELSE 0 END) AS null_signup_date,
  SUM(CASE WHEN loyalty_tier IS NULL THEN 1 ELSE 0 END) AS null_loyalty_tier,
  SUM(CASE WHEN city IS NULL THEN 1 ELSE 0 END) AS null_city,
  SUM(CASE WHEN state IS NULL THEN 1 ELSE 0 END) AS null_state,
  SUM(CASE WHEN country IS NULL THEN 1 ELSE 0 END) AS null_country,
  SUM(CASE WHEN annual_income_inr IS NULL THEN 1 ELSE 0 END) AS null_annual_income_inr,
  SUM(CASE WHEN acquisition_channel IS NULL THEN 1 ELSE 0 END) AS null_acquisition_channel,
  SUM(CASE WHEN is_inactive IS NULL THEN 1 ELSE 0 END) AS null_is_inactive
FROM Customers;

--3.2  CHECK NULL VALUE IN ORDERS TABLE 
SELECT 
  SUM(CASE WHEN order_id IS NULL THEN 1 ELSE 0 END) AS null_order_id,
  SUM(CASE WHEN customer_id IS NULL THEN 1 ELSE 0 END) AS null_customer_id,
  SUM(CASE WHEN order_date IS NULL THEN 1 ELSE 0 END) AS null_order_date,
  SUM(CASE WHEN product_category IS NULL THEN 1 ELSE 0 END) AS null_product_category,
  SUM(CASE WHEN product_name IS NULL THEN 1 ELSE 0 END) AS null_product_name,
  SUM(CASE WHEN quantity IS NULL THEN 1 ELSE 0 END) AS null_quantity,
  SUM(CASE WHEN unit_price IS NULL THEN 1 ELSE 0 END) AS null_unit_price,
  SUM(CASE WHEN discount_percent IS NULL THEN 1 ELSE 0 END) AS null_discount_percent,
  SUM(CASE WHEN subtotal IS NULL THEN 1 ELSE 0 END) AS null_subtotal,
  SUM(CASE WHEN shipping_cost IS NULL THEN 1 ELSE 0 END) AS null_shipping_cost,
  SUM(CASE WHEN tax_amount IS NULL THEN 1 ELSE 0 END) AS null_tax_amount,
  SUM(CASE WHEN payment_method IS NULL THEN 1 ELSE 0 END) AS null_payment_method,
  SUM(CASE WHEN order_status IS NULL THEN 1 ELSE 0 END) AS null_order_status,
  SUM(CASE WHEN shipping_method IS NULL THEN 1 ELSE 0 END) AS null_shipping_method,
  SUM(CASE WHEN sales_channel IS NULL THEN 1 ELSE 0 END) AS null_sales_channel,
  SUM(CASE WHEN coupon_code IS NULL THEN 1 ELSE 0 END) AS null_coupon_code,
  SUM(CASE WHEN warehouse_region IS NULL THEN 1 ELSE 0 END) AS null_warehouse_region,
  SUM(CASE WHEN delivery_days IS NULL THEN 1 ELSE 0 END) AS null_delivery_days  
FROM Orders;

--3.3  COUNT NULL VALUES IN CUSTOMERS TABLE 
SELECT
    'customer_id' AS column_name,
    SUM(CASE WHEN customer_id IS NULL THEN 1 ELSE 0 END) AS null_count
FROM customers

UNION ALL

SELECT
    'gender',
    SUM(CASE WHEN gender IS NULL THEN 1 ELSE 0 END)
FROM customers

UNION ALL

SELECT
    'annual_income_inr',
    SUM(CASE WHEN annual_income_inr IS NULL THEN 1 ELSE 0 END)
FROM customers

UNION ALL

SELECT
    'acquisition_channel',
    SUM(CASE WHEN acquisition_channel IS NULL THEN 1 ELSE 0 END)
FROM customers;
	
--3.5 COUNT NULL IN ORDERS TABLE 
SELECT
    'Order_id' AS column_name,
    SUM(CASE WHEN order_id IS NULL THEN 1 ELSE 0 END) AS null_count
FROM orders

UNION ALL

SELECT
    'coupon_code',
    SUM(CASE WHEN coupon_code IS NULL THEN 1 ELSE 0 END)
FROM orders

UNION ALL

SELECT
    'delivery_days',
    SUM(CASE WHEN delivery_days IS NULL THEN 1 ELSE 0 END)
FROM orders;

--STEP 4 -  DATA CLEANING
--4.1 CREATE A VIEW WITH CLEANED DATA IN CUSTOMERS TABLE 

CREATE OR REPLACE VIEW clean_customers AS
SELECT
    customer_id,
    BTRIM(first_name) AS first_name,
    BTRIM(last_name) AS last_name,
    age,
    COALESCE(NULLIF(BTRIM(gender), ''), 'Unknown') AS gender,
    signup_date,
    COALESCE(NULLIF(BTRIM(loyalty_tier), ''), 'Unknown') AS loyalty_tier,
    BTRIM(city) AS city,
    BTRIM(state) AS state,
    BTRIM(country) AS country,
    annual_income_inr,
    COALESCE(NULLIF(BTRIM(acquisition_channel), ''), 'Unknown') AS acquisition_channel,
    is_inactive
FROM customers;

-- 4.2 CREATE A VIEW WITH CLEANED DATA IN CUSTOMERS TABLE 

CREATE OR REPLACE VIEW clean_orders AS
SELECT
    order_id, customer_id, order_date,
    BTRIM(product_category) AS product_category,
    BTRIM(product_name) AS product_name,
    quantity, unit_price, discount_percent, subtotal, shipping_cost,
    tax_amount, total_amount,
    BTRIM(payment_method) AS payment_method,
    CASE WHEN TRIM(order_status:: TEXT) = 'Processin' THEN 'Processing'
         ELSE TRIM(order_status:: TEXT) END AS order_status,
    BTRIM(shipping_method) AS shipping_method,
    BTRIM(sales_channel) AS sales_channel,
    COALESCE(NULLIF(BTRIM(coupon_code), ''), 'NO_COUPON') AS coupon_code,
    BTRIM(warehouse_region) AS warehouse_region,
    delivery_days
FROM orders;
