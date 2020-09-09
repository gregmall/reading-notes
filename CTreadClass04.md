# PostgreSQL Joins
* **JOIN** is used to combine columns form one or more tables based on the values of the common columns between related tables
- **primary key** columns of the first table **foreign key** columns from the second table.
- Example 
```
CREATE TABLE basket_a (
    a INT PRIMARY KEY,
    fruit_a VARCHAR (100) NOT NULL
);

CREATE TABLE basket_b (
    b INT PRIMARY KEY,
    fruit_b VARCHAR (100) NOT NULL
);

INSERT INTO basket_a (a, fruit_a)
VALUES
    (1, 'Apple'),
    (2, 'Orange'),
    (3, 'Banana'),
    (4, 'Cucumber');

INSERT INTO basket_b (b, fruit_b)
VALUES
    (1, 'Orange'),
    (2, 'Apple'),
    (3, 'Watermelon'),
    (4, 'Pear');
```
- inner join
-  joins the first table (basket_a) with the second table (basket_b) by matching the values in the fruit_a and fruit_b columns
``` 
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
INNER JOIN basket_b
    ON fruit_a = fruit_b;
```
- left join
- the basket_a table with the basket_b table.
```
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
LEFT JOIN basket_b 
   ON fruit_a = fruit_b;
```
- left outer join
- use the left join with a WHERE clause.
```
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
LEFT JOIN basket_b 
    ON fruit_a = fruit_b
WHERE b IS NULL;
```
- right join
- right join to join the basket_a table with the basket_b table
```
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
RIGHT JOIN basket_b ON fruit_a = fruit_b;
```
- right inner join
-  get rows from the right table that do not have matching rows from the left table by adding a WHERE clause as follows
```
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
RIGHT JOIN basket_b 
   ON fruit_a = fruit_b
WHERE a IS NULL;
```
- full outer join
- returns a result set that contains all rows from both left and right tables, with the matching rows from both sides if available
```
SELECT
    a,
    fruit_a,
    b,
    fruit_b
FROM
    basket_a
FULL OUTER JOIN basket_b 
    ON fruit_a = fruit_b;
```
# One-to-one (data model)
* A relationship between two entities where one element of A may only be linked to one element of B.  In a relational database, it is where one row in a table may be linked with only one row in another table.

# One-to-many (data model)
* A relationship between two entities  where one element of A may be linked to many elements of B but a member of B is linked to only one element of A.
In a relational database, it is where one row in table A may be linked with many rows in table B but one row in table B is linked to only one row in table A.

# Many-to-many (data model)
* A relationship between two entities where A and B in which A may contain a parent instances for which there are many children in B and vice versa.  In a relational database, these relationships are implemented by means of an associative table(join table).