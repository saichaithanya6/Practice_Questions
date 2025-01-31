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
SELECT patient_id , patient_name, conditions
FROM Patients
WHERE conditions like "DIAB1%" OR conditions like "% DIAB1%"


### Question2:
Table: Employee
Column Name | Type 
id          | int  
salary      | int  

Write a solution to find the second highest distinct salary from the Employee table. If there is no second highest salary, return null (return None in Pandas).

Solution:
SELECT max(salary) as SecondHighestSalary 
FROM (SELECT id, salary, DENSE_RANK() OVER(ORDER BY salary desc) AS ran
FROM Employee
) AS t
WHERE ran = 2
