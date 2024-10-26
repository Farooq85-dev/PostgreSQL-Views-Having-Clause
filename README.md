# PostgreSQL-Views-Having-Clause

## This repository is how to use views and having clause in PostgreSQL.

### 1) `What is view?`

```
    In PostgreSQL, a view is a virtual table that is based on the result of a SQL query. It does not store data itself but provides a way to present data from one or more tables in a specific format. Views can simplify complex queries, enhance security by restricting access to specific data, and encapsulate frequently used queries.
```

#### Key Features of Views:

- Virtual Table: Views act like tables but do not hold data.
- Simplified Queries: They can simplify complex SQL queries by encapsulating them.
- Security: You can grant access to a view without exposing the underlying tables.
- Updatable: Some views can be updated, allowing you to change data in the underlying tables.

### 2) `Create a emplyees table?`

```
CREATE TABLE employees (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    salary NUMERIC
);
```

### 3) `Create a department table?`

```
CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```

### 4) `Create view that shows employees along with their department names`

```
CREATE VIEW employee_departments AS
SELECT
    e.id,
    e.name AS employee_name,
    d.name AS department_name,
    e.salary
FROM
    employees e
JOIN
    departments d ON e.department_id = d.id;
```

### 5) `querying view`

```
SELECT * FROM employee_departments;
```

### 6) `Update view`

```
UPDATE employee_departments
SET salary = salary * 1.10
WHERE department_name = 'Sales';
```

### 7) `Drop view`

```
DROP VIEW employee_departments;
```

### `What is having clause?`

```
The HAVING clause in PostgreSQL is used to filter the results of a GROUP BY query. It is similar to the WHERE clause but is applied after the aggregation of data has occurred. This means that HAVING can filter based on aggregate functions like SUM(), COUNT(), AVG(), etc.
```

### 1) `Create a sales table`

```
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    product VARCHAR(100),
    quantity INT,
    price NUMERIC
);

```

### 2) `Insert dummy data into sales table`

```
INSERT INTO sales (product, quantity, price) VALUES
('Widget A', 10, 5.00),
('Widget B', 20, 7.50),
('Widget A', 5, 5.00),
('Widget C', 15, 10.00);
```

### 3) `Querying a view`

```
SELECT product, SUM(quantity) AS total_quantity
FROM sales
GROUP BY product
HAVING SUM(quantity) > 20;
```
