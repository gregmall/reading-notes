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
* 