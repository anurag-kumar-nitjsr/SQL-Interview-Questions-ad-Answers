## Practice Questions
- HackerRank [SQL Solutions](https://github.com/anurag-kumar-nitjsr/SQL-Interview-Questions-ad-Answers/tree/main/HackerRank)
- LeetCode [SQL Solutions](https://github.com/anurag-kumar-nitjsr/SQL-Interview-Questions-ad-Answers/tree/main/LeetCode)


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

### Q1. What is SQL and what is it used for?

#### SQL (Structured Query Language)

**SQL (Structured Query Language)** is the standardized, domain-specific, declarative language used for managing and querying **Relational Database Management Systems (RDBMS)**. Beyond traditional relational databases, modern SQL dialects such as **PostgreSQL 18** and **DuckDB 1.2** support **semi-structured data (JSONB)** and **vector embeddings** for **RAG (Retrieval-Augmented Generation)** workflows.

---

#### Core Components

| Component | Description |
|-----------|-------------|
| **DDL (Data Definition Language)** | Defines database schema objects (e.g., `CREATE`, `ALTER`, `DROP`) |
| **DML (Data Manipulation Language)** | Manages row-level data (e.g., `INSERT`, `UPDATE`, `DELETE`, `MERGE`) |
| **DCL (Data Control Language)** | Manages authorization and security (e.g., `GRANT`, `REVOKE`) |
| **TCL (Transaction Control Language)** | Controls transactions (e.g., `COMMIT`, `ROLLBACK`, `SAVEPOINT`) |
| **DQL (Data Query Language)** | Retrieves data using `SELECT` statements |

---

#### Modern Database Management Tasks

- 📊 Complex data retrieval using aggregation and window functions.
- 🔒 ACID compliance for reliable transactions.
- 🤖 Vector search using SQL extensions (e.g., **pgvector**) for semantic search and AI applications.
- ⚡ Query optimization using **B-Tree**, **LSM-Tree**, and **BRIN** indexes.
- 🌐 Horizontal scaling through **Sharding** and **Replication**.

---

#### Essential SQL Features

- **SELECT** – Retrieve data with support for **CTEs** and **Window Functions**.
- **MERGE** – Perform **UPSERT** operations efficiently.
- **LATERAL JOIN** – Reference preceding tables inside subqueries.
- **MATERIALIZED VIEW** – Cache expensive query results for faster reporting.

---

#### Example: Modern SQL Syntax

#### Schema Definition

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
```

#### Using a Common Table Expression (CTE)

```sql
WITH DepartmentStats AS (
    SELECT
        dept_id,
        COUNT(*) AS emp_count
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

#### Performance Considerations (2026)

#### Index Scan vs Sequential Scan

- Query planners choose between **Index Scan** and **Sequential Scan** based on **cardinality** and **selectivity**.
- Proper indexing avoids costly full-table scans and improves lookup performance.

#### Execution Plans

Use:

```sql
EXPLAIN ANALYZE
```

to inspect the query execution plan, identify bottlenecks, and optimize performance.

#### Concurrency

Modern databases use **MVCC (Multi-Version Concurrency Control)**, allowing:

- Readers to access consistent data without blocking writers.
- Writers to update records without blocking readers.
- High throughput in concurrent environments.

---

#### Key Takeaways

- SQL is the standard language for relational databases.
- Supports schema creation, data manipulation, security, transactions, and querying.
- Modern SQL supports **JSON**, **Vector Search**, **CTEs**, **Window Functions**, and **Materialized Views**.
- Performance depends on proper indexing, execution plans, and optimized query design.
- MVCC enables efficient concurrent transactions in modern database systems.
---

### Q2. Describe the difference between SQL and NoSQL databases

#### SQL vs NoSQL Databases (2026)

The distinction between **SQL (Relational)** and **NoSQL (Non-Relational)** databases has evolved into a **hybrid ecosystem**. While SQL databases focus on **data consistency and relational modeling**, NoSQL databases prioritize **scalability, flexibility, and high performance**.

Modern database systems have blurred the boundaries by supporting **multi-model data**, distributed architectures, and advanced features such as **JSON**, **vector search**, and **ACID transactions**.

---

#### Fundamental Differences

| SQL (Relational Database) | NoSQL (Non-Relational Database) |
|---------------------------|---------------------------------|
| Based on the **Relational Model (Codd, 1970)** | Designed for flexible and distributed data models |
| Stores data in **tables** with predefined schemas | Stores data in **documents, key-value pairs, graphs, or wide-columns** |
| Strong **ACID** compliance | Often follows **CAP Theorem** with eventual consistency |
| Best for structured data | Best for semi-structured and unstructured data |
| Supports complex joins and relational queries | Joins are generally avoided through denormalization |

---

#### 2026 Paradigm Shifts

#### Hybrid Databases

Modern SQL databases now support **semi-structured data**.

Examples:

- PostgreSQL 18+ supports **JSONB**
- SQL databases can store relational and JSON data together

Similarly, NoSQL databases now support **multi-document ACID transactions**.

Examples:

- MongoDB 8+
- Azure Cosmos DB
- Amazon DocumentDB

---

#### Distributed SQL

Traditional SQL databases were considered vertically scalable.

Modern Distributed SQL databases provide:

- Horizontal Sharding
- Automatic Replication
- Global Distribution
- High Availability

Examples:

- CockroachDB
- TiDB
- YugabyteDB

---

#### Types of NoSQL Databases

#### 1. Document Database

Stores data as JSON/BSON documents.

#### Examples

- MongoDB
- CouchDB

#### Use Cases

- Content Management
- E-commerce
- REST APIs
- AI Applications

#### 2026 Trend

Supports **Vector Search** for Retrieval-Augmented Generation (RAG).

---

#### 2. Key-Value Database

Stores data as **Key → Value** pairs.

#### Examples

- Redis
- Amazon DynamoDB
- Riak

#### Use Cases

- Session Storage
- Caching
- Shopping Cart
- Feature Store

#### Performance

- Lookup Complexity: **O(1)**

---

#### 3. Wide-Column Database

Stores sparse data using column families.

#### Examples

- Apache Cassandra
- HBase
- Google Bigtable

#### Use Cases

- Time-Series Data
- IoT
- Logging Systems
- Analytics

---

#### 4. Graph Database

Stores relationships as **Nodes** and **Edges**.

#### Examples

- Neo4j
- Amazon Neptune
- TigerGraph

#### Use Cases

- Social Networks
- Fraud Detection
- Recommendation Systems
- Knowledge Graphs

---

#### SQL vs NoSQL Comparison

| Feature | SQL | NoSQL |
|---------|------|--------|
| Data Model | Relational Tables | Document, Key-Value, Graph, Wide-Column |
| Schema | Schema-on-Write | Schema-on-Read |
| Transactions | ACID | BASE / Eventual Consistency (Many now support ACID) |
| Scalability | Vertical + Distributed SQL | Native Horizontal Scaling |
| Joins | Supported | Usually Avoided |
| Query Language | Standard SQL | Vendor-Specific APIs |
| Consistency | Strong | Tunable / Eventual |
| Best For | Banking, ERP, CRM | Big Data, IoT, AI, Real-Time Apps |

---

#### Data Modeling

#### SQL

Uses **Normalization** (typically 3NF) to reduce redundancy.

#### Advantages

- Eliminates duplicate data
- Improves consistency
- Reduces update anomalies
- Maintains referential integrity

---

#### NoSQL

Uses **Denormalization**.

#### Advantages

- Faster reads
- No joins required
- Better performance in distributed systems

---

#### ACID Compliance

Modern SQL databases guarantee:

- **Atomicity**
- **Consistency**
- **Isolation**
- **Durability**

Modern enterprise NoSQL databases also support **ACID transactions**, although many still allow **tunable consistency** to balance performance and reliability.

---

#### Transaction & Consistency Models

#### SQL

Uses protocols such as:

- Two-Phase Commit (2PC)
- Paxos
- Raft

to guarantee consistency across distributed systems.

---

#### NoSQL

Common approaches include:

- Vector Clocks
- Last-Write-Wins (LWW)
- Eventual Consistency

Applications often handle conflict resolution and idempotency.

---

#### When to Use SQL

Choose **SQL** when:

- Data integrity is critical
- Transactions are required
- Complex joins are needed
- Reporting and analytics are important
- Relationships between entities are well-defined

#### Examples

- Banking Systems
- Payroll
- ERP
- CRM
- Hospital Management
- Inventory Management

---

#### When to Use NoSQL

Choose **NoSQL** when:

- High write throughput is required
- Data schema changes frequently
- Massive scalability is needed
- Working with JSON or unstructured data
- Building AI or IoT applications

#### Examples

- Chat Applications
- Social Media
- IoT Platforms
- Logging Systems
- Recommendation Engines
- Real-Time Analytics

---

#### Architectural Recommendation (2026)

| Use SQL | Use NoSQL |
|----------|-----------|
| Strong consistency | Flexible schema |
| ACID transactions | High scalability |
| Complex joins | High-speed reads/writes |
| Structured data | Semi-structured or unstructured data |
| Financial applications | IoT, AI, Streaming, Real-time systems |

If you need **both SQL capabilities and horizontal scalability**, consider **Distributed SQL** solutions such as **CockroachDB**, **TiDB**, or **YugabyteDB**.

---

#### Key Takeaways

- SQL databases emphasize **consistency, relational integrity, and complex querying**.
- NoSQL databases prioritize **flexibility, scalability, and performance**.
- Modern SQL databases now support **JSON, vector search, and distributed architectures**.
- Modern NoSQL databases increasingly support **ACID transactions**.
- Choose the database based on **application requirements**, not trends.
- Distributed SQL combines the strengths of both SQL and NoSQL for cloud-native applications.
---

### Q3. What are the different types of SQL commands?

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

### Q4. Explain the purpose of the SELECT statement

#### Overview

The **SELECT** statement is the primary **Data Query Language (DQL)** command in SQL. It is used to **retrieve, project, and transform data** from one or more database tables.

In modern SQL databases, the `SELECT` statement supports advanced features such as:

- JSON data querying
- Common Table Expressions (CTEs)
- Window Functions
- Vector Search (e.g., pgvector)
- Analytical (OLAP) queries

---

#### Logical Order of Execution

Although a `SELECT` query is written in one order, the database executes it in the following logical sequence:

| Execution Order | Clause | Purpose |
|-----------------|--------|---------|
| **1** | `FROM` / `JOIN` | Identifies the source tables |
| **2** | `WHERE` | Filters individual rows |
| **3** | `GROUP BY` | Groups rows for aggregation |
| **4** | `HAVING` | Filters grouped results |
| **5** | `SELECT` | Retrieves required columns and expressions |
| **6** | `DISTINCT` | Removes duplicate rows |
| **7** | `ORDER BY` | Sorts the final result |
| **8** | `LIMIT / OFFSET` | Restricts the number of returned rows |

> **Interview Tip:**  
> Remember the execution order because it is one of the most frequently asked SQL interview questions.

---

#### Modern SELECT Features (2026)

Modern SQL databases such as **PostgreSQL**, **DuckDB**, and **SQL Server** extend the `SELECT` statement with powerful capabilities.

#### 1. JSON Support

Query and manipulate JSON/JSONB data directly.

```sql
SELECT customer_data->>'name'
FROM customers;
```

---

#### 2. Common Table Expressions (CTEs)

The `WITH` clause improves readability and simplifies complex queries.

```sql
WITH SalesSummary AS (
    SELECT customer_id, SUM(amount) AS total_sales
    FROM orders
    GROUP BY customer_id
)
SELECT *
FROM SalesSummary;
```

---

#### 3. Window Functions

Window functions perform calculations without collapsing rows.

```sql
SELECT
    employee_name,
    salary,
    RANK() OVER (ORDER BY salary DESC) AS salary_rank
FROM employees;
```

Common window functions:

- `ROW_NUMBER()`
- `RANK()`
- `DENSE_RANK()`
- `LEAD()`
- `LAG()`
- `SUM() OVER()`
- `AVG() OVER()`

---

#### 4. Vector Search

Modern SQL databases support AI-powered semantic search.

```sql
SELECT content
FROM documents
ORDER BY embedding <=> '[...]'
LIMIT 5;
```

---

#### Practical Applications

The `SELECT` statement is commonly used for:

- Retrieving records
- Joining multiple tables
- Data analysis
- Business reporting
- Dashboard generation
- REST API responses
- GraphQL queries
- JSON aggregation
- AI and Vector Search

---

#### Example: Modern SQL Query

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
    GROUP BY
        o.OrderID,
        o.OrderDate,
        c.CustomerName,
        e.LastName
)

SELECT *
FROM OrderSummary
WHERE TotalValue > 1000
ORDER BY OrderDate DESC
LIMIT 100;
```

---

#### Performance Considerations

#### Full Table Scan

Without indexes, the database scans every row.

**Time Complexity:** **O(n)**

---

#### Index Scan

With **B-Tree**, **GIN**, or **BRIN** indexes, the database can quickly locate matching rows.

**Time Complexity:** **O(log n)**

---

#### Query Optimization

Use:

```sql
EXPLAIN ANALYZE
```

to inspect:

- Query execution plan
- Join strategy
- Index usage
- Cost estimation
- Execution time

---

#### Common Join Strategies

Modern query optimizers choose different join algorithms depending on the data.

| Join Strategy | Best Used For |
|--------------|---------------|
| Nested Loop Join | Small datasets or indexed lookups |
| Hash Join | Large tables with equality conditions |
| Merge Join | Sorted datasets with indexes |

---

#### Best Practices

- Use `SELECT` only for required columns instead of `SELECT *`.
- Apply `WHERE` filters as early as possible.
- Use indexes on frequently queried columns.
- Use **CTEs** for complex queries.
- Prefer **Window Functions** over self-joins when possible.
- Analyze execution plans using `EXPLAIN ANALYZE`.
- Use `LIMIT` when only a subset of rows is needed.
- Avoid unnecessary `DISTINCT` operations.

---

#### Key Takeaways

- `SELECT` is the primary SQL command for retrieving data.
- SQL executes query clauses in a logical order different from the written syntax.
- Modern SQL supports **CTEs**, **Window Functions**, **JSON**, and **Vector Search**.
- Proper indexing improves query performance from **O(n)** to **O(log n)**.
- `EXPLAIN ANALYZE` is an essential tool for query optimization.
- Understanding the execution order of `SELECT` is a common SQL interview topic.
  
---

### Q5. What is the difference between WHERE and HAVING clauses?

Both **`WHERE`** and **`HAVING`** clauses are used to filter data in SQL, but they operate at **different stages** of query execution.

- **WHERE** filters **individual rows** before grouping.
- **HAVING** filters **groups of rows** after aggregation.

Understanding their execution order is one of the most frequently asked SQL interview topics.

---

#### Key Differences

| Feature | WHERE | HAVING |
|---------|--------|---------|
| Filters | Individual rows | Groups of rows |
| Executes | Before `GROUP BY` | After `GROUP BY` |
| Uses Aggregate Functions | ❌ No | ✅ Yes |
| Works With | `SELECT`, `UPDATE`, `DELETE` | `SELECT` with `GROUP BY` |
| Performance | Faster | Slower |
| Index Usage | Can utilize indexes | Usually cannot utilize indexes directly |

---

#### WHERE Clause

The **`WHERE`** clause filters rows **before** any grouping or aggregation takes place.

#### Characteristics

- Filters individual records
- Executes immediately after the `FROM` / `JOIN` phase
- Cannot use aggregate functions (`SUM()`, `COUNT()`, `AVG()`, etc.)
- Can take advantage of indexes for better performance

---

#### Syntax

```sql
SELECT *
FROM Employees
WHERE Salary > 50000;
```

---

#### Example

Retrieve employees earning more than ₹50,000.

```sql
SELECT EmployeeID, Name, Salary
FROM Employees
WHERE Salary > 50000;
```

---

#### HAVING Clause

The **`HAVING`** clause filters **groups** created by the `GROUP BY` clause.

It is mainly used with **aggregate functions**.

---

#### Characteristics

- Filters grouped records
- Executes after `GROUP BY`
- Supports aggregate functions
- Used for summarized data

---

#### Syntax

```sql
SELECT DepartmentID, COUNT(*) AS TotalEmployees
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 10;
```

---

#### Example

Retrieve departments having more than 10 employees.

```sql
SELECT DepartmentID,
       COUNT(*) AS TotalEmployees
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 10;
```

---

#### Execution Order

The SQL engine processes a query in the following logical order:

```text
1. FROM / JOIN
2. WHERE
3. GROUP BY
4. HAVING
5. SELECT
6. DISTINCT
7. ORDER BY
8. LIMIT / OFFSET
```

---

#### Example Using WHERE and HAVING Together

```sql
SELECT DepartmentID,
       AVG(Salary) AS AverageSalary
FROM Employees
WHERE Salary > 30000
GROUP BY DepartmentID
HAVING AVG(Salary) > 60000
ORDER BY AverageSalary DESC;
```

#### Explanation

- `WHERE Salary > 30000`
  - Filters employees before grouping.
- `GROUP BY DepartmentID`
  - Groups employees by department.
- `HAVING AVG(Salary) > 60000`
  - Filters departments whose average salary is greater than ₹60,000.

---

#### Performance Comparison

#### WHERE

- Applied before grouping
- Can use **B-Tree indexes**
- Reduces rows early
- Faster execution
- Lookup Complexity: **O(log n)** (with indexes)

---

#### HAVING

- Applied after grouping
- Works on aggregated data
- Usually requires sorting or hashing
- More computationally expensive
- Complexity: **O(n log n)**

---

#### Common Errors

#### ❌ Using Aggregate Functions in WHERE

```sql
SELECT DepartmentID
FROM Employees
WHERE COUNT(*) > 5;
```

**Error:** Aggregate functions cannot be used in the `WHERE` clause.

---

#### ✅ Correct

```sql
SELECT DepartmentID
FROM Employees
GROUP BY DepartmentID
HAVING COUNT(*) > 5;
```

---

# Best Practices

- Use **`WHERE`** whenever possible to filter rows early.
- Use **`HAVING`** only for filtering aggregated results.
- Create indexes on columns frequently used in `WHERE`.
- Avoid using `HAVING` when a `WHERE` clause can achieve the same result.
- Use `HAVING` only with aggregate conditions such as `COUNT()`, `SUM()`, `AVG()`, `MIN()`, or `MAX()`.

---

#### Interview Tips

#### Use **WHERE** when:

- Filtering individual rows
- No aggregate functions are involved
- Better query performance is desired

#### Use **HAVING** when:

- Filtering grouped data
- Aggregate functions are required
- Working with `GROUP BY`

---

#### Quick Summary

| WHERE | HAVING |
|--------|---------|
| Filters rows | Filters groups |
| Before `GROUP BY` | After `GROUP BY` |
| Cannot use aggregate functions | Can use aggregate functions |
| Faster | Slower |
| Uses indexes | Usually works on aggregated data |

---

#### Key Takeaways

- **`WHERE`** filters rows before aggregation.
- **`HAVING`** filters groups after aggregation.
- `WHERE` is generally more efficient because it reduces the number of rows processed.
- `HAVING` is intended for conditions involving aggregate functions.
- Understanding the execution order of `WHERE` and `HAVING` is a common SQL interview question.
---

⬆️ **Back to Top**

### Q6. Define what a JOIN is in SQL and list its types.

A **JOIN** is a relational operation used to combine rows from **two or more tables** based on a related column or join condition.

JOINs are one of the most powerful features of SQL and are widely used to retrieve related data stored across multiple tables while maintaining data normalization.

---

#### Why Do We Use JOIN?

JOINs are used to:

- Retrieve related data from multiple tables
- Reduce data redundancy
- Maintain normalized database design
- Generate reports and analytics
- Build relationships between entities

---

#### How JOIN Works

A JOIN combines rows based on a **join condition** specified using the `ON` clause.

```sql
SELECT columns
FROM Table1
JOIN Table2
ON Table1.column = Table2.column;
```

---

#### Types of SQL JOIN

| JOIN Type | Description |
|-----------|-------------|
| **INNER JOIN** | Returns only matching rows from both tables |
| **LEFT JOIN (LEFT OUTER JOIN)** | Returns all rows from the left table and matching rows from the right table |
| **RIGHT JOIN (RIGHT OUTER JOIN)** | Returns all rows from the right table and matching rows from the left table |
| **FULL JOIN (FULL OUTER JOIN)** | Returns all rows from both tables, filling unmatched values with `NULL` |
| **CROSS JOIN** | Returns the Cartesian Product of both tables |
| **SELF JOIN** | Joins a table with itself |

---

#### INNER JOIN

Returns only the rows where the join condition matches in both tables.

#### Syntax

```sql
SELECT e.emp_name,
       d.department_name
FROM Employees e
INNER JOIN Departments d
ON e.department_id = d.department_id;
```

#### Example

**Employees**

| Employee | DepartmentID |
|----------|--------------|
| Alice | 1 |
| Bob | 2 |
| John | 3 |

**Departments**

| DepartmentID | Department |
|--------------|------------|
| 1 | HR |
| 2 | IT |

**Result**

| Employee | Department |
|----------|------------|
| Alice | HR |
| Bob | IT |

---

#### LEFT JOIN

Returns **all records from the left table** and matching records from the right table.

If there is no match, the right-side columns contain `NULL`.

```sql
SELECT e.emp_name,
       d.department_name
FROM Employees e
LEFT JOIN Departments d
ON e.department_id = d.department_id;
```

---

#### RIGHT JOIN

Returns **all records from the right table** and matching records from the left table.

```sql
SELECT e.emp_name,
       d.department_name
FROM Employees e
RIGHT JOIN Departments d
ON e.department_id = d.department_id;
```

---

#### FULL OUTER JOIN

Returns all rows from both tables.

If no matching row exists, missing values are filled with `NULL`.

```sql
SELECT
    COALESCE(e.department_id, d.department_id) AS DepartmentID,
    e.emp_name,
    d.department_name
FROM Employees e
FULL OUTER JOIN Departments d
ON e.department_id = d.department_id;
```

---

#### CROSS JOIN

Produces the **Cartesian Product** of two tables.

If Table A has **m** rows and Table B has **n** rows,

Total rows returned = **m × n**

```sql
SELECT *
FROM Employees
CROSS JOIN Departments;
```

#### Complexity

```
O(n × m)
```

---

#### SELF JOIN

A **SELF JOIN** joins a table with itself.

It is commonly used for:

- Employee–Manager relationships
- Organizational hierarchy
- Category hierarchy
- Family tree

```sql
SELECT
    E.Name AS Employee,
    M.Name AS Manager
FROM Employee E
LEFT JOIN Employee M
ON E.ManagerID = M.EmpID;
```

---

#### Recursive Hierarchy Using CTE

Modern SQL uses **Recursive CTEs** instead of repeated self joins.

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

---

#### JOIN Complexity

| Join Algorithm | Average Complexity |
|---------------|-------------------|
| Nested Loop Join | **O(n × m)** |
| Hash Join | **O(n + m)** |
| Sort Merge Join | **O(n + m)** *(after sorting)* |

Modern query optimizers automatically choose the most efficient join strategy based on:

- Available indexes
- Table statistics
- Memory
- Data size

---

#### Performance Optimization

#### Avoid `SELECT *`

Instead of:

```sql
SELECT *
FROM Employees e
JOIN Departments d
ON e.department_id = d.department_id;
```

Use:

```sql
SELECT
    e.emp_name,
    d.department_name
FROM Employees e
JOIN Departments d
ON e.department_id = d.department_id;
```

Benefits:

- Reduced network traffic
- Lower I/O
- Better execution plans
- Prevents schema drift issues

---

#### Index Join Columns

Create indexes on frequently joined columns.

```sql
CREATE INDEX idx_employee_department
ON Employees(department_id);
```

---

#### Use Proper Join Conditions

Always specify the join condition.

```sql
ON Employees.department_id = Departments.department_id
```

Missing the `ON` clause may result in a Cartesian Product.

---

#### Best Practices

- Use explicit `INNER JOIN` instead of implicit joins.
- Retrieve only required columns.
- Index foreign key and join columns.
- Avoid unnecessary joins.
- Prefer `INNER JOIN` over `OUTER JOIN` when possible.
- Use `COALESCE()` to handle `NULL` values in `FULL JOIN`.
- Analyze execution plans using `EXPLAIN ANALYZE`.

---

#### Interview Tips

#### INNER JOIN

Returns matching rows only.

#### LEFT JOIN

Returns all rows from the left table.

#### RIGHT JOIN

Returns all rows from the right table.

#### FULL JOIN

Returns all rows from both tables.

#### CROSS JOIN

Returns every possible combination of rows.

#### SELF JOIN

Joins a table with itself.

---

#### Quick Summary

| JOIN | Returns |
|------|----------|
| INNER JOIN | Matching rows only |
| LEFT JOIN | All left rows + matching right rows |
| RIGHT JOIN | All right rows + matching left rows |
| FULL JOIN | All rows from both tables |
| CROSS JOIN | Cartesian Product |
| SELF JOIN | Same table joined with itself |

---

#### Key Takeaways

- JOIN combines related data from multiple tables.
- **INNER JOIN** returns matching records only.
- **LEFT**, **RIGHT**, and **FULL JOIN** are outer joins that preserve unmatched rows.
- **CROSS JOIN** generates all possible row combinations.
- **SELF JOIN** is useful for hierarchical data.
- Modern databases optimize joins using **Hash Join**, **Merge Join**, and **Nested Loop Join** strategies.
- Proper indexing and selecting only required columns significantly improve JOIN performance.

---

### Q7. What is a Primary Key?

A **Primary Key (PK)** is a database constraint that **uniquely identifies each record (row)** in a table. It ensures **Entity Integrity**, meaning every row can be uniquely identified and accessed.

A table can have **only one Primary Key**, which may consist of one or multiple columns (Composite Primary Key).

---

#### Key Characteristics

#### 1. Uniqueness

Every value in the Primary Key must be **unique**.

✔ No duplicate values are allowed.

```text
StudentID
---------
101
102
103
104
```

❌ Duplicate values are not permitted.

---

#### 2. NOT NULL

A Primary Key **cannot contain NULL values**.

Every record must have a valid identifier.

```sql
CREATE TABLE Students (
    student_id INT PRIMARY KEY
);
```

---

#### 3. Immutability

Primary Key values should **never change**.

Changing a Primary Key may require updates to:

- Foreign Keys
- Indexes
- Related tables

This increases maintenance cost and may affect performance.

---

#### Role of Primary Key

A Primary Key serves several important purposes.

#### Entity Integrity

Ensures every row represents a unique real-world entity.

Example:

| StudentID | Name |
|-----------|------|
| 101 | Rahul |
| 102 | Priya |

---

#### Relationship Between Tables

Primary Keys are referenced by **Foreign Keys** to establish relationships.

Example

```text
Students
---------
StudentID (PK)

Enrollments
-----------
StudentID (FK)
```

---

#### Indexing

In most relational databases, a Primary Key automatically creates a **Unique Index**.

Examples:

- MySQL (InnoDB)
- PostgreSQL
- SQL Server

This improves:

- Searching
- Sorting
- Joining

---

#### Performance Considerations

#### Narrow Keys

Use smaller data types whenever possible.

Recommended:

- `INT`
- `BIGINT`
- `UUID`

Smaller keys consume:

- Less memory
- Less disk space
- Smaller indexes
- Faster joins

---

#### Join Optimization

Most JOIN operations are performed using **Primary Key** and **Foreign Key** relationships.

Example

```sql
SELECT s.first_name,
       d.department_name
FROM Students s
JOIN Departments d
ON s.department_id = d.department_id;
```

Proper indexing significantly improves JOIN performance.

---

#### UUID vs Integer Keys

#### Integer (BIGINT)

✔ Faster indexing

✔ Smaller storage

✔ Best for single-node databases

---

#### UUID

✔ Globally unique

✔ Better for distributed systems

✔ No collision across servers

Modern systems often prefer **UUIDv7**, which provides sequential ordering and reduces index fragmentation.

---

#### Best Practices

#### Use Surrogate Keys

Prefer system-generated identifiers instead of business values.

✔ Good

```text
StudentID
```

❌ Avoid

```text
Email
Phone Number
SSN
```

Business values can change over time.

---

#### Keep Primary Keys Small

Choose compact data types.

Example:

```text
INT
BIGINT
UUID
```

Avoid large string-based primary keys.

---

#### Composite Primary Keys

Use composite keys only when multiple columns together uniquely identify a record.

Example

```sql
PRIMARY KEY (StudentID, CourseID)
```

Common in many-to-many relationship tables.

---

#### Example: Creating a Primary Key

```sql
CREATE TABLE Students (

    student_id BIGINT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,

    first_name VARCHAR(50) NOT NULL,

    last_name VARCHAR(50) NOT NULL,

    grade_level INT NOT NULL,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);
```

---

#### Example Using UUID

```sql
CREATE TABLE Students (

    student_id UUID PRIMARY KEY DEFAULT gen_random_uuid(),

    first_name VARCHAR(50) NOT NULL,

    last_name VARCHAR(50) NOT NULL,

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP

);
```

---

#### Creating an Index

```sql
CREATE UNIQUE INDEX idx_students_uuid
ON Students(student_id);
```

---

#### Advantages of Primary Key

- Ensures unique records
- Prevents duplicate data
- Cannot contain NULL values
- Maintains entity integrity
- Improves search performance
- Optimizes JOIN operations
- Automatically creates a unique index in most databases

---

#### Interview Tips

#### Can a table have multiple Primary Keys?

❌ No.

A table can have **only one Primary Key**, but it can consist of multiple columns (Composite Primary Key).

---

#### Can a Primary Key contain NULL values?

❌ No.

---

#### Can Primary Key have duplicate values?

❌ No.

---

#### Difference Between Primary Key and Unique Key

| Primary Key | Unique Key |
|--------------|------------|
| Only one per table | Multiple allowed |
| Cannot contain NULL | Can contain NULL (database-dependent) |
| Automatically creates a unique index | Also creates a unique index |
| Used to uniquely identify records | Used to enforce uniqueness |

---

#### Best Practices (2026)

- Use **BIGINT** or **UUIDv7** as surrogate keys.
- Avoid business attributes (Email, SSN, Phone Number) as Primary Keys.
- Keep key width small to reduce index size and improve cache efficiency.
- Use Composite Primary Keys only for many-to-many relationship tables.
- Align Primary Keys with Foreign Keys to optimize JOIN performance.

---

#### Key Takeaways

- A **Primary Key (PK)** uniquely identifies every row in a table.
- It **must be unique** and **cannot contain NULL values**.
- Most databases automatically create a **unique index** for the Primary Key.
- Primary Keys are referenced by **Foreign Keys** to establish relationships.
- Choosing compact data types such as **BIGINT** or **UUIDv7** improves indexing and query performance.
- Well-designed Primary Keys are essential for maintaining data integrity and efficient database operations.
  
---

### Q8. Explain what a Foreign Key is.

A **Foreign Key (FK)** is a database constraint that establishes a relationship between two tables by referencing the **Primary Key (PK)** or **Unique Key** of another table.

It enforces **Referential Integrity**, ensuring that relationships between tables remain valid and consistent.

---

#### Key Functions of a Foreign Key

#### 1. Referential Integrity

A Foreign Key ensures that every value in the child table either:

- Matches an existing Primary Key (or Unique Key) in the parent table.
- Is `NULL` (unless the column is defined as `NOT NULL`).

This prevents invalid or orphaned records.

---

#### 2. Relationship Mapping

Foreign Keys create relationships between tables, enabling efficient data retrieval using **JOIN** operations.

Example:

```text
Departments
-----------
department_id (PK)

Employees
---------
department_id (FK)
```

---

#### 3. Declarative Referential Integrity (DRI)

Instead of enforcing relationships in application code, the database automatically maintains consistency.

Benefits:

- Prevents invalid references
- Simplifies application logic
- Improves data integrity

---

#### 4. Lifecycle Management

Foreign Keys support automatic actions when parent records are updated or deleted.

Common options include:

- `CASCADE`
- `RESTRICT`
- `SET NULL`
- `NO ACTION`
- `SET DEFAULT` *(database-dependent)*

---

#### Foreign Key Rules

- A Foreign Key must reference a **Primary Key** or **Unique Key**.
- A Foreign Key **can contain duplicate values**.
- A Foreign Key **can contain NULL values** unless defined as `NOT NULL`.
- A table can have multiple Foreign Keys.
- Foreign Keys maintain relationships between parent and child tables.

---

#### Parent and Child Table

#### Parent Table

Contains the **Primary Key**.

```text
Departments
-----------
department_id (PK)
```

---

#### Child Table

Contains the **Foreign Key**.

```text
Employees
---------
department_id (FK)
```

Many employees can belong to the same department.

---

#### Example

#### Parent Table

```sql
CREATE TABLE departments (

    department_id INT PRIMARY KEY,

    name VARCHAR(100) NOT NULL

);
```

---

#### Child Table

```sql
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
```

---

#### Indexing Foreign Keys

Most relational databases **do not automatically create an index** on Foreign Key columns.

Creating an index improves:

- JOIN performance
- DELETE operations
- UPDATE operations
- Query execution

```sql
CREATE INDEX idx_employees_department_id
ON employees(department_id);
```

---

#### Referential Actions

#### ON DELETE CASCADE

Deletes child records automatically when the parent record is deleted.

```sql
ON DELETE CASCADE
```

---

#### ON DELETE RESTRICT

Prevents deletion of a parent row if related child rows exist.

```sql
ON DELETE RESTRICT
```

---

#### ON DELETE SET NULL

Sets the Foreign Key value to `NULL` after deleting the parent row.

```sql
ON DELETE SET NULL
```

---

#### ON UPDATE CASCADE

Automatically updates Foreign Key values when the referenced Primary Key changes.

```sql
ON UPDATE CASCADE
```

---

#### Performance Considerations

#### Foreign Key Validation

When inserting or updating data, the database verifies that the referenced parent key exists.

With an indexed parent key, validation typically operates in:

**Time Complexity:** **O(log n)**

---

#### Join Performance

Proper indexing on Foreign Key columns improves JOIN performance.

Example:

```sql
SELECT
    e.name,
    d.name AS department_name
FROM employees e
JOIN departments d
ON e.department_id = d.department_id;
```

---

#### Distributed Databases

In distributed SQL databases (e.g., CockroachDB, YugabyteDB), excessive cross-node Foreign Key constraints can increase transaction latency.

Consider minimizing cross-region Foreign Key relationships when designing globally distributed systems.

---

#### Best Practices

- Reference only **Primary Keys** or **Unique Keys**.
- Create indexes on frequently queried Foreign Key columns.
- Use meaningful constraint names for easier debugging.
- Choose appropriate referential actions (`CASCADE`, `RESTRICT`, `SET NULL`) based on business rules.
- Keep Foreign Key columns consistent with the referenced key's data type.
- Use `NOT NULL` if the relationship is mandatory.

---

#### Common Misconception

#### ❌ Foreign Key values must be unique.

**Incorrect.**

A Foreign Key **does not need to be unique**.

Example:

```text
Employees
-------------------------
EmployeeID  DepartmentID
1           101
2           101
3           101
4           102
```

Multiple employees can belong to the same department.

The **referenced Primary Key** in the parent table must be unique.

---

#### Primary Key vs Foreign Key

| Feature | Primary Key | Foreign Key |
|---------|-------------|-------------|
| Purpose | Uniquely identifies a row | Creates a relationship between tables |
| Duplicate Values | ❌ Not Allowed | ✅ Allowed |
| NULL Values | ❌ Not Allowed | ✅ Allowed (unless `NOT NULL`) |
| Number per Table | One (can be composite) | Multiple |
| Creates Relationship | No | Yes |
| References Another Table | No | Yes |

---

#### Interview Tips

#### Can a table have multiple Foreign Keys?

✅ Yes.

---

#### Can a Foreign Key contain NULL?

✅ Yes, unless it is defined as `NOT NULL`.

---

#### Can a Foreign Key have duplicate values?

✅ Yes.

Many child rows can reference the same parent row.

---

#### Does a Foreign Key automatically create an index?

❌ No.

In most databases, you should create an index manually for better performance.

---

#### Key Takeaways

- A **Foreign Key (FK)** establishes a relationship between two tables.
- It references a **Primary Key** or **Unique Key** in the parent table.
- Foreign Keys enforce **Referential Integrity** and prevent invalid relationships.
- Foreign Key values **can be duplicated** and **can contain NULL values** unless restricted.
- Indexing Foreign Key columns significantly improves JOIN and DML performance.
- Choosing appropriate referential actions helps maintain consistent and reliable database relationships.
---

### Q9. How can you prevent SQL Injection?

**SQL Injection (SQLi)** is one of the most common and critical web application security vulnerabilities. It occurs when an application improperly handles **user input**, allowing attackers to manipulate SQL queries executed by the database.

The primary goal of SQL Injection prevention is to **separate data from SQL code**, ensuring that user input is always treated as data and never as executable SQL.

---

#### How SQL Injection Works

Consider the following vulnerable query:

```sql
SELECT *
FROM users
WHERE username = 'admin'
AND password = 'password';
```

If an attacker enters:

```text
Username: admin
Password: ' OR '1'='1
```

The query becomes:

```sql
SELECT *
FROM users
WHERE username = 'admin'
AND password = '' OR '1'='1';
```

Since `'1'='1'` is always true, the attacker may bypass authentication.

---

#### SQL Injection Prevention Techniques

#### 1. Parameterized Queries (Prepared Statements) ⭐ Recommended

Prepared Statements are the **most effective defense** against SQL Injection.

The SQL statement is sent to the database first, while user input is passed separately as parameters.

This ensures user input is always treated as **data**, not executable SQL.

#### Example (Python - SQLAlchemy)

```python
from sqlalchemy import text

stmt = text("""
SELECT *
FROM users
WHERE username = :username
AND password = :password
""")

result = session.execute(
    stmt,
    {
        "username": username,
        "password": password
    }
)
```

#### Advantages

- Prevents SQL Injection
- Separates SQL code from user data
- Supports query execution plan caching
- Improves performance
- Easy to maintain

---

#### 2. Stored Procedures

Stored Procedures encapsulate SQL logic inside the database.

They are secure **only when parameterized queries are used internally**.

#### Safe Example

```sql
CREATE PROCEDURE GetEmployee
    @EmployeeID INT
AS
BEGIN
    SELECT *
    FROM Employees
    WHERE EmployeeID = @EmployeeID;
END;
```

#### Avoid

Building SQL strings dynamically inside stored procedures.

```sql
SET @sql =
'SELECT * FROM Users WHERE Name=''' + @Name + '''';
```

Dynamic SQL without parameterization remains vulnerable.

---

#### 3. Input Validation (Allow-listing)

Validate user input before sending it to the database.

Examples:

- Username
- Email
- Phone Number
- Date
- Age

Only allow expected values.

#### Example (Pydantic)

```python
from pydantic import BaseModel, StringConstraints
from typing import Annotated

class UserLogin(BaseModel):

    username: Annotated[
        str,
        StringConstraints(
            pattern=r'^[a-zA-Z0-9_]{3,20}$'
        )
    ]
```

#### Benefits

- Blocks malicious input
- Improves application security
- Validates data format
- Provides defense in depth

---

#### 4. Principle of Least Privilege (PoLP)

Applications should connect to the database using an account with **minimum required permissions**.

#### Best Practices

- Do not use `root`, `sa`, or `superuser`.
- Grant only required permissions.
- Use Role-Based Access Control (RBAC).
- Restrict access to sensitive tables.
- Remove unnecessary privileges such as:

  - `DROP`
  - `TRUNCATE`
  - `ALTER`
  - `GRANT`

This limits damage even if an attack succeeds.

---

#### 5. Use ORM Frameworks

Modern Object-Relational Mappers (ORMs) automatically generate **parameterized queries**, reducing the risk of SQL Injection.

Popular ORMs include:

- Hibernate
- JPA
- SQLAlchemy
- Entity Framework
- Prisma
- Django ORM

#### Example (Hibernate)

```java
TypedQuery<User> query =
entityManager.createQuery(
    "FROM User WHERE username = :username",
    User.class
);

query.setParameter("username", username);
```

Avoid concatenating user input into raw SQL queries.

---

#### What to Avoid

#### ❌ Dynamic SQL

```java
String sql =
"SELECT * FROM users WHERE username='"
+ username + "'";
```

If `username` contains malicious SQL, the query becomes vulnerable.

---

#### ❌ Manual Escaping

Using string replacement or regular expressions to sanitize input is **not recommended**.

Example:

```java
username.replace("'", "");
```

This approach is:

- Error-prone
- Difficult to maintain
- Vulnerable to encoding tricks

Prefer parameterized queries instead.

---

#### Best Practices

- Always use Prepared Statements.
- Validate user input using allow-lists.
- Use ORM frameworks whenever possible.
- Apply the Principle of Least Privilege.
- Avoid dynamic SQL generation.
- Never trust client-side validation alone.
- Keep database software and libraries up to date.
- Monitor and log suspicious database activity.

---

#### SQL Injection Prevention Checklist

| Security Measure | Recommended |
|------------------|:-----------:|
| Prepared Statements | ✅ |
| Parameterized Queries | ✅ |
| ORM Frameworks | ✅ |
| Input Validation | ✅ |
| Least Privilege | ✅ |
| Stored Procedures (Parameterized) | ✅ |
| Dynamic SQL | ❌ |
| Manual Escaping | ❌ |

---

#### Interview Tips

#### What is SQL Injection?

A security vulnerability that allows attackers to manipulate SQL queries through malicious user input.

---

#### Best Defense Against SQL Injection?

**Parameterized Queries (Prepared Statements).**

---

#### Are Stored Procedures Always Safe?

No.

Stored Procedures are secure only when they use **parameterized SQL** internally.

---

#### Can ORM Prevent SQL Injection?

Yes.

Most modern ORMs generate parameterized queries by default. However, raw SQL queries must still use parameter binding.

---

#### Key Takeaways

- SQL Injection occurs when user input is treated as executable SQL.
- **Prepared Statements** are the most effective defense.
- Validate all user input using allow-listing.
- Follow the **Principle of Least Privilege (PoLP)** for database accounts.
- Use modern ORM frameworks that default to parameterized queries.
- Avoid dynamic SQL string concatenation and manual input escaping.
- Combining multiple security techniques provides **defense in depth** against SQL Injection attacks.

---

### Q10. What is Normalization?

**Normalization** is the process of organizing data in a relational database to **minimize redundancy**, **eliminate data anomalies**, and **improve data integrity**. It is achieved by dividing large tables into smaller, related tables and defining relationships using **Primary Keys** and **Foreign Keys**.

Normalization is based on **functional dependencies** and follows a series of **Normal Forms (NF)**.

---

#### Objectives of Normalization

- Eliminate duplicate data
- Reduce data redundancy
- Prevent insertion, update, and deletion anomalies
- Improve data consistency
- Maintain referential integrity
- Simplify database maintenance

---

#### Types of Normal Forms

| Normal Form | Purpose |
|-------------|---------|
| **1NF (First Normal Form)** | Eliminates repeating groups and ensures atomic values |
| **2NF (Second Normal Form)** | Removes partial dependencies |
| **3NF (Third Normal Form)** | Removes transitive dependencies |
| **BCNF (Boyce-Codd Normal Form)** | Every determinant must be a candidate key |
| **4NF (Fourth Normal Form)** | Removes multi-valued dependencies |

---

#### First Normal Form (1NF)

A table is in **First Normal Form (1NF)** if:

- Every column contains **atomic (single) values**.
- There are **no repeating groups or arrays**.
- Each row is uniquely identifiable.

#### ❌ Unnormalized Table (0NF)

| StudentID | Name | Subjects |
|-----------|------|----------|
| 101 | Rahul | Java, SQL, Spring |

The `Subjects` column contains multiple values.

---

#### ✅ 1NF

| StudentID | Name | Subject |
|-----------|------|---------|
| 101 | Rahul | Java |
| 101 | Rahul | SQL |
| 101 | Rahul | Spring |

Each column now contains a single value.

---

#### Second Normal Form (2NF)

A table is in **Second Normal Form (2NF)** if:

- It is already in **1NF**.
- Every non-key column is **fully dependent** on the entire Primary Key.
- There are **no partial dependencies**.

#### ❌ Example

| InvoiceNo | ProductID | ProductName | Quantity |
|------------|-----------|-------------|----------|

Primary Key:

```text
(InvoiceNo, ProductID)
```

`ProductName` depends only on `ProductID`, not on the complete composite key.

---

#### ✅ 2NF

**Products**

| ProductID | ProductName |
|------------|-------------|
| 101 | Laptop |

**Invoice_Items**

| InvoiceNo | ProductID | Quantity |
|------------|-----------|----------|

Partial dependency has been removed.

---

#### Third Normal Form (3NF)

A table is in **Third Normal Form (3NF)** if:

- It is already in **2NF**.
- There are **no transitive dependencies**.
- Non-key attributes depend only on the Primary Key.

#### ❌ Example

| StudentID | StudentName | Department | HOD |
|------------|-------------|------------|-----|

Here:

```text
StudentID → Department
Department → HOD
```

`HOD` depends on `Department`, not directly on `StudentID`.

---

#### ✅ 3NF

**Students**

| StudentID | StudentName | DepartmentID |
|------------|-------------|--------------|

**Departments**

| DepartmentID | Department | HOD |
|--------------|------------|-----|

Transitive dependency has been removed.

---

#### Boyce-Codd Normal Form (BCNF)

BCNF is a stricter version of **3NF**.

A table is in **BCNF** if:

> For every functional dependency **X → Y**, **X must be a candidate key**.

BCNF removes anomalies that may still exist in some 3NF tables.

---

#### Fourth Normal Form (4NF)

A table is in **Fourth Normal Form (4NF)** if:

- It is already in **BCNF**.
- It contains **no multi-valued dependencies**.

This prevents storing multiple independent sets of data in the same table.

---

#### Normalization Example

#### Customers

```sql
CREATE TABLE Customers (

    CustomerID INT PRIMARY KEY,

    CustomerName VARCHAR(255) NOT NULL

);
```

---

#### Products

```sql
CREATE TABLE Products (

    ProductID INT GENERATED ALWAYS AS IDENTITY PRIMARY KEY,

    Description TEXT NOT NULL,

    UnitPrice DECIMAL(12,2)
        CHECK (UnitPrice >= 0)

);
```

---

#### Invoices

```sql
CREATE TABLE Invoices (

    InvoiceNo INT PRIMARY KEY,

    CustomerID INT NOT NULL
        REFERENCES Customers(CustomerID),

    InvoiceDate TIMESTAMPTZ
        DEFAULT CURRENT_TIMESTAMP

);
```

---

#### Invoice Items

```sql
CREATE TABLE Invoice_Items (

    InvoiceNo INT
        REFERENCES Invoices(InvoiceNo),

    ProductID INT
        REFERENCES Products(ProductID),

    Quantity INT
        CHECK (Quantity > 0),

    PRIMARY KEY (InvoiceNo, ProductID)

);
```

---

#### Benefits of Normalization

- Eliminates duplicate data
- Improves data consistency
- Prevents update anomalies
- Prevents insertion anomalies
- Prevents deletion anomalies
- Saves storage space
- Improves maintainability
- Ensures referential integrity

---

#### Disadvantages of Normalization

- Requires more tables
- Increases the number of JOIN operations
- Can reduce read performance for complex queries
- Database design becomes more complex

---

#### Normalization vs Denormalization

| Normalization | Denormalization |
|---------------|-----------------|
| Reduces redundancy | Introduces redundancy intentionally |
| Better data integrity | Faster read performance |
| More JOIN operations | Fewer JOIN operations |
| Ideal for OLTP systems | Ideal for OLAP systems |
| Easier updates | Better reporting performance |

---

#### OLTP vs OLAP (2026)

#### OLTP (Online Transaction Processing)

- Highly normalized (typically **3NF**)
- Frequent INSERT, UPDATE, DELETE operations
- Ensures ACID compliance
- Best for transactional applications

Examples:

- Banking
- E-commerce
- ERP
- CRM

---

#### OLAP (Online Analytical Processing)

- Often denormalized
- Optimized for analytics and reporting
- Uses **Star Schema** or **Snowflake Schema**
- Reduces JOIN complexity

Examples:

- Business Intelligence
- Data Warehousing
- Dashboards
- Reporting

---

#### Best Practices

- Normalize transactional databases up to **3NF**.
- Use **BCNF** or **4NF** only when required by the data model.
- Use Primary Keys and Foreign Keys to maintain relationships.
- Avoid over-normalization when it negatively impacts performance.
- Consider denormalization for reporting and analytical workloads.

---

#### Interview Tips

#### Why is normalization used?

To eliminate redundancy and maintain data consistency.

---

#### Which Normal Form is most commonly used?

**Third Normal Form (3NF)**

---

#### Difference Between 2NF and 3NF

| 2NF | 3NF |
|------|------|
| Removes partial dependency | Removes transitive dependency |

---

#### Is normalization always good?

No.

For analytical systems, controlled denormalization often improves query performance.

---

#### Key Takeaways

- **Normalization** organizes data to reduce redundancy and improve integrity.
- **1NF** ensures atomic values.
- **2NF** removes partial dependencies.
- **3NF** removes transitive dependencies.
- **BCNF** strengthens dependency rules beyond 3NF.
- **4NF** eliminates multi-valued dependencies.
- Transactional databases typically use **3NF**, while analytical systems often use denormalized schemas for better read performance.
  

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

