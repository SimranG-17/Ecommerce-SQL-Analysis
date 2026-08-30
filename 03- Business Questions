--STEP 7 Business Questions

--7.1 Does the loyalty program improve customer retention?
WITH customer_orders AS (
    SELECT c.customer_id, c.loyalty_tier,
        COUNT(o.order_id) AS delivered_orders
    FROM clean_customers c
    LEFT JOIN clean_orders o
        ON c.customer_id = o.customer_id
       AND o.order_status = 'Delivered'
    GROUP BY c.customer_id, c.loyalty_tier
)
SELECT loyalty_tier,
    COUNT(*) AS total_customers,
    SUM( CASE WHEN delivered_orders >= 2 THEN 1 ELSE 0 END
    ) AS repeat_customers,
    ROUND( 100.0 * AVG(
            CASE WHEN delivered_orders >= 2 THEN 1.0 ELSE 0 END
        ),1)  AS retention_rate,
    ROUND(AVG(delivered_orders), 2) AS avg_delivered_orders
FROM customer_orders
GROUP BY loyalty_tier
ORDER BY retention_rate DESC;

--7.2  Which high-value customers are at risk?
--This defines high-value customers as the top 25% by delivered spending and at-risk customers as those inactive for more than 90 days.

WITH customer_summary AS (
    SELECT  c.customer_id,
        CONCAT(c.first_name, ' ', c.last_name) AS customer_name,
        c.loyalty_tier,
        COUNT(o.order_id) AS delivered_orders,
        COALESCE(SUM(o.total_amount), 0) AS total_spend,
        MAX(o.order_date) AS last_order_date,
		NTILE(4) OVER (
            ORDER BY COALESCE(SUM(o.total_amount), 0) DESC,
                     c.customer_id ) AS spending_group
    FROM clean_customers c
    LEFT JOIN clean_orders o
        ON c.customer_id = o.customer_id
       AND o.order_status = 'Delivered'
    GROUP BY c.customer_id, c.first_name, c.last_name, c.loyalty_tier
)
SELECT
    customer_id, customer_name, loyalty_tier, delivered_orders,
    ROUND(total_spend, 2) AS total_spend,
    last_order_date,
    DATE '2025-12-31' - last_order_date AS days_inactive
FROM customer_summary
WHERE spending_group = 1
  AND last_order_date < DATE '2025-10-02'
ORDER BY total_spend DESC;

--7.3 Which fulfilment combinations are underperforming?

SELECT
    warehouse_region, shipping_method,
    COUNT(*) AS total_orders,
    SUM( CASE
         WHEN order_status IN ('Cancelled', 'Returned') THEN 1
         ELSE 0 END) AS failed_orders,
    ROUND(100.0 * AVG(CASE
         WHEN order_status IN ('Cancelled', 'Returned') THEN 1.0
         ELSE 0 END), 1) AS failure_rate,
    ROUND(100.0 * AVG(
            CASE WHEN order_status = 'Delivered' THEN 1.0 
			ELSE 0 END),1) AS delivery_rate,
    ROUND(AVG(delivery_days)
          FILTER (WHERE order_status = 'Delivered'),2) AS avg_delivery_days
FROM clean_orders
GROUP BY warehouse_region, shipping_method
HAVING COUNT(*) >= 20
ORDER BY failure_rate DESC
LIMIT 5;
