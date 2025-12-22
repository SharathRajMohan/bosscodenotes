# SQL Interview Best Practices & Patterns

## 1. General Approach

- **Understand the Problem:** Read the question carefully. Clarify requirements and expected output.
- **Break Down Complex Queries:** Divide into manageable subqueries or CTEs.
- **Start Simple:** Build the query incrementally, testing each step.

## 2. Patterns to Remember

### a. Filtering Data

- Use `WHERE` for row-level filtering.
- Use `HAVING` for aggregate filtering after `GROUP BY`.

### b. Aggregations

- Common functions: `COUNT`, `SUM`, `AVG`, `MIN`, `MAX`.
- Use `GROUP BY` to aggregate by columns.
- Combine with `CASE WHEN` for conditional aggregation.

### c. Joins

- **INNER JOIN:** Only matching rows.
- **LEFT JOIN:** All rows from left, matched from right.
- **RIGHT JOIN:** All rows from right, matched from left.
- **FULL OUTER JOIN:** All rows from both tables.
- **Self Join:** Join a table to itself for hierarchical data.

### d. Window Functions

- Use `ROW_NUMBER()`, `RANK()`, `DENSE_RANK()`, `LEAD()`, `LAG()` for advanced analytics.
- Partition data with `PARTITION BY`.
- Order within partitions using `ORDER BY`.

### e. Subqueries & CTEs

- Use subqueries for intermediate results.
- Use CTEs (`WITH` clause) for readability and reuse.

### f. Data Transformation

- Use `CASE WHEN` for conditional logic.
- Use string/date functions for formatting and extraction.

## 3. Concepts to Remember

- **NULL Handling:** Use `IS NULL`, `IS NOT NULL`, and `COALESCE`.
- **Indexes:** Know how they affect performance.
- **Normalization/Denormalization:** Understand table design implications.
- **Set Operations:** Use `UNION`, `INTERSECT`, `EXCEPT` for combining results.
- **Apply mathematical functions only after making sure the type is numeric:** Use CAST or `::` to cast the value to the desired data type before applying type specific functions.
Ex.

```ROUND(AVG(a2.timestamp - a1.timestamp)::numeric, 3) AS processing_time```
## 4. Optimization Tips

- Avoid SELECT *; specify columns.
- Use indexes wisely.
- Minimize subqueries and nested SELECTs.
- Profile queries with `EXPLAIN` or similar tools.
- Use Joins over subqueries in order to improve performance.

## 5. Common Interview Patterns

- **Top N per Group:** Use window functions or correlated subqueries.
- **Gaps and Islands:** Identify sequences or missing data.
- **Pivot/Unpivot:** Transform rows to columns and vice versa.
- **Duplicates:** Find with `GROUP BY` and `HAVING COUNT(*) > 1`.

## 6. Final Checklist

- Validate output against sample data.
- Check for edge cases (NULLs, empty sets).
- Comment complex logic for clarity.
- Optimize for readability and performance.

---

**Reference this guide for structured, efficient SQL problem solving in interviews.**