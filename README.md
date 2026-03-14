

# Mens-Fashion-Sales-Analysis

### Dashboard Link : https://app.powerbi.com/links/aTyA5pShA1?ctid=7f0a8e90-4ba3-4cc7-b920-c1f6074e28a2&pbi_source=linkShare

## Problem Statement

This dashboard helps businesses understand the sales performance of men's fashion brands. It enables businesses to analyze pricing strategies, discount percentages, product varieties and profit margins across different brands.

Retail fashion datasets often contain missing values, inconsistent pricing formats and incorrect data types which make analysis difficult. By cleaning and transforming the dataset using Azure SQL Database and Power BI, meaningful insights can be generated to help businesses improve their pricing strategies.

Through this dashboard businesses can analyze:

-  Top brands by discount percentage

-  Brands with highest profit percentage

-  Brand wise product varieties

-  Average sales price across brands

Using these insights, companies can identify which brands offer higher discounts, which brands generate higher profit margins and which brands dominate the product variety in the dataset.

### Steps followed 

- Step 1 : Azure SQL Database was created in Microsoft Azure Portal and deployment was completed.

- Step 2 : Firewall settings were configured to allow database access.

- Step 3 : Azure SQL database was connected with SQL Server Management Studio (SSMS) using server name, SQL authentication username and password.

- Step 4 : A database named Test was created inside Azure SQL Server.

- Step 5 : Dataset containing men's t-shirt product data was imported using Import Flat File option in SSMS.

- Step 6 : Data inspection was performed using Azure SQL Query Editor using the following query:

          SELECT TOP (1000) * FROM men_tshirt
- Step 7 : It was observed that Original Price and Sale Price columns contained unwanted characters such as ?.

Example values: 

     ?1,749
     ?525


- Step 8 : Data cleaning was performed using SQL update query to remove unwanted characters.

Following SQL expression was written:

    UPDATE men_tshirt
    SET original_price = TRIM(REPLACE(CAST(original_price AS VARCHAR(MAX)),'?',' '))
    WHERE original_price LIKE '%?%';

    UPDATE men_tshirt
    SET sale_price = TRIM(REPLACE(CAST(sale_price AS VARCHAR(MAX)),'?',' '))
    WHERE sale_price LIKE '%?%';

- Step 9 : Azure SQL database was connected to Power BI Desktop using Azure SQL connector.

Two authentication methods were used:

Database authentication using SQL username and password
• Microsoft account authentication using Azure Entra ID

- Step 10 : Power Query Editor was opened to understand and clean the dataset further.
- Step 11 : It was observed that Original Price column contained NA values.
  To handle missing values, a conditional column named Factor was created.

Logic used:

                If Original Price = NA → Factor = 1.5
                Else → Factor = 0

- Step 12 :A custom column was created using the following formula:

               A custom column was created using the following formula:

- Step 13 : Another conditional column was created to replace missing values.

Logic used:

                 If Original Price = NA
                 Then Sales * Factor
                 Else Original Price

- Step 14 :After data transformation, the cleaned dataset was loaded into Power BI.


- step 15 : New Calculated Column was created to find Discount     Percentage.

  Following DAX expression was written to find Discount % :

              Discount % =
              DIVIDE(
              Tshirt[Marked Price] - Tshirt[Sales Price],
              Tshirt[Marked Price]
              ) * 100

  This column calculates the discount percentage applied on products.

  snap of new calculated column,

  <img width="131" height="728" alt="Image" src="https://github.com/user-attachments/assets/d08e7365-8ede-455d-96ee-eeb7e2db991b" />


- step 16 : New Calculated Column was created to find Cost Price.

  Following DAX expression was written to find Cost Price :

               Cost Price =
               DIVIDE(
               100 * Tshirt[Sales Price],
               100 + Tshirt[profit%%]
                )
 This column estimates the cost price based on profit percentage.

snap of new calculated column,

<img width="133" height="723" alt="Image" src="https://github.com/user-attachments/assets/37226e42-e2b2-4071-a739-dfe6ee32cca1" />

- step 17 : New Calculated Column was created to find Profit Percentage.

  Following DAX expression was written to find Profit % :

           profit%% =
           RANDBETWEEN(1,20)

 This generates random profit percentage values between 1% and 20%.

snap of new calculated column,

<img width="92" height="725" alt="Image" src="https://github.com/user-attachments/assets/90a4f808-6040-4b04-bb8d-c68ea279bb8c" />


 - Step 18 : The report was then published to Power BI Service.
 
 
<img width="622" height="368" alt="Image" src="https://github.com/user-attachments/assets/a9b61479-b57f-4b41-a8d2-51af5a181e12" />

# Snapshot of Dashboard (Power BI Service)

## Page 1

<img width="1906" height="912" alt="Image" src="https://github.com/user-attachments/assets/a76ef0ff-f80a-40e9-b2a0-946ab99ea59d" />

 
## Page 2

<img width="1896" height="902" alt="Image" src="https://github.com/user-attachments/assets/323a7f86-4f70-4751-82c7-59dc971b0d13" />

 # Report Snapshot (Power BI DESKTOP)

## Page 1

<img width="1413" height="702" alt="Image" src="https://github.com/user-attachments/assets/be19c5cd-60c0-41c4-876e-0860224f887e" />

## page 2

<img width="1413" height="726" alt="Image" src="https://github.com/user-attachments/assets/a7437b29-a22d-41d1-9678-fdac4e120716" />

# Insights

A multi-page dashboard was created on Power BI Desktop and published to Power BI Service.

Following insights can be derived from the dashboard:

### [1] Brand Discount Analysis

Some brands provide significantly higher discount percentages compared to others, indicating aggressive pricing strategies.
           
### [2] Product Variety

   Certain brands dominate the dataset in terms of product varieties available in the men's fashion category.
  
  
  ### [3] Average Sales Price

Sales prices vary significantly across brands, indicating different product positioning strategies in the market.

 ### [4] Profit Distribution

Profit margins vary across brands, suggesting different pricing and discount models used by retailers.

 ### [5] Discount Impact

Higher discounts directly affect final sales price and influence brand competitiveness.
