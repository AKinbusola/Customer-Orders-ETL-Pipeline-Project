# Customer-Orders-ETL-Pipeline-Project

##  Overview

This project demonstrates a complete **ETL (Extract, Transform, Load)** pipeline using **Python (Pandas, SQLAlchemy)** and **MySQL Workbench**. The data used comes from a Kaggle dataset (`orders.csv`) containing historical order transactions. The objective is to clean, enrich, and standardize the data, then move it between databases in a professional workflow.

---

##  Objectives

- Load raw order data into a MySQL database (`raw_data`)
- Extract the data into Python using **Jupyter Notebook**
- Perform data cleaning and transformation:
  - Format `Customer ID` to uniform 11-character IDs (e.g., `C0000000579`)
  - Normalize `Customer Status` values (e.g., `Gold`, `Silver`)
  - Format `Order ID` and `Product ID` by prefixing with `ORD` and `PRD`
  - Compute `Total Profit` per order:

    ```
    total_profit = total_retail_price - (quantity_ordered * cost_price_per_unit)
    ```

  - Clean column names by removing spaces and converting to snake_case
- Load the cleaned data into a new MySQL database (`analytics_data`)

---

##  Raw Data Sample (`orders.csv`)

| Customer ID | Customer Status | Date Order was placed | Delivery Date | Order ID | Product ID | Quantity Ordered | Total Retail Price for This Order | Cost Price Per Unit |
|-------------|------------------|------------------------|----------------|----------|------------|-------------------|-------------------------------|---------------------|
| 29101       | Silver           | 5-Aug-21               | 5-Aug-21       | 124301718| 2.407E+11  | 5                 | 34.95                         | 10.3                |
| 23334       | Platinum         | 25-Jul-19              | 25-Jul-19      | 123609712| 2.407E+11  | 3                 | 17.97                         | 10.23               |

---

## Tools & Technologies

- **Python** (Pandas, SQLAlchemy, mysql-connector-python)
- **MySQL Workbench**
- **Jupyter Notebook**
- **Kaggle Dataset** (Order History)

---

## Transformation Steps

| Step | Description |
|------|-------------|
|  1 | Loaded raw CSV into `raw_data` schema in MySQL using Python |
|  2 | Read the data from MySQL into a Pandas DataFrame |
|  3 | Cleaned column names (e.g., `Date Order was placed` → `order_date`) |
|  4 | Formatted `customer_id` as `C000000####` using `str.zfill()` |
|  5 | Normalized `customer_status` to proper case using `.str.title()` |
|  6 | Prefixed `order_id` and `product_id` with `ORD` and `PRD` |
|  7 | Calculated `total_profit` column |
|  8 | Loaded final cleaned data into a new schema: `analytics_data` |

---

## Cleaned Data Sample

| customer_id   | customer_status | order_date | delivery_date | order_id     | product_id       | quantity_ordered | total_retail_price | cost_price_per_unit | total_profit |
|---------------|------------------|------------|----------------|---------------|-------------------|-------------------|---------------------|----------------------|---------------|
| C0000000579   | Silver           | 01-Jan-17  | 07-Jan-17     | ORD123002578  | PRD220101400106   | 2                 | 92.6                | 20.70                | 51.20         |
| C0000007574   | Silver           | 01-Jan-17  | 05-Jan-17     | ORD123004074  | PRD210201000009   | 1                 | 21.7                | 9.95                 | 11.75         |
| C0000028861   | Gold             | 01-Jan-17  | 04-Jan-17     | ORD123000871  | PRD230100500068   | 1                 | 1.7                 | 0.80                 | 0.90          |

---

##  MySQL Schema Summary

### `raw_data.orders`
> Contains the uncleaned imported dataset from Kaggle.

### `analytics_data.orders`
> Contains the cleaned and transformed version of the dataset.


