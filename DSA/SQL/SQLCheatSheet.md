## 🧠 1) NULL Handling — Use Standard Functions

In PostgreSQL you **do NOT use `IFNULL()`** (from SQLite/MySQL) — you use:

### ✅ `COALESCE()`

Returns the first non-NULL value (ANSI-SQL standard).
✔ Better than `IFNULL`. Also accepts more than two arguments. ([Stack Overflow][1])

```sql
SELECT COALESCE(salary, 0) AS salary_or_zero
FROM employees;

SELECT COALESCE(primary_email, secondary_email, 'no_email') AS email;
```

### ✅ `NULLIF()`

Returns `NULL` if two expressions are equal — useful to avoid divide by zero or treat empty strings as NULL. ([learnsql.com][2])

```sql
SELECT value / NULLIF(divisor, 0) AS safe_ratio;

SELECT COALESCE(NULLIF(name, ''), 'unknown') AS name_clean;
```

📌 *Tip:* PostgreSQL treats `''` (empty string) as **different** from `NULL` (unlike Oracle). You often need `NULLIF()` to unify them. ([Reddit][3])

---

## 📅 2) Date & Time — Prefer Standard Patterns

### 🎯 Difference Between Dates

PostgreSQL lets you **subtract dates directly** (standard approach):

```sql
SELECT date2 - date1 AS days_diff;
```

This replaces vendor-specific functions like `DATEDIFF()`. ([learnsql.com][4])

### 📆 Add / Subtract Intervals

```sql
SELECT created_at + INTERVAL '7 days' AS next_week;
SELECT created_at - INTERVAL '1 month' AS last_month;
```

### 🕰 Extract Components

Use `EXTRACT()` or `DATE_PART()`:

````sql
SELECT EXTRACT(YEAR FROM hire_date) AS year_hired;
SELECT DATE_PART('month', timestamp_col) AS month_;
``` :contentReference[oaicite:4]{index=4}

### ⏱ Current Time/Date

```sql
SELECT CURRENT_DATE, CURRENT_TIME, CURRENT_TIMESTAMP;
````

---

## 🔤 3) String Processing — Standard & PostgreSQL Idioms

### 🔹 Concatenation

✔ Standard:

```sql
SELECT CONCAT(first_name, ' ', last_name);
```

✔ PostgreSQL alternative using `||`:

````sql
SELECT first_name || ' ' || last_name;
``` :contentReference[oaicite:5]{index=5}

### 🔹 Case Conversion

```sql
SELECT UPPER(name), LOWER(name);
````

### 🔹 Other Useful Text Functions

````sql
SELECT LENGTH(username);
SELECT SUBSTRING(username FROM 1 FOR 5);
SELECT TRIM(both ' ' FROM username);
SELECT INITCAP('hello world');  -- Capitalizes each word
``` :contentReference[oaicite:6]{index=6}

---

## 🧩 4) Conditional Logic — Clear and Standard

### `CASE` — The portable IF/ELSE

```sql
SELECT
  CASE WHEN score >= 90 THEN 'A'
       WHEN score >= 80 THEN 'B'
       ELSE 'C'
  END AS grade
FROM results;
````

### Combined with COALESCE

```sql
SELECT
  CASE WHEN COALESCE(discount, 0) > 0 THEN 'Has Discount'
       ELSE 'No Discount'
  END
FROM sales;
```

*Always prefer `CASE` and `COALESCE` over non-standard `IIF()`.* ([PostgreSQL][5])

---

## 🔎 5) Additional PostgreSQL-Specific Tips

### 🪄 Casting

PostgreSQL has multiple casting styles:

```sql
SELECT '2024-01-01'::date;
SELECT CAST('2024-01-01' AS date);
```

Both work — the `::` style is very common in PostgreSQL. ([Reddit][6])

### 🪡 SQL Standard Functions You *Should* Know

| Category      | PostgreSQL Function        |   |   |
| ------------- | -------------------------- | - | - |
| NULL handling | `COALESCE()`, `NULLIF()`   |   |   |
| Date parts    | `EXTRACT()`, `DATE_PART()` |   |   |
| Intervals     | `INTERVAL 'x unit'`        |   |   |
| Date math     | `date2 - date1`            |   |   |
| String concat | `CONCAT()` or `            |   | ` |
| String length | `LENGTH()`                 |   |   |
| Substring     | `SUBSTRING()`              |   |   |
| Case          | `CASE WHEN ... END`        |   |   |

---

## 🧯 Common Pitfalls (and How to Avoid Them)

### ❌ Using Functions Not In PostgreSQL

| Wrong (Other SQL)       | Right (PostgreSQL)        |
| ----------------------- | ------------------------- |
| `IFNULL(col, val)`      | `COALESCE(col, val)`      |
| `DATEDIFF(day, d1, d2)` | `d2 - d1`                 |
| `YEAR(date)`            | `EXTRACT(YEAR FROM date)` |

Refer to the cheat sheet logic rather than memorizing function names for each platform. ([Stack Overflow][1])

---

## 📌 Quick Interview Practice Checklist

✅ Always think ANSI SQL first
✅ Convert dialect-specific functions to PostgreSQL equivalents
✅ Use `COALESCE` for null defaults
✅ Do date math with `-` and `INTERVAL`
✅ Use `CASE` for conditional logic

[1]: https://stackoverflow.com/questions/43934155/sqlite-ifnull-in-postgres?utm_source=chatgpt.com "postgresql - sqlite IFNULL() in postgres - Stack Overflow"
[2]: https://learnsql.com/blog/postgresql-cheat-sheet/?utm_source=chatgpt.com "PostgreSQL Cheat Sheet | LearnSQL.com"
[3]: https://www.reddit.com/r/PostgreSQL/comments/r2iiom?utm_source=chatgpt.com "How to convert empty string ('') as NULL in postgres in config level."
[4]: https://learnsql.com/blog/postgresql-cheat-sheet/postgresql-cheat-sheet-ledger.pdf?utm_source=chatgpt.com "PostgreSQL Cheat Sheet"
[5]: https://www.postgresql.org/docs/16/functions-conditional.html?utm_source=chatgpt.com "PostgreSQL: Documentation: 16: 9.18. Conditional Expressions"
[6]: https://www.reddit.com/r/SQL/comments/1avjuek?utm_source=chatgpt.com "Snowflake vs PostgreSQL syntax differences"
