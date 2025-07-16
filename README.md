# City-Level-Sales-Estimation-and-SKU-Availability-Analytics-on-Blinkit-Inventory-Data
This project derives a city-level insights table (blinkit_city_insights) by integrating and analyzing real-world SKU inventory data from Blinkit, a quick-commerce platform. It focuses on estimating quantity sold (est_qty_sold), calculating revenue metrics, and assessing product availability across dark stores and cities.

# Tech Stack
SQL (PostgreSQL)
Data Engineering Concepts
Window Functions (LAG, ROW_NUMBER)
Aggregate Functions (MODE, COUNT, SUM)
Data Cleaning & Transformation

# Source Tables
1. all_blinkit_category_scraping_stream
Raw scraped inventory data per SKU, store, and timestamp
Includes: sku_id, inventory, selling_price, mrp, created_at
2. blinkit_categories
Maps SKUs to categories and subcategories
3. blinkit_city_map
Maps store_id to city_name

# Objective
Create a derived table blinkit_city_insights containing:
Estimated quantity sold per SKU per city per day
Estimated revenue (based on selling price and MRP)
Product availability (on-shelf availability metrics)
Discounts and pricing insights
Cleanly mapped category and brand information

# Key Features & Logic
Estimation of est_qty_sold:
Calculated by comparing inventory values over time using LAG.
Inventory decrease → counted as sales
Inventory increase → treated as restock (initially ignored)

# Business KPIs Computed:
est_sales_sp = Estimated sales using selling price
est_sales_mrp = Estimated sales using MRP
wt_osa = On-shelf availability across all stores
wt_osa_ls = On-shelf availability across listed stores
discount = Relative difference between MRP and SP
Mode-based selection of sp and mrp for clean aggregation

# Data Cleaning:
Excluded store records with no city mapping
Normalized SKU data using category and city joins

