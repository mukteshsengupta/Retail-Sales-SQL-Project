🛒 **Retail Sales Analysis using SQL**

📌 **Project Overview**


This project focuses on extracting insights from a retail sales dataset using SQL. By leveraging SQL queries, the project aims to perform in-depth analysis of key metrics such as total revenue, sales trends, product performance, and customer behavior. The dataset includes detailed transactional data which is cleaned and queried to generate meaningful business insights.


🗃️ **Database Objective**

1. Set up a retail sales database: create and populate a retail sales database with the provided sales data
2. Data Cleaning: Identify and remove any records with missing or null values.
3. Exploratory Data Analysis: Perform basic atory data analysis to understand the dataset.
4. Business Analysis: Use SQL to answer specific business questions and derive insights from sales data.


🧱**Project Structure**

1. 🗃️**Database Setup:**

'''sql
create database  project1;
use project1;
'''

'''sql
create table reteil_sales
(
transactions_id int primary key,
sale_date date, 
sale_time time,	
customer_id int,
	gender varchar(10),
    age int,
	category varchar(25),	
    quantiy int,
	price_per_unit float,
    cogs float,	
    total_sale float
    );
'''




2. 🧹**Data Cleaning:**

'''sql

select  * from reteil_sales
where 
sale_date is null
or
sale_time is null
or
customer_id is null
or
gender is null
or
age is null
or
category is null
or
quantiy is null
or
price_per_unit is null
or
cogs is null
or
total_sale is null;
'''





3.🔍 **Data Exploration:**

-- **how many sales we have?**

'''sql
select count(total_sale)
from reteil_sales;
'''

-- **how many customers we have?**
'''sql
select count(distinct customer_id)
from reteil_sales;
'''

-- **types of categories**

'''sql
select distinct category
from reteil_sales;
'''




4.📊  **Business Analysis & Findings**:

-- Q1 **Retrive all columns for sales made on 2022-11-05**

'''sql
select * from reteil_sales
where sale_date = '2022-11-05';
'''


-- Q2 **caluculate the total sales(total_sale) for each category.**


'''sql
select  category, sum(total_sale)
from  reteil_sales
group by category;
'''

-- Q3 **find the average age of customers who purchased items from the beauty category**

'''sql

select 
round (avg(age),2) as avg_age
from reteil_sales
where category = 'Beauty';
'''

-- Q4 **Find all transactions id where the total_sale is greater than 1000**

'''sql
select transactions_id
from reteil_sales
where total_sale > 1000;
'''






-- Q5 **find the total numbar of transactions (id) made by each gender in each catrgory**

'''sql


select 
category,
gender,
count(*)as total_transactions
from  reteil_sales
group by category,gender
order by category
;
'''

-- Q6 calculate the avg sale for each month, find out the best selling monh in each year.

'''sql


SELECT 
    YEAR(sale_date) AS year,
    MONTH(sale_date) AS month,
    ROUND(AVG(total_sale), 2) AS avg_monthly_sale
FROM reteil_sales
GROUP BY YEAR(sale_date), MONTH(sale_date)
ORDER BY year, month;
'''
'''sql
WITH monthly_avg AS (
    SELECT 
        YEAR(sale_date) AS year,
        MONTH(sale_date) AS month,
        ROUND(AVG(total_sale), 2) AS avg_monthly_sale
    FROM reteil_sales
    GROUP BY YEAR(sale_date), MONTH(sale_date)
)
SELECT *
FROM monthly_avg m
WHERE avg_monthly_sale = (
    SELECT MAX(avg_monthly_sale)
    FROM monthly_avg
    WHERE year = m.year
)
ORDER BY year;

'''

