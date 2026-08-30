# Ecommerce-SQL-Analysis-

This project uses PostgreSQL to analyze customer and order data for an e-commerce business. The work covers database creation, data-quality checks, data cleaning, KPI calculation, and exploratory analysis to identify customer, product, regional, and monthly sales trends.

**Data Preparation Workflow**

1. Created the customers and orders tables
2. Previewed the data and verified row counts
3. Checked important columns for missing values
4. Trimmed inconsistent text values
5. Replaced missing categories with clear default values
6. Corrected the Processin order-status typo to Processing
7. Created reusable clean_customers and clean_orders views.

**SQL Skills Demonstrated**
1. SELECT, WHERE, and ORDER BY
2. COUNT, SUM, and AVG
3. GROUP BY
4. JOIN
5. CASE, COALESCE, and NULLIF
6. Data-cleaning views
7. Window function: DENSE_RANK

**Business Insights**

1. Electronics generated the highest delivered sales at approximately ₹6.21M.
2. Noise Cancelling Headphones were the top product by total order value at approximately ₹2.19M.
3. The South warehouse region recorded the highest order value at approximately ₹7.67M, followed by the West at ₹7.44M.
4. Maharashtra was the leading customer state by gross revenue at approximately ₹6.97M.
5. November 2025 was the strongest month for delivered sales at approximately ₹1.43M.
6. 764 of 1,000 customers placed at least one order, leaving an opportunity to activate customers who have not purchased yet.
