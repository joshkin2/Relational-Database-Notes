# Start Here

## Connect to PostgreSQL

```sql
psql -U username -d postgres
```

## Create a Database

```sql
CREATE DATABASE my_database;
```

## Connect to a Database

```sql
\c my_database
```

---

# Main Project

## Mario Database

The Mario Database project demonstrates:

* One-to-one relationships
* One-to-many relationships
* Many-to-many relationships
* Foreign key constraints
* SQL joins
* Data normalization

---

# Example Schema

```sql
CREATE TABLE characters (
  character_id SERIAL PRIMARY KEY,
  name VARCHAR(30) NOT NULL,
  homeland VARCHAR(50),
  favorite_color VARCHAR(20)
);
```

---

# Learning Reflections

Working on relational databases helped me understand:

* Why data integrity matters
* How backend systems structure information
* Why relationships between tables are critical
* How schema design impacts scalability
* How efficient queries improve application performance
* How relational databases support real-world software systems

---

# Future Improvements

* Stored procedures
* Database views
* Query optimization
* Advanced indexing
* Database backups and restoration
* Role-based permissions

---

````

---

## Connect to PostgreSQL

```sql
psql -U <username> -d <database_name>
````

If you do not have a custom database yet, PostgreSQL includes a default database called:

```sql
postgres
```

Example:

```sql
psql -U freecodecamp -d postgres
```

---

# Useful psql Commands

| Command            | Description              |
| ------------------ | ------------------------ |
| `\l`               | List all databases       |
| `\c database_name` | Connect to database      |
| `\d`               | list all tables in current DB |
| `\d table_name`    | Describe table structure |
| `\q`               | Exits the PostgreSQL client|

---

# Create a Database

```sql
CREATE DATABASE my_database;
```

---

# Connect to a Database

```sql
\c my_database
```

---

# Delete a Database

```sql
DROP DATABASE my_database;
```

````

---

# fundamentals/creating_tables.md

```md id="5k3lf4"
# Creating Tables

## Basic Table Structure

```sql
CREATE TABLE table_name(
  column1 data_type constraint,
  column2 data_type constraint
);
````

---

# Example

```sql
CREATE TABLE products (
  id SERIAL PRIMARY KEY,
  name VARCHAR(255)
);
```

---

# Snake Case Naming Convention

Use lowercase words separated by underscores.

Example:

```sql
delivery_orders
```

---

# Add Columns to Existing Tables

```sql
ALTER TABLE products
ADD COLUMN price NUMERIC(5,2);
```

---

# Rename Columns

```sql
ALTER TABLE products
RENAME COLUMN price TO product_price;
```

---

# Remove Columns

```sql
ALTER TABLE products
DROP COLUMN product_price;
```

---

# Delete Tables

```sql
DROP TABLE products;
```

````

---

# fundamentals/data_types.md

```md id="s2l7ee"
# SQL Data Types

## Numeric Types

```sql
INTEGER
FLOAT
SERIAL
DECIMAL
NUMERIC
````

---

# Character Types

```sql
VARCHAR(50)
TEXT
CHAR
```

---

# Date and Time Types

```sql
DATE
TIME
TIMESTAMP
TIMESTAMP WITH TIME ZONE
```

---

# Boolean Type

```sql
BOOLEAN
```

---

# Examples

```sql
units_sold INTEGER

name VARCHAR(50)

event_date DATE

start_time TIME

event_timestamp TIMESTAMP

is_active BOOLEAN
```

---

# SERIAL in PostgreSQL

```sql
id SERIAL
```

SERIAL automatically:

* Creates an integer column
* Prevents NULL values
* Auto increments values

---

# MySQL Equivalent

```sql
id INT AUTO_INCREMENT
```

````

---

# fundamentals/inserting_data.md

```md id="lkjlwm"
# Inserting Data

## Create Example Table

```sql
CREATE TABLE dogs(
  id SERIAL,
  name VARCHAR(100),
  age INTEGER
);
````

---

# Insert One Row

```sql
INSERT INTO dogs (name, age)
VALUES ('Gino', 3);
```

---

# Insert Multiple Rows

```sql
INSERT INTO dogs (name, age)
VALUES
  ('Gino', 3),
  ('Nora', 2);
```

---

# Insert Data into Mario Database

```sql
INSERT INTO characters(name, homeland, favorite_color)
VALUES
('Mario', 'Mushroom Kingdom', 'Red'),
('Luigi', 'Mushroom Kingdom', 'Green'),
('Peach', 'Mushroom Kingdom', 'Pink');
```

````

---

# fundamentals/querying_data.md

```md id="b7f9i6"
# Querying Data

## Select All Columns

```sql
SELECT *
FROM dogs;
````

---

# Select Specific Columns

```sql
SELECT name, age
FROM dogs;
```

---

# Filter Data with WHERE

```sql
SELECT *
FROM dogs
WHERE age < 3;
```

---

# Another Example

```sql
SELECT age
FROM dogs
WHERE name = 'Gino';
```

---

# Order Results

```sql
SELECT *
FROM characters
ORDER BY character_id;
```

---

# Aggregate Functions

## COUNT()

```sql
SELECT COUNT(*)
FROM characters;
```

## AVG()

```sql
SELECT AVG(weight)
FROM more_info;
```

## GROUP BY

```sql
SELECT favorite_color, COUNT(*)
FROM characters
GROUP BY favorite_color;
```

````

---

# fundamentals/updating_and_deleting.md

```md id="9woxw0"
# Updating and Deleting Data

## Update Existing Rows

```sql
UPDATE characters
SET favorite_color='Orange'
WHERE name='Daisy';
````

---

# Another Update Example

```sql
UPDATE characters
SET name='Toad'
WHERE favorite_color='Red';
```

---

# Delete Specific Rows

```sql
DELETE FROM second_table
WHERE username='Luigi';
```

---

# Delete Entire Table

```sql
DROP TABLE second_table;
```

````

---

# fundamentals/constraints_and_keys.md

```md id="9m8m4u"
# Constraints and Keys

## Primary Key

```sql
CREATE TABLE students (
  student_id SERIAL PRIMARY KEY,
  name VARCHAR(100)
);
````

Primary keys:

* Must be unique
* Cannot contain NULL values

---

# Composite Primary Key

```sql
CREATE TABLE course_enrollments (
  student_id INT,
  course_id INT,
  PRIMARY KEY(student_id, course_id)
);
```

---

# Foreign Key

```sql
CREATE TABLE orders (
  order_id SERIAL PRIMARY KEY,
  customer_id INTEGER,
  FOREIGN KEY (customer_id)
  REFERENCES customers(customer_id)
);
```

---

# UNIQUE Constraint

```sql
ALTER TABLE sounds
ADD COLUMN filename VARCHAR(40) NOT NULL UNIQUE;
```

---

# NOT NULL Constraint

```sql
ALTER TABLE more_info
ALTER COLUMN character_id
SET NOT NULL;
```

````

---

# relationships/joins.md

```md id="2up76v"
# SQL Joins

## INNER JOIN

Returns matching rows from both tables.

```sql
SELECT *
FROM products
INNER JOIN sales
ON products.product_id = sales.product_id;
````

---

# FULL OUTER JOIN

Returns all rows from both tables.

```sql
SELECT *
FROM products
FULL OUTER JOIN sales
ON products.product_id = sales.product_id;
```

---

# LEFT JOIN

Returns all rows from the left table.

```sql
SELECT *
FROM products
LEFT JOIN sales
ON products.product_id = sales.product_id;
```

---

# RIGHT JOIN

Returns all rows from the right table.

```sql
SELECT *
FROM products
RIGHT JOIN sales
ON products.product_id = sales.product_id;
```

---

# Join Three Tables

```sql
SELECT *
FROM character_actions
FULL JOIN characters
ON character_actions.character_id = characters.character_id
FULL JOIN actions
ON character_actions.action_id = actions.action_id;
```

````

---

# relationships/one_to_one.md

```md id="4w6r0x"
# One-to-One Relationships

A one-to-one relationship means:

- One record matches exactly one other record

Example:

- One character has one profile

---

# Example

```sql
CREATE TABLE more_info (
  more_info_id SERIAL PRIMARY KEY,
  birthday DATE,
  height NUMERIC(4,1),
  weight NUMERIC(4,1),
  character_id INT UNIQUE REFERENCES characters(character_id)
);
````

````

---

# relationships/one_to_many.md

```md id="7fwh1r"
# One-to-Many Relationships

A one-to-many relationship means:

- One record can relate to many records

Example:

- One character can have many sounds

---

# Example

```sql
CREATE TABLE sounds (
  sound_id SERIAL PRIMARY KEY,
  filename VARCHAR(40),
  character_id INT REFERENCES characters(character_id)
);
````

````

---

# relationships/many_to_many.md

```md id="skf3sy"
# Many-to-Many Relationships

A many-to-many relationship means:

- One record can connect to many records
- Those records can also connect back

Example:

- A character can perform many actions
- An action can belong to many characters

---

# Example

```sql
CREATE TABLE character_actions (
  character_id INT REFERENCES characters(character_id),
  action_id INT REFERENCES actions(action_id),
  PRIMARY KEY(character_id, action_id)
);
````

````

---

# projects/mario_database/mario_database_schema.sql

```sql id="fxcxls"
CREATE TABLE characters (
  character_id SERIAL PRIMARY KEY,
  name VARCHAR(30) NOT NULL,
  homeland VARCHAR(50),
  favorite_color VARCHAR(20)
);

CREATE TABLE more_info (
  more_info_id SERIAL PRIMARY KEY,
  birthday DATE,
  height NUMERIC(4,1),
  weight NUMERIC(4,1),
  character_id INT UNIQUE NOT NULL
  REFERENCES characters(character_id)
);

CREATE TABLE sounds (
  sound_id SERIAL PRIMARY KEY,
  filename VARCHAR(40) NOT NULL UNIQUE,
  character_id INT NOT NULL
  REFERENCES characters(character_id)
);

CREATE TABLE actions (
  action_id SERIAL PRIMARY KEY,
  action VARCHAR(20) NOT NULL
);

CREATE TABLE character_actions (
  character_id INT REFERENCES characters(character_id),
  action_id INT REFERENCES actions(action_id),
  PRIMARY KEY(character_id, action_id)
);
````

---

# projects/mario_database/mario_database_queries.sql

```sql id="3k1mfu"
INSERT INTO characters(name, homeland, favorite_color)
VALUES
('Mario', 'Mushroom Kingdom', 'Red'),
('Luigi', 'Mushroom Kingdom', 'Green'),
('Peach', 'Mushroom Kingdom', 'Pink');

SELECT *
FROM characters;

SELECT *
FROM characters
ORDER BY character_id;

SELECT *
FROM characters
FULL JOIN sounds
ON characters.character_id = sounds.character_id;
```

---

# advanced/indexing.md

````md id="8m4xcz"
# Indexing

Indexes improve query performance by speeding up searches.

---

# Create an Index

```sql
CREATE INDEX idx_character_name
ON characters(name);
````

---

# Why Indexes Matter

Indexes help databases:

* Search faster
* Reduce query execution time
* Improve scalability

---

# Tradeoffs

Indexes improve reads but can slightly slow down:

* INSERT operations
* UPDATE operations
* DELETE operations

````

---

# advanced/transactions.md

```md id="cx1h0n"
# Transactions

Transactions ensure database consistency.

---

# Example

```sql
BEGIN;

UPDATE characters
SET favorite_color='Blue'
WHERE name='Mario';

COMMIT;
````

---

# Rollback Example

```sql
BEGIN;

DELETE FROM characters
WHERE name='Luigi';

ROLLBACK;
```

---

# Why Transactions Matter

Transactions help maintain:

* Data integrity
* Reliability
* Consistency

````

---

# advanced/normalization.md

```md id="0bdz8h"
# Database Normalization

Normalization helps organize data efficiently.

---

# First Normal Form (1NF)

Rules:

- No repeating groups
- Each column stores atomic values

---

# Second Normal Form (2NF)

Rules:

- Must satisfy 1NF
- Remove partial dependencies

---

# Third Normal Form (3NF)

Rules:

- Must satisfy 2NF
- Remove transitive dependencies

---

# Benefits of Normalization

- Reduces duplicate data
- Improves consistency
- Makes databases easier to maintain
````

---

# cheatsheets/postgresql_cheatsheet.md

````md id="0h3n4k"
# PostgreSQL Cheat Sheet

## Database Commands

```sql
\l
\c database_name
\d
\d table_name
````

---

# Create Database

```sql
CREATE DATABASE my_database;
```

---

# Create Table

```sql
CREATE TABLE users (
  user_id SERIAL PRIMARY KEY,
  username VARCHAR(50)
);
```

---

# Insert Data

```sql
INSERT INTO users(username)
VALUES('admin');
```

---

# Query Data

```sql
SELECT * FROM users;
```

---

# Update Data

```sql
UPDATE users
SET username='administrator'
WHERE user_id=1;
```

---

# Delete Data

```sql
DELETE FROM users
WHERE user_id=1;
```

---

# Joins

```sql
INNER JOIN
LEFT JOIN
RIGHT JOIN
FULL OUTER JOIN
```

---

# SQL Basics

---
## Queries: Requests to retrieve specific data from the database.
---
```sql
SELECT * FROM dogs WHERE age < 3;
```
* WHERE clause: Filter results based on conditions. Use comparison operators like <, =, >, etc.
## Select with ORDER BY: Retrieve and sort results based on a column.
```sql
SELECT columns FROM table_name ORDER BY column_name;
```
## Table Operations

CREATE TABLE Statement: This statement is used to create a new table in a database.
```sql
CREATE TABLE first_table();
```
ALTER TABLE ADD COLUMN Statement: This statement is used to add a column to an existing table.
```sql
ALTER TABLE table_name ADD COLUMN column_name DATATYPE;
```
ALTER TABLE DROP COLUMN Statement: This statement is used to drop a column from an existing table.
```sql
ALTER TABLE table_name DROP COLUMN column_name;
```
ALTER TABLE RENAME COLUMN Statement: This statement is used to rename a column in a table.
```sql
ALTER TABLE table_name RENAME COLUMN column_name TO new_name;
```
DROP TABLE Statement: This statement is used to drop an entire table from the database.
```sql
DROP TABLE table_name;
```
ALTER DATABASE RENAME Statement: This statement is used to rename a database.
```sql
ALTER DATABASE database_name RENAME TO new_database_name;
```
DROP DATABASE Statement: This statement is used to drop an entire database.
```sql
DROP DATABASE database_name;
```
# Constraints & Data Integrity
## ALTER TABLE ADD COLUMN with Constraint: This statement is used to add a column with a constraint to an existing table.
```sql
ALTER TABLE table_name ADD COLUMN column_name DATATYPE CONSTRAINT;
```
NOT NULL Constraint: This constraint ensures that a column cannot have NULL values.
```sql
column_name VARCHAR(50) NOT NULL
```
ALTER TABLE ADD PRIMARY KEY Statement: This statement is used to add a primary key constraint to a table.
```sql
ALTER TABLE table_name ADD PRIMARY KEY(column_name);
```
ALTER TABLE DROP CONSTRAINT Statement: This statement is used to drop a constraint from a table.
```sql
ALTER TABLE table_name DROP CONSTRAINT constraint_name;
```
ALTER TABLE ADD COLUMN with Foreign Key: This statement is used to add a foreign key column that references another table.
```sql
ALTER TABLE table_name ADD COLUMN column_name DATATYPE REFERENCES referenced_table_name(referenced_column_name);
```
ALTER TABLE ADD UNIQUE Statement: This statement is used to add a UNIQUE constraint to a column.
```sql
ALTER TABLE table_name ADD UNIQUE(column_name);
```
ALTER TABLE ALTER COLUMN SET NOT NULL Statement: This statement is used to set a NOT NULL constraint on an existing column.
```sql
ALTER TABLE table_name ALTER COLUMN column_name SET NOT NULL;
```
INSERT Statement with NULL Values: This statement demonstrates how to insert NULL values into a table.
```sql
INSERT INTO table_name(column_a) VALUES(NULL);
-- or
INSERT INTO table_name(column_b) VALUES('value'); -- if column_a allows nulls
```
Composite Primary Key: This constraint defines a primary key that consists of multiple columns.
```sql
CREATE TABLE course_enrollments (
    student_id INT,
    course_id INT,
    PRIMARY KEY (student_id, course_id)
);
```
## Data Manipulation (CRUD)
INSERT Statement: This statement is used to insert a single row into a table.
```sql
INSERT INTO table_name(column_1, column_2) VALUES(value1, value2);
```
INSERT Statement with Omitted Columns: This statement shows how to insert values without explicitly listing the column names, relying on the default column order in the table.
```sql
INSERT INTO dogs VALUES ('Gino', 3);
```
INSERT Statement with Multiple Rows: This statement is used to insert multiple rows into a table in a single operation.
```sql
INSERT INTO dogs (name, age) VALUES 
('Gino', 3),
('Nora', 2);
```
UPDATE Statement: This statement is used to update existing data in a table based on a condition.
```sql
UPDATE table_name SET column_name=new_value WHERE condition;
```
DELETE Statement: This statement is used to delete rows from a table based on a condition.
```sql
DELETE FROM table_name WHERE condition;
```
# Data Types
NUMERIC Data Type: This data type is used to store precise decimal numbers with a specified precision and scale.
```sql
price NUMERIC(10, 2)
```
TEXT Data Type: This data type is used to store variable-length character strings with no specific length limit.
```sql
column_name TEXT
```
INTEGER Data Type: This data type is used to store whole numbers without decimal places.
```sql
units_sold INTEGER
```
- SMALLINT and BIGINT Data Types: These are variants of INTEGER with smaller and larger ranges respectively.

- SERIAL Data Type: This data type is used to create auto-incrementing integer columns in PostgreSQL.
```sql
id SERIAL
```
AUTO_INCREMENT Attribute: This attribute is used in MySQL to create auto-incrementing integer columns.
```sql
id INT AUTO_INCREMENT
```
VARCHAR Data Type: This data type is used to store variable-length character strings with a specified maximum length.
```sql
name VARCHAR(50)
```
DATE Data Type: This data type is used to store date values (year, month, day).
```sql
event_date DATE
```
TIME Data Type: This data type is used to store time values (hour, minute, second).
```sql
start_time TIME
```
TIMESTAMP Data Type: This data type is used to store date and time values, optionally with time zone information.
```sql
event_timestamp TIMESTAMP
event_timestamp TIMESTAMP WITH TIME ZONE
```
BOOLEAN Data Type: This data type is used to store true/false values.
```sql
is_active BOOLEAN
```
# Advanced SQL (Joins)
INNER JOIN Statement: This join returns only the rows that have matching values in both tables.
```sql
SELECT *
FROM products
INNER JOIN sales ON products.product_id = sales.product_id;
```
FULL OUTER JOIN Statement: This join returns all rows from both tables, including unmatched rows from either table.
```sql
SELECT *
FROM products
FULL OUTER JOIN sales ON products.product_id = sales.product_id;
```
LEFT OUTER JOIN Statement: This join returns all rows from the left table and matching rows from the right table.
```sql
SELECT *
FROM products
LEFT JOIN sales ON products.product_id = sales.product_id;
```
RIGHT OUTER JOIN Statement: This join returns all rows from the right table and matching rows from the left table.
```sql
SELECT *
FROM products
RIGHT JOIN sales ON products.product_id = sales.product_id;
```
SELF JOIN Statement: This join is used to join a table with itself to compare rows within the same table.
```sql
SELECT A.column_name, B.column_name
FROM table_name A
JOIN table_name B ON A.related_column = B.related_column;
```
CROSS JOIN Statement: This join returns the Cartesian product of two tables, combining every row from the first table with every row from the second table.
```sql
SELECT *
FROM table1
CROSS JOIN table2;
```
```
```
```
