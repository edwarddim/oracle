# 8. Using Subqueries to Solve Queries

```sql
Single-Row Subquery:
SELECT first_name
FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);

Multi-Row Subquery:
SELECT first_name
FROM employees
WHERE department_id IN (
  SELECT department_id FROM departments WHERE location_id = 1700
);

Correlated Subquery:
SELECT e1.first_name
FROM employees e1
WHERE salary > (
  SELECT AVG(salary)
  FROM employees e2
  WHERE e1.department_id = e2.department_id
);

EXISTS:
SELECT department_name
FROM departments d
WHERE EXISTS (
  SELECT 1 FROM employees e WHERE e.department_id = d.department_id
);
```