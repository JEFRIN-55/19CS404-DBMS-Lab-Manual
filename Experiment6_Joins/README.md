# Experiment 6: Joins

## AIM
To study and implement different types of joins.

## THEORY

SQL Joins are used to combine records from two or more tables based on a related column.

### 1. INNER JOIN
Returns records with matching values in both tables.

**Syntax:**
```sql
SELECT columns
FROM table1
INNER JOIN table2
ON table1.column = table2.column;
```

### 2. LEFT JOIN
Returns all records from the left table, and matched records from the right.

**Syntax:**

```sql
SELECT columns
FROM table1
LEFT JOIN table2
ON table1.column = table2.column;
```
### 3. RIGHT JOIN
Returns all records from the right table, and matched records from the left.

**Syntax:**

```sql
SELECT columns
FROM table1
RIGHT JOIN table2
ON table1.column = table2.column;
```
### 4. FULL OUTER JOIN
Returns all records when there is a match in either left or right table.

**Syntax:**

```sql
SELECT columns
FROM table1
FULL OUTER JOIN table2
ON table1.column = table2.column;
```

**Question 1**
--
From the following tables write a SQL query to find salespeople who received commissions of more than 12 percent from the company. Return Customer Name, customer city, Salesman, commission.  

Sample table: customer
| customer_id | cust_name       | city        | grade | salesman_id |
|-------------|-----------------|-------------|-------|-------------|
| 3002        | Nick Rimando    | New York    | 100   | 5001        |
| 3007        | Brad Davis      | New York    | 200   | 5001        |
| 3005        | Graham Zusi     | California  | 200   | 5002        |
| 3008        | Julian Green    | London      | 300   | 5002        |
| 3004        | Fabian Johnson  | Paris       | 300   | 5006        |
| 3009        | Geoff Cameron   | Berlin      | 100   | 5003        |
| 3003        | Jozy Altidor    | Moscow      | 200   | 5007        |
| 3001        | Brad Guzan      | London      |       | 5005        |
Sample table: salesman
| salesman_id | name        | city      | commission |
|-------------|-------------|-----------|------------|
| 5001        | James Hoog  | New York  | 0.15       |
| 5002        | Nail Knite  | Paris     | 0.13       |
| 5005        | Pit Alex    | London    | 0.11       |
| 5006        | Mc Lyon     | Paris     | 0.14       |
| 5007        | Paul Adam   | Rome      | 0.13       |
| 5003        | Lauson Hen  | San Jose  | 0.12       |


```sql
select c.cust_name as 'Customer Name',c.city as 'city',s.name as 'Salesman',s.commission 
from customer c join salesman s on c.salesman_id = s.salesman_id 
where s.commission > 0.12;

```

**Output:**

![image](https://github.com/user-attachments/assets/c3edc9da-24f8-44f3-b92d-1b8c6903437f)

**Question 2**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![unnamed](https://github.com/user-attachments/assets/0fa80a74-f053-4b8c-b5d5-b21b228e2b00)
TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
![unnamed](https://github.com/user-attachments/assets/dae95cd3-8942-4093-987d-ab03f9e8282b)

```sql
select p.first_name as 'patient_name',t.result_id,t.patient_id,t.test_name,t.result,t.test_date 
from patients p inner join test_results t on p.patient_id = t.patient_id ;
```

**Output:**

![image](https://github.com/user-attachments/assets/932d7382-03cf-4d89-88f1-4810a2afdf82)

**Question 3**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.
PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![unnamed](https://github.com/user-attachments/assets/0fa80a74-f053-4b8c-b5d5-b21b228e2b00)
TEST_RESULT TABLES:

ATTRIBUTES - result_id, patient_id, test_name, result, test_date
![unnamed](https://github.com/user-attachments/assets/dae95cd3-8942-4093-987d-ab03f9e8282b)
```sql
select p.first_name as 'patient_name',t.result_id,t.patient_id,t.test_name,t.result,t.test_date 
from patients p inner join test_results t on p.patient_id = t.patient_id 
where t.test_name='Blood Pressure';
```

**Output:**

![image](https://github.com/user-attachments/assets/acc8521f-be62-44ca-b479-38b355c8d5de)

**Question 4**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with an order date later than '2012-08-17'.

CUSTOMER TABLE:
![unnamed](https://github.com/user-attachments/assets/13bf7547-dcb9-4d6c-bb38-40e4ec116937)
ORDERS TABLE:
![unnamed](https://github.com/user-attachments/assets/2f97ad25-df75-4159-ab25-6d34b7914f36)

```sql
select c.*
from customer c left join orders o on c.customer_id = o.customer_id
where o.ord_date > '2012-08-17';
```

**Output:**

![image](https://github.com/user-attachments/assets/f4f167a0-c365-40ef-b8c0-efd18787faf1)

**Question 5**
---
From the following tables write a SQL query to find the details of an order. Return ord_no, ord_date, purch_amt, Customer Name, grade, Salesman, commission. 

Sample table: orders
| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|--------------|--------------|
| 70001  | 150.5     | 2012-10-05 | 3005         | 5002         |
| 70009  | 270.65    | 2012-09-10 | 3001         | 5005         |
| 70002  | 65.26     | 2012-10-05 | 3002         | 5001         |
| 70004  | 110.5     | 2012-08-17 | 3009         | 5003         |
| 70007  | 948.5     | 2012-09-10 | 3005         | 5002         |
| 70005  | 2400.6    | 2012-07-27 | 3007         | 5001         |
| 70008  | 5760      | 2012-09-10 | 3002         | 5001         |
| 70010  | 1983.43   | 2012-10-10 | 3004         | 5006         |
| 70003  | 2480.4    | 2012-10-10 | 3009         | 5003         |
| 70012  | 250.45    | 2012-06-27 | 3008         | 5002         |
| 70011  | 75.29     | 2012-08-17 | 3003         | 5007         |
| 70013  | 3045.6    | 2012-04-25 | 3002         | 5001         |

Sample table: customer
| customer_id | cust_name       | city        | grade | salesman_id |
|-------------|------------------|-------------|--------|--------------|
| 3002        | Nick Rimando    | New York    | 100    | 5001         |
| 3007        | Brad Davis      | New York    | 200    | 5001         |
| 3005        | Graham Zusi     | California  | 200    | 5002         |
| 3008        | Julian Green    | London      | 300    | 5002         |
| 3004        | Fabian Johnson  | Paris       | 300    | 5006         |
| 3009        | Geoff Cameron   | Berlin      | 100    | 5003         |
| 3003        | Jozy Altidor    | Moscow      | 200    | 5007         |
| 3001        | Brad Guzan      | London      |        | 5005         |


Sample table: salesman
| salesman_id | name        | city      | commission |
|-------------|-------------|-----------|------------|
| 5001        | James Hoog  | New York  | 0.15       |
| 5002        | Nail Knite  | Paris     | 0.13       |
| 5005        | Pit Alex    | London    | 0.11       |
| 5006        | Mc Lyon     | Paris     | 0.14       |
| 5007        | Paul Adam   | Rome      | 0.13       |
| 5003        | Lauson Hen  | San Jose  | 0.12       |

```sql
select o.ord_no,o.ord_date,o.purch_amt,c.cust_name as 'Customer Name',c.grade,s.name as 'Salesman',s.commission
from orders o 
join customer c on o.customer_id = c.customer_id 
join salesman s on c.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/52383c0c-7dff-4d76-a32d-92de5150d7a7)

**Question 6**
---
Write the SQL query that achieves the selection of all columns from the "customer" table (aliased as "c"), with a left join on the "salesman_id" column and a condition filtering for salesmen with the name 'Mc Lyon'.

CUSTOMER TABLE:
![unnamed](https://github.com/user-attachments/assets/13bf7547-dcb9-4d6c-bb38-40e4ec116937)
ORDERS TABLE:
![unnamed](https://github.com/user-attachments/assets/2f97ad25-df75-4159-ab25-6d34b7914f36)

```sql
select c.* from customer c left join salesman s on c.salesman_id = s.salesman_id 
where s.name = 'Mc Lyon';
```

**Output:**

![image](https://github.com/user-attachments/assets/fbc53a9e-5899-4983-a1a4-1cf55631ef8c)

**Question 7**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 

Sample table: orders
| ord_no | purch_amt | ord_date   | customer_id | salesman_id |
|--------|-----------|------------|--------------|--------------|
| 70001  | 150.5     | 2012-10-05 | 3005         | 5002         |
| 70009  | 270.65    | 2012-09-10 | 3001         | 5005         |
| 70002  | 65.26     | 2012-10-05 | 3002         | 5001         |
| 70004  | 110.5     | 2012-08-17 | 3009         | 5003         |
| 70007  | 948.5     | 2012-09-10 | 3005         | 5002         |
| 70005  | 2400.6    | 2012-07-27 | 3007         | 5001         |
| 70008  | 5760      | 2012-09-10 | 3002         | 5001         |
| 70010  | 1983.43   | 2012-10-10 | 3004         | 5006         |
| 70003  | 2480.4    | 2012-10-10 | 3009         | 5003         |
| 70012  | 250.45    | 2012-06-27 | 3008         | 5002         |
| 70011  | 75.29     | 2012-08-17 | 3003         | 5007         |
| 70013  | 3045.6    | 2012-04-25 | 3002         | 5001         |

Sample table: customer
| customer_id | cust_name       | city        | grade | salesman_id |
|-------------|------------------|-------------|--------|--------------|
| 3002        | Nick Rimando    | New York    | 100    | 5001         |
| 3007        | Brad Davis      | New York    | 200    | 5001         |
| 3005        | Graham Zusi     | California  | 200    | 5002         |
| 3008        | Julian Green    | London      | 300    | 5002         |
| 3004        | Fabian Johnson  | Paris       | 300    | 5006         |
| 3009        | Geoff Cameron   | Berlin      | 100    | 5003         |
| 3003        | Jozy Altidor    | Moscow      | 200    | 5007         |
| 3001        | Brad Guzan      | London      |        | 5005         |


Sample table: salesman
| salesman_id | name        | city      | commission |
|-------------|-------------|-----------|------------|
| 5001        | James Hoog  | New York  | 0.15       |
| 5002        | Nail Knite  | Paris     | 0.13       |
| 5005        | Pit Alex    | London    | 0.11       |
| 5006        | Mc Lyon     | Paris     | 0.14       |
| 5007        | Paul Adam   | Rome      | 0.13       |
| 5003        | Lauson Hen  | San Jose  | 0.12       |



```sql
select o.ord_no,o.purch_amt,o.ord_date,c.cust_name,c.city as 'customer_city',c.grade,s.name as 'salesman_name',s.city as 'salesman_city',s.commission from orders o 
inner join customer c on o.customer_id = c.customer_id 
inner join salesman s on c.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/c91f23b0-7e9b-41dd-bc38-fb3cef11f149)

**Question 8**
---
From the following tables write a SQL query to locate those salespeople who do not live in the same city where their customers live and have received a commission of more than 12% from the company. Return Customer Name, customer city, Salesman, salesman city, commission
Sample table: customer
| customer_id | cust_name       | city        | grade | salesman_id |
|-------------|------------------|-------------|--------|--------------|
| 3002        | Nick Rimando    | New York    | 100    | 5001         |
| 3007        | Brad Davis      | New York    | 200    | 5001         |
| 3005        | Graham Zusi     | California  | 200    | 5002         |
| 3008        | Julian Green    | London      | 300    | 5002         |
| 3004        | Fabian Johnson  | Paris       | 300    | 5006         |
| 3009        | Geoff Cameron   | Berlin      | 100    | 5003         |
| 3003        | Jozy Altidor    | Moscow      | 200    | 5007         |
| 3001        | Brad Guzan      | London      |        | 5005         |


Sample table: salesman
| salesman_id | name        | city      | commission |
|-------------|-------------|-----------|------------|
| 5001        | James Hoog  | New York  | 0.15       |
| 5002        | Nail Knite  | Paris     | 0.13       |
| 5005        | Pit Alex    | London    | 0.11       |
| 5006        | Mc Lyon     | Paris     | 0.14       |
| 5007        | Paul Adam   | Rome      | 0.13       |
| 5003        | Lauson Hen  | San Jose  | 0.12       |

```sql
select c.cust_name as 'Customer Name',c.city,s.name as 'Salesman',s.city,s.commission 
from customer c join salesman s on c.salesman_id = s.salesman_id 
where c.city != s.city and commission > 0.12;
```

**Output:**

![image](https://github.com/user-attachments/assets/6dac85c3-bf65-45ac-b682-55f61c7ff3d7)

**Question 9**
---
Write the SQL query that achieves the selection of the date of birth from the "patients" table (aliased as "p") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id
![unnamed](https://github.com/user-attachments/assets/3c6aca40-78f4-4e3e-bdf3-ca8c743f3e81)
APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date
![unnamed](https://github.com/user-attachments/assets/0c3e4134-1e55-42b4-9f68-55976549fd01)

```sql
select p.date_of_birth,a.appointment_id,a.patient_id,a.doctor_id,a.appointment_date from patients p join appointments a on p.patient_id = a.patient_id 
where p.first_name = 'Alice';
```

**Output:**

![image](https://github.com/user-attachments/assets/6ff750f1-d2c2-4ac8-8a94-bdd3596e4263)

**Question 10**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.
Sample table: customer
| customer_id | cust_name       | city        | grade | salesman_id |
|-------------|------------------|-------------|--------|--------------|
| 3002        | Nick Rimando    | New York    | 100    | 5001         |
| 3007        | Brad Davis      | New York    | 200    | 5001         |
| 3005        | Graham Zusi     | California  | 200    | 5002         |
| 3008        | Julian Green    | London      | 300    | 5002         |
| 3004        | Fabian Johnson  | Paris       | 300    | 5006         |
| 3009        | Geoff Cameron   | Berlin      | 100    | 5003         |
| 3003        | Jozy Altidor    | Moscow      | 200    | 5007         |
| 3001        | Brad Guzan      | London      |        | 5005         |


Sample table: salesman
| salesman_id | name        | city      | commission |
|-------------|-------------|-----------|------------|
| 5001        | James Hoog  | New York  | 0.15       |
| 5002        | Nail Knite  | Paris     | 0.13       |
| 5005        | Pit Alex    | London    | 0.11       |
| 5006        | Mc Lyon     | Paris     | 0.14       |
| 5007        | Paul Adam   | Rome      | 0.13       |
| 5003        | Lauson Hen  | San Jose  | 0.12       |

```sql
select o.ord_no,o.purch_amt,c.cust_name,c.city from orders o join customer c on o.customer_id = c.customer_id
where o.purch_amt between 500 and 2000;
```

**Output:**

![image](https://github.com/user-attachments/assets/b979a7aa-39e9-4a61-bc56-f3adc8a649ca)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
