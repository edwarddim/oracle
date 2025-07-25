# Oracle 1Z0-071 Cheat Sheet (Sections 6–12)

# 10. Manipulating Data

```sql
INSERT:
INSERT INTO employees (employee_id, first_name) VALUES (300, 'John');

UPDATE:
UPDATE employees SET salary = salary * 1.1 WHERE department_id = 50;

DELETE:
DELETE FROM employees WHERE employee_id = 300;

Transaction Control:
COMMIT       - Save changes permanently
ROLLBACK     - Undo changes
SAVEPOINT sp1;
ROLLBACK TO sp1;
```

# 11. Using DDL Statements to Create and Manage Tables

```sql
CREATE TABLE:
CREATE TABLE departments (
  dept_id NUMBER PRIMARY KEY,
  name VARCHAR2(50) NOT NULL
);

ALTER TABLE:
ALTER TABLE departments ADD (location_id NUMBER);
ALTER TABLE departments MODIFY (name VARCHAR2(100));
ALTER TABLE departments DROP COLUMN location_id;

DROP TABLE:
DROP TABLE departments;

Constraints:
PRIMARY KEY, FOREIGN KEY, NOT NULL, UNIQUE, CHECK
ALTER TABLE employees ADD CONSTRAINT emp_dept_fk
FOREIGN KEY (department_id) REFERENCES departments(dept_id);
```

# 12. Creating Other Schema Objects

```sql
VIEW:
CREATE VIEW emp_view AS
SELECT first_name, salary FROM employees;

SEQUENCE:
CREATE SEQUENCE emp_seq START WITH 100 INCREMENT BY 1;

INDEX:
CREATE INDEX emp_name_idx ON employees (last_name);

SYNONYM:
CREATE SYNONYM emp FOR employees;
```

