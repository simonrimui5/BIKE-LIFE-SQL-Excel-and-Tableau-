# BIKE-LIFE-SQL-Excel-and-Tableau-

## Table of Contents

- [Introduction](#introduction)
- [Steps Followed](#steps-followed)
  - [Step 1](#step-1)
  - [Step 2](#step-2)
  - [Step 3](#step-3)
  - [Step 4](#step-4)
- [Analyzing the data ](#analyzing-the-data)
  - [Annual Revenue Analysis](#annual-revenue-analysis)
  - [Monthly Revenue Analysis](#monthly-revenue-analysis)
  - [Statewise Revenue Distribution](#statewise-revenue-distribution)
  - [Brandwise Revenue Distribution](#brandwise-revenue-distribution)
  - [Categorywise Revenue Distribution](#categorywise-revenue-distribution)
  - [Top Customers Analysis](#top-customers-analysis)
  - [Sales Representative Performance Analysis](#sales-representative-performance-analysis)
- [Conclusions](#conclusions)
- [Recommendations](#recommendations)

## Introduction

In this project I combined SQL, Excel and Tableau. Bike Life's (a retail bicycle company) management wanted to know the sales activities of the company to gain insights to the various trends happening in the sales volume over the 2016-2018 period. They also wanted to know the revenue per region, per store, per product category and per brand, a list of the top customers and sales reps was also insightful. Having understood the needs and goals of the company, I needed to present this information in the most organized and digestible way. My number one task was to make the management team’s lives as easy as possible. As such I settled on Excel and Tableau to show the various metrics. Although either Excel or Tableau would have sufficed I needed to use both of them to show my flexibility in this particular project. 

## Steps Followed  

## Step 1

I tapped into the company’s relational database and retrieved the data through sql by writing an sql code to generate a detailed dataset that provided me with all the data and information I needed to put together a dynamic sales dashboard for the executive team.

```sql
SELECT 
	ord.order_id,
	CONCAT(cus.first_name,' ',cus.last_name) AS 'customers',
	cus.city,
	cus.state,
	ord.order_date,
    SUM(ite.quantity) AS 'total_units',
	SUM(ite.quantity * ite.list_price) AS 'revenue',
	pro.product_name,
	cat.category_name,
	sto.store_name,
	CONCAT(sta.first_name,' ',sta.last_name) AS 'sales_rep'
FROM sales.orders ord
JOIN sales.customers cus
ON ord.customer_id=cus.customer_id
JOIN sales.order_items ite
ON ord.order_id=ite.order_id
JOIN production.products pro
ON ite.product_id=pro.product_id
JOIN production.categories cat
ON pro.category_id =cat.category_id
JOIN sales.stores sto
ON ord.store_id = sto.store_id
JOIN sales.staffs sta
ON ord.staff_id = sta.staff_id
GROUP BY
	ord.order_id,
	CONCAT(cus.first_name,' ', cus.last_name),
	cus.city,
	cus.state,
	ord.order_date,
	pro.product_name,
	cat.category_name,
	sto.store_name,
	CONCAT(sta.first_name,' ',sta.last_name);
```

*OUT 1*

![sql table](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/2076f2cc-1541-48e4-ad20-2d45499be12d)


## Step 2
I created a new workbook in Excel and called it Bike stores. I connected the entire Excel workbook to the company’s database and then imported the data set directly into the worksheet which formed a connection between the work book and the data base so that any changes made in the database are automatically reflected in the Excel version of the data set sparing me the trouble of manually having to update the Excel version of the dataset whenever an update is made.

*IN 2*

![importing into Excel](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/f2316e9b-67a4-4b4b-87f3-868b70407b9f)

*OUT 2*

![Screenshot 2024-02-05 144134](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/9a81d3a4-3622-4b26-8c1b-15a73c812c30)



## Step 3

In Excel I used pivot tables to generate a dynamic dashboard. 

*Pivot tables*

![pivot tables](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/be7217e9-e497-4925-8fc3-007997bd39b8)

*Excel dashboard*

![Dashboard](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/8e753d72-d401-4121-b355-7f9af1a6b1e6)


## Step 4
I then connected the Excel data sheet that contains the sql generated data set to Tableau, checked to ensure that all fields had been imported correctly and used the data to generate a visually pleasing dashboard for management. 

*Importing data from Excel to Tableau*

![Screenshot 2024-02-05 145455](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/a06a495a-a352-47ad-8e8e-c3afddee8ccb)

*Tableau Dashboard*

![1705072910367](https://github.com/simonrimui5/BIKE-LIFE-SQL-Excel-and-Tableau-/assets/155226875/65501d30-4111-49ed-9ced-4227ee104ab0)


# Analyzing the data

## Annual Revenue Analysis:

•	The bar chart visually represents the annual revenue for Bike Life.

•	In 2017, the company achieved the highest revenue, reaching $3,845,515.

•	The second-highest revenue was recorded in 2016, amounting to $2,709,484.

•	2018 reflects the lowest annual revenue, totaling $2,023,989.

## Monthly Revenue Analysis:

•	The line chart illustrates the monthly revenue trends for Bike Life.

•	In 2016, September emerges as the month with the highest revenue, reaching $303,283. This peak could be attributed to specific promotions, seasonal factors, or other business strategies.

•	August follows closely with a revenue of $253,131, indicating strong performance during this period.

•	February registers the lowest revenue among the months, amounting to $175,768. Further investigation may be necessary to understand the factors contributing to this lower performance in February.

•	In 2017, April had the lowest revenue at $254,106, while June recorded the highest revenue of $419,892.

•	In 2018, April experienced a significant revenue boost, reaching $909,179, making it the highest revenue month across all years. However, the subsequent months from June to December had comparatively lower revenues, ranging from $210 to $8,000.

## Statewise Revenue Distribution:

•	In 2016, the state of New York led in revenue with $1,781,132, followed by California with $628,495, and Texas with the lowest revenue at $299,408.

•	In 2017, New York maintained its leading position with a substantial revenue increase to $2,764,466. California and Texas also experienced revenue growth, with California remaining in second place.

•	In 2018, New York continued to dominate with $1,280,644 in revenue, followed by California with $531,118. Texas remained at the bottom with $212,227 in revenue.

## Brandwise Revenue Distribution:

•	The Pie Chart highlights brand-wise revenue distribution.

•	In 2016, Baldwin Bikes led with $1,781,132, followed by Santa Cruz Bikes and Rowlett Bikes.

•	In 2017, Baldwin Bikes maintained its lead with $2,764,466, followed by Santa Cruz Bikes and Rowlett Bikes.

•	Analyzing brand-wise performance can inform marketing and sales strategies, emphasizing the strengths of top-performing brands.

•	In 2018, Baldwin Bikes led with $1,280,644 in revenue, followed by Rowlett Bikes with $531,118, and Santa Cruz Bikes with $212,227.

•	Analyzing brandwise performance allows for strategic planning and resource allocation, focusing on the strengths and growth areas of each brand.

## Categorywise Revenue Distribution:

•	**2016:** Mountain Bikes generated the highest revenue, contributing 48.97% of the total revenue ($1,326,766). Child Bikes had the lowest revenue at $98,066 (3.62% of the total).

•	**2017:** Mountain Bikes and Road Bikes were the top categories, with revenues of $1,252,294 and $1,161,451, respectively. Child Bikes had the lowest revenue at $165,374 (4.30% of the total).

•	**2018:** Road Bikes led with $695,105 (34.15% of the total), followed by Mountain Bikes with $451,716. Child Bikes had the lowest revenue at $64,448 (3.18% of the total).

## Top Customers Analysis:

•	**2016:** Elinore Aguilar, Shary Hopkins, and Debra Burks were the top three customers, while Genoveva Baldwin, Robby Sykes, and Emmitt Sanchez were the bottom three in terms of spending.

•	**2017:** Corrina Sawyer, Emmitt Sanchez, and Robby Sykes were the top three customers, while Lyndsey Bean, Lorrie Becker, and Pamela Newman were the bottom three in terms of spending.

•	**2018:** Sharyn Hopkins, Tameka Fisher, and Genoveva Baldwin were the top three customers, while Corrina Sawyer, Robby Sykes, and Melanie Hayes were the bottom three in terms of spending.

## Sales Representative Performance Analysis:

**2016:**

•	Venita Daniel was the highest-ranked sales rep in 2016, achieving a total sales figure of $955,812.

•	Marcelene Boyer and Genna Serrano secured the second and third positions with $825,319 and $355,425 in sales, respectively.

**2017:**

•	Marcelene Boyer emerged as the top-performing sales rep in 2017, achieving $1,528,096 in total sales.

•	Venita Daniel, the highest-ranked sales rep in 2016, secured the second position with $1,236,370 in sales.

•	Genna Serrano maintained a strong performance, ranking third with $319,427 in sales.

**2018:**

•	Venita Daniel continued her success as the highest-ranked sales rep in 2018, with $695,171 in total sales.

•	Marcelene Boyer retained a strong position, securing the second spot with $585,473 in sales.

•	Genna Serrano maintained consistent performance, ranking third with $277,870 in sales.

## Conclusions

The comprehensive analysis of Bike Life's performance across the years 2016, 2017, and 2018 provides valuable insights into various aspects of the business. Here are the key conclusions drawn from the report:

## Brand and Category Performance:

•	Baldwin Bikes consistently led in revenue across the years, reflecting its strong market presence.

•	Mountain Bikes and Road Bikes emerged as top-performing categories, contributing significantly to the overall revenue.

## Sales Representative Contributions:

•	Venita Daniel and Marcelene Boyer consistently stood out as top-performing sales representatives, showcasing their dedication and effectiveness in driving sales.

•	Genna Serrano, while maintaining a top-three position, demonstrated variability in performance, warranting further analysis and support.

## Customer Dynamics:

•	The identification of top and bottom customers in each year provides insights into customer spending patterns and loyalty.

•	Implementing customer retention strategies and understanding the preferences of high-value customers can further enhance customer relationships.

## Category Preferences:

•	The treemap analysis of categorywise revenue distribution highlights the popularity of Mountain Bikes and Road Bikes.

•	Diversifying products within these popular categories and understanding market demand can contribute to sustained growth.

## Geographic and Seasonal Trends:

•	Monitoring statewise revenue variations is crucial for strategic planning and resource allocation.

•	Understanding seasonal trends can guide inventory management and promotional activities to capitalize on peak months.

## Top Customer Analysis:

•	Recognizing the highest and lowest spending customers provides opportunities for targeted marketing and personalized engagement.

•	Implementing loyalty programs and maintaining strong relationships with high-value customers is essential for long-term success.

In conclusion, a holistic approach to business strategy, including brand management, category optimization, customer engagement, and sales team support, will contribute to sustained growth and success for Bike Life. Continued monitoring, adaptability, and proactive decision-making are key in navigating the dynamic landscape of the bike industry.


## Recommendations:

•	Implement a recognition program for top-performing sales representatives to boost morale and motivation.

•	Provide additional training and support to sales representatives showing variability in performance.

•	Diversify product offerings based on category performance and market demand.

•	Encourage team collaboration and knowledge-sharing to enhance overall sales team performance.

•	Monitor and adjust sales goals regularly to align with individual performance and market conditions.










