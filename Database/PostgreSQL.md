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
