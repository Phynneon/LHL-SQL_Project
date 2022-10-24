What are your risk areas? Identify and describe them.

 1. The database has a lot of missing and duplicate values, risking to provide a revenue that's too high (if duplicate) or too low (if missing).

 2. Price numbers that are overinflated, risking to mess up revenue calculation.

 3. Wrong or missing terms in country and city names. Which will cause aggregation functions to not work properly. 

 4. Multiple tables containing similar types of data, making it hard to know which table contains the data more suited for our analysis. 


QA Process:
Describe your QA process and include the SQL queries used to execute it.

1. To solve the problem of duplicate data, the best way is to use the DISTINCT function when doing query. It is possible to double check if a table has duplicate rows by doing
```SQL
SELECT DISTINCT * FROM table_name
```
and comparing it to the original table row number
```SQL
SELECT * FROM table_name
```
For the missing values, it is possible to use a case function to replace them with the average from the other values of the same column if the number of missing values is small. 
```SQL
SELECT CASE
    WHEN column_name IS NULL THEN AVG(column_name) OVER()
    ELSE column_name
END as column_name
FROM table_name
```
Otherwise it may be better to remove or simply not use the column if most of its values are missing.

2. The first step would be to look at any column involving unit price or revenue and perform a basic query to find MIN, MAX, AVG of that column.
```SQL
SELECT MIN(column_name), MAX(column_name), AVG(column_name)
FROM table_name
WHERE column_name > 0 
```
In this database the prouct prices and revenue are all inflated by 1,000,000. In order to fix it,
the columns concerned had to be divided by 1,000,000. The code for that is shown in the cleaning data section. 

3. I did not manage to properly tackle this section because of time constraints. I kind of let it slide because it did not impact my query significantly. With more time, I would have used a SELECT function to find cities with mismatched country then use a case function to try and fix it. 

4. I decided to use the table that provides the highest amount of unique data. Using
```SQL 
SELECT COUNT(*)
FROM (
    SELECT DISTINCT * 
    FROM table_name
    WHERE column_name IS NOT NULL
)
```
In this case column_name is revenue and the analytics table is the one with the highest amount of data by far. It has over 10000 distinct rows with non NULL revenue values while the all_sessions table only has 81 with non NULL total_transction_revenue. 
