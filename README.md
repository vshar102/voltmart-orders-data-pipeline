# Voltmart Orders Data Pipeline

## 📌 Project Overview
This repository contains a PySpark-based data cleaning and preprocessing pipeline developed for **Voltmart**, an electronics e-commerce company. The primary goal of this project is to process and refine historical order data from the past year. The cleaned dataset (`orders_data_clean.parquet`) is generated specifically for the Machine Learning team to build a highly accurate **Demand Forecasting Model**.

## 🛠️ Technology Stack
- **Python 3.8+**
- **PySpark** (`pyspark.sql`)
- **Pandas** (for tabular data exploration)
- **Jupyter Notebook**

## 📂 Dataset Information
**Input File:** `orders_data.parquet` (Raw Sales Data)
**Output File:** `orders_data_clean.parquet` (Processed Data)

The dataset contains the following key columns:
`order_date`, `time_of_day`, `order_id`, `product`, `product_id`, `category`, `purchase_address`, `purchase_state`, `quantity_ordered`, `price_each`, `cost_price`, `turnover`, `margin`.

## 🧹 Data Cleaning & Preprocessing Steps
The PySpark script `notebook.ipynb` performs several crucial transformations to ensure data quality and align with the ML team's requirements:

1. **Temporal Feature Engineering & Filtering:**
   - Extracts the hour from `order_date` to create a `time_of_day` feature categorized as `morning` (6 AM - 11 AM), `afternoon` (12 PM - 5 PM), and `evening` (6 PM - 11 PM).
   - Identifies and **removes "night" orders** (placed between 12 AM and 5 AM).
   - Casts the `order_date` column from `Timestamp` format to `Date` format to strip unnecessary time data.

2. **Text Normalization:**
   - Converts the `product` and `category` columns perfectly to lowercase for consistency.

3. **Product Line Filtering:**
   - Removes any rows where the `product` name contains the string `"tv"`, reflecting Voltmart's business decision to discontinue TV sales.

4. **Address Parsing & State Extraction:**
   - Splits the `purchase_address` string to robustly extract the 2-letter US **State Abbreviation** (e.g., MA, OR, CA) into a newly created `purchase_state` column.

5. **Data Export:**
   - Saves the final polished DataFrame using the Parquet format to `orders_data_clean.parquet`, overwriting any previous instances.

## 🚀 How to Run
1. Ensure you have Apache Spark and PySpark installed on your local machine or cluster.
2. Launch Jupyter Notebook / JupyterLab and open `notebook.ipynb`.
3. Run all cells to initialize the Spark session, process `orders_data.parquet`, and generate the output parquet directory.

## 📝 License
This project is created for Voltmart's internal Machine Learning operations.
