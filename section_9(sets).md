# 9. Using SET Operators
 -  Set operators are used to combine the results from different SELECT statements into one single result output
 -  Sometimes you want a single output from more than one table
 -  If you join the tables, the rows that meet the join criteria are returned, but what if a join will return a result set that doesn't meet your needs?
 -  This is where SET operators come in
 -  They can return the rows found in multiple SELECT statements, the rows that are in one table and not the other, or the rows common to both statements

```sql
-- The UNION operator returns all rows from both tables, after eliminating duplicates
SELECT a_id
FROM a
  UNION
SELECT b_id
FROM b;

--  The UNION ALL operator returns all rows from both tables, without eliminating duplicates
SELECT a_id
FROM a
  UNION ALL
SELECT b_id
FROM b;

-- The INTERSECT operator returns all rows common to both tables
SELECT a_id
FROM a
  INTERSECT
SELECT b_id
FROM b;

-- The MINUS operator returns all rows found in one table but not the other
-- This is A MINUS B, so all elements in A but not in B
SELECT a_id
FROM a
  MINUS
SELECT b_id
FROM b;
```
#### Set Operator Examples
 -  Sometimes if you are selecting rows from tables that do not have columns in common, you may have to create your own columns in order to match the number of columns in the queries
 -  The easiest way to do this is to include one or more NULL values in the select list
 -  Remember to give each one a suitable alias and matching data type
```sql
SELECT hire_date, employee_id, job_id
FROM employees
  UNION
SELECT TO_DATE(NULL),employee_id,
job_id
FROM job_history;

-- When using ORDER BY only use on one SELECT
SELECT hire_date, employee_id, job_id
FROM employees
  UNION
SELECT TO_DATE(NULL),employee_id, job_id
FROM job_history
ORDER BY employee_id;
```

#### There are a few rules to remember when using SET operators:
 1. The number of columns and the data types of the columns must be identical in all of the SELECT statements used in the query
 2.  The names of the columns need not be identical
 3. Column names in the output are taken from the column names in the first SELECT statement
