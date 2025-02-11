### Notes:
Different date extractions with **MySQL**:

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

### Question3:

![image](https://github.com/user-attachments/assets/0cba33ae-0c35-4033-93af-bd4b42f4b5a6)

- Write a solution to find the users who have valid emails.

A valid e-mail has a prefix name and a domain where:

The prefix name is a string that may contain letters (upper or lower case), digits, underscore '_', period '.', and/or dash '-'. The prefix name must start with a letter.
The domain is '@leetcode.com'.
```go
SELECT *
FROM Users
WHERE mail REGEXP '^[a-zA-Z][a-zA-Z0-9_.-]*@leetcode[.]com$'
```
In the above code, It uses the regular expression to match 0-9 nums, a-z letters and it must include @leetcode[.]com. We didn't include this inside because a char [ ] means "match any one of the characters inside it". Also ^ represents starting of the email. $ represents ending

### Question4:
Write a solution to display the records with three or more rows with consecutive id's, and the number of people is greater than or equal to 100 for each.

![image](https://github.com/user-attachments/assets/d2059ca1-3dd9-4d09-980c-f82a1ef9fcfa)

```go
WITH stadium_rnk AS (SELECT *, id- rnk AS island
FROM (SELECT id, visit_date, people, RANK() OVER(ORDER BY id) AS rnk
FROM Stadium
WHERE people >= 100) AS t)

SELECT id, visit_date, people
FROM stadium_rnk 
WHERE island IN (SELECT island
FROM stadium_rnk
GROUP BY island
HAVING COUNT(*) >= 3)
ORDER BY visit_date
```
- Here we have ranked on id with count of people greater than or equal to 100. We group by the rank col so that we can get the rows with more than 3 ids.

