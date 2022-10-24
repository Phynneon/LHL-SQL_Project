# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
The goal of this project is to process the information in a database called ecommerce. We use the information to look for trend in the revenue and sales from the company. 

## Process
### 1. Importing And Cleaning the Data
### 2. Using Query to Find Trend in Sales and Revenue 

## Results
From the data obtained in the Ecommerce Database, we are shown that the main customers that make purchases from the company comes from the United States. Revenue generated from sales in other countries is very insignificant compared to the revenue genereated in the United States. Within the United States, we are shown that different cities have different purchasing habits, such as Montain View buying a lot of Nest products, and Sunnyvale buying a lot of Housewares. 

This data can help the company decide what type of product to stock near different locations (inside their warehouse) as well as what new type of products to introdude to their customers (that match the category purchase trend).

## Challenges 
The quality of the raw data imported is definitely the biggest challenge faced in this project. The tables either have too many missing or misplaced values (all_sessions), too many duplicate values (analytics) or similar value types(sales_by_sku, sales_reports). 

The other main challenge is the time constrain. Not having enough time to properly process the data means that we cannot draw very confident conclusions from our processed data. 

## Future Goals
The main change I would make if I were given more time is to clean and process the raw data better. 

- There are wrong country/city names that needs to be changed and missing city values that needs to be filled.  
- Filter out or fix some values that does not make sense in the database, such as the visit_start_time from analytics table and time column in the all_sessions table.
- There are a lot of products (~250) that have missing product categories. Those products needs to be properly categorized to provide a better understanding of the data. 
