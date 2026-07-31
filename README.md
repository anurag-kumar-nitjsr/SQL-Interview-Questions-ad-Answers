## Practice Questions
- HackerRank [SQL Solutions](https://github.com/anurag-kumar-nitjsr/SQL-Interview-Questions-ad-Answers/tree/main/HackerRank)
- LeetCode [SQL Solutions](https://github.com/anurag-kumar-nitjsr/SQL-Interview-Questions-ad-Answers/tree/main/LeetCode)



# 📊 SQL Cheatsheet

A practical **SQL Cheatsheet** covering **DDL, DML, DQL, DCL, TCL, Joins, Indexes, Views, Stored Procedures, and commonly used SQL queries**.

Whether you're preparing for **interviews**, learning SQL, or need a quick reference, this guide has you covered.

---

## 📑 Table of Contents

- Introduction
- SQL Basics
- Data Definition Language (DDL)
- Data Manipulation Language (DML)
- Data Query Language (DQL)
- Data Control Language (DCL)
- Transaction Control Language (TCL)
- Joins
- Indexes
- Views
- Stored Procedures
- Examples

---

# Introduction

**SQL (Structured Query Language)** is the standard language used to:

- Create databases
- Store data
- Retrieve data
- Update data
- Delete data
- Control permissions
- Manage transactions

---

# SQL Basics

SQL commands are divided into five categories:

| Category | Purpose |
|----------|----------|
| DDL | Define database structure |
| DML | Manipulate data |
| DQL | Retrieve data |
| DCL | Manage permissions |
| TCL | Manage transactions |

---

# Data Definition Language (DDL)

DDL commands define and modify database objects.

## CREATE

Creates a new database object.

```sql
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100),
    position VARCHAR(50)
);
```

---

## ALTER

Modifies an existing table.

```sql
ALTER TABLE employees
ADD salary DECIMAL(10,2);
```

---

## DROP

Deletes a table.

```sql
DROP TABLE employees;
```

---

## TRUNCATE

Removes all records while keeping the table structure.

```sql
TRUNCATE TABLE employees;
```

---

## RENAME

Renames a table.

```sql
ALTER TABLE employees
RENAME TO employee_details;
```

---

# Data Manipulation Language (DML)

Used to insert, update, and delete records.

---

## INSERT

```sql
INSERT INTO employees (id, name, position)
VALUES (1, 'Alice', 'Manager');
```

---

## UPDATE

```sql
UPDATE employees
SET position = 'Senior Manager'
WHERE id = 1;
```

---

## DELETE

```sql
DELETE FROM employees
WHERE id = 1;
```

---

# Data Query Language (DQL)

Used to retrieve data.

---

## SELECT

```sql
SELECT * FROM employees;
```

---

## WHERE

```sql
SELECT *
FROM employees
WHERE position = 'Manager';
```

---

## DISTINCT

```sql
SELECT DISTINCT position
FROM employees;
```

---

## ORDER BY

```sql
SELECT *
FROM employees
ORDER BY salary DESC;
```

---

## LIMIT

```sql
SELECT *
FROM employees
LIMIT 5;
```

---

## GROUP BY

```sql
SELECT department,
COUNT(*)
FROM employees
GROUP BY department;
```

---

## HAVING

```sql
SELECT department,
COUNT(*)
FROM employees
GROUP BY department
HAVING COUNT(*) > 5;
```

---

# Data Control Language (DCL)

Controls user permissions.

---

## GRANT

```sql
GRANT SELECT
ON employees
TO user1;
```

---

## REVOKE

```sql
REVOKE SELECT
ON employees
FROM user1;
```

---

# Transaction Control Language (TCL)

Manages transactions.

---

## COMMIT

```sql
BEGIN;

UPDATE employees
SET salary = salary + 1000;

COMMIT;
```

---

## ROLLBACK

```sql
BEGIN;

UPDATE employees
SET salary = 0;

ROLLBACK;
```

---

## SAVEPOINT

```sql
BEGIN;

SAVEPOINT before_update;

UPDATE employees
SET salary = salary + 500;

ROLLBACK TO before_update;
```

---

# SQL Joins

Joins combine data from multiple tables.

---

## INNER JOIN

Returns matching rows.

```sql
SELECT e.name,
       d.department_name
FROM employees e
INNER JOIN departments d
ON e.department_id = d.id;
```

---

## LEFT JOIN

Returns all rows from the left table.

```sql
SELECT *
FROM employees e
LEFT JOIN departments d
ON e.department_id = d.id;
```

---

## RIGHT JOIN

Returns all rows from the right table.

```sql
SELECT *
FROM employees e
RIGHT JOIN departments d
ON e.department_id = d.id;
```

---

## FULL OUTER JOIN

Returns all matching and non-matching rows.

```sql
SELECT *
FROM employees e
FULL OUTER JOIN departments d
ON e.department_id = d.id;
```

---

## CROSS JOIN

Returns the Cartesian product.

```sql
SELECT *
FROM employees
CROSS JOIN departments;
```

---

# Indexes

Indexes improve query performance.

Create an index:

```sql
CREATE INDEX idx_employee_name
ON employees(name);
```

Drop an index:

```sql
DROP INDEX idx_employee_name;
```

---

# Views

Views are virtual tables.

Create a view:

```sql
CREATE VIEW manager_view AS
SELECT *
FROM employees
WHERE position = 'Manager';
```

Use the view:

```sql
SELECT *
FROM manager_view;
```

---

# Stored Procedures

Stored procedures store reusable SQL logic.

```sql
CREATE PROCEDURE GetEmployeeById(IN emp_id INT)
BEGIN
    SELECT *
    FROM employees
    WHERE id = emp_id;
END;
```

Execute:

```sql
CALL GetEmployeeById(1);
```

---

# Examples

## Create Table

```sql
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(100),
    price DECIMAL(10,2)
);
```

---

## Insert Data

```sql
INSERT INTO products
(product_id, product_name, price)
VALUES
(1, 'Laptop', 999.99);
```

---

## Update Data

```sql
UPDATE products
SET price = 899.99
WHERE product_id = 1;
```

---

## Delete Data

```sql
DELETE FROM products
WHERE product_id = 1;
```

---

## Select Data

```sql
SELECT *
FROM products;
```

---

## Filter Data

```sql
SELECT *
FROM products
WHERE price > 500;
```

---

## Sort Data

```sql
SELECT *
FROM products
ORDER BY price DESC;
```

---

## Aggregate Functions

```sql
SELECT
COUNT(*) AS total_products,
AVG(price) AS average_price,
MAX(price) AS highest_price,
MIN(price) AS lowest_price,
SUM(price) AS total_price
FROM products;
```

---

# Quick SQL Command Summary

| Command | Description |
|----------|-------------|
| CREATE | Create database objects |
| ALTER | Modify table structure |
| DROP | Delete database objects |
| TRUNCATE | Remove all rows |
| INSERT | Add new records |
| UPDATE | Modify existing records |
| DELETE | Remove records |
| SELECT | Retrieve data |
| WHERE | Filter records |
| GROUP BY | Group rows |
| HAVING | Filter grouped data |
| ORDER BY | Sort results |
| DISTINCT | Remove duplicates |
| LIMIT | Limit returned rows |
| JOIN | Combine tables |
| INDEX | Improve query performance |
| VIEW | Virtual table |
| PROCEDURE | Reusable SQL program |
| GRANT | Give permissions |
| REVOKE | Remove permissions |
| COMMIT | Save transaction |
| ROLLBACK | Undo transaction |
| SAVEPOINT | Partial rollback point |

---

# 🎯 Interview Tips

- Understand the difference between **DDL, DML, DQL, DCL, and TCL**.
- Practice **JOINs**, **GROUP BY**, and **HAVING**.
- Learn how **Indexes** improve query performance.
- Understand **Normalization** and **Denormalization**.
- Know the difference between **DELETE**, **TRUNCATE**, and **DROP**.
- Be comfortable writing **subqueries** and **CTEs**.
- Use **EXPLAIN** to analyze query execution plans.
- Understand **ACID properties** and transaction management.

---

⭐ If this cheatsheet helps you, consider giving your repository a **Star**!

