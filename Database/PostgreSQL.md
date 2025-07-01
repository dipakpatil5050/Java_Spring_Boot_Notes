**Day 1 of PostgreSQL Preparation**.

---

# 📘 **Day 1: PostgreSQL Fundamentals for Backend Devs**

### 🎯 Goal:

Understand the core SQL building blocks needed for backend development with PostgreSQL. Practice essential commands with examples.

---

## 🔧 Step 1: Setup PostgreSQL

### ✅ Install Options:

- **Local**: [Download PostgreSQL](https://www.postgresql.org/download/) + install **pgAdmin** (GUI client)
- **GUI Client Alternative**: [DBeaver](https://dbeaver.io/)
- **Online Playground (Optional)**: [https://www.db-fiddle.com](https://www.db-fiddle.com)

---

## 📗 Section 1: Create & Manage Database

### ✅ Create a New Database

```sql
CREATE DATABASE shopdb;
```

### ✅ Connect to a Database

```bash
\c shopdb  -- in psql CLI
```

---

## 📗 Section 2: Creating Tables & Inserting Data

### ✅ Create a Table

```sql
CREATE TABLE users (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    email VARCHAR(100) UNIQUE NOT NULL,
    age INT,
    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

### ✅ Insert Data

```sql
INSERT INTO users (name, email, age) VALUES
('Dipak', 'dipak@mail.com', 24),
('Amit', 'amit@mail.com', 27);
```

### ✅ View All Records

```sql
SELECT * FROM users;
```

---

## 📗 Section 3: CRUD Operations

### ✅ Read (SELECT)

```sql
SELECT name, email FROM users WHERE age > 25 ORDER BY age DESC;
```

### ✅ Update

```sql
UPDATE users SET age = 28 WHERE name = 'Amit';
```

### ✅ Delete

```sql
DELETE FROM users WHERE age < 25;
```

---

## 📗 Section 4: Constraints & Data Types

### ✅ Constraints

- `PRIMARY KEY` → Unique identifier
- `UNIQUE` → No duplicates
- `NOT NULL` → Value required
- `DEFAULT` → Default value
- `CHECK` → Validates condition
- `FOREIGN KEY` → Refers to another table

### ✅ Example

```sql
CREATE TABLE products (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    price DECIMAL(10,2) CHECK (price > 0),
    stock INT DEFAULT 0
);
```

---

## 📗 Section 5: Filtering & Conditions

### ✅ WHERE, AND, OR

```sql
SELECT * FROM users WHERE age > 20 AND age < 30;
```

### ✅ LIKE (pattern matching)

```sql
SELECT * FROM users WHERE email LIKE '%@mail.com';
```

### ✅ BETWEEN

```sql
SELECT * FROM users WHERE age BETWEEN 20 AND 30;
```

---

## 📗 Section 6: Sorting & Limiting

### ✅ ORDER BY

```sql
SELECT * FROM users ORDER BY age DESC;
```

### ✅ LIMIT

```sql
SELECT * FROM users ORDER BY age LIMIT 3;
```

---

## 📗 Section 7: Aggregate Functions

### ✅ COUNT, AVG, SUM, MAX, MIN

```sql
SELECT COUNT(*) FROM users;
SELECT AVG(age) FROM users;
```

---

## 📗 Section 8: Aliasing & DISTINCT

### ✅ AS (aliasing columns)

```sql
SELECT name AS "User Name", age AS "User Age" FROM users;
```

### ✅ DISTINCT (unique values)

```sql
SELECT DISTINCT age FROM users;
```

---

## 🧪 Practice Task for Today

Create the following table and perform insert + queries:

```sql
CREATE TABLE employees (
    emp_id SERIAL PRIMARY KEY,
    emp_name VARCHAR(100),
    department VARCHAR(50),
    salary INT,
    join_date DATE DEFAULT CURRENT_DATE
);
```

**Insert 5 records**, and try:

- Get employees in "Sales"
- Get salary > 50000
- Order by join date
- Count number of employees in each department

---

## ✅ Summary of Commands Today

| Action       | Command Example                             |
| ------------ | ------------------------------------------- |
| Create DB    | `CREATE DATABASE shopdb;`                   |
| Create Table | `CREATE TABLE users (...);`                 |
| Insert Data  | `INSERT INTO users (...) VALUES (...);`     |
| Read Records | `SELECT * FROM users;`                      |
| Update Data  | `UPDATE users SET ... WHERE ...;`           |
| Delete Data  | `DELETE FROM users WHERE ...;`              |
| Filter       | `WHERE`, `LIKE`, `BETWEEN`, `AND`, `OR`     |
| Sort & Limit | `ORDER BY`, `LIMIT`                         |
| Aggregate    | `COUNT()`, `AVG()`, `SUM()`                 |
| Constraints  | `PRIMARY KEY`, `UNIQUE`, `CHECK`, `DEFAULT` |

---

---

# 📘 **Day 2: JOINs, Aggregate Functions & Subqueries in PostgreSQL**

---

## 🎯 **Goal**:

* Understand how to link tables with JOINs
* Use aggregate functions to summarize data
* Use subqueries to write complex conditions

---

## 🔧 Prerequisite Tables

We'll use these sample tables today:

```sql
-- Table 1: departments
CREATE TABLE departments (
    dept_id SERIAL PRIMARY KEY,
    dept_name VARCHAR(50) NOT NULL
);

-- Table 2: employees (already created yesterday, adding FK now)
ALTER TABLE employees ADD COLUMN dept_id INT;
ALTER TABLE employees ADD CONSTRAINT fk_dept FOREIGN KEY (dept_id) REFERENCES departments(dept_id);
```

### ✅ Sample Data

```sql
-- Insert into departments
INSERT INTO departments (dept_name) VALUES 
('Engineering'), 
('Sales'), 
('HR'), 
('Marketing'), 
('Finance');

-- Update employees to assign dept_id
UPDATE employees SET dept_id = 1 WHERE dept = 'Engineering';
UPDATE employees SET dept_id = 2 WHERE dept = 'Sales';
UPDATE employees SET dept_id = 3 WHERE dept = 'HR';
UPDATE employees SET dept_id = 4 WHERE dept = 'Marketing';
UPDATE employees SET dept_id = 5 WHERE dept = 'Finance';
```

---

## ✅ Section 1: JOINS

### 🔸 `INNER JOIN`: Match records in both tables

```sql
SELECT e.emp_id, e.fname, d.dept_name
FROM employees e
INNER JOIN departments d ON e.dept_id = d.dept_id;
```

### 🔸 `LEFT JOIN`: Get all employees, even if no matching department

```sql
SELECT e.emp_id, e.fname, d.dept_name
FROM employees e
LEFT JOIN departments d ON e.dept_id = d.dept_id;
```

### 🔸 `RIGHT JOIN`: Get all departments, even if no employees

```sql
SELECT e.fname, d.dept_name
FROM employees e
RIGHT JOIN departments d ON e.dept_id = d.dept_id;
```

### 🔸 `FULL JOIN`: Everything from both sides

```sql
SELECT e.fname, d.dept_name
FROM employees e
FULL JOIN departments d ON e.dept_id = d.dept_id;
```

---

## ✅ Section 2: Aggregate Functions

### 🔸 COUNT, SUM, AVG, MAX, MIN

```sql
-- Count total employees
SELECT COUNT(*) FROM employees;

-- Average salary
SELECT AVG(salary) FROM employees;

-- Maximum salary in Engineering
SELECT MAX(salary) FROM employees WHERE dept = 'Engineering';

-- Salary stats per department
SELECT dept, COUNT(*) AS emp_count, AVG(salary) AS avg_salary
FROM employees
GROUP BY dept;
```

---

## ✅ Section 3: GROUP BY & HAVING

### 🔸 Group + Filter aggregate results

```sql
-- Total salary per department
SELECT dept, SUM(salary) AS total_salary
FROM employees
GROUP BY dept;

-- Only departments where total salary > 100000
SELECT dept, SUM(salary) AS total_salary
FROM employees
GROUP BY dept
HAVING SUM(salary) > 100000;
```

---

## ✅ Section 4: Subqueries

### 🔸 Subquery in `WHERE` clause

```sql
-- Employees with salary > average salary
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### 🔸 Subquery in `FROM` clause (Derived Table)

```sql
SELECT dept, avg_salary
FROM (
  SELECT dept, AVG(salary) AS avg_salary
  FROM employees
  GROUP BY dept
) AS dept_avg
WHERE avg_salary > 50000;
```

### 🔸 Subquery in `SELECT` clause

```sql
SELECT fname, lname,
  (SELECT dept_name FROM departments d WHERE d.dept_id = e.dept_id) AS department
FROM employees e;
```

---

## 🧪 Practice Task for Today

> **Task:** Write and test these queries:

1. Get employee names and their department names (using JOIN)
2. Find employees who joined in the last 6 months
3. Find departments with more than 2 employees
4. Show department-wise max salary
5. Show employees whose salary is more than the average salary
6. Show employees who work in a department that has "Sales" in its name (using JOIN + LIKE)

---

## ✅ Day 2 Summary

| Concept    | Key Queries                         |
| ---------- | ----------------------------------- |
| JOINs      | `INNER`, `LEFT`, `RIGHT`, `FULL`    |
| Aggregates | `COUNT`, `SUM`, `AVG`, `MAX`, `MIN` |
| Grouping   | `GROUP BY`, `HAVING`                |
| Subqueries | In `SELECT`, `WHERE`, `FROM`        |

---