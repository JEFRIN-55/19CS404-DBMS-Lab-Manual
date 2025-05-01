# Experiment 4: Aggregate Functions, Group By and Having Clause

## AIM
To study and implement aggregate functions, GROUP BY, and HAVING clause with suitable examples.

## THEORY

### Aggregate Functions
These perform calculations on a set of values and return a single value.

- **MIN()** – Smallest value  
- **MAX()** – Largest value  
- **COUNT()** – Number of rows  
- **SUM()** – Total of values  
- **AVG()** – Average of values

**Syntax:**
```sql
SELECT AGG_FUNC(column_name) FROM table_name WHERE condition;
```
### GROUP BY
Groups records with the same values in specified columns.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name;
```
### HAVING
Filters the grouped records based on aggregate conditions.
**Syntax:**
```sql
SELECT column_name, AGG_FUNC(column_name)
FROM table_name
GROUP BY column_name
HAVING condition;
```

**Question 1**
--
How many medical records does each doctor have?
Sample table:MedicalRecords Table
![image (6)](https://github.com/user-attachments/assets/b2acc02d-4342-4cfa-bf94-951f79b956b5)

```sql
select DoctorID,
count(*) as TotalRecords from MedicalRecords 
group by DoctorID ;
```

**Output:**

![image](https://github.com/user-attachments/assets/bf623453-05a2-4ed5-940f-5bd4bfeda8b8)

**Question 2**
---
What is the most common diagnosis among patients?
Sample table:MedicalRecords Table
![image (6)](https://github.com/user-attachments/assets/e1cd5ca0-f32a-4bfa-b8f1-721a1040413f)

```sql
select Diagnosis,
count(*) as DiagnosisCount from MedicalRecords 
group by Diagnosis
order by DiagnosisCount DESC limit 1;
```

**Output:**

![image](https://github.com/user-attachments/assets/e0616024-de48-42a3-8469-672427bca55e)

**Question 3**
---
How many appointments are scheduled for each patient?
Sample table: Appointments Table
| Name                | Type      |
|---------------------|-----------|
| AppointmentID       | INTEGER   |
| PatientID           | INTEGER   |
| DoctorID            | INTEGER   |
| AppointmentDateTime | DATETIME  |
| Purpose             | TEXT      |
| Status              | TEXT      |

```sql
select PatientID,
count(*) as TotalAppointments from Appointments 
group by PatientID;
```

**Output:**

![image](https://github.com/user-attachments/assets/bc46b97a-3ccc-4297-b39f-7daaa9f305b4)

**Question 4**
---
Write a SQL query to find the maximum purchase amount.
Sample table: orders
| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|-------------|-------------|
| 70001  | 150.5     | 2012-10-05 | 3005        | 5002        |
| 70009  | 270.65    | 2012-09-10 | 3001        | 5005        |
| 70002  | 65.26     | 2012-10-05 | 3002        | 5001        |


```sql
select max(purch_amt) as MAXIMUM from orders ;
```

**Output:**

![image](https://github.com/user-attachments/assets/cae62290-7132-42b4-ab7c-794633ceb87f)

**Question 5**
---
Write a SQL query to find What is the age difference between the youngest and oldest employee in the company.
Table: employee
| name   | type    |
|--------|---------|
| id     | INTEGER |
| name   | TEXT    |
| age    | INTEGER |
| city   | TEXT    |
| income | INTEGER |

```sql
select max(age) - min(age) as age_difference from employee;
```

**Output:**

![image](https://github.com/user-attachments/assets/6f177a35-175f-42ee-b154-28de541a6c4a)

**Question 6**
---
Write a SQL query to find how many employees have an income greater than 50K?
Table: employee
| Name   | Type    |
|--------|---------|
| id     | INTEGER |
| name   | TEXT    |
| age    | INTEGER |
| city   | TEXT    |
| income | INTEGER |

```sql
select count(*) as employees_count from employee 
where income > 50000;
```

**Output:**

![image](https://github.com/user-attachments/assets/727c55d0-e5ff-46d6-bab2-345b8a696e28)

**Question 7**
---
Write a SQL query to find the youngest employee in the company?
Table: employee
| Name   | Type    |
|--------|---------|
| id     | INTEGER |
| name   | TEXT    |
| age    | INTEGER |
| city   | TEXT    |
| income | INTEGER |


```sql
select name as Employee_Name,min(age) as Age from employee;
```

**Output:**

![image](https://github.com/user-attachments/assets/5c75e99d-1472-453a-984a-ae5856d5297f)

**Question 8**
---
Write an SQL query that groups the customer data into 5-year age intervals, calculates the minimum salary for each group, and excludes groups where the minimum salary is not less than 2000.
Table: customer1
![unnamed](https://github.com/user-attachments/assets/ad339d4a-b6ff-43e6-b492-d2e77bc5552c)

```sql
select 
(age/5) * 5 || '-' || ((age/5)*5 +4) as age_group,
min(salary) as 'MIN(salary)'
from customer1
group by (age/5) 
having min(salary) < 2000;
```

**Output:**

![image](https://github.com/user-attachments/assets/e69e7a68-df95-4354-b24e-002fec148c9f)

**Question 9**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.
Sample table: customer1
![unnamed](https://github.com/user-attachments/assets/92695009-3199-4b2e-a162-e5c24ea8e455)

```sql
select address,
sum(salary) as 'SUM(salary)' from customer1
group by address
having sum(salary) > 2000;
```

**Output:**

![image](https://github.com/user-attachments/assets/76aa88be-4e23-413c-9e03-ad61bc283d51)

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the total work hours for each date, and excludes dates where the total work hour sum is not greater than 40.
Sample table: employee1
![unnamed](https://github.com/user-attachments/assets/24d67d96-19c0-469a-94eb-0b61ee884492)

```sql
select jdate,
sum(workhour) as 'SUM(workhour)' from employee1
group by jdate
having sum(workhour) > 40;
```

**Output:**

![image](https://github.com/user-attachments/assets/4c64d457-19d8-472f-a924-10445a04ccc5)


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
