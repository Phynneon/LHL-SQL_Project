Question 1: 
Provide a count of unique visitors on the website.
SQL Queries:
```SQL
SELECT COUNT(DISTINCT full_visitor_id) as visitor_count, 
    MIN(date) as period_start, 
    MAX(date) as period_end
FROM analytics
```
Answer: 

There are a total of 120018 unique visitors between 2017-05-01 and 2017-08-01.


Question 2: 
What portion of visitors make at least one purchase?

SQL Queries:
```SQL
SELECT COUNT(DISTINCT full_visitor_id) as visitor_count,
	(SELECT COUNT(DISTINCT full_visitor_id)
	 		FROM analytics
			WHERE units_sold > 0) as buyer_count
FROM analytics
```
Answer:

Only 16063 visitors bought something out 120018 total visitors 


Question 3: How many visitors made more than one visit?

SQL Queries:
```SQL
SELECT DISTINCT full_visitor_id, COUNT(DISTINCT date) as visit
FROM (
	SELECT DISTINCT * 
	FROM analytics 
) AS alt
GROUP BY full_visitor_id
HAVING COUNT(DISTINCT date) > 1
ORDER BY visit DESC 
```

Answer:

There are 11553 unique visitors that made more than one visit to the website. The visitor with the highest amount of visit had made 50 visits. 
