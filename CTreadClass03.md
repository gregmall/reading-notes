# Inside a Computer 
* Motherboard
    - main circuit board inside a computer where cpu, hard drive, ram, video controllers and ports connect to
* CPU
    - Main processing chip for the computer located on the motherboard.  Generally it is covered by a heatsink in order to keep it cool
* RAM
    - Random access memory.  
    - Short term memory for the computer.  
    - Is erased when computer is shut off
* Hard drive
    - place where software, documents and other files are stored.  
    - long term storage for the computer
* Power supply unit
    - powers the computer using A/C power from a standard wall outlet
* Expansion cards
    - video card
        - responsible for graphics seen on the monitor
        - contain a GPU ( Graphics processing unit)
    - sound card
        - also called audio card
        - responsible for what you hear in the speakers or headphones
    - network card
        -  allows computer to communicate over a network and access the internet
    - bluetooth card(or adapter)
        - allows for wireless connection of peripheral devices (mouse, keyboard, etc)

# PostgreSQL INSERT
* **INSERT** statement allows you to insert a new row into a table
- example:
```
INSERT INTO table_name(column1, column2, …)
VALUES (value1, value2, …);
```
* **RETURN** returns the information of the inserted row
- example:
```
INSERT INTO table_name(column1, column2, …)
VALUES (value1, value2, …)
RETURNING *;
```
- the following returns the **id** of the inserted row:
```
INSERT INTO table_name(column1, column2, …)
VALUES (value1, value2, …)
RETURNING id;
```
- rename using **AS** :
```
INSERT INTO table_name(column1, column2, …)
VALUES (value1, value2, …)
RETURNING output_expression AS output_name;
```
* the following creates a new table called **links**:
```
DROP TABLE IF EXISTS links;

CREATE TABLE links (
	id SERIAL PRIMARY KEY,
	url VARCHAR(255) NOT NULL,
	name VARCHAR(255) NOT NULL,
	description VARCHAR (255),
        last_update DATE
);
```
* inserting single row into a table:
```
INSERT INTO links (url, name)
VALUES('https://www.postgresqltutorial.com','PostgreSQL Tutorial');
```
# PostgreSQL SELECT
* syntax of **SELECT** statement:
  nb
- **SELECT** statement to find the first names of all customers from the customer table:
```
SELECT first_name FROM customer;
```
- **SELECT** statement to select data from all columns of the customer table:
```
SELECT * FROM customer;
```
 - **SELECT** statement to return full names and emails of customers:
 ```
 SELECT 
   first_name || ' ' || last_name,
   email
FROM 
   customer;
```
# PostgreSQL UPDATE
* **UPDATE** allows you to modify data in the table
- example:
```
UPDATE table_name
SET column1 = value1,
    column2 = value2,
    ...
WHERE condition;
```
- returning updated rows:
```
UPDATE table_name
SET column1 = value1,
    column2 = value2,
    ...
WHERE condition
RETURNING * | output_expression AS output_name;
```
- **UPDATE** statement to update the course with id 3:
```
SELECT * 
FROM courses
WHERE course_id = 3;
```
- modifies published_date of the course to 2020-07-01 and returns the updated course:
```
UPDATE courses
SET published_date = '2020-07-01'
WHERE course_id = 2
RETURNING *;
```
# PostegreSQL DELETE
* **DELETE** allows you to delete one or more rows from a table
- basic syntax example:
```
DELETE FROM table_name
WHERE condition;
```
- to return deleted rows to the client use **RETURNING** :
```
DELETE FROM table_name
WHERE condition
RETURNING (select_list | *)
```
* example table:
```
DROP TABLE IF EXISTS links;

CREATE TABLE links (
        id serial PRIMARY KEY,
        url varchar(255) NOT NULL,
        name varchar(255) NOT NULL,
        description varchar(255),
        rel varchar(10),
        last_update date DEFAULT now()
);

INSERT INTO
    links
VALUES

```
- deleting one frow from the table:
```
DELETE FROM links
WHERE id = 8;
```

- deleting a row and returning deleted row:
```
DELETE FROM links
WHERE id = 7
RETURNING *;
```
- deleting multiple rows:
```
DELETE FROM links
WHERE id IN (6,5)
RETURNING *;
```
- deleting all rows from table:
```
DELETE FROM links;
```