## SQL Joins: Types, Use Cases, and Examples

SQL joins are used to combine rows from two or more tables based on a related column between them. Here are the main types of joins, their use cases, and examples:

### 1. INNER JOIN
**Use Case:**
Returns only the rows where there is a match in both tables. Use when you want data that exists in both tables.

**Example:**
```sql
SELECT employees.name, departments.dept_name
FROM employees
INNER JOIN departments ON employees.dept_id = departments.id;
```

### 2. LEFT JOIN (LEFT OUTER JOIN)
**Use Case:**
Returns all rows from the left table, and matched rows from the right table. Unmatched rows from the right table will have NULLs. Use when you want all records from the left table, even if there is no match in the right table.

**Example:**
```sql
SELECT customers.name, orders.order_date
FROM customers
LEFT JOIN orders ON customers.id = orders.customer_id;
```

### 3. RIGHT JOIN (RIGHT OUTER JOIN)
**Use Case:**
Returns all rows from the right table, and matched rows from the left table. Unmatched rows from the left table will have NULLs. Use when you want all records from the right table, even if there is no match in the left table.

**Example:**
```sql
SELECT orders.order_date, customers.name
FROM orders
RIGHT JOIN customers ON orders.customer_id = customers.id;
```

### 4. FULL JOIN (FULL OUTER JOIN)
**Use Case:**
Returns all rows when there is a match in one of the tables. Rows without a match in either table will have NULLs for missing columns. Use when you want all records from both tables, regardless of matches.

**Example:**
```sql
SELECT a.name, b.salary
FROM employees a
FULL OUTER JOIN payroll b ON a.id = b.emp_id;
```

### 5. CROSS JOIN
**Use Case:**
Returns the Cartesian product of both tables (every combination of rows). Use when you need all possible combinations, such as generating test data or pairing every item with every other item.

**Example:**
```sql
SELECT a.color, b.size
FROM colors a
CROSS JOIN sizes b;
```

---
**Summary Table:**

| Join Type      | Returns Rows From         | Use When You Need...                |
|---------------|--------------------------|-------------------------------------|
| INNER JOIN    | Both tables (matches)    | Only matching data                   |
| LEFT JOIN     | Left + matched right     | All left, even if no right match     |
| RIGHT JOIN    | Right + matched left     | All right, even if no left match     |
| FULL JOIN     | Both tables (all rows)   | All data, regardless of matches      |
| CROSS JOIN    | All combinations         | Every possible pair of rows          |

---
Choose the join type based on which data you want to include in your results and how you want to handle unmatched rows.


## Filtering Join Results

You can further filter the results of a join by:

### 1. Adding Conditions in the `ON` Clause

You can include additional matching criteria directly in the `ON` clause. This restricts which rows are considered a match during the join.

**Example:**
```sql
SELECT employees.name, departments.dept_name
FROM employees
INNER JOIN departments
    ON employees.dept_id = departments.id
    AND departments.active = 1;
```
This returns only employees in active departments.

### 2. Using a `WHERE` Clause

After the join, you can use a `WHERE` clause to filter the combined result set further.

**Example:**
```sql
SELECT customers.name, orders.order_date
FROM customers
LEFT JOIN orders ON customers.id = orders.customer_id
WHERE orders.order_date >= '2024-01-01';
```
This returns customers with orders placed in 2024 or later.

**Note:**  
- Conditions in the `ON` clause affect which rows are joined.
- Conditions in the `WHERE` clause filter the final result set after the join.
- For `OUTER JOIN`s, placing conditions in the `WHERE` clause may filter out unmatched rows (i.e., rows with `NULL` values), so use with care.