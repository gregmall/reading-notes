# SQLBolt (5-8)
**JOIN** combines row data across two separate tables
    **INNER JOIN** process that matches rows from the first table and the second table which have the same key to create a result row with the combined columns from both tables.
Select query with INNER JOIN on multiple tables
SELECT column, another_table_column, …
FROM mytable
INNER JOIN another_table 
    ON mytable.id = another_table.id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
    **OUTER JOIN**
    - LEFT JOIN, RIGHT JOIN, FULL JOIN

Select query with LEFT/RIGHT/FULL JOINs on multiple tables
SELECT column, another_column, …
FROM mytable
INNER/LEFT/RIGHT/FULL JOIN another_table 
    ON mytable.id = another_table.matching_id
WHERE condition(s)
ORDER BY column, … ASC/DESC
LIMIT num_limit OFFSET num_offset;
**NULL**
 - needed when database needs to store incomplete data

 Select query with constraints on NULL values
SELECT column, another_column, …
FROM mytable
WHERE column IS/IS NOT NULL
AND/OR another_condition
AND/OR …;

# Database Normalization (explained in Simple English)

* Database normalization: process used to organize a database into tables and columns
- Purposes 
    - Identify sales people in your organization
    - List all customers your company calls upon to sell a product
    - Identify which salespeople call on specific customers.
* Reasons for Database Normalization
- minimize data duplication
- minimize data modification issues
- simplify queries
* Data Duplication and Modification Anomalies
- data duplication increases storage/decreases performance and becomes more difficult to maintain changes
* Database Normalization Definition
    - First Normal Form – The information is stored in a relational table with each column containing atomic values. There are no repeating groups of columns.
    - Second Normal Form – The table is in first normal form and all the columns depend on the table’s primary key.
    - Third Normal Form – the table is in second normal form and all of its columns are not transitively dependent on the primary key

# Visual Representation of SQL joins
This is a great resource to see joins in SQL  website here for further reference: https://www.codeproject.com/Articles/33052/Visual-Representation-of-SQL-Joins