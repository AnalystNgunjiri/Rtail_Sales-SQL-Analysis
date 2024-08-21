## 1. Database Set up

### Database creation
The project starts by creating a database named 'Retail_sales_db'.

### Table Creation
 A table named 'Retail_Sales' is created to store the data. The table structure colums for transaction id, sales date. sales time, customer id,gender,age product category, quantity sold, price per unit, cost of goods sold,cogs and total sales.



**sql**
CREATE DATABASE sql_project_p2;

CREATE TABLE retail_sales
            (
                transaction_id INT PRIMARY KEY,	
                sale_date DATE,	 
                sale_time TIME,	
                customer_id	INT,
                gender	VARCHAR(15),
                age	INT,
                category VARCHAR(15),	
                quantity	INT,
                price_per_unit FLOAT,	
                cogs	FLOAT,
                total_sale FLOAT
            );
'''
### 2. Data Exploration & Cleaning

-**Record Count**: Determine the total number of records in the dataset.
-**Customer Count**: Find the number of unique customers in the dataset.
-**Category Count**: Identify all unique products categories in the dataset
-**Null Value Check**: Checks for al null values in the dataset and delete records with missing data.



'''sql
    select count(*) from retail_sales;
    select distinct(count customer_id) from retail_sales;
    select distinct category from retail_sales;
    select * from retail_sales
    where
    sales_date is null or sales_time is null or customer_id is null or gender is null 
    or age is null or category is null or quantity is null or price_per_unit is null or cogs is numm;

   DELETE FROM retail_sales
   WHERE 
    transaction_id IS NULL
    OR sale_date IS NULL
    OR sale_time IS NULL
    OR gender IS NULL
    OR category IS NULL
    OR quantity IS NULL
    OR cogs IS NULL
    OR total_sale IS NULL;  
'''


### 3. Data analysis & Finding

The following sql queries were developed to answer specific business questions:
1. **Retieve sales made on specific date**

   
'''sql
   SELECT *
   FROM retail_sales
   WHERE sale_date = '2022-11-05';
'''


2. **Q.1 Write a SQL query to retrieve all columns for sales made on '2022-11-05**


'''
   SELECT *
   FROM retail_sales
   WHERE 
    category = 'Clothing'
    AND 
    TO_CHAR(sale_date, 'YYYY-MM') = '2022-11'
    AND
    quantity >= 4
'''   

 
 3. **Calculate the total sales per category**

    
'''
    SELECT 
    category,
    SUM(total_sale) as net_sale,
    COUNT(*) as total_orders
    FROM retail_sales
    GROUP BY 1
'''


4. **Write a SQL query to find the average age of customers who purchased items from the 'Beauty' category.**

   
'''
    select round(avg(age), 2) as avg_sales
    from retail_sales
    where category = 'Beauty';
'''


5. **Write a SQL query to find all transactions where the total_sale is greater than 1000.**

   
'''
  SELECT * FROM retail_sales
  WHERE total_sale > 1000
'''


6. **Write a SQL query to find the total number of transactions (transaction_id) made by each gender in each category.**

    
'''
 SELECT 
 category,
 gender,
 COUNT(*) as total_trans
FROM retail_sales
GROUP BY category, gender
ORDER BY 1
'''


7. **Write a SQL query to calculate the average sale for each month. Find out best selling month in each year**

    
'''
SELECT  year,
month,
rank
FROM
(	
select
EXTRACT(YEAR FROM sales_date) as year,
EXTRACT(MONTH FROM sales_date) as month,
AVG(total_sales) as avg_sale,
rank() over(partition by EXTRACT(YEAR FROM sales_date) order by AVG(total_sales) DESC ) as rank
FROM retail_sales
GROUP BY 1, 2
) as T1
where rank = 1


SELECT 
EXTRACT(YEAR FROM sales_date) as year,
EXTRACT(MONTH FROM sales_date) as month,
AVG(total_sales) as avg_sale,
rank() over(partition by EXTRACT(MONTH FROM sales_date) order by AVG(total_sales) DESC )
FROM retail_sales
GROUP BY 1, 2
'''
	


8. **WWrite a SQL query to find the top 5 customers based on the highest total sales .**

   
'''
select 
total_sales as highest
from retail_sales 
order by highest desc
limit 5
'''



9. **Write a SQL query to find the number of unique customers who purchased items from each category.**

    
'''
select 
category,
count(transaction_id) as Unique_id
from retail_sales 
group by category
'''



10. **Write a SQL query to create each shift and number of orders (Example Morning <=12, Afternoon Between 12 & 17, Evening >17)**

    
'''
select * from retail_sales

with hourly_sales
as
(
SELECT *,
CASE
when EXTRACT(hour from sales_time) < 12  then 'Morning'
when EXTRACT(hour from sales_time) between 12 and 17 then 'Afternoon'
else 'Evening'
end as Shift
from retail_sales	
)
select 
shift,
count(*)as total_orders
from hourly_sales
group by shift
'''

## Findings

-**Customer Demographics**: The dataset includes customres from various age groups, with sales distributed across different categories such as clothing and buauty.

-**High-Value Transaction**: Some transaction had a total sale amount ore that 1000, indication premium sales.

-**Sales Trend**: Monthly analysis shows variation in slaes, helping identify peak saeson.

-**Customer Insights**: The analysis identifies the top speding customers and the most popular products category.



## Reports

-**Sales Summary**: A detailed report summarizing total sales, customer demographics and category perfomance.

-**Trend Analysis**: Insights into sales trends across different months and shifts.


## Conclusion

This pproject serves a comprehensive introduction to SQL for data analysis, covering database setup, data cleaning, exploratory data analysis and 
business-driven SQL queries. The findoinfg from this project can help drive business decisions by understaxnding sales patterns, customer behavior
and product perfomance.


## How to use
1. **Clone the Repository**: Clone this project repository from GitHub.

2. **Set Up the Database**: Run the script provided in the 'database_setup.sql' file to create and populate the database.

3. **Run the Queries**: Use the SQL queries provided in the 'analysis_queries.sql' file to perform your analyis.

4. **Explore and Modify**: Feel free to modify the queries to explore different aspects of the dataset or answer additional business questions.


## Author- AnalystNgunjiri

This project is part of my portfolio, where i showcase the skills essenstial as a data analysts. If you gave any questions, feedback, or would like to collaborate, feel free to get in touch!


## Stay Updated and Join the Community

-**LinkedIn**: [Conect with my profile on the linkedIn page](https://www.linkedin.com/in/isaac-ngunjiri-35429026a)

-**PowerBI Profile**: [Interact with my reporting profile here](https://app.powerbi.com/groups/me/reports/0c5c1ec0-8774-45fc-b5d6-dd3de0ffa709/ReportSection?                 experience=power-bi)

-**Email**: [Reach of via my official mail](ngunjiriisaac6@gmail.com)

Thank you for your support, and I look forward to reconneccting with you.
