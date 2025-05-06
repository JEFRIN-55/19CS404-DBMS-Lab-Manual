# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is EQUAL TO $1500.
Sample table: CUSTOMERS
| ID | NAME     | AGE | ADDRESS    | SALARY |
|----|----------|-----|------------|--------|
| 1  | Ramesh   | 32  | Ahmedabad  | 2000   |
| 2  | Khilan   | 25  | Delhi      | 1500   |
| 3  | Kaushik  | 23  | Kota       | 2000   |
| 4  | Chaitali | 25  | Mumbai     | 6500   |
| 5  | Hardik   | 27  | Bhopal     | 8500   |
| 6  | Komal    | 22  | Hyderabad  | 4500   |
| 7  | Muffy    | 24  | Indore     | 10000  |

```sql
select * from customers 
where salary = 1500;
```

**Output:**

![image](https://github.com/user-attachments/assets/348e488c-ae96-4bbd-a6b1-da9d17303362)

**Question 2**
---
Write a SQL query to Identify customers whose city is different from the city of the customer with the highest ID
SAMPLE TABLE: customer
| Column Name | Data Type |
|-------------|-----------|
| id          | INTEGER   |
| name        | TEXT      |
| city        | TEXT      |
| email       | TEXT      |
| phone       | INTEGER   |

```sql
select * from customer 
where city not in (
select city from customer 
where id = (select max(id) from customer));
```

**Output:**

![image](https://github.com/user-attachments/assets/b5a74e95-3ce9-4d68-81ff-cc3ec17093a7)

**Question 3**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose AGE is LESS than $30

Sample table: CUSTOMERS
| ID | NAME     | AGE | ADDRESS    | SALARY |
|----|----------|-----|------------|--------|
| 1  | Ramesh   | 32  | Ahmedabad  | 2000   |
| 2  | Khilan   | 25  | Delhi      | 1500   |
| 3  | Kaushik  | 23  | Kota       | 2000   |
| 4  | Chaitali | 25  | Mumbai     | 6500   |
| 5  | Hardik   | 27  | Bhopal     | 8500   |
| 6  | Komal    | 22  | Hyderabad  | 4500   |
| 7  | Muffy    | 24  | Indore     | 10000  |

```sql
select * from customers where age < 30;
```

**Output:**

![image](https://github.com/user-attachments/assets/5ced5926-de33-41b3-bd09-67a120e24102)

**Question 4**
---
Write a SQL query to Retrieve the names and cities of customers who have the same city as customers with IDs 3 and 7

SAMPLE TABLE: customer
| Column Name | Data Type |
|-------------|-----------|
| id          | INTEGER   |
| name        | TEXT      |
| city        | TEXT      |
| email       | TEXT      |
| phone       | INTEGER   |

```sql
select name,city from customer where city in 
(select city from customer where id = 3 or id =  7);
```

**Output:**

![image](https://github.com/user-attachments/assets/df62511c-a401-4633-8d62-c58a4d391a94)

**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose salary is LESS than $2500.

Sample table: CUSTOMERS
| ID | NAME     | AGE | ADDRESS    | SALARY |
|----|----------|-----|------------|--------|
| 1  | Ramesh   | 32  | Ahmedabad  | 2000   |
| 2  | Khilan   | 25  | Delhi      | 1500   |
| 3  | Kaushik  | 23  | Kota       | 2000   |
| 4  | Chaitali | 25  | Mumbai     | 6500   |
| 5  | Hardik   | 27  | Bhopal     | 8500   |
| 6  | Komal    | 22  | Hyderabad  | 4500   |
| 7  | Muffy    | 24  | Indore     | 10000  |

```sql
select * from customers 
where salary < 2500;
```

**Output:**

![image](https://github.com/user-attachments/assets/c4369436-8124-4144-afc9-bed2bd72ad33)

**Question 6**
---
From the following tables write a SQL query to count the number of customers with grades above the average in New York City. Return grade and count.

customer table
| Column Name  | Data Type |
|--------------|-----------|
| customer_id  | int       |
| cust_name    | text      |
| city         | text      |
| grade        | int       |
| salesman_id  | int       |

```sql
select grade,COUNT(*)
from customer 
where grade > (
select avg(grade) from customer where city = 'New York')
group by grade ;
```

**Output:**

![image](https://github.com/user-attachments/assets/de7e4329-aee6-49ce-a0b9-79fa31068559)

**Question 7**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table
| Column Name | Data Type |
|-------------|-----------|
| id          | INTEGER   |
| name        | TEXT      |
| age         | INTEGER   |
| city        | TEXT      |
| income      | INTEGER   |

```sql
select * from employee 
where age < (
select avg(age) from employee where income > 250000 
);
```

**Output:**

![image](https://github.com/user-attachments/assets/45fd2db5-38bc-4ff2-ac87-640baa84d8c4)

**Question 8**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE
| Column Name | Data Type |
|-------------|-----------|
| ord_no      | int       |
| purch_amt   | real      |
| ord_date    | text      |
| customer_id | int       |
| salesman_id | int       |

```sql
select ord_no, purch_amt,strftime('%Y-%m-%d',ord_date) AS ord_date,customer_id, salesman_id
from orders 
where purch_amt > (
select avg(purch_amt) 
from orders 
where ord_date = '2012-10-10'
);
```

**Output:**

![image](https://github.com/user-attachments/assets/13db13e9-a2b8-4f15-89d4-8a003d1941c8)

**Question 9**
---
From the following tables write a SQL query to find all orders generated by New York-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table
| Column Name   | Data Type        |
|---------------|------------------|
| salesman_id   | numeric(5)       |
| name          | varchar(30)      |
| city          | varchar(15)      |
| commission    | decimal(5,2)     |


orders table 
| Column Name | Data Type |
|-------------|-----------|
| ord_no      | int       |
| purch_amt   | real      |
| ord_date    | text      |
| customer_id | int       |
| salesman_id | int       |

```sql
select * from orders 
where salesman_id in (
select salesman_id from salesman where city = 'New York'
);
```

**Output:**

![image](https://github.com/user-attachments/assets/f641b1b5-ed53-46a3-b198-ffdab3bc7dad)

**Question 10**
---
From the following tables write a SQL query to find all orders generated by London-based salespeople. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

salesman table
| Column Name   | Data Type        |
|---------------|------------------|
| salesman_id   | numeric(5)       |
| name          | varchar(30)      |
| city          | varchar(15)      |
| commission    | decimal(5,2)     |

orders table 
| Column Name | Data Type |
|-------------|-----------|
| ord_no      | int       |
| purch_amt   | real      |
| ord_date    | text      |
| customer_id | int       |
| salesman_id | int       |


```sql
select * from orders 
where salesman_id in (
select salesman_id from salesman where city = 'London'
);
```

**Output:**

![image](https://github.com/user-attachments/assets/8f7a2f3e-8623-4527-8724-8563d6edad78)


## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
