# Final-Project-Transforming-and-Analyzing-Data-with-SQL

## Project/Goals
Transforming and Analyzing Data with SQL

## Process
### Created the required database and imported the provided tables into ther database
### Studied the dataset and cleaned the data containing NULL values, or inconsistent datatypes and also deleted redundant columns not needed for analysis
### Document any Quality Assurance (QA) notes.
### Answer questions from the data generated including part 3: starting with questions and part 4: starting with data

## Results
![schema](https://github.com/Jagunmolu-dev/SQL-Final-Project/assets/67484584/332c6b0a-a616-4e28-8d82-21646709f310)
### From studhying the dataset i had to find the connection between the tables provided, noting differnt names for the same column in different tables. Thereby using them as either primary keys or foreign keys for the different tables. The understanding of this connection helps to join tables as seen in the ERD diagram above

## Challenges 
1. Deciding on whether to replace null values in numeric fields with 0 or any of the measure of central tendency but i decided to replace with zero because the available values account for less 40% of the data so it would not make sense to use the mean or median.
2. Dealing with Duplicates
3. Inconsistent naming conventions

## Future Goals
1. Consult a subject matter expert to better understand the problem and the data. THEN irrelevant columns/tables could be dropped.
2. Redo the data export of the CSV so that the data/columns are in the correct tables.
3. Minimize duplicate data in the CSV files PRIOR to importing them into the database.
4. DIve more into the data to perform more ststistical analysis on the data

