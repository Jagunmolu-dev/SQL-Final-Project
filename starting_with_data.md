Question 1: Search for duplicates using the visitorid

SQL Queries:
SELECT fullvisitorid, COUNT(*) as count
FROM all_sessions
GROUP BY fullvisitorid
HAVING COUNT(*) > 1;

Answer: 
-- returns 863 duplicates


Question 2: Display the products ordered by each customer limiting it to the first 10 

SQL Queries:

SELECT visitid, productSKU, v2ProductName as ProdName, v2ProductCategory as ProdCategory
FROM all_sessions
JOIN products ON all_sessions.productSKU = products.SKU
GROUP BY visitid, productSKU, ProdName, ProdCategory
Order By visitid
LIMIT 10

Answer:
![image](https://github.com/Jagunmolu-dev/SQL-Final-Project/assets/67484584/b6e3c2b4-6643-4273-8155-7dfc7535c248)



Question 3: 

SQL Queries:

Answer:



Question 4: 

SQL Queries:

Answer:



Question 5: 

SQL Queries:

Answer:
