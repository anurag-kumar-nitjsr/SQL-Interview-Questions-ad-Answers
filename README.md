## Practice Questions
- HackerRank [SQL Solutions](https://github.com/anurag-kumar-nitjsr/SQL-Interview-Questions-ad-Answers/tree/main/HackerRank)
- LeetCode [SQL Solutions](https://github.com/anurag-kumar-nitjsr/SQL-Interview-Questions-ad-Answers/tree/main/LeetCode)



# SQL Interview Questions and Answers

A complete collection of SQL Interview Questions and Answers for Freshers and Experienced Developers.

---

## Table of Contents

- [Q1. What is SQL and what is it used for?](#q1-what-is-sql-and-what-is-it-used-for)
- [Q2. Describe the difference between SQL and NoSQL databases.](#q2-describe-the-difference-between-sql-and-nosql-databases)
- [Q3. What are the different types of SQL commands?](#q3-what-are-the-different-types-of-sql-commands)
- [Q4. Explain the purpose of the SELECT statement.](#q4-explain-the-purpose-of-the-select-statement)
- [Q5. What is the difference between WHERE and HAVING clauses?](#q5-what-is-the-difference-between-where-and-having-clauses)
- [Q6. Define what a JOIN is in SQL and list its types.](#q6-define-what-a-join-is-in-sql-and-list-its-types)
- [Q7. What is a Primary Key?](#q7-what-is-a-primary-key)
- [Q8. Explain Foreign Key.](#q8-explain-foreign-key)
- [Q9. How can you prevent SQL Injection?](#q9-how-can-you-prevent-sql-injection)
- [Q10. What is Normalization?](#q10-what-is-normalization)
- [Q11. Explain Denormalization.](#q11-explain-denormalization)
- [Q12. What are Indexes?](#q12-what-are-indexes)
- [Q13. Explain GROUP BY.](#q13-explain-group-by)
- [Q14. What is a Subquery?](#q14-what-is-a-subquery)
- [Q15. Explain ORDER BY Clause.](#q15-explain-order-by-clause)

---

# Q1. What is SQL and what is it used for?

SQL (Structured Query Language)

SQL is the standardized domain-specific, declarative language for managing and querying Relational Database Management Systems (RDBMS). Beyond legacy relational models, modern SQL dialects (e.g., PostgreSQL 18, DuckDB 1.2) now incorporate support for semi-structured data (JSONB) and vector embeddings for RAG (Retrieval-Augmented Generation) workflows.

## Core Components

- DDL (Data Definition Language): Defines schema objects (CREATE, ALTER, DROP)
- DML (Data Manipulation Language): INSERT, UPDATE, DELETE, MERGE
- DCL (Data Control Language): GRANT, REVOKE
- TCL (Transaction Control Language): COMMIT, ROLLBACK, SAVEPOINT
- DQL (Data Query Language): SELECT

## Modern Database Management Tasks

- Data Retrieval
- ACID Compliance
- Vector Search
- Normalization & Optimization
- Distributed Scaling

## Essential SQL Commands

- SELECT
- MERGE
- LATERAL JOIN
- MATERIALIZED VIEW

### Example

```sql
CREATE TABLE Department (
    dept_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    dept_name VARCHAR(100) NOT NULL
);

CREATE TABLE Employee (
    emp_id INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,
    emp_name VARCHAR(255) NOT NULL,
    dept_id INT REFERENCES Department(dept_id)
);

WITH DepartmentStats AS (
    SELECT dept_id, COUNT(*) AS emp_count
    FROM Employee
    GROUP BY dept_id
)

SELECT
    e.emp_name,
    d.dept_name,
    ds.emp_count
FROM Employee e
JOIN Department d
ON e.dept_id = d.dept_id
JOIN DepartmentStats ds
ON d.dept_id = ds.dept_id
WHERE ds.emp_count > 0;
```

---

# Q2. Describe the difference between SQL and NoSQL databases

## SQL

- Relational Database
- Fixed Schema
- ACID Compliance
- Supports Complex Joins
- SQL Query Language

## NoSQL

- Non-Relational Database
- Flexible Schema
- Horizontal Scaling
- Document, Key-Value, Graph, Wide Column
- Eventual Consistency

### Comparison

| Feature | SQL | NoSQL |
|----------|-----|--------|
| Schema | Fixed | Flexible |
| Scaling | Vertical / Distributed | Horizontal |
| Joins | Supported | Limited |
| ACID | Strong | Depends |
| Use Case | Banking | Big Data |

---

# Q3. What are the different types of SQL commands?

## DQL

- SELECT
- FROM
- WHERE
- GROUP BY
- HAVING
- JOIN
- WITH

## DDL

- CREATE
- ALTER
- DROP
- TRUNCATE
- COMMENT

## DML

- INSERT
- UPDATE
- DELETE
- MERGE

## TCL

- COMMIT
- ROLLBACK
- SAVEPOINT

## DCL

- GRANT
- REVOKE
- DENY

---

# Q4. Explain the purpose of the SELECT statement

The SELECT statement retrieves data from one or more tables.

Logical execution order:

1. FROM
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. DISTINCT
7. ORDER BY
8. LIMIT

Example

```sql
WITH OrderSummary AS (

SELECT
    o.OrderID,
    o.OrderDate,
    c.CustomerName,
    e.LastName AS SalesRep,
    SUM(od.UnitPrice * od.Quantity) AS TotalValue

FROM Orders o

JOIN Customers c
ON o.CustomerID = c.CustomerID

JOIN Employees e
ON o.EmployeeID = e.EmployeeID

JOIN OrderDetails od
ON o.OrderID = od.OrderID

GROUP BY 1,2,3,4

)

SELECT *
FROM OrderSummary
WHERE TotalValue > 1000
ORDER BY OrderDate DESC
LIMIT 100;
```

---

# Q5. What is the difference between WHERE and HAVING clauses?

## WHERE

- Filters rows before GROUP BY
- Cannot use aggregate functions
- Better performance
- Uses indexes efficiently

## HAVING

- Filters groups after GROUP BY
- Supports aggregate functions
- Used with COUNT(), SUM(), AVG(), MAX(), MIN()

Execution Order

FROM

↓

WHERE

↓

GROUP BY

↓

HAVING

↓

SELECT

↓

ORDER BY

---

⬆️ **Back to Top**

# Q6. Define what a JOIN is in SQL and list its types.

A JOIN clause in SQL is a relational operator used to combine rows from two or more tables based on a common column or join condition.

## Types of JOIN

### 1. INNER JOIN
Returns only matching records from both tables.

```sql
SELECT T1.A, T1.B, T2.C
FROM Table1 AS T1
INNER JOIN Table2 AS T2
ON T1.B = T2.B;
```

---

### 2. LEFT JOIN

Returns all rows from the left table and matching rows from the right table.

---

### 3. RIGHT JOIN

Returns all rows from the right table and matching rows from the left table.

---

### 4. FULL JOIN

Returns all records from both tables.

```sql
SELECT
    COALESCE(T1.B, T2.B) AS B,
    T1.A,
    T2.C
FROM Table1 AS T1
FULL JOIN Table2 AS T2
ON T1.B = T2.B;
```

---

### 5. CROSS JOIN

Returns the Cartesian Product of two tables.

Complexity:

```
O(n × m)
```

---

### 6. SELF JOIN

A table joined with itself.

Example (Recursive CTE)

```sql
WITH RECURSIVE Hierarchy AS (

SELECT
    EmpID,
    Name,
    ManagerID
FROM Employee
WHERE ManagerID IS NULL

UNION ALL

SELECT
    E.EmpID,
    E.Name,
    E.ManagerID

FROM Employee E

INNER JOIN Hierarchy H
ON E.ManagerID = H.EmpID

)

SELECT *
FROM Hierarchy;
```

Manager Example

```sql
SELECT
    E.Name AS Employee,
    M.Name AS Manager

FROM Employee E

LEFT JOIN Employee M
ON E.ManagerID = M.EmpID;
```

---

# Q7. What is a Primary Key?

A Primary Key uniquely identifies every record in a table.

## Characteristics

- Unique
- NOT NULL
- Immutable
- Entity Identity
- Used by Foreign Keys
- Clustered Index (most databases)

## Best Practices

- Prefer Surrogate Keys
- Use BIGINT IDENTITY
- UUIDv7 for distributed systems
- Keep keys small
- Composite Keys only when necessary

Example

```sql
CREATE TABLE Students (

    student_id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,

    student_uuid UUID DEFAULT gen_random_uuid(),

    grade_level INT NOT NULL,

    first_name VARCHAR(50) NOT NULL,

    last_name VARCHAR(50) NOT NULL,

    created_at TIMESTAMPTZ DEFAULT CURRENT_TIMESTAMP

);

CREATE UNIQUE INDEX idx_students_uuid
ON Students(student_uuid);
```

---

# Q8. Explain what a Foreign Key is.

A Foreign Key (FK) is a constraint that establishes a relationship between two tables while maintaining Referential Integrity.

## Functions

- Referential Integrity
- Relationship Mapping
- Declarative Referential Integrity
- Lifecycle Management

## Best Practices

- Reference Primary Key or Unique Key
- Allow NULL unless mandatory
- Create Index on Foreign Key
- Use ON DELETE RESTRICT
- Use ON UPDATE CASCADE

Example

```sql
CREATE TABLE departments (

    department_id INT PRIMARY KEY,

    name VARCHAR(100) NOT NULL

);

CREATE TABLE employees (

    employee_id INT PRIMARY KEY,

    name VARCHAR(100) NOT NULL,

    department_id INT,

    CONSTRAINT fk_department

    FOREIGN KEY (department_id)

    REFERENCES departments(department_id)

    ON DELETE RESTRICT

    ON UPDATE CASCADE

);

CREATE INDEX idx_employees_department_id
ON employees(department_id);
```

---

# Q9. How can you prevent SQL Injection?

SQL Injection occurs when user input is interpreted as executable SQL code.

## Prevention Techniques

### 1. Parameterized Queries

- Prepared Statements
- Bound Parameters
- Prevents SQL Injection

Example

```python
from sqlalchemy import text

stmt = text(
"SELECT * FROM users
WHERE username=:u
AND password=:p"
)

result = session.execute(
stmt,
{
"u": username,
"p": password
}
)
```

---

### 2. Stored Procedures

Use parameterized stored procedures.

---

### 3. Input Validation

Validate user inputs using allow-listing.

Example

```python
class UserLogin(BaseModel):

    username:
    Annotated[
        str,
        StringConstraints(
            pattern=r'^[a-zA-Z0-9_]{3,20}$'
        )
    ]
```

---

### 4. Principle of Least Privilege

- Never connect as Super User
- Use RBAC
- Restrict DROP/TRUNCATE
- Restrict GRANT

---

### 5. Use ORM

Modern ORMs automatically use Parameterized Queries.

---

# Q10. What is Normalization?

Normalization is the process of organizing data to reduce redundancy and eliminate update anomalies.

## Normal Forms

### 1NF

- Atomic Values
- No repeating groups

### 2NF

- No Partial Dependency

### 3NF

- No Transitive Dependency

### BCNF

Every determinant must be a candidate key.

### 4NF

No Multi-valued Dependency.

---

## Example

### Products

```sql
CREATE TABLE Products (

ProductID INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,

Description TEXT NOT NULL,

UnitPrice DECIMAL(12,2)

CHECK(UnitPrice>=0)

);
```

### Customers

```sql
CREATE TABLE Customers (

CustomerID INT PRIMARY KEY,

CustomerName VARCHAR(255) NOT NULL

);
```

### Invoices

```sql
CREATE TABLE Invoices (

InvoiceNo INT PRIMARY KEY,

CustomerID INT NOT NULL
REFERENCES Customers(CustomerID),

InvoiceDate TIMESTAMPTZ
DEFAULT CURRENT_TIMESTAMP

);
```

### Invoice Items

```sql
CREATE TABLE Invoice_Items (

InvoiceNo INT
REFERENCES Invoices(InvoiceNo),

ProductID INT
REFERENCES Products(ProductID),

Quantity INT CHECK(Quantity>0),

PRIMARY KEY(
InvoiceNo,
ProductID
)

);
```

---

⬆️ **Back to Top**

# Q11. Describe the concept of Denormalization and when you would use it.

Denormalization is the intentional introduction of redundancy into a database schema to improve read performance and reduce expensive JOIN operations.

---

## Refined Techniques

### 1. Flattening Relationships

- Merge related tables
- Reduce JOIN operations
- Improve query speed

---

### 2. Pre-aggregation & Materialized Views

- Store precomputed values
- Reduce runtime calculations
- Improve reporting performance

---

### 3. Redundant Attribute Replication

- Store frequently accessed data
- Common in Star Schema
- Optimized for OLAP workloads

---

## Use Cases

### OLTP

- Prefer Normalization
- ACID Compliance

### OLAP

- Star Schema
- Snowflake Schema
- Faster Reporting

### Distributed Systems

- Reduce Cross-Shard Joins
- Improve Read Performance

### Vector Search

- Store embeddings with metadata
- Enable semantic + relational filtering

---

## Trade-offs

- Increased Storage
- Write Amplification
- Harder Schema Evolution
- Application manages consistency

---

## Best Practice

- Normalize transactional databases.
- Use Materialized Views or Read Replicas first.
- Denormalize only after performance profiling.

---

# Q12. What are Indexes and how can they improve query performance?

Indexes are auxiliary data structures that speed up data retrieval by reducing table scans.

---

## Benefits

- Faster Search
- Reduced Disk I/O
- Better JOIN Performance
- Index Only Scan
- Covering Indexes

---

## Types of Indexes

### B+ Tree

- Standard Index
- Range Queries
- O(log n)

---

### LSM Tree

- Write-heavy systems
- Distributed Databases

---

### Hash Index

- O(1) Lookups
- In-memory databases

---

### BRIN Index

- Massive datasets
- Time-series data

---

### GIN / GiST

- Full Text Search
- JSONB
- Spatial Data

---

## Trade-offs

- More Storage
- Slower INSERT
- Slower UPDATE
- Slower DELETE

---

## Best Practices

- Index high-cardinality columns
- Use Partial Indexes
- Follow Left Prefix Rule
- Create Covering Indexes
- Keep Statistics Updated

---

# Q13. Explain the purpose of the GROUP BY clause.

The GROUP BY clause groups rows having the same values into summary rows.

---

## Uses

- Data Aggregation
- Reporting
- Dimensional Analysis
- HAVING Clause

---

### Example

```sql
SELECT
    Region,
    SUM(Amount) AS TotalSales
FROM Sales
GROUP BY Region;
```

---

### WHERE vs HAVING

```sql
SELECT
    Region,
    COUNT(*) AS HighValueTransactions

FROM Sales

WHERE Amount > 100

GROUP BY Region

HAVING COUNT(*) > 50;
```

---

### Window Function Example

```sql
SELECT
    Region,
    Product,

    SUM(Amount)
    /
    SUM(SUM(Amount))
    OVER(PARTITION BY Region)

AS RelativeContribution

FROM Sales

GROUP BY Region, Product;
```

---

## Performance Notes

- Hash Aggregation
- Stream Aggregation
- Index grouping columns
- Partition-wise aggregation

Complexity

```
O(N log N)

or

O(N)
```

---

# Q14. What is a Subquery and when would you use one?

A Subquery is a query nested inside another SQL query.

---

## Types

### Scalar Subquery

Returns one row and one column.

---

### Table Subquery

Returns multiple rows or columns.

---

### Correlated Subquery

Depends on the outer query.

---

## Modern Alternatives

- CTE (WITH)
- Window Functions
- LATERAL JOIN

---

### Example 1

```sql
WITH AvgValue AS (

SELECT AVG(salary) AS global_avg

FROM employees

)

SELECT
    emp_name,
    salary

FROM employees,
     AvgValue

WHERE salary >
      AvgValue.global_avg;
```

---

### Example 2

```sql
SELECT
    c.customer_name,
    o.order_date

FROM customers c

CROSS JOIN LATERAL (

SELECT order_date

FROM orders

WHERE customer_id = c.id

ORDER BY order_date DESC

LIMIT 1

) o;
```

---

## Best Practices

- Prefer CTEs for readability.
- Avoid deeply nested queries.
- Use EXPLAIN ANALYZE.
- Prefer Window Functions where appropriate.

---

# Q15. Describe the functions of the ORDER BY clause.

ORDER BY sorts the result set into a deterministic order.

---

## Features

- Ascending Order (ASC)
- Descending Order (DESC)
- Multiple Columns
- NULLS FIRST
- NULLS LAST

---

## Performance

Sorting Complexity

```
O(N log N)
```

Using an Index

```
O(N)
```

---

## Best Practices

- Use explicit column names.
- Avoid ORDER BY column position.
- Avoid ORDER BY RANDOM() on large tables.
- Prefer Window Functions for Top-N queries.

---

### Example

```sql
SELECT
    product_name,
    sale_date,
    units_sold

FROM sales

WHERE sale_date = '2026-05-20'

ORDER BY

units_sold DESC NULLS LAST,

product_name ASC

LIMIT 3;
```

---

### Top-N Ranking Example

```sql
SELECT
    product_name,
    units_sold

FROM (

SELECT
    product_name,
    units_sold,

    RANK() OVER(
        ORDER BY units_sold DESC
    ) AS rnk

FROM sales

WHERE sale_date='2026-05-20'

) t

WHERE rnk <= 3;
```

---

## 📚 Conclusion

This README contains SQL interview questions covering:

- SQL Basics
- SQL vs NoSQL
- SQL Commands
- SELECT Statement
- WHERE vs HAVING
- JOINs
- Primary Key
- Foreign Key
- SQL Injection
- Normalization
- Denormalization
- Indexes
- GROUP BY
- Subqueries
- ORDER BY

⭐ If this repository helped you, consider giving it a **Star**.

---

⬆️ **Back to Top**

