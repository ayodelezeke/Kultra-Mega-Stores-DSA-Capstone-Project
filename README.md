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

## Data Optimization
Some columns were formatted into two decimal places for better analysis and insight

Columns formatted are: Sales, Discount, Profit, Unit_Price, Shipping_Cost and Product_Base_Margin

SQL Snippet example:
``` SQL
ALTER TABLE [dbo].[KMS Sql Case Study]
ALTER COLUMN Sales DECIMAL (15,2)
```

Query was repeated for relevant columns

## Queries and Insights
### Case Scenario I
1. Goal: Which product category had the highest sales?
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 1 Product_Category, SUM(Sales) AS [Sales]
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Product_Category
   ORDER BY [Sales] DESC
   ```

   Output:

   ![Output 1](https://github.com/user-attachments/assets/c4a1a851-2787-4e6e-a897-e40539324b59)



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

   ![Output 2](https://github.com/user-attachments/assets/69dd1b9a-5d63-4c4b-9f17-d6ecc28f3788)


   SQL Snippet:
   ``` SQL
   --BOTTOM 3
   SELECT TOP 3 Region, SUM(Sales) AS [Sales]
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Region
   ORDER BY [Sales] ASC
   ```

   Output:

   ![Output 3](https://github.com/user-attachments/assets/21c86c10-da6c-4ed3-9789-c2674e64713c)


3. Goal: What were the total sales of appliances in Ontario?
   
   SQL Snippet:
   ``` SQL
   SELECT SUM(Sales) AS [Total Sales]
   FROM [dbo].[KMS Sql Case Study]
   WHERE Region = 'Ontario' AND Product_Sub_Category = 'Appliances'
   ```

   Output:

   ![Output 4](https://github.com/user-attachments/assets/266f61af-c7de-46df-95f9-2b7de604eb1f)

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

   ![Output 5](https://github.com/user-attachments/assets/56816368-6eb3-459b-9f50-e2add18fc753)


   Some actions that can be taken to increase the revenue from these customers are:
   - Sending personalized emails or SMS.
   - Recommending complementary or higher-value products.
   - Enrolling them in a loyalty program.
   - Offering targeted discounts or bundles.

5. Goal: KMS incurred the most shipping cost using which shipping method? 
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 1 Ship_Mode, SUM(Shipping_Cost) AS [Total Shipping Cost]
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Ship_Mode
   ORDER BY [Total Shipping Cost] DESC
   ```

   Output:

   ![Output 6](https://github.com/user-attachments/assets/abb5ada3-79f1-4017-8478-4c804d10d1ed)

### Case Scenario II
6. Goal: Who are the most valuable customers, and what products or services do they typically purchase?
   
   SQL Snippet:
   ``` SQL
   SELECT SUM(Sales) AS [Total Sales]
   FROM [dbo].[KMS Sql Case Study]
   WHERE Region = 'Ontario' AND Product_Sub_Category = 'Appliances'
   ```

   Output:

   ![Output 4](https://github.com/user-attachments/assets/266f61af-c7de-46df-95f9-2b7de604eb1f)



