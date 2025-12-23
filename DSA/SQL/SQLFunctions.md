# SQL Functions

## 1. Aggregate Functions
Used to perform calculations on multiple rows and return a single value.

- **COUNT()**: Counts the number of rows.
    - *Usage*: `SELECT COUNT(*) FROM employees;`
- **SUM()**: Adds up numeric values.
    - *Usage*: `SELECT SUM(salary) FROM employees;`
- **AVG()**: Calculates the average value.
    - *Usage*: `SELECT AVG(age) FROM users;`
- **MIN()**: Finds the minimum value.
    - *Usage*: `SELECT MIN(price) FROM products;`
- **MAX()**: Finds the maximum value.
    - *Usage*: `SELECT MAX(score) FROM results;`

#### HELPER CLAUSES:
- **FILTER**: The `FILTER` clause is utilized with aggregate functions to specify a condition that determines which rows are included in the calculation. It is written immediately after the aggregate function, enclosed in parentheses.
    - Syntax: 
        ``` SELECT aggregate_function(column) FILTER (WHERE condition) FROM table_name;```
    - Example Query:
        ``` SELECT COUNT(*) FILTER (WHERE status = 'active') AS active_count FROM users; ```

## 2. String Functions
Used to manipulate string data.

- **CONCAT()**: Concatenates two or more strings.
    - *Usage*: `SELECT CONCAT(first_name, ' ', last_name) FROM users;`
- **UPPER() / LOWER()**: Converts text to uppercase/lowercase.
    - *Usage*: `SELECT UPPER(name) FROM products;`
- **SUBSTRING()**: Extracts part of a string.
    - *Usage*: `SELECT SUBSTRING(name, 1, 3) FROM products;`
- **LENGTH()**: Returns the length of a string.
    - *Usage*: `SELECT LENGTH(description) FROM items;`
- **TRIM()**: Removes leading/trailing spaces.
    - *Usage*: `SELECT TRIM(name) FROM customers;`

## 3. Date and Time Functions
Used to manipulate date and time values.

- **NOW() / CURRENT_TIMESTAMP**: Returns current date and time.
    - *Usage*: `SELECT NOW();`
- **DATE()**: Extracts the date part.
    - *Usage*: `SELECT DATE(order_date) FROM orders;`
- **YEAR(), MONTH(), DAY()**: Extracts year, month, or day.
    - *Usage*: `SELECT YEAR(birthdate) FROM users;`
- **DATEDIFF()**: Calculates difference between two dates.
    - *Usage*: `SELECT DATEDIFF(end_date, start_date) FROM projects;`

## 4. Numeric Functions
Used to perform operations on numeric data.

- **ROUND()**: Rounds a number to specified decimals.
    - *Usage*: `SELECT ROUND(price, 2) FROM products;`
- **CEIL() / FLOOR()**: Rounds up/down to nearest integer.
    - *Usage*: `SELECT CEIL(rating) FROM reviews;`
- **ABS()**: Returns absolute value.
    - *Usage*: `SELECT ABS(balance) FROM accounts;`
- **MOD()**: Returns remainder of division.
    - *Usage*: `SELECT MOD(id, 2) FROM users;`

## 5. Conditional Functions
Used to return values based on conditions.

- **CASE**: Conditional logic in queries.
    - *Usage*: 
        1. Transform or Categorize Values
        ```sql
        SELECT name,
            CASE 
                WHEN score >=90 THEN 'Distinction'
                WHEN score >= 60 THEN 'Pass'
                ELSE 'Fail'
            END AS result
        FROM students;
        ```
        2. Handle NULL or Missing Data
        ```sql
        SELECT employee_name,
             CASE 
                WHEN bonus IS NULL THEN 0
                ELSE bonus 
            END AS bonus_final
        FROM payroll;
        ```
        3. Conditional Aggregates [IMPORTANT] (Compute sums, counts, etc., based on conditions):
        ```sql
        SELECT department,
            SUM(CASE WHEN status = 'active' THEN 1 ELSE 0 END) AS active_count
        FROM employees
        GROUP BY department;
        ```
        4. Custom Ordering
        ```sql
        SELECT *
        FROM products
        ORDER BY
        CASE
            WHEN category = 'Electronics' THEN 1
            WHEN category = 'Clothing' THEN 2
            ELSE 3
        END;
        ```
    - Important Points:
        - Put the most specific conditions first — SQL evaluates WHENs in order.
        - Always include an ELSE to avoid unintended NULLs, unless NULL is actually what you want.
        - Keep the results from all WHEN branches the same data type so the SQL engine doesn’t have to convert them internally.
        - Use indentation and spacing for readability — interviewers love neat SQL.

- **COALESCE()**: Returns first non-null value.
    - *Usage*: `SELECT COALESCE(phone, 'N/A') FROM contacts;`
- **NULLIF()**: Returns NULL if two expressions are equal.
    - *Usage*: `SELECT NULLIF(a, b) FROM table;`

---

> **Tip:** Use these functions in `SELECT`, `WHERE`, `ORDER BY`, and `GROUP BY` clauses as needed for data analysis and transformation.