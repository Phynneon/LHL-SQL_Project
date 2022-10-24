What issues will you address by cleaning the data?

1. First issue addressed is the product price inside the all_session table. The original price range vary between 0 and 298,000,000 USD. Which is about 1,000,000 times higher value of the products listed in the sku column in the products table. The same goes for all the other columns containing transactions.

2. Removing the columns that only have null values, such as the product_refund_amount column from all_sessions table.

3. Removing columns containing duplicate data. The transaction_revenue from all_sessions table only contain 4 values and they are identical to the values in total_transaction_revenue. It is safe to remove the transaction_revenue colum without losing data.





Queries:
Below, provide the SQL queries you used to clean your data.

The code for changing the values of the product_prices and related transactions inside all_sessions table.
``` SQL
UPDATE all_sessions
SET product_price = product_price/1000000,
    total_transaction_revenue = total_transaction_revenue/1000000,
    product_revenue = product_revenue/1000000,
    transaction_revenue = transaction_revenue/1000000
```
the code used to change the price in the analytics table
```SQL
UPDATE analytics
SET unit_price = unit_price/1000000,
	revenue = revenue/1000000
```
The code for finding columns with only NULL values
```SQL
SELECT COUNT(column_name)
FROM table_name
WHERE column_name IS NOT NULL
```
The code for removing columns with only NULL values
```SQL
ALTER TABLE all_sessions
DROP COLUMN product_refund_amount,
DROP COLUMN item_quantity,
DROP COLUMN item_revenue,
DROP COLUMN search_keyword
```
```SQL
ALTER TABLE analytics
DROP COLUMN user_id
```
The code for removing columns with duplicate data
```SQL
ALTER TABLE all_sessions
DROP COLUMN transaction_revenue
```
