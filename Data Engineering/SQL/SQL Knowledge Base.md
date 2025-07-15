### Basic SQL Questions

1. **What is SQL?**
   - **Answer:** SQL (Structured Query Language) is a standard programming language specifically designed for managing and manipulating relational databases.

2. **What is a primary key?**
   - **Answer:** A primary key is a column or a set of columns that uniquely identifies each row in a table. It cannot contain NULL values.

3. **What is a foreign key?**
   - **Answer:** A foreign key is a column or a set of columns in one table that uniquely identifies rows in another table. It establishes a link between the two tables.

4. **What is the difference between `INNER JOIN` and `LEFT JOIN`?**
   - **Answer:** `INNER JOIN` returns only the rows that have matching values in both tables. `LEFT JOIN` returns all rows from the left table and the matched rows from the right table; if no match is found, NULL values are returned for columns from the right table.

5. **What is a `SELECT` statement?**
   - **Answer:** A `SELECT` statement is used to query the database and retrieve data from one or more tables.

   **Example:**
   ```sql
   SELECT * FROM employees;
   ```

6. **How do you create a table in SQL?**
   - **Answer:**
   ```sql
   CREATE TABLE employees (
       id INT PRIMARY KEY,
       name VARCHAR(100),
       age INT,
       department VARCHAR(100)
   );
   ```

7. **What is the `WHERE` clause used for?**
   - **Answer:** The `WHERE` clause is used to filter records that meet a certain condition.

   **Example:**
   ```sql
   SELECT * FROM employees WHERE age > 30;
   ```

8. **Explain the `GROUP BY` clause.**
   - **Answer:** The `GROUP BY` clause groups rows that have the same values in specified columns into summary rows.

   **Example:**
   ```sql
   SELECT department, COUNT(*) FROM employees GROUP BY department;
   ```

9. **What is an `ORDER BY` clause?**
   - **Answer:** The `ORDER BY` clause is used to sort the result set in ascending or descending order.

   **Example:**
   ```sql
   SELECT * FROM employees ORDER BY age DESC;
   ```

10. **What is the purpose of the `HAVING` clause?**
    - **Answer:** The `HAVING` clause is used to filter groups based on aggregate functions, which the `WHERE` clause cannot do.

    **Example:**
    ```sql
    SELECT department, COUNT(*) FROM employees GROUP BY department HAVING COUNT(*) > 5;
    ```

### Intermediate SQL Questions

11. **Explain the concept of normalization.**
    - **Answer:** Normalization is the process of organizing data in a database to reduce redundancy and improve data integrity. It involves dividing large tables into smaller tables and defining relationships between them.

12. **What are the different types of normalization forms?**
    - **Answer:** The common normalization forms are:
      - 1NF (First Normal Form)
      - 2NF (Second Normal Form)
      - 3NF (Third Normal Form)
      - BCNF (Boyce-Codd Normal Form)
      - 4NF (Fourth Normal Form)
      - 5NF (Fifth Normal Form)

13. **How do you use the `JOIN` statement to combine rows from two or more tables?**
    - **Answer:**
    ```sql
    SELECT employees.name, departments.name 
    FROM employees 
    INNER JOIN departments ON employees.department_id = departments.id;
    ```

14. **What is a subquery and how is it used?**
    - **Answer:** A subquery is a query nested inside another query. It can be used in SELECT, INSERT, UPDATE, or DELETE statements.

    **Example:**
    ```sql
    SELECT name 
    FROM employees 
    WHERE department_id = (SELECT id FROM departments WHERE name = 'Sales');
    ```

15. **What is the difference between `UNION` and `UNION ALL`?**
    - **Answer:** `UNION` combines the results of two queries and removes duplicate rows, while `UNION ALL` combines the results of two queries and includes all duplicate rows.

16. **How do you insert data into a table?**
    - **Answer:**
    ```sql
    INSERT INTO employees (id, name, age, department) 
    VALUES (1, 'John Doe', 30, 'Engineering');
    ```

17. **How do you update existing records in a table?**
    - **Answer:**
    ```sql
    UPDATE employees 
    SET age = 31 
    WHERE id = 1;
    ```

18. **How do you delete records from a table?**
    - **Answer:**
    ```sql
    DELETE FROM employees 
    WHERE id = 1;
    ```

19. **What is a transaction in SQL?**
    - **Answer:** A transaction is a sequence of one or more SQL operations treated as a single unit of work. Transactions ensure data integrity by following the ACID properties (Atomicity, Consistency, Isolation, Durability).

20. **What are ACID properties?**
    - **Answer:**
      - **Atomicity:** Ensures that all operations within a transaction are completed; if not, the transaction is aborted.
      - **Consistency:** Ensures that the database remains in a consistent state before and after the transaction.
      - **Isolation:** Ensures that transactions are isolated from each other until they are completed.
      - **Durability:** Ensures that the results of a completed transaction are permanently stored in the database.

### Advanced SQL Questions

21. **What is a view in SQL?**
    - **Answer:** A view is a virtual table based on the result set of an SQL query. It can encapsulate complex queries and simplify data access.

    **Example:**
    ```sql
    CREATE VIEW employee_view AS 
    SELECT id, name, department 
    FROM employees 
    WHERE age > 30;
    ```

22. **How do you create an index in SQL?**
    - **Answer:**
    ```sql
    CREATE INDEX idx_department 
    ON employees (department);
    ```

23. **What is a stored procedure?**
    - **Answer:** A stored procedure is a precompiled collection of one or more SQL statements that can be executed as a unit. It can take parameters and return results.

    **Example:**
    ```sql
    CREATE PROCEDURE get_employee(IN emp_id INT)
    BEGIN
        SELECT * FROM employees WHERE id = emp_id;
    END;
    ```

24. **What is a trigger in SQL?**
    - **Answer:** A trigger is a special kind of stored procedure that automatically executes in response to certain events on a table or view, such as insertions, updates, or deletions.

    **Example:**
    ```sql
    CREATE TRIGGER update_timestamp 
    BEFORE UPDATE ON employees 
    FOR EACH ROW 
    SET NEW.updated_at = NOW();
    ```

25. **Explain the concept of indexing and its types.**
    - **Answer:** Indexing improves the speed of data retrieval operations on a table. Types of indexes include:
      - **Clustered Index:** Determines the physical order of data in a table.
      - **Non-Clustered Index:** Does not alter the physical order but creates a separate object within the table.

26. **How do you handle NULL values in SQL?**
    - **Answer:**
    ```sql
    SELECT COALESCE(column_name, 'default_value') 
    FROM table_name;
    ```

27. **What is a `CASE` statement in SQL?**
    - **Answer:** A `CASE` statement is used to create conditional logic in SQL queries.

    **Example:**
    ```sql
    SELECT name,
           CASE 
               WHEN age < 18 THEN 'Minor'
               WHEN age >= 18 AND age < 60 THEN 'Adult'
               ELSE 'Senior'
           END AS age_group
    FROM employees;
    ```

28. **What is the difference between `RANK`, `DENSE_RANK`, and `ROW_NUMBER`?**
    - **Answer:**
      - **RANK:** Assigns a rank to each row within the partition of a result set, with gaps in ranking.
      - **DENSE_RANK:** Assigns a rank to each row within the partition of a result set, without gaps in ranking.
      - **ROW_NUMBER:** Assigns a unique sequential integer to rows within the partition of a result set.

    **Example:**
    ```sql
    SELECT name, salary, 
           RANK() OVER (ORDER BY salary DESC) AS rank,
           DENSE_RANK() OVER (ORDER BY salary DESC) AS dense_rank,
           ROW_NUMBER() OVER (ORDER BY salary DESC) AS row_number
    FROM employees;
    ```

29. **What are window functions in SQL?**
    - **Answer:** Window functions perform calculations across a set of table rows that are related to the current row. They include functions like `RANK`, `DENSE_RANK`, `ROW_NUMBER`, `LEAD`, `LAG`, etc.

    **Example:**
    ```sql
    SELECT name, salary, 
           SUM(salary) OVER (PARTITION BY department) AS department_salary
    FROM employees;
    ```

30. **Explain the concept of partitioning in databases.**
    - **Answer:** Partitioning divides a large database table

### `LAG` Function

The `LAG` function provides access to a value in a previous row in the same result set. It allows you to look back a specific number of rows.

**Syntax:**
```sql
LAG(column_name, offset, default_value) OVER (PARTITION BY partition_column ORDER BY order_column)
```

- `column_name`: The column from which to retrieve the value.
- `offset`: The number of rows back from the current row (default is 1).
- `default_value`: A value to return if the specified number of rows back is not available (default is `NULL`).

**Example:**
```sql
-- Create the example table
CREATE TABLE sales (
    id INT,
    sales_date DATE,
    amount DECIMAL(10, 2)
);

-- Insert sample data
INSERT INTO sales (id, sales_date, amount) VALUES
(1, '2023-01-01', 100.00),
(2, '2023-01-02', 200.00),
(3, '2023-01-03', 150.00),
(4, '2023-01-04', 250.00),
(5, '2023-01-05', 300.00);

-- Query using LAG to find the previous day's sales amount
SELECT 
    id,
    sales_date,
    amount,
    LAG(amount, 1, 0) OVER (ORDER BY sales_date) AS previous_day_amount
FROM sales;
```

**Output:**
```
id | sales_date | amount | previous_day_amount
---+------------+--------+---------------------
1  | 2023-01-01 | 100.00 | 0.00
2  | 2023-01-02 | 200.00 | 100.00
3  | 2023-01-03 | 150.00 | 200.00
4  | 2023-01-04 | 250.00 | 150.00
5  | 2023-01-05 | 300.00 | 250.00
```

### `LEAD` Function

The `LEAD` function provides access to a value in a subsequent row in the same result set. It allows you to look forward a specific number of rows.

**Syntax:**
```sql
LEAD(column_name, offset, default_value) OVER (PARTITION BY partition_column ORDER BY order_column)
```

- `column_name`: The column from which to retrieve the value.
- `offset`: The number of rows forward from the current row (default is 1).
- `default_value`: A value to return if the specified number of rows forward is not available (default is `NULL`).

**Example:**
```sql
-- Query using LEAD to find the next day's sales amount
SELECT 
    id,
    sales_date,
    amount,
    LEAD(amount, 1, 0) OVER (ORDER BY sales_date) AS next_day_amount
FROM sales;
```

**Output:**
```
id | sales_date | amount | next_day_amount
---+------------+--------+----------------
1  | 2023-01-01 | 100.00 | 200.00
2  | 2023-01-02 | 200.00 | 150.00
3  | 2023-01-03 | 150.00 | 250.00
4  | 2023-01-04 | 250.00 | 300.00
5  | 2023-01-05 | 300.00 | 0.00
```

### Use Cases for `LEAD` and `LAG`

1. **Trend Analysis:** Analyze how a value changes over time by comparing it to the previous or next value.
2. **Running Totals:** Calculate running totals or cumulative sums by comparing current and past values.
3. **Gap Analysis:** Identify gaps or differences between consecutive rows.
4. **Time-Series Data:** Analyze time-series data by comparing values from one period to another.

### Additional Example with Partitioning

Suppose you want to calculate the difference in sales amount between consecutive days for each product in a sales table.

**Example:**
```sql
-- Create the example table with a product_id column
CREATE TABLE product_sales (
    id INT,
    product_id INT,
    sales_date DATE,
    amount DECIMAL(10, 2)
);

-- Insert sample data
INSERT INTO product_sales (id, product_id, sales_date, amount) VALUES
(1, 101, '2023-01-01', 100.00),
(2, 101, '2023-01-02', 200.00),
(3, 101, '2023-01-03', 150.00),
(4, 102, '2023-01-01', 250.00),
(5, 102, '2023-01-02', 300.00);

-- Query to calculate the sales difference using LAG
SELECT 
    id,
    product_id,
    sales_date,
    amount,
    LAG(amount, 1, 0) OVER (PARTITION BY product_id ORDER BY sales_date) AS previous_day_amount,
    amount - LAG(amount, 1, 0) OVER (PARTITION BY product_id ORDER BY sales_date) AS sales_diff
FROM product_sales;
```

**Output:**
```
id | product_id | sales_date | amount | previous_day_amount | sales_diff
---+------------+------------+--------+---------------------+-----------
1  | 101        | 2023-01-01 | 100.00 | 0.00                | 100.00
2  | 101        | 2023-01-02 | 200.00 | 100.00              | 100.00
3  | 101        | 2023-01-03 | 150.00 | 200.00              | -50.00
4  | 102        | 2023-01-01 | 250.00 | 0.00                | 250.00
5  | 102        | 2023-01-02 | 300.00 | 250.00              | 50.00
```

This query demonstrates how `LAG` can be used to calculate the difference between the sales amount of the current day and the previous day for each product.

---