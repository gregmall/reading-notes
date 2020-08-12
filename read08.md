# Complete SQL Bold
* SQL- structured Query Language   
    - designed to allow both technical and non technical users to query, manipulate and transform data from a relational database.
- Relational database
    - represents a collection of related tables (similar to excel spreadsheets)
 * Select queries
- Select Statements (queries)
    - Select query for a specific columns
        SELECT column, another_column, …
        FROM mytable;
    - Select query for all columns (use asterisk)
        SELECT * 
        FROM mytable;
* Queries with constraints (pt 1)
    - Select query with constraints (use **WHERE** clause)
        SELECT column, another_column, …
        FROM mytable
        WHERE condition
            AND/OR another_condition
            AND/OR …;
* Queries with constraints (pt 2)
    - logical operators can be used
* Filtering and sorting query results
    - **DISTINCT** discards rows that have duplicate column value
        SELECT DISTINCT column, another_column, …
        FROM mytable
        WHERE condition(s);
    - **ORDER BY** sort by ascending/descending order
        SELECT column, another_column, …
        FROM mytable
        WHERE condition(s)
        ORDER BY column ASC/DESC;
    - **LIMIT** and **OFFSET** (limit reduces number of rows, offset specifies where to begin)
        SELECT column, another_column, …
        FROM mytable
        HERE condition(s)
        ORDER BY column ASC/DESC
        LIMIT num_limit OFFSET num_offset;
* Order of execution of a Query
SELECT DISTINCT column, AGG_FUNC(column_or_expression), …
FROM mytable
    JOIN another_table
      ON mytable.column = another_table.column
    WHERE constraint_expression
    GROUP BY column
    HAVING constraint_expression
    ORDER BY column ASC/DESC
    LIMIT count OFFSET COUNT;

   **FROM** and **JOIN** s
        - first executed to determine the total working set of data being queried
   **WHERE** 
        - constraints applied to individual rows. 
   **GROUP BY**
        - grouped by unique values in the column
   **HAVING**
        - constraint applied 
   **SELECT**
        - part of teh query that are finally computed
   **DISTINCT**
        - will discard duplicate values
   **ORDER BY**
        - set order
   **LIMIT/OFFSET**
        - rows outside this range are discarded
* Inserting rows
    - schema- describes the structure of each table and the datatypes that each colum of the table can contain
    - Inserting new data
        - **INSERT** 
        - Insert statement with values for all columns
        INSERT INTO mytable
        VALUES (value_or_expr, another_value_or_expr, …),
       (value_or_expr_2, another_value_or_expr_2, …),
       …;       
        - Insert statement with specific columns
        INSERT INTO mytable
        (column, another_column, …)
        VALUES (value_or_expr, another_value_or_expr, …),
        (value_or_expr_2, another_value_or_expr_2, …),
        …;
        - Example Insert statement with expressions
        NSERT INTO boxoffice
        (movie_id, rating, sales_in_millions)
        VALUES (1, 9.9, 283742034 / 1000000);
* Updating rows
    - **UPDATE** must specify exactly which table, column, row to update
    - Update statement with values
    UPDATE mytable
    SET column = value_or_expr, 
    other_column = another_value_or_expr, 
      …
    WHERE condition;
* Deleting rows
    - **DELETE** to **WHERE**
    - Delete statement with condition
    DELETE FROM mytable
    WHERE condition;
* Creating Tables
    - **CREATE TABLE**
    - Create table statement w/ optional table constraint and default value
        CREATE TABLE IF NOT EXISTS mytable (
            column DataType TableConstraint DEFAULT default_value,
            another_column DataType TableConstraint DEFAULT default_value,
            …
* Altering Tables
    - **ALTER TABLE** to add, remove or modify columns and table constraints
    - Altering table to add new column(s)
    ALTER TABLE mytable
    ADD column DataType OptionalTableConstraint 
        DEFAULT default_value;   
    - Removing columns
    - Altering table to remove column(s)
    ALTER TABLE mytable
    DROP column_to_be_deleted;  
    - Renaming the table
    - Altering table name
    ALTER TABLE mytable
    RENAME TO new_table_name;
* Dropping tables
    - **DROP TABLE** 
    - Drop table statement
    DROP TABLE IF EXISTS mytable;

# W3 schools practice
 Great hands on practice with SQL.  It let me put some of the things I learned in the tutorial into action.  FUN!

        




