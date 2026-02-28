## Project Title: Retail Sales Analysis
Database: sql_project_p1

Project Overview
---
This project demonstrates SQL-based analysis of transactional retail sales data to evaluate revenue performance, customer behavior, and product category trends using SQL. After designing and structuring a relational database to store transaction-- level data, the dataset was cleaned and validated to remove incomplete records and ensure data integrity. Exploratory Data Analysis (EDA) was then performed using SQL aggregations, filtering, grouping, date-based analysis, and window functions to examine sales distribution,, customer concentration, seasonal patterns, and high-value transactions. The analysis addresses practical business problems such as identifying top-performing categories, ranking high-revenue customers, detecting peak sales months, evaluating demographic purchasing behavior, and understanding time-based sales patterns,, demonstrating how raw sales data can be transformed into actionable business insights relevant to performance monitoring and financial analysis.

Objectives
---
* Set up a retail sales database: Create and populate a retail sales database with the provided sales data.
* Data Cleaning: Identify and remove any records with missing or null values.
* Exploratory Data Analysis (EDA): Perform basic exploratory data analysis to understand the dataset.
* Business Analysis: Use SQL to answer specific business questions and derive insights from the sales data.

Project Structure
---

1. Database
   Database Creation: The project starts by creating a database named p1_retail_db.
2. Table Creation
  A structured table retail_sales was designed to capture key transaction-level variables including; transaction ID | sale date  | sale time  | customer ID  | gender  | age  | product category  | quantity sold  |   price per unit  | cost of goods sold (COGS)  | and total sale amount.


---


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


---

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


---

3. Business Analysis & Key Queries
The following SQL queries were developed to simulate real business analysis scenarios.



1. **Write a SQL query to retrieve all columns for sales made on '2022-11-05**:
```sql
SELECT *
FROM retail_sales
WHERE sale_date = '2022-11-05';
```
Retrieves all transactions recorded on 5th November 2022 from the retail_sales table.


2. **Write a SQL query to retrieve all transactions where the category is 'Clothing' and the quantity sold is more than 4 in the month of Nov-2022**
```sql
SELECT 
  *
FROM retail_sales
WHERE 
    category = 'Clothing'
    AND 
    TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND
    quantity >= 4
```
Displays Clothing sales with quantity ≥ 4 during November 2022.
Filters Clothing transactions with quantity of 4 or more in November 2022.




3. **Write a SQL query to calculate the total sales (total_sale) for each category.**:
```sql
SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
FROM retail_sales
GROUP BY 1
```
Summarizes category-wise revenue and transaction count.




4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**:
```sql
SELECT
    ROUND(AVG(age), 2) as avg_age
FROM retail_sales
WHERE category = 'Beauty'
```
Computes the average customer age for Beauty category purchases, rounded to two decimal places.




5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**:
```sql
SELECT * FROM retail_sales
WHERE total_sale > 1000
```
Highlights premium transactions with total sales above 1000 to examine high-revenue purchases.




6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**:
```sql
SELECT 
    category,
    gender,
    COUNT(*) as total_trans
FROM retail_sales
GROUP 
    BY 
    category,
    gender
ORDER BY 1
```
Highlights transaction distribution by gender within each product category.




7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**:
```sql
SELECT 
       year,
       month,
    avg_sale
FROM 
(    
SELECT 
    EXTRACT(YEAR FROM sale_date) as year,
    EXTRACT(MONTH FROM sale_date) as month,
    AVG(total_sale) as avg_sale,
    RANK() OVER(PARTITION BY EXTRACT(YEAR FROM sale_date) ORDER BY AVG(total_sale) DESC) as rank
FROM retail_sales
GROUP BY 1, 2
) as t1
WHERE rank = 1
```
Identifies the top-selling month in each year based on average sales, revealing seasonal revenue patterns and year-wise performance variations. This ranking-based approach allows comparison of monthly performance within each year and highlights periods of peak sales activity.




8. **Write a SQL query to find the top 5 customers based on the highest total sales **:
```sql
SELECT 
    customer_id,
    SUM(total_sale) as total_sales
FROM retail_sales
GROUP BY 1
ORDER BY 2 DESC
LIMIT 5
```
Ranks customers by total sales and isolates the top five contributors, helping assess revenue concentration and customer-level impact on overall performance.




9. **Write a SQL query to find the number of unique customers who purchased items from each category.**:
```sql
SELECT 
    category,    
    COUNT(DISTINCT customer_id) as cnt_unique_cs
FROM retail_sales
GROUP BY category
```
Reveals customer penetration across categories by counting distinct buyers in each segment.




10. **Write a SQL query to create each shift and number of orders (Example Morning <12, Afternoon Between 12 & 17, Evening >17)**:
```sql
WITH hourly_sale
AS
(
SELECT *,
    CASE
        WHEN EXTRACT(HOUR FROM sale_time) < 12 THEN 'Morning'
        WHEN EXTRACT(HOUR FROM sale_time) BETWEEN 12 AND 17 THEN 'Afternoon'
        ELSE 'Evening'
    END as shift
FROM retail_sales
)
SELECT 
    shift,
    COUNT(*) as total_orders    
FROM hourly_sale
GROUP BY shift
```
Segments transactions into Morning, Afternoon, and Evening shifts and counts total orders in each period, revealing how sales activity is distributed across different times of the day.




Findings
---
* Customer Demographics: The dataset includes customers from various age groups, with sales distributed across different categories such as Clothing and Beauty.
* Revenue concentration is uneven across product categories, with certain segments contributing disproportionately to overall sales performance.
*High-value transactions above the defined threshold highlight the presence of premium purchasing behavior and revenue clustering among select transactions.
* Monthly ranking analysis reveals distinct seasonal peaks, indicating periods of stronger sales intensity within each year.
* Time-of-day segmentation identifies variation in order volume across operational shifts, highlighting periods of peak transaction activity.
  



Reports
---

Sales Summary:
Provides a consolidated view of total revenue, order volume, and category-level contribution, highlighting which product segments drive overall sales performance and where revenue concentration exists.

Trend Analysis:
Examines monthly sales averages and ranks peak-performing months within each year to identify seasonal revenue patterns and performance fluctuations. Time-of-day segmentation further evaluates how transaction activity varies across operational shifts.

Customer Insights:
Identifies top revenue-generating customers and measures unique customer distribution across categories, revealing revenue concentration and customer penetration by segment.





Conclusion
---
This project applies SQL-based exploratory data analysis to structured retail transaction data to uncover patterns in revenue distribution, customer contribution, and seasonal performance. By combining aggregation, filtering, and ranking techniques, the analysis highlights category-level revenue drivers, customer concentration at the top end, and time-based demand variation. The findings demonstrate how transactional data can be systematically examined to evaluate sales performance and support data-informed business assessment.

   
   









