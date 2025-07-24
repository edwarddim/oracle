# Oracle 1Z0-071 - Section 5: Conversion Functions and Conditional Expressions

---

## 🔄 1. Conversion Functions

Oracle SQL often requires **explicit or implicit conversion** of data types.

### TO_CHAR (date/number → string)

```sql
SELECT TO_CHAR(SYSDATE, 'YYYY-MM-DD') AS today FROM dual;
SELECT TO_CHAR(12345.67, '99999.99') FROM dual;
```

**Common Date Format Models:**

| Format   | Meaning        |
|----------|----------------|
| 'YYYY'   | 4-digit year   |
| 'MM'     | Month (01–12)  |
| 'DD'     | Day (01–31)    |
| 'HH24'   | 24-hour format |
| 'MI'     | Minutes        |

---

### TO_DATE (string → date)

```sql
SELECT TO_DATE('2025-07-09', 'YYYY-MM-DD') FROM dual;
```

🔸 Format model must match the input string.

---

### TO_NUMBER (string → number)

```sql
SELECT TO_NUMBER('1,234.56', '9,999.99') FROM dual;
```

---

## ❓ 2. Handling NULLs with Conversion Functions

### NVL

```sql
SELECT NVL(commission_pct, 0) FROM employees;
```

### NVL2

```sql
SELECT NVL2(commission_pct, 'Has Commission', 'No Commission') FROM employees;
```

### NULLIF

```sql
SELECT NULLIF(salary, bonus) FROM employee_salaries;
```

### COALESCE

```sql
SELECT COALESCE(phone_work, phone_mobile, 'No Phone') FROM contacts;
```

---

## 🔀 3. Conditional Expressions

### Simple CASE

```sql
SELECT job_id,
       CASE job_id
           WHEN 'IT_PROG' THEN 'Programmer'
           WHEN 'HR_REP' THEN 'HR'
           ELSE 'Other'
       END AS job_title
FROM employees;
```

### Searched CASE

```sql
SELECT salary,
       CASE
           WHEN salary < 3000 THEN 'Low'
           WHEN salary BETWEEN 3000 AND 7000 THEN 'Medium'
           ELSE 'High'
       END AS salary_level
FROM employees;
```

---

### DECODE

```sql
SELECT DECODE(job_id,
              'IT_PROG', 'Programmer',
              'HR_REP', 'HR',
              'Other') AS job_title
FROM employees;
```

| CASE vs DECODE | CASE handles complex conditions; DECODE is simpler but only handles equality |

---

## 🧪 Common Exam Tips

| Concept          | Example               | Notes                      |
|------------------|------------------------|-----------------------------|
| Implicit Conversion | `'100' + 50`         | Converts string to number   |
| Explicit Conversion | `TO_CHAR(SYSDATE, 'DD-MON')` | Use in reports |
| NVL vs COALESCE  | `NVL(col, 'N/A')`      | COALESCE handles >2 values  |
| CASE vs DECODE   | `CASE WHEN ...`        | CASE is ANSI SQL            |

---

## ✅ Summary Table

| Function     | Purpose                                 |
|--------------|------------------------------------------|
| TO_CHAR      | Format number/date as string             |
| TO_DATE      | Parse string as date                     |
| TO_NUMBER    | Convert string to number                 |
| NVL          | Replace NULL with default                |
| NVL2         | Choose between 2 values based on NULL    |
| NULLIF       | Return NULL if 2 values are equal        |
| COALESCE     | Return first non-NULL value              |
| CASE         | Conditional logic with multiple options  |
| DECODE       | Oracle-specific equality condition       |
