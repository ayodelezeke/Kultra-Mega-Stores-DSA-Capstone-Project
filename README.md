# Kultra Mega Stores (KMS) Analysis 
Data Analysis and key insights into Kultra Mega Stores using SQL

## Overview
An Exploratory Data Analysis into data from Kultra Mega Stores(Abuja Division) to generate insights that can increase customer engagement, increase revenue in struggling areas and implement cost-saving measures across the board.

## Dataset
Two datasets were provided by the Business Manager of KMS. 
1. KMS Sql Case Study showing the order data from 2009 to 2012.
   
   Format: CSV
   
   Total Records: 8,399 rows, 21 columns
2. Order_Status showing the order status of some orders.
   
   Format: CSV
   
   Total Records: 572 rows, 2 columns

## Tools and Technologies
- SQL dialect used : T-SQL
- Environment: SQL Server Management Studio (SSMS)

## Queries and Insights
1. Goal: Which product category had the highest sales?
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 1 Product_Category, SUM(Sales) AS [Sales]
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Product_Category
   ORDER BY [Sales] DESC
   ```

   Output:

    ![Output 1](https://github.com/user-attachments/assets/96883b91-47d8-4504-a507-f71b5448f5e9)


2. Goal: What are the Top 3 and Bottom 3 regions in terms of sales?

   SQL Snippet:
   ``` SQL
   --TOP 3
   SELECT TOP 3 Region, SUM(Sales) AS [Sales]
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Region
   ORDER BY [Sales] DESC
   ```

   Output:

   ![Output 2](https://github.com/user-attachments/assets/161d4e77-bfa6-4974-a9c0-768a5194bad6)

   SQL Snippet:
   ``` SQL
   --BOTTOM 3
   SELECT TOP 3 Region, SUM(Sales) AS [Sales]
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Region
   ORDER BY [Sales] ASC
   ```

   Output:

   ![Output 3](https://github.com/user-attachments/assets/ca0f5e5d-7be4-45dd-8008-e3929ca3efb2)

3. Goal: What were the total sales of appliances in Ontario?
   
   SQL Snippet:
   ``` SQL
   SELECT SUM(Sales) AS [Total Sales]
   FROM [dbo].[KMS Sql Case Study]
   WHERE Region = 'Ontario' AND Product_Sub_Category = 'Appliances'
   ```

   Output:

   ![Output 4](https://github.com/user-attachments/assets/3a91d148-6dc3-44f0-9cb0-42271e61637a)

4. Goal:  Advise the management of KMS on what to do to increase the revenue from the bottom 10 customers.

   First identify who the bottom 10 customers are and what their revenue incurred is
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 10 Customer_Name, SUM(Sales) AS Sales
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Customer_Name
   ORDER BY Sales ASC
   ```

   Output:

   ![Output 5](https://github.com/user-attachments/assets/26e0174f-01e3-4349-8bcd-43106bcf10ac)

   Some actions that can be taken to increase the revenue from these customers are:
   - Sending personalized emails or SMS with incentives (e.g., 10% off next purchase).
   - Recommending complementary or higher-value products at checkout for repeat customers that buy low-value products.
   - Enroll them in a loyalty program with tiered rewards to encourage repeat purchases and build long-term engagement.
   - Offer targeted discounts or bundles based on their past purchases to build conversion and interest.

5. Goal: What were the total sales of appliances in Ontario?
   
   SQL Snippet:
   ``` SQL
   SELECT SUM(Sales) AS [Total Sales]
   FROM [dbo].[KMS Sql Case Study]
   WHERE Region = 'Ontario' AND Product_Sub_Category = 'Appliances'
   ```

   Output:

   ![Output 4](https://github.com/user-attachments/assets/3a91d148-6dc3-44f0-9cb0-42271e61637a)




