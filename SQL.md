### Notes:
Different date extractions with MySQL:

- Extracting Date from a Datetime Column:
```go
SELECT DATE(order_date) FROM orders;
```
- Using YEAR(), MONTH(), DAY()
```
SELECT YEAR(order_date), MONTH(order_date), DAY(order_date) FROM orders;
```
- Using DATE_FORMAT() for Custom Formats
```
SELECT DATE_FORMAT(order_date, '%Y-%m-%d') FROM orders;
```
- Using STR_TO_DATE() for Parsing
```
SELECT STR_TO_DATE('2025-02-02', '%Y-%m-%d');
```
- Using EXTRACT()
```
SELECT EXTRACT(YEAR FROM order_date) FROM orders;
```

We can extract specific contraint from date using substr. Ex:
```
substr(trans_date, 1, 7) as month
2018-12-18
Output: 2018-12
```

#### Using Postgres for Date Extractions:
Extracting Date from a Timestamp Column
```
SELECT created_at::DATE FROM orders;
OR
SELECT DATE(created_at) FROM orders;
```
Using EXTRACT()
```
SELECT EXTRACT(YEAR FROM created_at) AS year FROM orders;
```
Using TO_CHAR() for Custom Formats
```
SELECT TO_CHAR(created_at, 'YYYY-MM-DD') FROM orders;
```
Using DATE_TRUNC() to Round to a Specific Date Part
```
SELECT DATE_TRUNC('day', created_at) FROM orders;
```

### Question1:
Table: Patients

Column Name  | Type

patient_id   : int 

patient_name : varchar 

conditions   : varchar 

patient_id is the primary key (column with unique values) for this table.

'conditions' contains 0 or more code separated by spaces. 

This table contains information of the patients in the hospital.

Write a solution to find the patient_id, patient_name, and conditions of the patients who have Type I Diabetes. Type I Diabetes always starts with DIAB1 prefix.


Solution:
```
SELECT patient_id , patient_name, conditions
FROM Patients
WHERE conditions like "DIAB1%" OR conditions like "% DIAB1%"
```

### Question2:

Table: Employee

Column Name | Type 

id          | int

salary      | int  

Write a solution to find the second highest distinct salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).

Solution:
```
SELECT max(salary) as SecondHighestSalary 

FROM (SELECT id, salary, DENSE_RANK() OVER(ORDER BY salary desc) AS ran

FROM Employee
) AS t
WHERE ran = 2
```
