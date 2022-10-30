# SQL-Fundamentals
Fundamentals about Structured Query Language

### What is a database?
- A collection of data, like a Phonebook
- A method for accessing and manipulating that data, linke find all people with firstName='Ned'

### What is a Database Management System?
> (Jargon Terminology - DMS, DBMS, RDBMS etc)
- As the name suggests DBMS basically handles all transaction with DB, example PostgreSQL, MySQL, SQLite, Oracle Database etc.
- A structured set of computerized data with an accessible interface

### MySQL vs SQL
- SQL(Structured Query Language) is the language we use to talk to the DB.
  eg. SELECT * FROM Users WHERE Age>=18;
- MySQL is a DBMS which uses SQL as the medium of communication.
- Not only MySQL but all the Relational Databases(PostgreSQL etc) use SQL.

## Some basic commands:-
- to start mysql server:
`mysql-ctl start`
- to open mysql cli:
`mysql-ctl cli`
- to stop mysql server:
`mysql-ctl stop`
- to get help:
`help;`
- to display all available databases:
`show databases;`
- to display all available hosts:
`select @@hostname;`
- to quit cli:
`exit;`
`quit;`
`\q;`
<kbd>⌘ C</kbd>
- to exit your mysql setup out of strict mode:
`SET @@global.sql_mode= '';`
- to view warning only after it's raised in subsequent command:
`SHOW WARNINGS;`
- run sql file
`SOURCE <filename>.sql`

## Database:-
- create a new database:
```
CREATE DATABASE <db_name>;
```
- to select the database;
```
USE <db_name>;
```
- delete the database
```
DROP DATABASE <db_name>;
```
- to view currently working database:
```
SELECT database();
```
- comment lines in sql using `--` infront of them

## Table:-
- create table(keep table name plural):
```
CREATE TABLE  <name> 
(
	<column_name> <data_type> <constraints>, 
	<column_name> <data_type> <constraints>
);
```
- display all tables:
```
SHOW TABLES;
```
- display description of a table:
```
SHOW COLUMNS FROM <table_name>;
DESC <table_name>;
DESCRIBE <table_name>;
```
- deleting table:
```
DROP TABLE <table_name>;
```
- insert data into table:
```
INSERT INTO <table_name> (<column_name1>, <column_name2>)
VALUES (<value1>, <value2>);
```
- insert multiple data into table:
```
INSERT INTO <table_name> (<column_name1>, <column_name2>)
VALUES (<value1>, <value2>), (<value1>, <value2>), (<value1>, <value2>);
```
- not null constraint on column(column will be assigned default values and error thrown when NULL is passed):
```
CREATE TABLE  <name> (
	<column_name> <data_type> NOT NULL, ...
```
- unique constraint on column:
```
CREATE TABLE  <name> (
	<column_name> <data_type> UNIQUE, ...
```
- default constraint on column:
```
CREATE TABLE  <name> (
	<column_name> <data_type> DEFAULT <default_value>, ...
```
- primary key constraint on column making it a unique identifier:
```
CREATE TABLE  <name> (
	id INT NOT NULL,
	<column_name> <data_type> <constraints>,  ...
	PRIMARY KEY(id, ...)
);
```
```
CREATE TABLE  <name> (
	id INT NOT NULL PRIMARY KEY,
	<column_name> <data_type> <constraints>,  ...
);
```
- adding auto_increment constraint to assign primary key automatically:
```
CREATE TABLE  <name> (
	id INT NOT NULL AUTO_INCREMENT,
	<column_name> <data_type> <constraints>,  ...
	PRIMARY KEY(id, ...)
);
```
- foreign key constraint on column making it a unique identifier of other table:
```
CREATE TABLE  <table_name1> (
	id INT PRIMARY KEY,
	<column_name> <data_type> <constraints>,  ...
	fid INT,
	FOREIGN KEY(fid) REFERENCES <table_name2>(id)
);
```
- on delete cascade:
```
CREATE TABLE  <table_name1> (
	id INT PRIMARY KEY,
	<column_name> <data_type> <constraints>,  ...
	fid INT,
	FOREIGN KEY(fid) 
		REFERENCES <table_name2>(id) 
		ON DELETE CASCADE
);
```
- check constraint on column:
```
CREATE TABLE  <table_name> (
	<column_name> <data_type> CHECK(column_name <condition>),
	...
); 
```
- alter table (add column):
```
ALTER TABLE <table_name> ADD <column_name> <data_type> <constraints>;
```

## CRUD operations on table:-
- create data and table:
```
CREATE TABLE cats 
  ( 
     cat_id INT NOT NULL AUTO_INCREMENT, 
     name   VARCHAR(100), 
     breed  VARCHAR(100), 
     age    INT, 
     PRIMARY KEY (cat_id) 
  ); 
DESC cats;
INSERT INTO cats(name, breed, age) 
VALUES ('Ringo', 'Tabby', 4),
       ('Cindy', 'Maine Coon', 10),
       ('Dumbledore', 'Maine Coon', 11),
       ('Egg', 'Persian', 4),
       ('Misty', 'Tabby', 13),
       ('George Michael', 'Ragdoll', 9),
       ('Jackson', 'Sphynx', 7);
```
- read data from table:
```
SELECT * FROM <table_name>;
SELECT <column_name> FROM <table_name>;
SELECT <column_name>, <column_name> ... FROM <table_name>;
```

- read selective data from table(WHERE clause is case-insensitive by default):
```
SELECT * FROM <table_name> WHERE <condition>;
```
- display with aliases:
```
SELECT <column_name1> AS <column_alias> FROM <table_name>;
```
- updating data in the table(good practise to use SELECT before to check if correct data will be updated):
```
UPDATE <table_name> SET <new_value> WHERE <condition>;
```
- deleting data in the table(good practise to use SELECT before to check if correct data will be updated):
```
DELETE FROM <table_name> WHERE <condition>;
```
- delete all data from a table:
```
DELETE FROM <table_name>;
```

## String Operations(combination of operation is also allowed):-
- concat:
```
SELECT CONCAT("Hello", " ", " World", "!");
SELECT CONCAT(<column_name1>, <column_name2>, <text>, ...> FROM <table_name>;
```

-concat with separator:
```
SELECT CONCAT(<>, <string1>, <string2>, <string3>,...)
```

- substring(indexing starts from 1 not 0, negative index are counted from right):
```
SELECT SUBSTR(<string>,  start_index)
SELECT SUBSTRING(<string>,  start_index)
SELECT SUBSTRING(<string>,  start_index, end_index)
SELECT SUBSTRING(<column_name>,  start_index, end_index) FROM <table_name>;
```

- replace(this is case-sensitive):
```
SELECT REPLACE(<string>, <to_replace>, <replace_by>)
SELECT REPLACE(<column_name>, <to_replace>, <replace_by>) FROM <table_name>
```

- reverse:
```
SELECT REVERSE(<string>);
SELECT REVERSE(<column_name>) FROM <table_name>;
```

- length:
```
SELECT CHAR_LENGTH(<string>);
SELECT CHAR_LENGTH(<column_name>) FROM <table_name>;
```

- upper and lower:
```
SELECT UPPER(<string>);
SELECT LOWER(<string>);
SELECT UPPER(<column_name>) FROM <table_name>;
SELECT LOWER(<column_name>) FROM <table_name>;
```

-trim white spaces:
```
SELECT TRIM(<string>);
SELECT LTRIM(<string>);
SELECT RTRIM(<string>);
SELECT TRIM(<string>, <delimiter>);
```


## Constraints on SELECT:-
- distinct:
```
SELECT DISTINCT <column_name1>, <column_name2>,... FROM <table_name>;
```

- order by:
```
SELECT <column_name1>, <column_name2>,... FROM <table_name>
ORDER BY <column_name1> <order-ASC/DESC>;
SELECT <column_name1>, <column_name2>,... FROM <table_name>
ORDER BY <index> <order-ASC/DESC>;
SELECT <column_name1>, <column_name2>,... FROM <table_name>
ORDER BY <column_name1> <order-ASC/DESC>,  <column_name2> <order-ASC/DESC>;
```

- limit:
```
SELECT <column_name1>, <column_name2>,... FROM <table_name> LIMIT <count>;
SELECT <column_name1>, <column_name2>,... FROM <table_name> LIMIT <start_index>, <count>;
```

-like:
```
SELECT <table_name> SET <new_value> WHERE <column_name> LIKE <pattern>;
*pattern = % is wildcard for any (*), _  is wildcard for exactly one (.), is case-insensitive, \% and \_ are escape sequences
```

## Aggregate Functions:-
- count:
```
SELECT COUNT(*) FROM <table_name>;
SELECT COUNT(DISTINCT <column_name1>,  <column_name2>) FROM <table_name>;
SELECT <column_name>, COUNT(*) FROM <table_name> ORDER BY <column_name>;
```

- group by:
```
SELECT <column_name1>, <column_name2>,... FROM <table_name> GROUP BY <column_name1>,...;
* WHERE doesnot work after using group by so use Having instead
SELECT <column_name1>, <column_name2>,... FROM <table_name> 
GROUP BY <column_name1>,... HAVING <condition>;
```

- min & max:
```
SELECT MIN(<column_name>)  FROM <table_name>;
SELECT MAX(<column_name>)  FROM <table_name>;
```

- sum:
```
SELECT SUM(<column_name>)  FROM <table_name>;
```

- avg
```
SELECT AVG(<column_name>)  FROM <table_name>;
```

## Data Type
- Numeric Types = INT, SMALLINT, TINYINT, MEDIUMINT, BIGINT, DECIMAL, NUMERIC, FLOAT, DOUBLE, BIT, MONEY, REAL
- String Types = CHAR, VARCHAR, BINARY, VARBINARY, BLOB, TINYBLOB, MEGIUMBLOB, LONGBLOB, TEXT, TEXT, TINYTEXT, MEDIUMTEXT, LONGTEXT, ENUM
- Date Types = DATE, DATETIME, TIMESTAMP, TIME, YEAR

---
* CHAR(size) = fixed length, if less than specified length is present then space is added, overflow is omitted,  faster
* VARCHAR(size) = variable length, utilizes less space, overflow is omitted
* DECIMAL(size, afterDecimal) = accurate
* FLOAT,  DOUBLE = faster, less space, cost precision, fixed size of 4 and 8 bytes
* DATE = 'YYYY-MM-DD' format, CURDATE() to get current date
* TIME = 'HH:MM:SS' format, CURTIME() to get current time
* DATETIME = 'YYYY-MM-DD HH:MM:SS' format, NOW() to get current datetime, year range 1000-9999
- datetime functions: DAY(), DAYNAME(), DAYOFWEEK(), DAYOFYEAR(), MONTHNAME(), HOUR() etc.
- datetime formatting: DATE_FORMAT()
- datemath: DATEDIFF(),  DATE_ADD(NOW(), INTERVAL 1 MONTH)-SECOND-HOUR-QUARTER-YEAR
- datearithmetic: use +/- for operations
* TIMESTAMPS = year range 1979-2038 
`eg. created_at TIMESTAMP DEFAULT NOW() ON UPDATE CURRENT_TIMESTAMP`

- get type of data:
```
SELECT TYPEOF(<data>);
```

-integer division:
```
SELECT 1/2; --return 0
SELECT 1.0/2; --return 0.5
SELECT CAST(1 AS REAL)/2; --return 0.5
SELECT 1/2, 1%2; --return 0, 1
```

## Logical Operators:-
- where:
```
SELECT <column_name1>, ... FROM <table_name> WHERE <condition>;
*condition: a=b, a!=b, a>b, a<b, a<=b, a>=b, a IS NULL,
<condition1> && <condition2>,  
<condition1> AND <condition2>, 
<condition1> || <condition2>,  
<condition1> OR <condition2>, 
<column_name> BETWEEN <start> AND <end>,
<column_name> NOT BETWEEN <start> AND <end>,
<column_name> IN <list>,
<column_name> NOT IN <list>,
```

- where-like:
```
SELECT <column_name1>, ... FROM <table_name> WHERE <column_name> LIKE <pattern>;
SELECT <column_name1>, ... FROM <table_name> WHERE <column_name> NOT LIKE <pattern>;
```

- switch case:
```
SELECT <column_name1>, ...
    CASE 
        WHEN <condition> THEN <statement>
        WHEN <condition> THEN <statement> ...
        ELSE <statement>
    END
FROM <table_name>;
```


## Functions:-
- cast:
```
CAST('1980-01-01' AS DATETIME)
```

- is null check 
```
SELECT IFNULL(<column_name>, 0) FROM <table_name>;
```

-round:
```
SELECT ROUND(<float>, <decimal_places>;
```


## Relational Databases: 
- cartesian or cross join:
```
SELECT * FROM <table1>, <table2>;
SELECT * FROM <table1> JOIN <table2>;
```

- inner join:
```
SELECT * FROM <table1>, <table2> WHERE <table1>.id = <table2>.fid;
SELECT * FROM <table1> JOIN <table2> ON <table1>.id = <table2>.fid;
SELECT * FROM <table1> INNER JOIN <table2> ON <table1>.id = <table2>.fid;
```

- left join:
```
SELECT * FROM <table1> LEFT JOIN <table2> ON <table1>.id = <table2>.fid;
```

-right join:
```
SELECT * FROM <table1> RIGHT JOIN <table2> ON <table1>.id = <table2>.fid;
```

- multiple table join:
```
SELECT * FROM <table1> 
INNER JOIN <table2> ON <table1>.id = <table2>.fid
INNER JOIN <table3> ON <table1>.id = <table3>.fid;
```

- union(to combine all the columns):
```
SELECT * FROM <table1>
UNION
SELECT * FROM <table2>;
```


## Database Triggers(better to be done in backend server code these are just optional):-

- show triggers in the database:
```
SHOW TRIGGERS;
```

- create trigger:
```
CREATE TRIGGER <trigger_name>
	<trigger_time> <trigger_event> ON <table_name> FOR EACH ROW
	BEGIN
	...
	END;
*trigger_time: BEFORE, AFTER
*trigger_event: INSERT, UPDATE, DELETE
```

example:
```
DELIMITER $$

CREATE TRIGGER must_be_adult
	BEFORE INSERT ON users  FOR EACH ROW
	BEGIN
		IF NEW.age<18
		THEN
			SIGNAL SQLSTATE '45000'
				SET MESSAGE_TEXT='Must be an adult!';
		END IF;
	END;
$$

DELIMITER ;
```

- delete a trigger:
```
DROP TRIGGER <trigger_name>;
```


## Views (Basically tables can be combined to a view and then view can be used to interface with refined query):
- create view:
```
CREATE VIEW <view_name> AS <query>;
```

example:
`View: public.actor_info`

```
DROP VIEW public.actor_info;

CREATE OR REPLACE VIEW public.actor_info
 AS
 SELECT a.actor_id,
    a.first_name,
    a.last_name,
    group_concat(DISTINCT (c.name::text || ': '::text) || (( SELECT group_concat(f.title::text) AS group_concat
           FROM film f
             JOIN film_category fc_1 ON f.film_id = fc_1.film_id
             JOIN film_actor fa_1 ON f.film_id = fa_1.film_id
          WHERE fc_1.category_id = c.category_id AND fa_1.actor_id = a.actor_id
          GROUP BY fa_1.actor_id))) AS film_info
   FROM actor a
     LEFT JOIN film_actor fa ON a.actor_id = fa.actor_id
     LEFT JOIN film_category fc ON fa.film_id = fc.film_id
     LEFT JOIN category c ON fc.category_id = c.category_id
  GROUP BY a.actor_id, a.first_name, a.last_name;

ALTER TABLE public.actor_info
    OWNER TO postgres;
```

## Transactions
>To execute multiple queries in one session which improves performance
```
BEGIN TRANSACTION
// queries\\
END TRANSACTION
```

- revert the changes made in before transaction
```
ROLLBACK;
```
