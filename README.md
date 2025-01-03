Store Sales Staging Data Analysis
Author: Oyegoke Samuel Oluwatosin
Welcome to the Store Sales Staging Data Analysis project! This repository contains SQL queries designed to explore, analyse, and extract actionable insights from the store_sales_stagiing dataset. The queries focus on understanding sales performance, customer behaviour, product trends, and regional metrics to support data-driven decision-making.

Purpose of the Project
The primary goal of this project is to:

Provide a comprehensive exploration of the sales dataset.
Identify key trends and insights to improve business performance.
Enhance data querying and analysis skills using SQL.
Features
1. Data Exploration
View all records in the store_sales_stagiing table.
Inspect key metrics such as Order_Quantity, Unit_Price, and Shipping_Cost.
2. Data Filtering
Extract orders based on specific conditions, such as high quantities or specific Order_IDs.
3. Aggregation and Summarisation
Group and summarise data to calculate total, average, and maximum sales for various categories, customer segments, and provinces.
4. Trend Analysis
Discover sales trends across months and years.
Generate rolling totals to track cumulative monthly sales.
5. Ranking and Insights
Rank top-performing product categories and provinces using DENSE_RANK().
Extract dates with the highest sales and trends over time.
Usage
Clone this repository to your local machine:

bash
Copy code
git clone https://github.com/your-username/store-sales-staging.git  
Open the SQL script file in your SQL editor (e.g., SQL Server Management Studio, MySQL Workbench, or PostgreSQL).

Connect to your database containing the store_sales_stagiing table.

Execute the queries step by step or modify them to suit your analysis needs.

Key Queries
Data Exploration


SELECT * FROM store_sales_stagiing;  
Aggregated Sales by Product Category


SELECT Product_Category, SUM(Sales) AS Total_Sales  
FROM store_sales_stagiing  
GROUP BY Product_Category  
ORDER BY Total_Sales DESC;  
Monthly Sales Trends


SELECT  
    SUBSTRING(FORMAT(Order_Date, 'yyyy-MM-dd'), 1, 7) AS 'Month',  
    SUM(Sales) AS Monthly_Sales  
FROM store_sales_stagiing  
GROUP BY SUBSTRING(FORMAT(Order_Date, 'yyyy-MM-dd'), 1, 7)  
ORDER BY Month ASC;  
Ranking Provinces by Sales per Year

WITH Province_Year_Sales AS (  
    SELECT  
        Province,  
        YEAR(Order_Date) AS Year,  
        SUM(Sales) AS Annual_Sales  
    FROM store_sales_stagiing  
    GROUP BY Province, YEAR(Order_Date)  
),  
Ranked_Provinces AS (  
    SELECT  
        Province,  
        Year,  
        Annual_Sales,  
        DENSE_RANK() OVER (PARTITION BY Year ORDER BY Annual_Sales DESC) AS Rank  
    FROM Province_Year_Sales  
)  
SELECT *  
FROM Ranked_Provinces  
WHERE Rank <= 5;  

How to Contribute
I welcome contributions to improve the queries or add new features! If you'd like to contribute:

Fork this repository.
Create a new branch for your feature/bug fix.
Submit a pull request with a detailed description of the changes.

License
This project is licensed under the MIT License. Feel free to use and adapt it as needed.

Contact
If you have questions, feedback, or suggestions, feel free to reach out:

Email: oluwatosinoyegoke41@gmail.com
LinkedIn: (https://www.linkedin.com/in/tosinoyegoke120?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3BWiyM%2FXN6TDCA8q%2BarOf%2FjQ%3D%3D
Thank you for exploring my project! 😊
