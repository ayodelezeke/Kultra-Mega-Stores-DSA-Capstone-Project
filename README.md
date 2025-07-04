# Kultra Mega Stores (KMS) Analysis 
This project is an Exploratory Data Analysis using SQL into Kultra Mega Stores(Abuja Division) to generate insights that can increase customer engagement, increase revenue in struggling areas and implement cost-saving measures across the board.

## Overview
Key questions are asked such as:
- Strategies for increasing customer engagement
- Most profitable customers
- Top-performing product categories and regions
- Shipping cost apportionment

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
   --First: Identifying the most valuable customers in terms of total sales
   SELECT TOP 5 Customer_Name, SUM(Sales) AS Total_Sales
   FROM [dbo].[KMS Sql Case Study]
   GROUP BY Customer_Name
   ORDER BY Total_Sales DESC
   ```

   Output:

   ![Output 7](https://github.com/user-attachments/assets/ab6e669d-98b8-4893-82c1-822cc00d0e69)

   SQL Snippet:
   ``` SQL
   --Second: Identifying the products or services they purchase
   WITH Customer_Sales AS (
    SELECT Customer_Name, SUM(Sales) AS Total_Sales
    FROM [dbo].[KMS Sql Case Study]
    GROUP BY Customer_Name),
   Top_Customers AS (
    SELECT TOP 5 Customer_Name, Total_Sales
    FROM Customer_Sales
    ORDER BY Total_Sales DESC),
   Customer_Category_Sales AS (
    SELECT o.[Customer_Name], o.[Product_Category], SUM(o.[Sales]) AS Category_Sales
    FROM [dbo].[KMS Sql Case Study] AS o
    JOIN Top_Customers AS tc
    ON o.[Customer_Name] = tc.Customer_Name
    GROUP BY o.[Customer_Name], o.[Product_Category])

   SELECT 
    ccs.Customer_Name,
    ccs.Product_Category,
    ccs.Category_Sales
   FROM Customer_Category_Sales AS ccs
   ORDER BY ccs.Category_Sales DESC;

   ```

   Output:

   ![Output 8](https://github.com/user-attachments/assets/061740d4-758a-4365-9c69-a01261e6d204)
   
7. Goal: Which small business customer had the highest sales? 
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 1 Customer_Name, SUM(sales) AS [Highest Sales]
   FROM [dbo].[KMS Sql Case Study]
   WHERE Customer_Segment = 'Small Business'
   GROUP BY Customer_Name
   ORDER BY [Highest Sales] DESC
   ```

   Output:

   ![Output 9](https://github.com/user-attachments/assets/b0e8b7f4-1bc9-435c-8741-9c937448e399)

8. Goal: Which Corporate Customer placed the most number of orders in 2009 – 2012?
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 1 Customer_Name, SUM(Order_Quantity) AS [Number Of Orders]
   FROM [dbo].[KMS Sql Case Study]
   WHERE Customer_Segment = 'Corporate' AND YEAR(Order_Date) BETWEEN '2009' AND '2012'
   GROUP BY Customer_Name
   ORDER BY [Number Of Orders] DESC
   ```

   Output:

   ![Output 10](https://github.com/user-attachments/assets/c38588a8-8d14-4ea8-8030-b0add744e051)

9. Goal: Which consumer customer was the most profitable one? 
   
   SQL Snippet:
   ``` SQL
   SELECT TOP 1 Customer_Name, SUM(Profit) as Profit
   FROM [dbo].[KMS Sql Case Study]
   WHERE Customer_Segment = 'Consumer'
   GROUP BY Customer_Name
   ORDER BY Profit DESC
   ```

   Output:

   ![Output 11](https://github.com/user-attachments/assets/476702dc-5541-44aa-b208-8a95d0e60aee)


10. Goal: Which customer returned items, and what segment do they belong to?

    Firstly, the table Order_Status is added to the database. Then both tables are joined

    SQL Snippet:
    ``` SQL
    SELECT k.Customer_Name, k.Customer_Segment
    FROM [dbo].[KMS Sql Case Study] k
    JOIN Order_Status o
    ON k.Order_ID = o.Order_ID
    WHERE o.[Status] = 'Returned'
    ```
11. Goal:  If the delivery truck is the most economical but the slowest shipping method and Express Air is the fastest but the most expensive one, do you think the company appropriately spent shipping costs based on the Order Priority?

    SQL Snippet:
    ``` SQL
    SELECT Order_Priority,
           Ship_Mode,
           COUNT(Order_ID) AS Number_Of_Orders,
           SUM(Shipping_Cost) AS Total_Shipping_Cost,
           AVG(Shipping_Cost) AS Avg_Shipping_Cost
    FROM [dbo].[KMS Sql Case Study]
    GROUP BY Order_Priority, Ship_Mode
    ORDER BY Order_Priority, Avg_Shipping_Cost DESC
    ```

    Output:

    ![Output 12](https://github.com/user-attachments/assets/19d0fdae-0f6d-47f5-a79e-1f7072c288ba)

    Insight: The company did not appropriately spend shipping costs based on order priority. The data shows that some lower-priority orders incurred higher shipping costs than higher-priority ones

    










