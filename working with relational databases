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

# setup/postgresql_setup.md

```md id="13v7v8"
# PostgreSQL Setup

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
| `\d`               | Show all tables          |
| `\d table_name`    | Describe table structure |

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

```
```
