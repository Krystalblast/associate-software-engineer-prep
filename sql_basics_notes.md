# SQL Basics Notes

## 1. What is SQL?
- **SQL (Structured Query Language)** is the standard language for managing data in a **relational database**.
- It allows you to:
  - **Define** database structures (`CREATE`, `ALTER`, `DROP`)
  - **Manipulate** data (`INSERT`, `UPDATE`, `DELETE`)
  - **Query** data (`SELECT`)
  - **Control** access (`GRANT`, `REVOKE`)
  - **Manage** transactions (`COMMIT`, `ROLLBACK`)

---

## 2. SQL Data Types (Commonly Used)
Data types depend on the database system (MySQL, PostgreSQL, SQL Server, etc.), but these are the most common:

- **Numeric Types**
  - `INT` – whole numbers
  - `DECIMAL(p, s)` – exact decimal values (e.g., currency)
  - `FLOAT`, `REAL` – approximate values

- **String Types**
  - `CHAR(n)` – fixed-length string
  - `VARCHAR(n)` – variable-length string
  - `TEXT` – long text

- **Date & Time Types**
  - `DATE` – stores year, month, day
  - `TIME` – stores hour, minute, second
  - `DATETIME` / `TIMESTAMP` – stores full date and time

- **Other**
  - `BOOLEAN` – true/false
  - `BLOB` – binary large object (images, files)

---

## 3. SQL Commands

### 🔹 DDL (Data Definition Language)
Defines and manages schema.
```sql
CREATE DATABASE company;
CREATE TABLE employees (
    id INT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    salary DECIMAL(10,2),
    hire_date DATE
);
ALTER TABLE employees ADD department VARCHAR(50);
DROP TABLE employees;
```

### 🔹 DML (Data Manipulation Language)
Used to insert, update, or delete data.
```sql
INSERT INTO employees (id, name, salary, hire_date)
VALUES (1, 'Alice', 5500.00, '2022-01-01');

UPDATE employees
SET salary = 6000
WHERE id = 1;

DELETE FROM employees
WHERE id = 1;
```

### 🔹 DQL (Data Query Language)
Used for querying.
```sql
SELECT * FROM employees;
SELECT name, salary FROM employees WHERE salary > 5000;
SELECT DISTINCT department FROM employees;
```

### 🔹 DCL (Data Control Language)
Controls access.
```sql
GRANT SELECT, INSERT ON employees TO user1;
REVOKE INSERT ON employees FROM user1;
```

### 🔹 TCL (Transaction Control Language)
Manages transactions.
```sql
BEGIN;
UPDATE employees SET salary = salary + 1000 WHERE department = 'HR';
COMMIT;  -- save changes
ROLLBACK; -- undo changes
```

---

## 4. Clauses in SQL
- **`WHERE`** → filter rows  
- **`ORDER BY`** → sort results (`ASC` or `DESC`)  
- **`GROUP BY`** → group rows for aggregation  
- **`HAVING`** → filter groups after aggregation  
- **`LIMIT`** (or `TOP` in SQL Server) → restrict rows  

Example:
```sql
SELECT department, COUNT(*) AS num_employees, AVG(salary) AS avg_salary
FROM employees
WHERE salary > 3000
GROUP BY department
HAVING COUNT(*) > 5
ORDER BY avg_salary DESC
LIMIT 10;
```

---

## 5. SQL Joins
Joins combine rows from multiple tables based on related columns.

- **INNER JOIN** → only matching rows  
- **LEFT JOIN** → all from left + matching from right  
- **RIGHT JOIN** → all from right + matching from left  
- **FULL OUTER JOIN** → all rows from both  

```sql
SELECT e.name, d.department_name
FROM employees e
INNER JOIN departments d ON e.department_id = d.id;
```

---

## 6. Aggregate Functions
- `COUNT(*)` → count rows  
- `SUM(salary)` → total  
- `AVG(salary)` → average  
- `MIN(salary)` / `MAX(salary)` → smallest/largest  

```sql
SELECT department, COUNT(*) AS total, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

---

## 7. Constraints
Rules applied to table columns:
- `PRIMARY KEY` – unique & not null  
- `FOREIGN KEY` – links to another table  
- `UNIQUE` – no duplicates  
- `NOT NULL` – must have a value  
- `DEFAULT` – sets default value  

```sql
CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    order_date DATE NOT NULL,
    customer_id INT,
    FOREIGN KEY (customer_id) REFERENCES customers(id)
);
```

---

## 8. Indexes
Indexes improve search performance.
```sql
CREATE INDEX idx_name ON employees(name);
```

---

## 9. Example End-to-End Query
```sql
SELECT c.name, COUNT(o.order_id) AS total_orders, SUM(o.amount) AS total_spent
FROM customers c
JOIN orders o ON c.id = o.customer_id
WHERE o.order_date >= '2023-01-01'
GROUP BY c.name
HAVING total_spent > 1000
ORDER BY total_spent DESC;
```

---

## 📚 References
- [W3Schools – SQL Tutorial](https://www.w3schools.com/sql/)  
- [PostgreSQL Official Docs](https://www.postgresql.org/docs/current/sql.html)  
- [MySQL Reference Manual](https://dev.mysql.com/doc/refman/8.0/en/sql-statements.html)  
- [SQL Server Docs](https://learn.microsoft.com/en-us/sql/sql-server/)  
- [SQLite Documentation](https://www.sqlite.org/docs.html)  
