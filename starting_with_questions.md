Answer the following questions and provide the SQL queries used to find the answer.

    
**Question 1: Which cities and countries have the highest level of transaction revenues on the site?**


SQL Queries:
SELECT city, country, transaction_revenue_in_millions
FROM all_sessions
HAVING transaction_revenue_in_millions = (
    SELECT MAX(transaction_revenue_in_millions)
    FROM all_sessions
);


-- Alternative Solution
SELECT MAX(transaction_revenue_in_millions)
    FROM all_sessions

SELECT city, country, transaction_revenue_in_millions
FROM all_sessions
WHERE transaction_revenue_in_millions = 1005.5

Answer:
![image](https://github.com/Jagunmolu-dev/SQL-Final-Project/assets/67484584/86b286be-5bba-4699-b294-fe87453cd575)



**Question 2: What is the average number of products ordered from visitors in each city and country?**


SELECT  a.country, a.city, AVG(p.orderedquantity)
FROM all_sessions AS a
JOIN products AS p 
ON a.productsku = p.sku
WHERE 
    city <> '(not set)'
GROUP BY country, city
LIMIT 10;

Answer:
![image](https://github.com/Jagunmolu-dev/SQL-Final-Project/assets/67484584/e6819350-8e91-4ab3-a9f2-054848d32904)



**Question 3: Is there any pattern in the types (product categories) of products ordered from visitors in each city and country?**


SQL Queries:
SELECT  country, city, v2productname, v2productcategory
FROM all_sessions 
WHERE 
    city <> '(not set)'
GROUP BY v2productcategory, country, city, v2productname
LIMIT 10;

Answer:

![image](https://github.com/Jagunmolu-dev/SQL-Final-Project/assets/67484584/5ab10e35-e284-4ccb-b38e-ef96579f48d5)


From the result gathered there is no obvious pattern between the country and the product category

**Question 4: What is the top-selling product from each city/country? Can we find any pattern worthy of noting in the products sold?**


SQL Queries:

WITH top_products AS (
SELECT  a.v2productname, a.country, a.city,
       RANK() OVER (PARTITION BY a.v2productname ORDER BY SUM(p.orderedquantity) DESC) AS r
FROM all_sessions AS a
JOIN products AS p ON a.productsku = p.sku
GROUP BY  a.v2productname, a.country, a.city)

SELECT *
FROM top_products
WHERE r = 1
LIMIT 10;

Answer:
![image](https://github.com/Jagunmolu-dev/SQL-Final-Project/assets/67484584/af23073a-6f9f-4b6b-aaee-8718804856a6)





**Question 5: Can we summarize the impact of revenue generated from each city/country?**

SQL Queries:

SELECT *
FROM all_sessions
WHERE transaction_revenue_in_millions != 0 

Answer:
[data-1684344394700.csv](https://github.com/Jagunmolu-dev/SQL-Final-Project/files/11500992/data-1684344394700.csv)
From the result generated we cannot make any conclusions on the impact of revenue generated from each city/ country because the column "total_revenue_in_millions returned 2 rows which is insufficient to make conclusions






