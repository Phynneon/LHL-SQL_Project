Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?** 

SQL Queries:
```SQL
SELECT ses.country, ses.city, SUM(revenue) as revenue
FROM (
SELECT DISTINCT * 
FROM analytics
WHERE revenue IS NOT NULL
) as alt
JOIN all_sessions ses
USING(full_visitor_id)
GROUP BY country, city
ORDER BY revenue DESC
```

Answer:

The country with the highest transaction revenue (and by far) is the United States. Unforttunately most of the transactions do not have a specified city(not available in demo data). The named cities with the highest revenue is Mountain View, USA with 10439 USD followed by San Bruno, USA at 4229 USD.


**Question 2: What is the average number of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT ses.country, ses.city, ROUND(AVG(units_sold)) as avg_ordered
FROM (
SELECT DISTINCT * 
FROM analytics
WHERE units_sold IS NOT NULL
) as alt
JOIN all_sessions ses
USING(full_visitor_id)
GROUP BY country, city
ORDER BY avg_ordered DESC

```


Answer:
Excluding the cities in the USA with no names available in demo data, the average number of products sold vary between a highest of 

53 units sold per customer from San Bruno, USA

25 units sold per customer from the country of Czechia

20 units sold per customer from Montain View, USA

12 units sold per customer from San Jose, USA

less than 10 items per customer in the rest of the list of 102 rows.


**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
```SQL
SELECT ses.v2_productcategory, ses.country, ses.city,
	COUNT(ses.v2_productcategory) as count_category
FROM (
SELECT DISTINCT * 
FROM analytics
WHERE units_sold IS NOT NULL
) as alt
JOIN all_sessions ses
USING(full_visitor_id)
GROUP BY ses.v2_productcategory, ses.country, ses.city
ORDER BY count_category DESC, country, city
```

Answer:

The datta based on product category would suggest that:

1. In the United States, Pet accesories, accesories, apparels, NEST as well as notbooks & journals have high amount of units sold. 

2. The city of Mountain View, USA buy a lot of Nest. The city of Charlotte, USA buy a lot of bags and the city of Sunnyvale, USA buy a lot of housewares. 

3. The city of Hong Kong buy a lot of electronic accesories.

4. The other countries do not have enough purchase records to draw any confident conclusions


**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:
```SQL
SELECT DISTINCT ses.v2_productname, ses.country, ses.city, SUM(revenue) as revenue
FROM (
SELECT DISTINCT * 
FROM analytics
WHERE revenue IS NOT NULL
) as alt
JOIN all_sessions ses
USING(full_visitor_id)
GROUP BY v2_productname, country, city
ORDER BY revenue DESC
```

Answer:

The top selling product in the United States is Straw Beach Mat with 9522 USD revenue

When it comes to the cities in the United States :

- 22oz Youtube Bottle Infuser is the most popular in San Bruno at 3312 USD revenue

- Nest Cam Indoor Security Camera is the most popular in Mountain View at 1752 USD revenue

- Google Men's Convertible Vest-Jacket Pewter is the most popular item in Sunnyvale at 949 USD revenue

- Google Laptop Tech Backpack in Jersey City

- Google Lunch Bag in Charlotte 

- Collapsible Shopping Bag in New York

- The revenue generated in other countries is too low to provide enough data to obtain a trend




**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:
```SQL
SELECT ses.country, ses.city, SUM(revenue) as revenue, CASE
	WHEN NTILE(10) OVER(
		ORDER BY SUM(revenue)) > 7 THEN 'high'
	WHEN  NTILE(10) OVER(
		ORDER BY SUM(revenue)) > 4 THEN 'medium'
	ELSE 'low'
END as impact
FROM (
SELECT DISTINCT * 
FROM analytics
WHERE revenue IS NOT NULL
) as alt
JOIN all_sessions ses
USING(full_visitor_id)
GROUP BY country, city
ORDER BY revenue DESC
```

Answer:

From the data obtained, we can see all of the cities and locations that have a high and medium impact on the company revenue are located in the United States. The other countries that generate a revenue for the company, such as Canada, Germany, Japan and Switzerland, barely contribute to the total revenue of the company. 







