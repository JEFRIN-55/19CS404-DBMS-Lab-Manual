# Experiment 3: DML Commands

## AIM
To study and implement DML (Data Manipulation Language) commands.

## THEORY

### 1. INSERT INTO
Used to add records into a relation.
These are three type of INSERT INTO queries which are as
A)Inserting a single record
**Syntax (Single Row):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES (value_1, value_2, ...);
```
**Syntax (Multiple Rows):**
```sql
INSERT INTO table_name (field_1, field_2, ...) VALUES
(value_1, value_2, ...),
(value_3, value_4, ...);
```
**Syntax (Insert from another table):**
```sql
INSERT INTO table_name SELECT * FROM other_table WHERE condition;
```
### 2. UPDATE
Used to modify records in a relation.
Syntax:
```sql
UPDATE table_name SET column1 = value1, column2 = value2 WHERE condition;
```
### 3. DELETE
Used to delete records from a relation.
**Syntax (All rows):**
```sql
DELETE FROM table_name;
```
**Syntax (Specific condition):**
```sql
DELETE FROM table_name WHERE condition;
```
### 4. SELECT
Used to retrieve records from a table.
**Syntax:**
```sql
SELECT column1, column2 FROM table_name WHERE condition;
```
**Question 1**
--
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

| Name           | Type              |
|----------------|-------------------|
| product_id     | INT               |
| product_name   | VARCHAR(100)      |
| category       | VARCHAR(50)       |
| cost_price     | DECIMAL(10,2)     |
| sell_price     | DECIMAL(10,2)     |
| reorder_lvl    | INT               |
| quantity       | INT               |
| supplier_id    | INT               |

```sql
update products 
set reorder_lvl = 40 
where category = 'Grocery';
```

**Output:**

![image](https://github.com/user-attachments/assets/010d38b5-c7a5-46d6-9459-7d4fdf43e77b)

**Question 2**
---
Write a SQL statement to change the EMAIL and COMMISSION_PCT column of the following EMPLOYEES table with 'not available' and 0.55 for those employees whose DEPARTMENT_ID is 110.

Employees Table

| Column Name     |
|-----------------|
| employee_id     |
| first_name      |
| last_name       |
| email           |
| phone_number    |
| hire_date       |
| job_id          |
| salary          |
| commission_pct  |
| manager_id      |
| department_id   |

```sql
update Employees
set EMAIL = 'not available',COMMISSION_PCT = 0.55
where department_id = 110;
```

**Output:**

![image](https://github.com/user-attachments/assets/35a4b9d6-c8d7-4ef2-9bd0-768246ed3f5c)

**Question 3**
---
Write a SQL statement to Update the reorder level to 20 where the quantity in stock is less than 10 and product category is 'Snacks' in the products table.
Products Table

| Column Name     |
|-----------------|
| product_id      |
| product_name    |
| category        |
| cost_price      |
| sell_price      |
| reorder_lvl     |
| quantity        |
| supplier_id     |

```sql
update Products 
set reorder_lvl = 20 
where category = 'Snacks' and quantity < 10;
```

**Output:**

![image](https://github.com/user-attachments/assets/ce872e9f-c740-4c0b-9163-57b8380af12d)

**Question 4**
---
Write a SQL statement to increase the salary of employees under the department 40, 90 and 110 according to the company rules.
Salary will be increased by 25% for the department 40, 15% for department 90 and 10% for the department 110 and the rest of the departments will remain same.
Employees Table

| Column Name     |
|-----------------|
| employee_id     |
| first_name      |
| last_name       |
| email           |
| phone_number    |
| hire_date       |
| job_id          |
| salary          |
| commission_pct  |
| manager_id      |
| department_id   |

```sql
update Employees
set salary = 
case 
when department_id = 40 then round(salary*1.25)
when department_id = 90 then round(salary*1.15)
when department_id = 110 then round(salary*1.10)
else salary
end;
```

**Output:**

![image](https://github.com/user-attachments/assets/7abbf19c-a830-4366-8620-0d84599ba27e)

**Question 5**
---
Write a SQL statement to Double the salary for employees in department 20 who have a job_id ending with 'MAN'
| Column Name     |
|-----------------|
| employee_id     |
| first_name      |
| last_name       |
| email           |
| phone_number    |
| hire_date       |
| job_id          |
| salary          |
| commission_pct  |
| manager_id      |
| department_id   |

```sql
update Employees
set salary = salary * 2
where job_id like '%MAN';
```

**Output:**

![image](https://github.com/user-attachments/assets/07f693c3-9bcb-4a40-9eb5-48b1e0c86d7a)

**Question 6**
---
Write a SQL query to Delete a Specific Surgery whose ID is 3 or surgeon ID is 4.
Sample table: Surgeries
![image (1)](https://github.com/user-attachments/assets/7116f0f9-b5d6-4985-a05a-b183fd892bba)

```sql
delete from Surgeries 
where surgeon_id = 4 or surgery_id = 3;
```

**Output:**

![image](https://github.com/user-attachments/assets/d80f1eef-261c-471b-bdcc-e5ef8d553f54)

**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.
Sample table: Customer
| CUST_CODE | CUST_NAME | CUST_CITY | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT | OUTSTANDING_AMT | PHONE_NO | AGENT_CODE |
|-----------|-----------|-----------|--------------|--------------|-------|-------------|-------------|-------------|-----------------|----------|------------|
| C00013    | Holmes    | London    | London       | UK           | 2     | 6000.00     | 5000.00     | 7000.00     | 4000.00         | BBBBBBB  | A003       |
| C00001    | Micheal   | New York  | New York     | USA          | 2     | 3000.00     | 5000.00     | 2000.00     | 6000.00         | CCCCCCC  | A008       |
| C00020    | Albert    | New York  | New York     | USA          | 3     | 5000.00     | 7000.00     | 6000.00     | 6000.00         | BBBBSBB  | A008       |

```sql
delete from customer 
where grade%2 != 0;
```

**Output:**

![image](https://github.com/user-attachments/assets/4bd54fd2-4068-405b-93f4-cdb015074597)

**Question 8**
---
Write a SQL query to Delete All Doctors with a NULL Last Name
Sample table: Doctors
attributes : doctor_id, first_name, last_name, specialization

```sql
delete from doctors 
where last_name is null;
```

**Output:**

![image](https://github.com/user-attachments/assets/a57325f6-0fde-4ce0-ae8c-2ee349eb1a69)

**Question 9**
---
Write a query to fetch all the records from the EmployeeInfo table ordered by EmpLname in descending order and Department in the ascending order.
| EmpID | EmpFname | EmpLname | Department | Project | Address          | DOB         | Gender |
|-------|----------|----------|------------|---------|------------------|-------------|--------|
| 1     | Sanjay   | Mehra    | HR         | P1      | Hyderabad(HYD)   | 01/12/1976  | M      |
| 2     | Ananya   | Mishra   | Admin      | P2      | Delhi(DEL)       | 02/05/1968  | F      |

```sql
select * from EmployeeInfo 
order by EmpFname DESC, Department ASC;
```

**Output:**

![image](https://github.com/user-attachments/assets/bd7859d9-ca0c-4464-91a1-70f0b326f869)

**Question 10**
---
Write a SQL statement to display name and commission of first 5 salesmen.
table info
salesman(name,commission) 

```sql
select name,commission 
from salesman 
limit 5;
```

**Output:**

![image](https://github.com/user-attachments/assets/429ecfd8-583a-4548-b48d-601350146e39)

## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
