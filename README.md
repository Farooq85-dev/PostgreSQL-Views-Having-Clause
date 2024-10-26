# PostgreSQL-Views-Having-Clause

## This repository is how to use views and having clause in PostgreSQL.

### `What are views?`

```
A Postgres view is a virtual table in Postgres. It represents the result of a query to one or more underlying tables in Postgres. Views are used to simplify complex queries since these queries are defined once in the view, and can then be directly queried via the same.
```

### Key Features of Views:

- Virtual Table: Views act like tables but do not hold data.
- Simplified Queries: They can simplify complex SQL queries by encapsulating them.
- Security: You can grant access to a view without exposing the underlying tables.
- Updatable: Some views can be updated, allowing you to change data in the underlying tables.

### 1)`create a employees table`

```
create table employees ( id SERIAL PRIMARY KEY,
    name VARCHAR(100),
    department_id INT,
    salary NUMERIC
);
```

### 2)`create a department table`

```
CREATE TABLE departments (
    id SERIAL PRIMARY KEY,
    name VARCHAR(100)
);
```

### 3)`create a view of employees alongwith their department name`

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

### 4)`update a view`

```
UPDATE employee_departments
SET salary = salary \* 1.10
WHERE department_name = 'Sales';
```

### 5) `drop a view`

```
DROP VIEW employee_departments
```

### `What is having clause?`

```
The HAVING clause in PostgreSQL is used to filter the results of a GROUP BY query. It is similar to the WHERE clause but is applied after the aggregation of data has occurred. This means that HAVING can filter based on aggregate functions like SUM(), COUNT(), AVG(), etc.
```

### 1) `create a sales table`

```
CREATE TABLE sales (
    id SERIAL PRIMARY KEY,
    product VARCHAR(100),
    quantity INT,
    price NUMERIC
);
```

### 2) `insert a sample data in sales table`

```
INSERT INTO sales (product, quantity, price) VALUES
('Widget A', 10, 5.00),
('Widget B', 20, 7.50),
('Widget A', 5, 5.00),
('Widget C', 15, 10.00);
```

### 3) `having clause`

```
SELECT product, SUM(quantity) AS total_quantity
FROM sales
GROUP BY product
HAVING SUM(quantity) > 10;
```
