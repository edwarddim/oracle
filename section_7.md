# 7. Displaying Data from Multiple Tables Using Joins
 - CROSS JOINS return the two tables multiplied
```sql
-- Inner joins returns only matching rows
INNER JOIN:
SELECT e.first_name, d.department_name
FROM employees e
JOIN departments d ON (e.department_id = d.department_id);
```
```SQL
-- Outer joins all rows(matching and unmatched)
OUTER JOIN:
SELECT e.first_name, d.department_name
FROM employees e
LEFT JOIN departments d ON (e.department_id = d.department_id);
```

```SQL
USING Clause:
SELECT e.first_name, d.department_name
FROM employees e
JOIN departments d USING (department_id);

SELF JOIN:
SELECT worker.last_name, worker.manager_id, manager.last_name
AS "Manager name"
FROM employees worker JOIN employees manager
ON (worker.manager_id = manager.employee_id);

-- THREE TABLE JOIN:
SELECT last_name, department_name AS "Department", city
FROM employees JOIN departments USING (department_id)
JOIN locations USING (location_id);
```
 - OUTER JOIN and FULL OUTER JOIN is the same thing
![alt text](./imgs/joins_venn_diagram.png "Logo Title Text 1")

# 7.5 Hierarchical Queries (6-4)
 -  Hierarchical queries have their own new keywords: START WITH, CONNECT BY PRIOR, and LEVEL
 - START WITH identifies which row to use as the Root for the tree it i constructing, CONNECT BY PRIOR explains how to do the inter-row joins, and LEVEL specifies how
many branches deep the tree will traverse
```sql
SELECT employee_id, last_name, job_id, manager_id
FROM employees
START WITH employee_id = 100
CONNECT BY PRIOR employee_id = manager_id
```
 - LEVEL is a pseudo-column used with hierarchical queries, and it counts the number of steps it has taken from the root of the tree
```sql
SELECT LEVEL, last_name ||
' reports to ' ||
PRIOR last_name
AS "Walk Top Down"
FROM employees
START WITH last_name = 'King'
CONNECT BY PRIOR
employee_id = manager_id;
```