# Apply Filters to SQL Queries

**Course:** Google Cybersecurity Professional Certificate — Course 4: Tools of the Trade: Linux and SQL

## Project Description

My organization needed help investigating potential security issues and identifying which employee machines required updates. Using the `log_in_attempts` and `employees` tables in the organization's database, I wrote SQL queries with the `AND`, `OR`, `NOT`, and `LIKE` filters to pull exactly the records needed for each task.

## Retrieve After-Hours Failed Login Attempts

A potential security incident occurred after business hours (after 18:00), so all failed login attempts after that time needed to be investigated.

```sql
SELECT *
FROM log_in_attempts
WHERE login_time > '18:00' AND success = FALSE;
```

- Started by selecting all columns from `log_in_attempts`.
- Used `AND` with two conditions so that **both** had to be true: `login_time > '18:00'` (after business hours) and `success = FALSE` (the login failed).
- **Result: 19 rows** matched both conditions.

## Retrieve Login Attempts on Specific Dates

A suspicious event occurred on 2022-05-09, so login activity on that date and the day before needed review.

```sql
SELECT *
FROM log_in_attempts
WHERE login_date = '2022-05-09' OR login_date = '2022-05-08';
```

- Selected all columns from `log_in_attempts`.
- Used `OR` so that **either** date would be returned — `login_date = '2022-05-09'` or `login_date = '2022-05-08'`.
- **Result: 75 rows.** Output screenshot shows the first and last portions of the result set.

## Retrieve Login Attempts Outside of Mexico

The suspicious login activity was believed not to have originated from Mexico, so all login attempts from outside Mexico needed to be pulled. The `country` column represents Mexico with two different values — `MEX` and `MEXICO` — so the filter needed to catch both.

```sql
SELECT *
FROM log_in_attempts
WHERE NOT country LIKE 'MEX%';
```

- Selected all columns from `log_in_attempts`.
- Used `NOT` to return everything **except** the matched condition.
- Used `LIKE` with the `%` wildcard so `'MEX%'` matches any value starting with "MEX" — covering both `MEX` and `MEXICO` in a single condition.
- **Result: 144 rows.** Output screenshot is cropped to the first and last portions.

## Retrieve Employees in Marketing

The team needed to update machines for employees in the Marketing department specifically within the East building.

```sql
SELECT *
FROM employees
WHERE department = 'Marketing' AND office LIKE 'East%';
```

- Selected all columns from `employees`.
- Used `AND` so **both** conditions had to be true: `department = 'Marketing'` and `office LIKE 'East%'`.
- Used `LIKE` with `%` for the office condition because the East building has multiple office numbers (`East-170`, `East-460`, etc.), not one fixed value.
- **Result: 7 rows.**

## Retrieve Employees in Finance or Sales

A different update was needed for employees in the Finance and Sales departments.

```sql
SELECT *
FROM employees
WHERE department = 'Finance' OR department = 'Sales';
```

- Selected all columns from `employees`.
- Used `OR` so that employees from **either** department would be returned, since the two departments' data wasn't yet combined.
- **Result: 71 rows.** Output screenshot shows the first and last portions.

## Retrieve All Employees Not in IT

The Information Technology department had already received an update; every other department still needed it.

```sql
SELECT *
FROM employees
WHERE NOT department = 'Information Technology';
```

- Selected all columns from `employees`.
- Used `NOT` to return every row **except** where `department = 'Information Technology'`.
- **Result: 161 rows.**

## Summary

When a database holds a large volume of records, filtering down to only the data relevant to a security task makes investigations and remediation faster and more accurate. Across both tables, I used the `AND`, `OR`, and `NOT` operators — combined with `LIKE` and the `%` wildcard for pattern matching — to isolate exactly the login attempts and employee records needed for each security decision.

---
📄 [View original document](Portfolio%20Activity%204.pdf)

*Part of [security-projects](../).*
