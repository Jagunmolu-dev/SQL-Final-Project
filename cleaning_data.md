What issues will you address by cleaning the data?
Conversion of datatypes from either integer or character varying to double precision to acccomodate the floating values after dividing by 1000000
Renamed the columns to reflect the unit of the converted columns i.e (in Millions)
Deleted duplicates from the tables
Replace NULL values of numeric columns with 0 and non Numeric columns with 'NA'


Queries:
Below, provide the SQL queries you used to clean your data.
-- Delete duplicates from the analytics and all_session table
DELETE FROM analytics
WHERE visitid IN (
    SELECT visitid
    FROM analytics
    GROUP BY visitid
    HAVING COUNT(*) > 1
);

DELETE FROM all_sessions_cleaned
WHERE fullvisitorid IN (
    SELECT fullvisitorid
    FROM all_sessions_cleaned
    GROUP BY fullvisitorid
    HAVING COUNT(*) > 1
);


-- To replace the 'not available in demo dataset' and '(not set)' in the city column by the values in the country field
UPDATE all_sessions_cleaned
SET city = CASE
    WHEN city = 'not available in demo dataset' OR city = '(not set)'
        THEN country
    ELSE city
    END;

-- Update the null values of numeric fields wit 0 
UPDATE all_sessions 
SET timeonsite = COALESCE(timeonsite, '0')

UPDATE analytics
SET timeonsite = COALESCE(timeonsite, '0')

UPDATE products
SET sentimentmagnitude = COALESCE(sentimentmagnitude, '0')

-- Converting datatype
ALTER TABLE all_sessions
ALTER COLUMN totaltransactionrevenue TYPE double precision
USING totaltransactionrevenue::double precision;

ALTER TABLE analytics_cleaned
ALTER COLUMN visitstarttime TYPE time
USING TIME '00:00:00' + visitstarttime * INTERVAL '1 second';

ALTER TABLE all_sessions
ALTER COLUMN productrevenue TYPE double precision
USING productrevenue::double precision;

-- Deleting columns
ALTER TABLE all_sessions
DROP COLUMN searchkeyword

-- Update the transactionrevenue column to cast it as divided by 1000000
UPDATE all_sessions 
SET transactionrevenue =  CAST (transactionrevenue/1000000 AS DECIMAL (10,3)) 

ALTER TABLE all_sessions 
RENAME COLUMN transactionrevenue TO transaction_revenue_in_millions;



UPDATE all_sessions
SET transactionrevenue =  COALESCE (transactionrevenue, '0') 

UPDATE all_sessions
SET ecommerceaction_option =  COALESCE (ecommerceaction_option, 'NA') 
