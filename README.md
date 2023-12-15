# Pizza Sales Analysis

## Table of Contents

- [Project Overview](#project-overview)
- [Data Sources](#data-sources)
- [Tools](#tools)
- [Data Cleaning/Preparation](#data-cleaningpreparation)
- [Exploratory Data Analysis](#exploratory-data-analysis)
- [Data Analysis](#data-analysis)
- [Data Visualization](#data-visualization)
- [Results/Findings](#resultsfindings)

### Project Overview
This project aims to analyze key indicators for the pizza sales data in order to gain insights into the business performance.





### Data Sources
Sales Data: The Primary dataset used for this analysis is the "pizza_sales.csv" file, containing detailed information about each sale made by the company.

### Tools
- Power Query Editor - Data Cleaning
- SQL Server - Data Analysis
- Power BI - Creating Reports/Visualization

### Data Cleaning/Preparation
In the Initail data preparation phase, I performed the following tasks;
-  Data Loading and Inspection
-  Data Cleaning and Formatting
-  Date Extraction

### Exploratory Data Analysis
EDA involved exploring the sales data to answer key questions, such as;
1. Daily/Monthly Trend for Total Orders
2. Percentage of Sales per Pizza Category/Size
3. Top 5 Best sellers by Total Revenue, Quantity & Order.
4. Bottom 5 Best sellers by Total Revenue, Quantity & Order.

### Data Analysis

```SQL
Select * from pizza_sales;
 
 --1. Total Revenue
Select 
 round(SUM(total_price), 2) AS total_revenue
 FROM pizza_sales
 ;

 -- 2. Average order value
 SELECT 
  SUM (total_price) / COUNT(DISTINCT order_id) AS Avg_order_value
  FROM pizza_sales
  ;

  -- 3. Total Pizza sold
   SELECT
   SUM (quantity) AS Total_sales
   FROM pizza_sales
  ;

  -- 4. Total orders placed

SELECT COUNT (DISTINCT order_id) AS Total_order
FROM pizza_sales
  ;

  --5. Average Pizza per order
  SELECT SUM (quantity)/ COUNT (distinct order_id) AS Avg_pizza_order
  FROM pizza_sales
  ;

  ----------------------------------------------

  -- 6. Daily Trend for total orders
  SELECT
  DATENAME (DW,order_date) as order_day, 
  COUNT (distinct order_id) AS Total_orders

  FROM pizza_sales
  GROUP BY DATENAME (DW, order_date)
  ;

  -- 7. Monthly Trends for total orders
  SELECT
  DATENAME(MONTH, order_date) AS Month_Name,
  COUNT (DISTINCT order_id) AS Total_orders
  FROM pizza_sales
  GROUP BY DATENAME(MONTH, order_date)
  ORDER BY 2 DESC
  ;

  -- 8. Percentage of sales by pizza category
   Select  
   pizza_category, SUM(total_price)  AS Total_sales, 
   SUM(total_price) * 100  / (SELECT sum(total_price) From pizza_sales) AS Percentage
   
   FROM pizza_sales
   GROUP BY pizza_category
   
   ;
 
  -- 9. Percentage of sales by pizza size

   Select  
   pizza_size, ROUND(SUM(total_price), 2) AS Total_sales, 
   ROUND(SUM(total_price) * 100  / (SELECT sum(total_price) From pizza_sales),2) AS Percentage
   
   FROM pizza_sales
   GROUP BY pizza_size
   ORDER BY Percentage DESC
   
   ;
 

 --10.  Total Pizza sold by pizza category
     SEE NUMBER 8.

  -- 11. TOP 5 BEST SELLERS BY REVENUE, QUANTITY & TOTAL ORDERS

  SELECT TOP 5
  pizza_name,
  SUM (total_price) AS Total_Revenue

  FROM pizza_sales
  GROUP BY pizza_name
  Order by Total_Revenue desc
;

SELECT TOP 5
  pizza_name,
  COUNT (DISTINCT order_id) AS Total_orders

  FROM pizza_sales
  GROUP BY pizza_name
  Order by Total_orders desc
;

SELECT TOP 5
  pizza_name,
  SUM (quantity) AS Total_quantity

  FROM pizza_sales
  GROUP BY pizza_name
  Order by Total_quantity desc
; 
```

### Data Visualization

![Pizza sales dashboard](https://github.com/Uzoblisz/Pizza-Sales-Project/assets/114764715/8960c033-88c3-413d-ac99-745e7088182e)

### Results/Findings

The analysis  results are summarized as follows;

