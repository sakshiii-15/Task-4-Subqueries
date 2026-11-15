# Task 4 — Subqueries and Nested Queries

A hands-on SQL project demonstrating how to use **subqueries** (nested queries) to solve complex, multi-step data problems. This task covers scalar subqueries, multi-row subqueries, correlated subqueries, and derived tables in `SELECT`, `WHERE`, and `FROM` clauses.

Built as part of a **SQL Developer Internship** task to master nested logic and data filtering.

---

## 🎯 Objective

Use subqueries in `SELECT`, `WHERE`, and `FROM` to retrieve data that depends on the result of another query. Learn the difference between standard subqueries and correlated subqueries.

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **DB Browser for SQLite** | Run queries locally|
| **GitHub** | Version control & submission |

---

## 🗄️ Database Schema

**Database name:** `task4`

Two tables are used to demonstrate subqueries:

### 1. `employees`
| Column | Type | Description |
|--------|------|-------------|
| `emp_id` | INTEGER (PK) | Unique employee ID |
| `emp_name` | VARCHAR(50) | Employee name |
| `department` | VARCHAR(30) | Department name (Sales, Marketing, IT, HR) |
| `salary` | DECIMAL(10,2) | Employee salary |

### 2. `sales`
| Column | Type | Description |
|--------|------|-------------|
| `sale_id` | INTEGER (PK) | Unique sale ID |
| `emp_id` | INTEGER (FK) | References `employees.emp_id` (Nullable) |
| `product` | VARCHAR(40) | Product sold |
| `amount` | DECIMAL(10,2) | Total sale amount |


---

## 💻 Sample Queries (Highlights)

### 1. Scalar Subquery (Single value)
```sql
SELECT emp_name, salary 
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```

### 2. Multi-row Subquery with `IN`
```sql
SELECT emp_name 
FROM employees
WHERE emp_id IN (SELECT emp_id FROM sales);
```

### 3. `EXISTS` Subquery
```sql
SELECT e.emp_name 
FROM employees e
WHERE EXISTS (SELECT 1 FROM sales s WHERE s.emp_id = e.emp_id);
```

### 4. Derived Table (Subquery in `FROM`)
```sql
SELECT * 
FROM (
    SELECT emp_name, salary 
    FROM employees 
    ORDER BY salary DESC
) AS top_earners
LIMIT 3;
```

### 5. Correlated Subquery (Row-by-row logic)
```sql
SELECT e1.emp_name, e1.department, e1.salary
FROM employees e1
WHERE salary = (
    SELECT MAX(salary) 
    FROM employees e2 
    WHERE e2.department = e1.department
);
```
---

## 🎓 Learning Outcomes

By completing this task, I gained hands-on experience with:

- **Scalar Subqueries** — returning a single value to use in `WHERE` or `SELECT`.
- **Multi-row Subqueries** — using `IN` and `NOT IN` to compare against a list of values.
- **Correlated Subqueries** — subqueries that reference the outer query and execute row-by-row (e.g., finding the highest earner *per department*).
- **Subqueries in `FROM`** — creating temporary derived tables to perform complex aggregations.
- **`EXISTS` vs `IN`** — understanding how `EXISTS` acts as a boolean check and can be more efficient.
- **NULL handling** — avoiding the `NOT IN` + `NULL` trap.
- **Nested logic** — breaking down complex business questions into readable, step-by-step SQL.

---

## ✅ Conclusion

I learned that: Subqueries act as **building blocks**, allowing the output of one query to feed into another.


