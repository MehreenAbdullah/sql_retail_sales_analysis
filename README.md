#Project Title: Retail Sales Analysis
Database: sql_project_p1

Project Overview

This project demonstrates SQL-based analysis of transactional retail sales data to evaluate revenue performance, customer behavior, and product category trends using SQL. After designing and structuring a relational database to store transaction-level data, the dataset was cleaned and validated to remove incomplete records and ensure data integrity. Exploratory Data Analysis (EDA) was then performed using SQL aggregations, filtering, grouping, date-based analysis, and window functions to examine sales distribution, customer concentration, seasonal patterns, and high-value transactions. The analysis addresses practical business problems such as identifying top-performing categories, ranking high-revenue customers, detecting peak sales months, evaluating demographic purchasing behavior, and understanding time-based sales patterns, demonstrating how raw sales data can be transformed into actionable business insights relevant to performance monitoring and financial analysis.

Objectives
* Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
* Data Cleaning: Identify and remove any records with missing or null values.
* Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
* Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.

Project Structure

1. Database
   Database Creation: The project starts by creating a database named p1_retail_db.
2. Table Creation
  A structured table retail_sales was designed to capture key transaction-level variables including; transaction ID | sale date  | sale time  | customer ID  | gender  | age  | product category  | quantity sold  | price per unit  | cost of goods sold (COGS)  | and total sale amount.

```sql
CREATE DATABASE p1_retail_db;

CREATE TABLE retail_sales
(
    transactions_id INT PRIMARY KEY,
    sale_date DATE,	
    sale_time TIME,
    customer_id INT,	
    gender VARCHAR(10),
    age INT,
    category VARCHAR(35),
    quantity INT,
    price_per_unit FLOAT,	
    cogs FLOAT,
    total_sale FLOAT
);
```
The table structure was designed to enable revenue analysis, profitability evaluation, and customer segmentation.

2. Data Exploration & Cleaning
   Before analysis, data validation was performed to ensure integrity and reliability.
   
   Record Count: Determine the total number of records in the dataset.
   Customer Count: Find out how many unique customers are in the dataset.
  Category Count: Identify all unique product categories in the dataset.
   Null Value Check: Check for any null values in the dataset and delete records with missing data.

   ```sql
SELECT COUNT(*) FROM retail_sales;
SELECT COUNT(DISTINCT customer_id) FROM retail_sales;
SELECT DISTINCT category FROM retail_sales;

SELECT * FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;

DELETE FROM retail_sales
WHERE 
    sale_date IS NULL OR sale_time IS NULL OR customer_id IS NULL OR 
    gender IS NULL OR age IS NULL OR category IS NULL OR 
    quantity IS NULL OR price_per_unit IS NULL OR cogs IS NULL;
```
This step ensures the dataset is clean and reliable for financial and performance analysis.

3.Analysis & Key Queries


   
   









