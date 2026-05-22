-- =========================================================
-- OLIST E-COMMERCE - DATA IMPORT SCRIPT (psql)
-- =========================================================
-- Run inside psql ONLY:
-- \set data_dir 'C:/path/to/your/csv_folder'
-- \i sql/01_schema.sql
-- \i sql/02_import.sql
-- =========================================================
-- IMPORTANT:
-- - Use forward slashes /
-- - CSV files must exist in data_dir
-- - This script assumes tables already created
-- =========================================================

-- =========================
-- LOAD ORDER (IMPORTANT)
-- 1. Base reference tables
-- 2. Orders
-- 3. Fact tables (items, payments, reviews)
-- =========================

-- =========================
-- 1. CUSTOMERS
-- =========================
\copy customers
FROM :'data_dir'/olist_customers_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 2. SELLERS
-- =========================
\copy sellers
FROM :'data_dir'/olist_sellers_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 3. PRODUCTS
-- =========================
\copy products
FROM :'data_dir'/olist_products_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 4. PRODUCT CATEGORY TRANSLATION
-- =========================
\copy product_category_name_translation
FROM :'data_dir'/product_category_name_translation.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 5. ORDERS
-- =========================
\copy orders
FROM :'data_dir'/olist_orders_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 6. ORDER ITEMS (FACT TABLE)
-- =========================
\copy order_items
FROM :'data_dir'/olist_order_items_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 7. ORDER PAYMENTS (FACT TABLE)
-- =========================
\copy order_payments
FROM :'data_dir'/olist_order_payments_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 8. ORDER REVIEWS (FACT TABLE)
-- =========================
\copy order_reviews
FROM :'data_dir'/olist_order_reviews_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');

-- =========================
-- 9. GEOLOCATION (REFERENCE DATA)
-- =========================
\copy geolocation
FROM :'data_dir'/olist_geolocation_dataset.csv
WITH (FORMAT csv, HEADER true, DELIMITER ',', ENCODING 'UTF8');
