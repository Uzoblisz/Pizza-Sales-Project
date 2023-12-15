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
- [Recommendations](#recommendations)

### Project Overview
This project aims to analyze key indicators for the pizza sales data in order to gain insights into the business performance.

![Pizza Monthly trend](https://github.com/Uzoblisz/Pizza-Sales-Project/assets/114764715/309ca249-06af-4cec-9416-d088892954d9)
![Pizza sales by category](https://github.com/Uzoblisz/Pizza-Sales-Project/assets/114764715/81b68f59-112b-44dc-babd-365c102dde9a)

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

The analysis results are summarized as follows;
1. The Classic Pizza category is the best category in terms of sales and revenue.
2. The company's sales have been steadily increasing over the month, with a noiticeable peak during the month of July before a drastic drop in sales in the month of October.
3. Fridays have the highest orders on a daily basis.
4. The best selling pizza by total quantity and total order is the Classic Deluxe Pizza where as, the Thai chicken Pizza is the best seller by total revenue.
5. The worst sellers by Total Revenue, Quantity & Order are the Spinach Pesto Pizza, the Soppressata pizza and the Chicken Pesto Pizza respectively.

### Recommendations

- Investigate October Sales Drop: Analyze the factors contributing to the drastic drop in sales in October as seasonality, external events, or marketing initiatives during that period may be a contributing factor. Understanding the cause will help in developing strategies to mitigate such drops in the future.
- Optimize Friday Operations: Given that Fridays have the highest orders, there may be a need to optimize staffing and resources to meet the increased demand on Fridays. Consider promotions or special deals on Fridays to capitalize on the peak ordering day.
- Promote Classic Deluxe and Thai Chicken Pizzas: Since the Classic Deluxe Pizza is the best seller by total quantity and total order, and the Thai Chicken Pizza leads in total revenue, focus on promoting these pizzas through special offers or marketing strategies to maximize their sales potential.
- Review and Adjust Pricing Strategy: Evaluate the pricing strategy for the Spinach Pesto Pizza, Soppressata Pizza, and Chicken Pesto Pizza, which are identified as the worst sellers by total revenue, quantity, and order. Consider adjusting prices, running promotions, or even repositioning these items on the menu to improve their performance.
- Explore Seasonal Variations: Given the noticeable peak in sales during July, consider exploring the reasons behind this increase. If it's related to seasonal trends or events, develop targeted seasonal promotions or menu additions to capitalize on similar patterns in the future.
- Collect and analyze customer feedback to understand preferences and areas for improvement. Engage with customers through surveys or social media to gather insights that can inform product development and marketing strategies.
