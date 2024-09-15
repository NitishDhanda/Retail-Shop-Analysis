Retail Shop Sales Analysis
Project Overview
This project focuses on analyzing retail sales data to gain insights into customer behavior, product performance, and sales trends. The project involves setting up a MySQL database, importing sales data, and running various SQL queries to answer business-related questions.

Objectives
Set up a Retail_Shop database and a table to store sales transactions.
Perform data validation by checking for null or missing values.
Address several business questions through SQL queries, such as:
Identifying sales on specific dates.
Tracking product category performance, like Clothing or Beauty.
Calculating total and average sales.
Analyzing customer demographics and purchase behavior.
Database Design
The project uses a single table Retail_sales, which includes the following columns:

transactions_id: (INT) Primary Key, Unique identifier for each transaction.
sale_date: (DATE) The date of the sale.
sale_time: (TIME) The time the transaction took place.
customer_id: (INT) Unique identifier for the customer.
gender: (VARCHAR) Gender of the customer.
age: (INT) Age of the customer.
category: (VARCHAR) Product category (e.g., 'Clothing', 'Beauty').
quantity: (INT) Number of items sold.
price_per_unit: (FLOAT) Price of a single unit of the product.
cogs: (FLOAT) Cost of goods sold.
total_sale: (FLOAT) The total revenue from the transaction.
Key Queries and Solutions
1. Checking for Missing or Null Values
We first ensured that there were no missing or NULL values in the dataset:

sql
Copy code
SELECT * FROM Retail_Sales
WHERE transactions_id IS NULL 
OR sale_date IS NULL
OR sale_time IS NULL
OR customer_id IS NULL
OR gender IS NULL
OR age IS NULL
OR category IS NULL
OR quantity IS NULL
OR cogs IS NULL
OR total_sale IS NULL
OR price_per_unit IS NULL;
2. Key Business Insights
Sales on Specific Date (2022-11-05):
sql
Copy code
SELECT * FROM Retail_sales WHERE sale_date = '2022-11-05';
Clothing Sales with Quantity > 10 in November 2022:
sql
Copy code
SELECT * FROM Retail_sales
WHERE category = 'Clothing'
AND quantity > 10
AND sale_date BETWEEN '2022-11-01' AND '2022-11-30';
Total Sales by Category:
sql
Copy code
SELECT category, SUM(total_sale) AS revenue
FROM Retail_sales
GROUP BY category;
Average Age of Customers Who Bought Beauty Products:
sql
Copy code
SELECT category, AVG(age)
FROM Retail_sales
WHERE category = 'Beauty'
GROUP BY category;
Transactions with Total Sales Greater than 1000:
sql
Copy code
SELECT * FROM Retail_sales WHERE total_sale > 1000;
Total Transactions by Gender and Category:
sql
Copy code
SELECT category, gender, COUNT(*) AS transactions
FROM Retail_sales
GROUP BY category, gender
ORDER BY category;
Average Sales per Month & Best-Selling Month:
sql
Copy code
SELECT * FROM (
    SELECT
        YEAR(sale_date) AS year,
        MONTH(sale_date) AS month,
        AVG(total_sale) AS avg_sale,
        RANK() OVER (PARTITION BY YEAR(sale_date) ORDER BY AVG(total_sale) DESC) AS rank
    FROM Retail_sales
    GROUP BY year, month
) AS ranked_sales
WHERE rank = 1;
Top 5 Customers by Total Sales:
sql
Copy code
SELECT customer_id, SUM(total_sale) AS total_sales
FROM Retail_sales
GROUP BY customer_id
ORDER BY total_sales DESC
LIMIT 5;
Unique Customers per Category:
sql
Copy code
SELECT COUNT(DISTINCT(customer_id)), category
FROM Retail_sales
GROUP BY category;
Conclusion
This project demonstrates how SQL can be used for powerful data analysis in retail sales. We have uncovered valuable insights into customer purchasing patterns, sales performance across categories, and identified key customer segments. These insights can help a retail shop make data-driven decisions.
