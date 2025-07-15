### 1. **Use Indexes Efficiently**

Indexes are crucial for optimising SQL queries as they allow the database to retrieve data more quickly. Key points to remember:

- **Types of Indexes**: Understand different types like B-tree, hash, and full-text indexes and their appropriate use cases.
  
- **Index Selection**: Choose columns for indexing based on how often they are used in WHERE, JOIN, and ORDER BY clauses.

Example:
```sql
-- Creating an index
CREATE INDEX idx_customers_lastname ON customers(last_name);

-- Query using the index
SELECT * FROM customers WHERE last_name = 'Smith';
```

### 2. **Optimize Joins**

Joins can significantly impact query performance. Techniques to optimize joins include:

- **Use INNER JOIN Instead of WHERE**: Prefer `INNER JOIN` syntax over joining tables in the `WHERE` clause.

- **Avoid Cartesian Products**: Ensure join conditions are properly defined to avoid unintentional Cartesian products.

Example:
```sql
-- Correct join syntax
SELECT orders.order_id, customers.customer_name
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;
```

### 3. **Avoid SELECT \***

Using `SELECT *` can be inefficient, especially if the table has many columns or if unnecessary columns are included.

Example:
```sql
-- Selecting specific columns
SELECT customer_name, order_date
FROM orders
INNER JOIN customers ON orders.customer_id = customers.customer_id;
```

### 4. **Limit the Result Set**

Limiting the number of rows returned can improve query performance, especially when dealing with large datasets.

Example:
```sql
-- Limiting results
SELECT * FROM orders LIMIT 100;
```

### 5. **Use EXISTS and IN Appropriately**

Choose `EXISTS` and `IN` based on the size of the subquery result set. `EXISTS` is generally faster for large datasets.

Example:
```sql
-- Using EXISTS
SELECT customer_id
FROM customers c
WHERE EXISTS (
    SELECT 1
    FROM orders o
    WHERE o.customer_id = c.customer_id
);
```

### 6. **Avoid Nested Queries**

Instead of using deeply nested subqueries, consider using `JOIN` operations or temporary tables, which can often be more efficient.

Example:
```sql
-- Using JOIN instead of nested query
SELECT customer_name, order_date
FROM customers
JOIN orders ON customers.customer_id = orders.customer_id;
```

### 7. **Aggregate Functions and GROUP BY**

Be mindful of how you use aggregate functions (`SUM`, `AVG`, `COUNT`, etc.) and `GROUP BY` clauses. These can affect query performance, especially on large datasets.

Example:
```sql
-- Using aggregate functions
SELECT department, AVG(salary) AS avg_salary
FROM employees
GROUP BY department;
```

### 8. **Avoid Functions in WHERE Clause**

Applying functions to columns in the `WHERE` clause can prevent indexes from being used efficiently. Consider precomputing or restructuring queries where possible.

Example:
```sql
-- Avoid using functions in WHERE clause
SELECT * FROM products WHERE UPPER(product_name) = 'PHONE';
```

### 9. **Use EXPLAIN to Analyze Queries**

Most database systems provide an `EXPLAIN` command that shows how the database will execute a query. This can help identify performance bottlenecks and suggest improvements.

Example (PostgreSQL):
```sql
-- Using EXPLAIN
EXPLAIN SELECT * FROM orders WHERE order_date >= '2023-01-01';
```

### 10. **Database Schema Design**

Good database design (normalization, appropriate data types, etc.) can improve query performance by reducing redundant data and optimizing storage.

Example:
```sql
-- Creating tables with proper normalization
CREATE TABLE customers (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(100),
    email VARCHAR(100)
);

CREATE TABLE orders (
    order_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE,
    FOREIGN KEY (customer_id) REFERENCES customers(customer_id)
);
```

---