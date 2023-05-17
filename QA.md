What are your risk areas? Identify and describe them.
Data Quality: The raw data provided contains a lot of inaccuracies, inconsistencies, duplicates, NULLS which must be addressed before any form of analysis can take place.


QA Process:
Describe your QA process and include the SQL queries used to execute it.
### I searched for nulls throughout the database
This is just som samples of colums i searched for nulls

SELECT *
FROM sales_by_sku
WHERE total_ordered IS NULL

SELECT *
FROM sales_report
WHERE sentimentmagnitude IS NULL

###Updated Null values for numeric fields with 0 and non numeric columns as 'NA'

UPDATE all_sessions 
SET timeonsite = COALESCE(timeonsite, '0')

UPDATE analytics
SET timeonsite = COALESCE(timeonsite, '0')

UPDATE products
SET sentimentmagnitude = COALESCE(sentimentmagnitude, '0')

UPDATE all_sessions
SET ecommerceaction_option =  COALESCE (ecommerceaction_option, 'NA') 



### Converted values to appropriate data types

ALTER TABLE analytics
ALTER COLUMN visitstarttime TYPE time
USING TIME '00:00:00' + visitstarttime * INTERVAL '1 second';


ALTER TABLE all_sessions
ALTER COLUMN totaltransactionrevenue TYPE double precision
USING totaltransactionrevenue::double precision;


ALTER TABLE all_sessions
ALTER COLUMN productrevenue TYPE double precision
USING productrevenue::double precision;

### Searching for duplicates
SELECT DISTINCT fullvisitorid
FROM all_sessions


### Deleting duplicates

DELETE FROM all_sessions
WHERE fullvisitorid IN (
    SELECT fullvisitorid
    FROM all_sessions
    GROUP BY fullvisitorid
    HAVING COUNT(*) > 1
