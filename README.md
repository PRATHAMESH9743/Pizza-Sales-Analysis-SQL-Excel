# PIZZA SALES ANALYSIS - SQL SERVER / EXCEL 2023

This project delves deep into the realm of data analysis, utilizing SQL and EXCEL to uncover crucial insights into Pizza sales. The featured eye-catching dashboards aid the pizza business in making informed decisions and strategic workforce planning, providing substantial benefits to the business.

Source Data:
pizza sales.csv
The source data contained Pizza sales 48621 records of year 2015. This is included in the repository.

## Database and Tools
1. MySQL
2. EXCEL

## PROBLEM STATEMENT
### A. KPI’s
Analyze the key indications for our pizza sales data to gain insights into our business performance. specifically, to calculate the following metrices:

1. Total Revenue:
   
   The sum of the total price of all pizza orders.
2. Average Order Value:
   
   The average amount spent per order, calculate by dividing the total revenue by the total numbers of orders.
3. Total Pizzas Sold:
   
   The sum of the quantities of all pizzas sold.
4. Total orders:
   
   The total numbers of orders placed.
5. Average Pizzas Per Order:
   
   The average number of pizzas sold per order, calculated by dividing the total number of pizzas sold  by the total numbers of orders.

 ## CHARTS REQIREMENTS
 To visualize various aproach of our pizza sales data to gain insights and understand key trends. we have identified the following requirements for creating charts:

1. Daily Trend For Total Orders:

   Create a bar chart that displays the daily trend of total orders over a specific time period. this chart will help us identify any patterns or fluctuations in order volumes on a daily 
   basis.
3. Monthly Trend for Total Orders:

   Create a line chart that illustrates the hourly trend of total orders throughout the day. This chart will allow us to identify peak hours or periods of high order activity.
5. Percentage of Sales by Pizza Category:

   Create a pie chart that shows the distribution os sales across different pizza categories. this chart will provide insights into the popularity of various pizza categories and their 
   contributions to overall sales      
4. Percentage of Sales by pizza size:

   Generate a pie chart that represents the percentage of sales attributed to different pizza sizes. this chart will help us undertsand customer preferences for pizza sizes and their impact 
   on sales.
5. Total Pizzas Sold by Pizza Category:

   Create a funnel chart that presents the total number of pizza sold for each pizza category. This chart will allow us to compare the sales performance of different pizza categories.
6. Top 5 Best Sellers by Revenue, Total Quality and Total Orders:

   Create a bar chart highlighting the top 5 best selling pizza based on the revenue. Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.
7.  Bottom 5 Worst Sellers by Revenue, Total Quality and Total Orders:

    Create a bar chart showcasing the bottom 5 worst selling pizza based on the revenue. Total Quantity, Total Orders. This chart will help us identify the most popular pizza options.

## Open Microsoft SQL Server Management Studio
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/eace9bfc-add8-4153-9c49-fa95cc7a024b)

 ### 1) Create Database
``` SQL
CREATE DATABASE Pizza_sales;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/96c8a885-a05b-4e59-8e72-866052f85798)

   ### 2) Import Data to SQL Server
- Right-click on  Pizza_sales > Tasks > Import Data
- Use import wizard to import Pizza_sales.csv.
- ![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/0af2635a-b60d-4ec6-aa1c-0d358ac06a0f)
  
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/0157c838-e670-466a-b009-362750b83135)

![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/58cb2583-cdd9-466a-8cfe-ef66c95accd3)

![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/2eabe31f-71e5-4ecc-9fdb-5034aa2174ef)

## 3) DATA CLEANING (we should modify the column)
## 1. change nvarchar(50) to varchar(50)
   
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/5a58ca6b-a55f-4d53-b474-39b7eb342ff3)

## 2. Pizza ingredients should be changed from nvarchar(50) to varchar(100), because the pizza ingredients length text is more , so change it to varchar(100).


![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/cd07ebd4-e74c-440d-a45e-797874023801)

## Change the pizza_id from small integer(smallint) to integer(int) and order_id from tiny integer(tinyint) to integer(int), 
Because the data is in 48621, then the id will be in thousands of numbers (the id will be of more integers), so it should not be in the small integers(smallint) so change it to integers(int), same should be done in case of the order id - change it to integers(int).
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/16ceeaa9-dbc6-4168-b9b7-29397143988b)

-  Verify that the import worked:
  
``` SQL
 use Pizza_sales;
```
``` SQL
select * from Pizza_sales;
```
## PIZZA SALES SQL QUERIES
A. KPI’s
## 1. Total Revenue:
``` SQL
SELECT SUM(total_price) AS Total_Revenue FROM pizza_sales;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/178c7a77-d096-475d-9c74-c282a23b7637)

## 2. Average Order Value

```SQL
SELECT (SUM(total_price) / COUNT(DISTINCT order_id)) AS Avg_order_Value FROM pizza_sales;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/22ba3003-edb6-4c2e-8df5-8a87f37902bc)

## 3. Total Pizzas Sold

```SQL
SELECT SUM(quantity) AS Total_pizza_sold FROM pizza_sales;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/71929715-202a-4b21-8569-42673d8ab47f)

## 4. Total Orders

 ```SQL
SELECT COUNT(DISTINCT order_id) AS Total_Orders FROM pizza_sales;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/baa89765-ad76-4669-bb1e-69fe06080f15)
  
## 5. Average Pizzas Per Order
 ```SQL
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2)) / 
CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS DECIMAL(10,2))
AS Avg_Pizzas_per_order
FROM pizza_sales;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/4e20ec8f-600b-4f40-b501-dbd59753f30b)

## B. Daily Trend for Total Orders
 ```SQL
SELECT DATENAME(DW, order_date) AS order_day, COUNT(DISTINCT order_id) AS total_orders 
FROM pizza_sales
GROUP BY DATENAME(DW, order_date);
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/26b7e461-2433-4a1d-a7fa-d511410d320f)

## C. Monthly Trend for Orders
```SQL
select DATENAME(MONTH, order_date) as Month_Name, COUNT(DISTINCT order_id) as Total_Orders
from pizza_sales
GROUP BY DATENAME(MONTH, order_date);
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/e286e688-ca46-4980-8fc3-e14fee86fa08)

## D. % of Sales by Pizza Category
```SQL
SELECT pizza_category, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_category;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/686eb282-ce75-4644-b57d-521b066af1ba)

## E. % of Sales by Pizza Size
```SQL
SELECT pizza_size, CAST(SUM(total_price) AS DECIMAL(10,2)) as total_revenue,
CAST(SUM(total_price) * 100 / (SELECT SUM(total_price) from pizza_sales) AS DECIMAL(10,2)) AS PCT
FROM pizza_sales
GROUP BY pizza_size
ORDER BY pizza_size;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/8248d570-433e-4861-be5e-ed41a98d1492)


## F. Total Pizzas Sold by Pizza Category
```SQL
SELECT pizza_category, SUM(quantity) as Total_Quantity_Sold
FROM pizza_sales
WHERE MONTH(order_date) = 2
GROUP BY pizza_category
ORDER BY Total_Quantity_Sold DESC;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/91371af4-620b-449a-97ab-460b328c5b2e)

## G. Top 5 Pizzas by Revenue
```SQL
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue DESC;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/cbdff847-d115-4c11-b964-68b089387a31)

## H. Bottom 5 Pizzas by Revenue

```SQL
SELECT Top 5 pizza_name, SUM(total_price) AS Total_Revenue
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Revenue ASC
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/b3117fc4-3331-4661-a570-5cb13c3c0142)

## I. Top 5 Pizzas by Quantity
```SQL
SELECT Top 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold DESC;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/7c752882-2cac-46b2-b14f-a9ebc7f9c6e7)

## J. Bottom 5 Pizzas by Quantity
```SQL
SELECT TOP 5 pizza_name, SUM(quantity) AS Total_Pizza_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Pizza_Sold ASC;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/6ade3001-8aa0-434e-9c26-5b57df57bd63)

## K. Top 5 Pizzas by Total Orders
```SQL
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders DESC;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/f0edd654-1e09-4560-80b6-08759e0d60bb)

## L. Bottom 5 Pizzas by Total Orders
```SQL
SELECT Top 5 pizza_name, COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Total_Orders ASC;
```
![image](https://github.com/PRATHAMESH9743/PIZZA-SALES-ANALYSIS/assets/154798147/c96c898d-bad6-41af-9f42-9610626298b6)


## Connecting Excel to MS SQL Server
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/bbd42149-7046-4a70-b4e9-693ae7ffd6b5)
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/183f072e-a2d4-4b55-b1f0-b3e2babcb696)


## Data Cleaning
Now we have to clean the data, here we will select the entire column of pizza size and replace the values , we will find the M size in the pizza size coulmn and replace it with Medium and same goes for the L and S , change them to Large and Regular  
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/40840b6d-1bdd-401d-9515-7a18bdf1e213)

## Data processing 
in order to calculate the order day, we will select the entire order date column and extract the order day from the order date 

step1. create a new column as order day and use the formula (text) and extract the order day from order date
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/6e8d5450-c681-4325-8a01-dd039adf417d)
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/5c9d13b2-4c98-4f7e-940b-b89b4c96f060)

## PIVOT TABLE
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/2723cab8-7d0b-4caf-8193-f329f48fdd8c)

KPI'S CREATION
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/30fb911c-3b9b-4ea5-b19b-c8b33331ed2f)

## DASHBOARD CREATION
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/b90e2900-a3c0-45a4-913d-c954e057ab01)

## B. Daily Trend for Total Orders.  # C. Hourly Trend for Orders
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/fe892789-1482-41dd-95e0-554b43f91bae)
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/2cba176a-e32c-4435-883e-0cd519542eca)

## D. % of Sales by Pizza Category.  # E. % of Sales by Pizza Size  # F. Total Pizzas Sold by Pizza Category
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/ffebe542-a1ee-4c6a-982d-f7971985ba41)
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/ddc7696e-d42d-4464-928d-63aa7fe30311)

## G. Top 5 Best Sellers by Total Pizzas Sold. # H. Bottom 5 Best Sellers by Total Pizzas Sold
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/f4471b4d-3bf3-4852-872d-0d6b456c1a73)
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/fcc91e9d-d032-4b20-a281-a0ca7aa318f0)

## INSIGHTS
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/1b3b73f9-aa25-4c87-b9b5-6199d594501e)

## DASHBOARD OVERVIEW
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/f3465287-0f17-45e8-9d4b-03db56ef3222)

## COMPLETE DASHBOARD
![image](https://github.com/PRATHAMESH9743/Pizza-Sales-Analysis-SQL-Excel/assets/154798147/1e22e22b-9f7a-4ae5-8690-034aea386857)

