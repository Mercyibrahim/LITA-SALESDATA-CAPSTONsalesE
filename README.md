## LITA-SALESDATA-CAPSTONE_PROJECT
A project analysis on the sales performance on some products in the different regions in Nigeria
### PROJECT TOPIC:ANALYSIS ON SALES PERFORMANCE IN DIFFERENT REGIONS IN NIGERIA
### PROJECT OVERVIEW
This data analysis is aimed to give a detailed view on the sales performaces in different regions in Nigeria.
we seek to have an insight in the top selling and bottom selling products in each regions, thereby having
a clear view of what works for the company, what products or region the company should focus on.
### DATA SOURCE
The data was shared on my LMS canvas through the incubator hub to carrry out analysis as my project work to 
completion of the 10 weeks class.
### TOOLS USED

- MICROSOFT EXCEL:

1. For initial data cleaning

2. For calculations

3. For Sales report

- SQL SERVER :

  Used sql to write queries to get results

- PowerBI:
  
for data visualstions

### KEY METRICS
- Products; There were six products that was sold in the four regions, the products include Gloves, hat
, Jacket, shirt shoes and socks.
- Region; the products was sold in four regions namely south, east, north and west regions


### EXPLORATORY DATA ANALYSIS
  Which of these products are the highest selling and which region has the highest sells so the company and increase productions of these
  products which will result to increase in total revenue.

### DEDUCTIONS AND RECOMMENDATIONS
Fron the data analysis carried out on the sales performance for all the regions, it was seen that South region has the highest sales(927820) and the west region has the lowest total sell (300345).The products that generated the highest revenue for the set period of 2023 to 2024 is shoes while socks generated the lowest income between 2023 to 2024.from these findings , the company can make much production of shirt to the south region and fom the analysis shoes, gloves and socks are the best selling products and its aviseable for the company to increase its productions. 

### DATA VISUALISATION

<img width="622" alt="POERBI VISUALS SALES DATA" src="https://github.com/user-attachments/assets/fa95ec50-36f0-4da2-84b7-caf76556f0e6">

<img width="616" alt="POWERBI VISUALS 2" src="https://github.com/user-attachments/assets/72058c8b-9a9d-4cc0-9684-5314275690db">

<img width="522" alt="POWERBI VISUAL SALES DATA3" src="https://github.com/user-attachments/assets/47098d00-2076-478a-853c-6ba10f187eb5">

- MICROSOFT EXCEL REORTS

<img width="432" alt="AVERAGE SALES PER PRODUCT AND REVENUE BY REGION  EXCEL Q2" src="https://github.com/user-attachments/assets/8bbc2650-0bf2-4a2b-8ffc-8affef99e039">

<img width="862" alt="EXCEL PIVOT CALCULATION" src="https://github.com/user-attachments/assets/fb99125b-4f19-4235-a9d1-c4bf9b1562ba">

<img width="468" alt="excel visual sales data 2" src="https://github.com/user-attachments/assets/8f5ba948-a3d3-405f-879b-24e1a8382eda">

<img width="662" alt="EXCEL VISUALS FOR SALES DATA" src="https://github.com/user-attachments/assets/af35f3bd-57ca-4365-b000-87759d3098fd">

- SQL SERVER RESULTS
  
<img width="445" alt="COUNT OF SALES IN REGION SQL SALES DATA" src="https://github.com/user-attachments/assets/84b7641b-e03c-4a9e-b3b5-5d3795c75f1a">

<img width="570" alt="HIGHEST SELLING PRODUCT SQL Q3" src="https://github.com/user-attachments/assets/d91d65b6-b83d-4c61-a5e3-3c478ba6f7a9">

<img width="505" alt="sql question 4 sales data" src="https://github.com/user-attachments/assets/df567317-4026-4e3d-9563-989af7b8713c">

<img width="221" alt="monthly sales total question 5" src="https://github.com/user-attachments/assets/2c388ced-fe01-494a-8b3a-102decf084d1">

<img width="189" alt="question 6 sql top 5 customers" src="https://github.com/user-attachments/assets/64df3836-9cd2-446c-858c-58cea8828cd9">

<img width="382" alt="SQL QUESTION 8 " src="https://github.com/user-attachments/assets/b90fe592-ca1a-4842-b635-5c2d48267923">

### DATA ANALYSIS ; SQL QUERIES AND excel formulars used

 ```SQL
  CREATE DATABASE SALES_DATA_CAPSTONE


SELECT * FROM [dbo].[SALES DATA_-27027859]

-----QUESTION 1 TOTAL SALES FOR EACH PRODUCT CATEGORY

SELECT PRODUCT,
    SUM(total_sales) AS TOTAL_SALES
	from 
	[dbo].[SALES DATA_-27027859]
Group by PRODUCT
order by TOTAL_SALES DESC

-----ADDING TOTAL SALES COLUMN TO THE TABLE

ALTER TABLE [dbo].[SALES DATA_]
ADD TOTAL_SALES bigint

-----updatingthe table to fill in the total sales column

update [dbo].[SALES DATA_]
set Total_sales = Quantity * UnitPrice

select * from [dbo].[SALES DATA_-]

-----Questions TWO, number of sales transactions in each region----

select
  Region,
  COUNT (*) AS NUMBER_OF_SALES_TRANSACTIONS
  FROM [dbo].[SALES DATA_-27027859]
  GROUP BY
      Region
  ORDER BY NUMBER_OF_SALES_TRANSACTIONS DESC

  ----QUESTION 3 HIGHEST SELLING PRODUCTS BY TOTAL SALES VALUE

  SELECT Top 1
     PRODUCT,
	 sum(Total_sales) As TOTAL_SALES_VALUE
 FROM
	 [SALES DATA_]
 GROUP BY
   PRODUCT
   ORDER BY 
   TOTAL_SALES_VALUE DESC
 
 -----QUESTION 4---CALCULATE TOTAL REVENUE PER PRODUCT-----
 SELECT
  PRODUCT, SUM(Total_sales) as TOTAL_REVENUE_PER_PRODUCT
  FROM [dbo].[SALES DATA_]
  GROUP BY
     PRODUCT
ORDER BY
  TOTAL_REVENUE_PER_PRODUCT DESC

  ALTER TABLE [dbo].[SALES DATA_]
  ADD OrderMonth nvarchar(50)
  
  UPDATE [dbo].[SALES DATA_]
  SET OrderMonth = DATENAME(MONTH, OrderDate)


  ALTER TABLE[dbo].[SALES DATA_]
 ADD OrderYear int

 UPDATE [dbo].[SALES DATA_]
 SET OrderYear = Year(OrderDate)

  SELECT *  from  [dbo].[SALES DATA_]

 -----Q5 Calculate monthly sales totals for the current year(2024)--

SELECT OrderMonth,
SUM(total_sales) as monthly_sales_totals
FROM [dbo].[SALES DATA_]
WHERE OrderYear = 2024
GROUP BY OrderMonth

--- Q6 find the top 5 customers by total purchase amount
SELECT Top 5 Customer_Id,SUM(Quantity) AS Total_Purchase
FROM[dbo].[SALES DATA_]
GROUP BY Customer_Id
ORDER BY Total_Purchase DESC

---Q7 calculate the percentage of total sales contributed by each region.
SELECT Region, sum(TOTAL_SALES)AS REGION_SALES,
 SUM(TOTAL_SALES)*100/(SELECT SUM(TOTAL_SALES) FROM[dbo].[SALES DATA_]
 AS Percentagetotalsales
 from [dbo].[SALES DATA_]
GROUP BY Region
ORDER BY 3 DESC


--Q8 Identify products with no sales in the last quarter
SELECT Product,SUM(Quantity) AS Sales
FROM [dbo].[SALES DATA_]
WHERE MONTH(OrderDate) BETWEEN 10 AND 12  
GROUP BY Product
HAVING SUM(Quantity)=0

SELECT * FROM [dbo].[SALES DATA_]
    ```                            























