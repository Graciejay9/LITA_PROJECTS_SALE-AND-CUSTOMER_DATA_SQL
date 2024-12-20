# LITA_PROJECTS_SALE-AND-CUSTOMER_DATA_SQL
## Store Sales Analysis

### Project Overview
---
This project analyszes customers' data, sales of products at a retail Store in order to ascertain customers pattern of purchasing Items, to identify which product has the highest selling rate and to determine opportunities for growth and things needed to be done

### Table of Contents
---
- Project Overview
- Table of Contents
- Data Source
- Data Set
- Tools Used
- Methodology
- Key Analysis and Findings
- SQL Queries
- Visualizations
- Insights and Recommendations

### Data Source
---
The data used for this analysis is sourced from the store sales records, with details on:
- Product categories
- Sales volume
- Revenue generated
- Customer segments

### Data Set
---
The dataset contains:
- Orderid(a unique identifier)
- Product (product name)
- Region (geographic region)
- Orderdate (date of order)
- Quantity (number of units sold)
- Unitprice (price per unit)
- Total revenue (Total revenue per order)

### Tools Used
---
This project was completed using:
- Microsoft Excel for data cleaning and preliminary analysis.
- SQL Structured Query Language for data processing and querying.
- Power BI for data visualization and dashboard creation.
- Github for building portfolio

### Methodology
---
1.  Data Cleaning:
- Removed duplicates and irrelevant columns.
- Handled missing values to ensure accurate analysis.
2.  Exploratory Data Analysis:
- Calculated average sales per product.
- Identified top-performing product categories.
- Analyzed seasonal and monthly sales trends.

### Data Analysis and Findings
---
#### Excel Analysis
Excel files containing the followng;
- Data filtering and sorting which involves cleaning up the data set and removing duplicates.

![Screenshot 2024-11-15 153104](https://github.com/user-attachments/assets/7a572ea3-076a-468e-999a-9ac182a0e357)

![Screenshot 2024-11-15 163839](https://github.com/user-attachments/assets/abe2563a-fbe0-49f1-819f-1d7c2aa42ae0)

Above is the dataset for sales data and customer subscription services, and to be able to analyze properly, we source for the duration in which each customers subscribed; hence our subscription duration column and also the Revenue from quantity and Unit price.

- Pivot Table for regional and products analysis

![Screenshot 2024-11-15 164939](https://github.com/user-attachments/assets/87c7e3e2-a859-4d7c-998a-5707a9070527)



![Screenshot 2024-11-15 171140](https://github.com/user-attachments/assets/51bcf15f-be57-4ef0-8751-cd1aa8af2b28)

#### SQL analysis
The SqL files contains the Queries for data extraction and filtering on excel. it aslo contains the Aggregate funtions for revenue and quantity calculation. It also help to know customers preference in each product.

##### SQL queries
Here are some of the SQL queries that is used to provide answers to the questions
1.  Total Sales by Products
 ```sql
  -------retrieve total sales from each category-------------
SELECT PRODUCT,SUM(revenue) as 'Total sales'
FROM[dbo].[SALES DATA LITA PROJECT]
group by Product



2.  ---------Number of Sales Transaction per Region----------
select region, count(*)as 'transaction sales'
from[dbo].[SALES DATA LITA PROJECT]
group by region



3. ---------CALCULATE MONTHLY SALES TOTAL FOR THE CURRENT YEAR-------
SELECT DATENAME(MONTH,ORDERDATE) AS 'SALESMONTH',
SUM(Revenue) AS 'TOTAL SALES'
FROM[dbo].[SALES DATA LITA PROJECT]
WHERE YEAR(ORDERDATE)=YEAR(GETDATE())
GROUP BY DATENAME(MONTH,OrderDate)
ORDER BY [Total Sales] desc;



4. -------------Top 5 Customers by Total Purchase Amount------------
select top 5 customer_id, sum(Revenue) as 'total purchase amount'
from[dbo].[SALES DATA LITA PROJECT]
group by [Customer_ID]




5. -----------Calculate the Percentage of Total Sales Contibuted by Each Region---------
select region,
cast((SUM(Revenue)*100/(select sum(Revenue) from [dbo].[SALES DATA LITA PROJECT])) as VARCHAR(10))+'%' 
as 'Sales Percentage'
from[dbo].[SALES DATA LITA PROJECT]
group by Region 
order by [Sales Percentage] desc;




6. ------------Identify Products with no Sales in the last Quarter--------------
select distinct product 
from[dbo].[SALES DATA LITA PROJECT]
where product not in(
select product
from[dbo].[SALES DATA LITA PROJECT]
where OrderDate>=dateadd(quarter, -1,getdate())
);
