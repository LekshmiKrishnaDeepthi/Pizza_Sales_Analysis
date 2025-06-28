**Pizza Sales Analysis Project**

**Tools Used: SQL Server Management, MS Excel**

**A. KPIs**

**Total  Revenue generated** 
SELECT SUM(total_price) AS total_revenue FROM pizza_sales;

**Average Order Value**
SELECT CAST(SUM(total_price)/COUNT(DISTINCT order_id) AS DECIMAL(10,2)) AS Avg_Order_Value 
FROM pizza_sales;

**Total Pizza Sold**
SELECT CAST(SUM(quantity) AS DECIMAL(10,0)) AS Total_Pizza_Sold
FROM pizza_sales;

**Total Orders**
SELECT COUNT(DISTINCT order_id) AS Total_Orders
FROM pizza_sales;

**Average Pizzas per Order**
SELECT CAST(CAST(SUM(quantity) AS DECIMAL(10,2))/ CAST(COUNT(DISTINCT order_id) AS DECIMAL(10,2)) 
AS DECIMAL(10,2)) AS UPT
FROM pizza_sales;

**B. Daily Trends for Orders**
SELECT DATENAME(DW,order_date) AS Week_Day, COUNT(DISTINCT(order_id)) AS Total_orders
FROM pizza_sales
GROUP BY DATENAME(DW,order_date), DATEPART(DW,order_date)
ORDER BY DATEPART(DW,order_date);

**C. Hourly Trend of Orders**
SELECT DATEPART(HOUR,order_time) AS No_of_Orders, COUNT(DISTINCT(order_id)) AS Total_orders
FROM pizza_sales
GROUP BY DATEPART(HOUR,order_time)
ORDER BY DATEPART(HOUR,order_time);

**D. Percentage of Sales by Category**
SELECT pizza_category,CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Sales,
CAST(SUM(total_price)*100/(SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS Sales_Percentage
FROM pizza_sales
GROUP BY pizza_category;

**E. Percentage of Sales by Pizza Sales**
SELECT pizza_size,CAST(SUM(total_price) AS DECIMAL(10,2)) AS Total_Sales,
CAST(SUM(total_price)*100/(SELECT SUM(total_price) FROM pizza_sales) AS DECIMAL(10,2)) AS Sales_Percentage
FROM pizza_sales
GROUP BY pizza_size;

**F. Total Pizzas Sold by Pizza Category**
SELECT pizza_category,SUM(quantity) AS Quantity_Sold
FROM pizza_sales
GROUP BY pizza_category;

**G. Top 5 Best Sellers by Total Pizzas Sold**
SELECT TOP 5 pizza_name,SUM(quantity) AS Quantity_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Quantity_Sold DESC;

**H. Bottom 5 Best Sellers by Total Pizzas Sold**
SELECT TOP 5 pizza_name,SUM(quantity) AS Quantity_Sold
FROM pizza_sales
GROUP BY pizza_name
ORDER BY Quantity_Sold ASC;


