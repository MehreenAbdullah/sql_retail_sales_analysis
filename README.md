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







