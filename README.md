# BRIGGS-COMPANY-ANALYSIS
Analysis of Briggs company using SQL(Structured Query Language)

-MOVIE DATA QUERIES

-QUESTION 1: WRITE A QUERY TO SHOW THE TITLES AND MOVIES RELEASED IN 2017 WHOSE VALUE COUNT IS MORE THAN 15 AND RUN TIME IS MORE THAN 100.

```sql
USE MOVIEDATA
SELECT * FROM moviedata


select original_title 
from moviedata
where vote_count > 15
AND release_date like  '%2017%'
AND runtime > 100
```

![QUERY 1  MOVIE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/58f717cb-e2ea-4f5e-b143-508f0ced6c85)


-WRITE A QUERY TO SHOW HOW MANY PIZZAS WERE ORDERED

```sql
use PIZZADATA
select * FROM orders

select count(order_id) as total_pizza_order
from orders
```
![QUERY 1  PIZZA DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/317a4211-89fe-4479-8a79-194d05b74c63)


-WRITE A QUERY TO SHOW HOW MANY SUCCESSFUL ORDERS WERE DELIVERED BY EACH RUNNER.

```sql
SELECT * FROM runnerorders

select runner_id, count(runner_id) as number_of_successful_orders
from runnerorders
where cancellation is null
group by runner_id
```
![QUERY 2  PIZZA DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/cd48306b-4939-48e1-af36-af60f79a5d56)


-WRITE A QUERY TO SHOW THE TOP 10 MOVIE TITLES WHOSE LANGUAGE IS ENGLISH AND FRENCH AND THE BUDGET IS MORE THAN 1,000,000.

```sql
USE MOVIEDATA
SELECT * FROM moviedata

SELECT TOP 10 original_title
from moviedata
where original_language in('en','fr') 
and [ budget ] > 1000000
```
![QUERY 2 MOVIE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/673529a6-fadc-4ca9-a532-a823d08332fd)


-WRITE A QUERY TO SHOW THE NUMBER OF EACH TYPE OF PIZZA THAT WAS DELIVERED
```sql
USE PIZZADATA
SELECT * FROM runnerorders
SELECT * FROM pizzanames

select p.pizza_name,count(o.pizza_id) as pizza_deliveries
from orders o
join pizzanames p
on o.pizza_id = p.pizza_id
where o.order_id in (select order_id from runnerorders where cancellation is null)
group by p.pizza_name

```

![QUERY 3  PIZZA DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/8eadbe9c-afda-4596-8b43-fca128ca418d)



-THE BRIGGS COMPANY WANTS TO SHIP SOME OF THEIR PRODUCT TO CUSTOMERS IN SELECTED CITIES BUT THEY WANT TO KNOW THE AVERAGE DAYS IT WILL TAKE TO DELIER SOME ITEMS TO 
--DALLAS,LOS ANGELES,SEATTLE AND MADISON
```sql

USE SUPERSTORE
SELECT * FROM Orders

select city,avg( DATEDIFF(day,[Order Date],[Ship date])) as average_delivery_days
from Orders
where city in ('Dallas', 'Los Angeles','Seattle', 'Madison')
group by City
```
![QUERY 1  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/6e4d9269-9caa-44fb-b425-d5e129a7f8a9)


-ITS GETTING TO THE END OF THE YEAR AND THE BRIGGS COMPANY WANTS TO REWARD THE CUSTOMER WHO MADE THE HIGHEST SALES EVER. WRITE A QUERY TO HELP THE COMPANY IDENTIFY 
THIS CUSTOMER AND CATEGORY OF BUSINESS DRIVING SALES
```sql
SELECT top 1 [Customer Name], Category, round(sum(sales),0) as total_sales
from Orders
group by [Customer Name],Category
order by total_sales desc
```
![QUERY 2  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/7ea8cc09-f582-417c-a409-a49216be4a06)


-THE BRIGGS COMPANY HAS 3 CATEGORIES OF BUSINESS GENERATING REVENUE FOR THE COMPANY.THEY WANT TO KNOW WHICH OF THEM IS DRIVING THE BUSINESS. WRITE A QUERY TO SHOW THE TOTALS SALES AND PERCENTAGE CONTRIBUTION BY EACH COUNTRY.
```sql
USE SUPERSTORE
SELECT category, ROUND(sum(sales),0) as total_sales, CONCAT(ROUND(sum(sales) / (select sum(sales) from Orders) * 100,0), '%') as percentage_contribution
from Orders
group by Category
order by percentage_contribution desc
```

![QUERY 4  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/2f37edf2-cef0-4809-b9b2-4b18cd09a8d9)

-AFTER SEEING THE SALES BY CATEGORY, THE BRIGGS COMPANY BECAME CURIOUS AND WANTED TO GET DEEPER TO SEE WHICH SUBCATEGORY IS SELLING THE MOST.
```sql
SELECT [Sub-Category], round(sum(sales),1) as total_sales
from Orders
group by [Sub-Category]
order by total_sales desc;
```
![QUERY 3  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/66dc1e6d-fb95-45d3-ba32-131653876e10)


-NOW THAT YOU IDENTIFIED PHONES AS THE BUSINESS DRIVER IN TERMS OF REVENUE. THE COMPANY WANTS TO KNOW THE TOTAL PHONES SALES BY YEAR TO UNDERSTAND HOW EACH YEAR PERFORMED.
```sql
SELECT * FROM Orders

SELECT SUM(Sales) as total_sales, DATEPART(year,[Order Date]) as sales_year_column 
from Orders
where [Sub-Category] = 'phones'
group by  DATEPART(year,[Order Date])
order by total_sales desc
```

![QUERY 5  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/e3fa2ad3-7055-4b11-a4f5-e86fc4ddb570)



-THE DIRECTION OF ANALYTICS IN BRIGGS COMPANY HAS REQUESTED FOR A DETAILED ANALYSIS.TO FULFILL HIS REQUEST, HE NEEDS YOU TO GENERATE A TABLE THAT DISPLAYS PROFIT MARGIN FOR EACH SEGMENT
```sql
USE SUPERSTORE
SELECT segment, round(sum(sales),0) as total_sales, round(sum(profit),0) as total_profit, concat(round(((sum(Profit)/sum(Sales)) * 100),2), '%') as profit_margin
FROM Orders
group by Segment
ORDER BY profit_margin desc
```

![QUERY 6  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/d44fcfc1-cb65-4ff0-8b28-739e5728557b)


-THECOMPANY STARTED CONSULTING FOR MICROBANK WHO NEEDS TO ANALYSE THEIR MARKETING DATA TO UNDERSTAND THEIR CUSTOMER BETTER. THIS WILL HELP THEM PLAN THEIR NEXT MARKETING
CAMPAIGN.YOU ARE BROUGHT ON BOARD AS THE ANALSYST FOR THE JOB. THEY HAVE AN OFFER FOR COUSTOMERS WHO ARE DIVORCED BUT THEY NEED DATA TO BACK UP THE CAMPAIGN. USING THE
MARKETING DATA, WRITE A QUERY TO SHOW THE PERCENTAGE OF CUSTOMERS WHO ARE DIVORCED AND HAVE BALANCES GREATER THAN 2000
```sql
USE marketingdata
SELECT CONCAT(ROUND((CAST(COUNT(*) as real)/(SELECT COUNT(*) FROM marketingdata) * 100), 2), '%')
FROM marketingdata
WHERE marital = 'Divorced'
AND balance > 2000
```

![QUERY 1  MARKETING DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/64d436a0-8929-400b-9153-9359c48d6f4b)

-MICRO BANK WANTS TO BE SURE THEY HAVE ENOUGH DATA FOR THE CAMPAIGN AND WOULD LIKE TO SEE THE TOTAL COUNT OF EACH JOB AS CONTAINED IN THE DATASET.
```sql
USE marketingdata
SELECT * FROM marketingdata
SELECT job, count(job) as job_count
from marketingdata
group by job
order by job_count desc
```
![QUERY 2  MARKETING DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/4a41883b-d30e-416b-88cc-ea0ce06511a3)


-THE MANAGER WANTS TO KNOW WHICH EDUCATION LEVEL GOT THE MOST MANAGEMENT JOB
```sql
SELECT education, job, count(job) as job_count
from marketingdata
where job= 'management'
group by job,education
order by job_count
```
![QUERY 3  MARKETING DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/e2f59c82-c5b8-41de-ab86-4519e16bdf05)


-WRITE A QUERY TO SHOW THE AVERAGE DURATION OF CUSTOMERS EMPLOYMENT IN THE MANAGEMENT POSITIONS. THE DURATION SHOULD BE IN YEARS
```sql
SELECT concat(round(AVG(duration/52),2),' ', 'years') as average_duration
from marketingdata
where job = 'management'
```
![QUERY 4  MARKETING DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/6adfdc73-da2c-49f1-a7df-c9953841d09e)



-WHAT IS THE TOTAL NUMBER OF CUSTOMERS THAT HAVE HOUSING, LOAN, AND ARE SINGLE?
```sql
SELECT housing, loan, marital, count(*) as total_customers
from marketingdata
where housing = 'yes'
and   loan = 'yes'
and   marital = 'single'
group by housing, loan, marital
order by total_customers
```

![QUERY 5  MARKETING DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/c16940be-bb61-4bc1-b731-987cd6df4d34)



-write a query to show the movie title with the runtime of atleast 250
```sql
SELECT title, runtime
FROM moviedata
where runtime > 250
order by runtime desc
```

![QUERY 3  MOVIE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/50eab065-ecce-4405-be5c-b566606d0716)


-write a query to show the employees first name, last name and their respective salaries. also show the average salary ofthe compay and also calculate the difference between each employees salary and the company average salary
```sql
use [EMPLOYEE DATA]
select first_name,
last_name, 
salary, 
(select avg(salary) from Employee_data) as company_avg_salary,
(salary - (select avg(salary) from Employee_data)) as salary_difference
from Employee_data
```

![QUERY 1  EMPLOYEE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/fb47ae8e-a46e-48ce-9809-10c1065413fa)

-write a query to show a table that displays the highest daily increase and the highest daily decrease
```sql
select round(max(_close - _open), 2) as highest_daily_increase,
min(_close - _open) as highest_daily_decrease
from share_price
```
![QUERY 2  EMPLOYEE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/dab2d1e4-da25-4451-b194-3e7088502173)

-OUR CLIENT IS PLANNING THEIR LOGISTICS FOR 2024, THEY WANT TO KNOW THE AVERAGE NUMBER OF DAYS IT TAKES TO SHIP TO THE TOP 10 STATES 
```sql
USE SUPERSTORE
 SELECT  Top 10 State,  AVG(datediff(day,[Order Date], [Ship Date])) as average_days
 FROM Orders
 GROUP BY State
 order by average_days
```

![QUERY 7  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/8d069e32-d34a-4859-8092-d52e95b4d0b1)

 
-Your company recieved a lot of bad reviews about somes of your products lately and the management wants to see which products they are and how many have been returned so far. write a query to see the top 5 most returened products from the company
```sql
	select * from Returns$
 select top 5 o.[Product Name], o.[Product ID], count([Product ID]) as product_count
 from Orders o
 join Returns$ r
 on o.[Order ID] = r.[Order ID]
 where r.Returned = 'yes'
 group by o.[Product ID], o.[Product Name]
 order by product_count desc
```
![QUERY 7  SUPERSTORE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/35eb5673-bf20-48a6-b9b8-c127c08fa019)


-using the employee dataset, write a query to show the ratio of the analyst job title to the entire job titles
```sql
 use [EMPLOYEE DATA]
 select sum( case when job_title = 'Analyst' then 1 else 0 end) as analyst_count,
 sum( case when job_title = 'Analyst' then 1 else 0 end) * 100/ count(*)  as analyst_to_total_ratio
 from Employee_data
```
![QUERY 3  EMPLOYEE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/ce1965ff-23ec-4492-a5d6-b6543468bead)

 
-write a query to show the job title and department with the highest salary
```sql
 SELECT top 1 job_title, department
 FROM Employee_data
 where salary = (select max(salary) from Employee_data)
```
![QUERY 4  EMPLOYEE DATA](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/06dfd121-cc54-4355-a5ea-708885ac1277)


-Write a query to determine the rank of each employee based on their salaries in each department . for each department, find the employee(s) with the highest salary and rank them in desc order
```sql
 select first_name, 
 last_name, 
 department, 
 salary, 
 RANK() over( partition by department order by salary desc) as salary_rank
 from Employee_data
```

![Screenshot (127)](https://github.com/Abasiifrekefriday/BRIGGS-COMPANY-ANALYSIS/assets/108738787/23158634-9d15-4493-88aa-52894844f1a5)





