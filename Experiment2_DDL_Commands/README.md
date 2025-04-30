# Experiment 2: DDL Commands

## AIM
To study and implement DDL commands and different types of constraints.

## THEORY

### 1. CREATE
Used to create a new relation (table).

**Syntax:**
```sql
CREATE TABLE (
  field_1 data_type(size),
  field_2 data_type(size),
  ...
);
```
### 2. ALTER
Used to add, modify, drop, or rename fields in an existing relation.
(a) ADD
```sql
ALTER TABLE std ADD (Address CHAR(10));
```
(b) MODIFY
```sql
ALTER TABLE relation_name MODIFY (field_1 new_data_type(size));
```
(c) DROP
```sql
ALTER TABLE relation_name DROP COLUMN field_name;
```
(d) RENAME
```sql
ALTER TABLE relation_name RENAME COLUMN old_field_name TO new_field_name;
```
### 3. DROP TABLE
Used to permanently delete the structure and data of a table.
```sql
DROP TABLE relation_name;
```
### 4. RENAME
Used to rename an existing database object.
```sql
RENAME TABLE old_relation_name TO new_relation_name;
```
### CONSTRAINTS
Constraints are used to specify rules for the data in a table. If there is any violation between the constraint and the data action, the action is aborted by the constraint. It can be specified when the table is created (using CREATE TABLE) or after it is created (using ALTER TABLE).
### 1. NOT NULL
When a column is defined as NOT NULL, it becomes mandatory to enter a value in that column.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) NOT NULL
);
```
### 2. UNIQUE
Ensures that values in a column are unique.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) UNIQUE
);
```
### 3. CHECK
Specifies a condition that each row must satisfy.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) CHECK (logical_expression)
);
```
### 4. PRIMARY KEY
Used to uniquely identify each record in a table.
Properties:
Must contain unique values.
Cannot be null.
Should contain minimal fields.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size) PRIMARY KEY
);
```
### 5. FOREIGN KEY
Used to reference the primary key of another table.
Syntax:
```sql
CREATE TABLE Table_Name (
  column_name data_type(size),
  FOREIGN KEY (column_name) REFERENCES other_table(column)
);
```
### 6. DEFAULT
Used to insert a default value into a column if no value is specified.

Syntax:
```sql
CREATE TABLE Table_Name (
  col_name1 data_type,
  col_name2 data_type,
  col_name3 data_type DEFAULT 'default_value'
);
```

**Question 1**
--
Create a table named Customers with the following columns:  
CustomerID as INTEGER  
Name as TEXT  
Email as TEXT  
JoinDate as DATETIME  

```sql
CREATE TABLE Customers (
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME);
```

**Output:**

![image](https://github.com/user-attachments/assets/c45401da-2a26-4c91-9383-100295cca6f6)  

**Question 2**
---
Create a table named ProjectAssignments with the following constraints:  
AssignmentID as INTEGER should be the primary key.  
EmployeeID as INTEGER should be a foreign key referencing Employees(EmployeeID).  
ProjectID as INTEGER should be a foreign key referencing Projects(ProjectID).  
AssignmentDate as DATE should be NOT NULL.

```sql
CREATE TABLE ProjectAssignments (
AssignmentID INTEGER PRIMARY KEY,
EmployeeID INTEGER ,
ProjectID INTEGER ,
AssignmentDate DATE NOT NULL,
FOREIGN KEY (EmployeeID) REFERENCES Employees(EmployeeID),
FOREIGN KEY (ProjectID) REFERENCES Projects(ProjectID)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/91ed7c28-5711-458c-a3bb-da4ab962874f)  

**Question 3**
---
Insert the below data into the Student_details table, allowing the Subject and MARKS columns to take their default values.

| RollNo | Name          | Gender |
|--------|---------------|--------|
| 204    | Samuel Black  | M      |


Note: The Subject and MARKS columns will use their default values.

```sql
INSERT INTO Student_details (RollNo,Name,Gender) 
VALUES
(204,'Samuel Black','M');
```

**Output:**

![image](https://github.com/user-attachments/assets/2b2b6798-6131-4be9-b879-20b3f8bc3058)  

**Question 4**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
CREATE TABLE Shipments (
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER ,
OrderID INTEGER,
FOREIGN KEY (SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);

```

**Output:**

![image](https://github.com/user-attachments/assets/19db0cee-c4e4-4b66-971c-d774ad67f3cb)  

**Question 5**
---
Write a SQL Query  to add attribute Date_of_joining as Date and rename the attribute job_title as Designation in the table 'Employees'

```sql
ALTER TABLE Employees 
ADD COLUMN Date_of_joining Date;

ALTER TABLE Employees
RENAME COLUMN job_title TO Designation;
```

**Output:**

![image](https://github.com/user-attachments/assets/ecb04c0c-1a76-4ca9-b47c-11970855e3e9)  

**Question 6**
---
Create a new table named orders with the following specifications:
ord_id as TEXT with a length of 4.
item_id as TEXT.
ord_date as DATE.
ord_qty as INTEGER.
cost as INTEGER.
The primary key is a composite key consisting of item_id and ord_date.
ord_id and item_id should not accept NULL

```sql
CREATE TABLE orders(
ord_id TEXT CHECK(LENGTH(ord_id)=4) NOT NULL,
item_id TEXT NOT NULL,
ord_date DATE,
ord_qty INTEGER,
cost INTEGER,
PRIMARY KEY (item_id , ord_date)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/502a6689-cb68-4dd3-b668-671dcd61d383)  

**Question 7**
---
In the Books table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

| ISBN            | Title                      | Author         | Publisher  | Year |
|-----------------|----------------------------|----------------|------------|------|
| 978-1234567890  | Introduction to AI         | John Doe       |            |      |
| 978-9876543210  | Deep Learning              | Jane Doe       | TechPress  | 2022 |
| 978-1122334455  | Cybersecurity Essentials   | Alice Smith    |            | 2021 |


```sql
INSERT INTO Books (ISBN,Title,Author)
VALUES ('978-1234567890','Introduction to AI','John Doe');

INSERT INTO Books (ISBN,Title,Author,Publisher,Year)
VALUES ('978-9876543210','Deep Learning','Jane Doe','TechPress',2022);

INSERT INTO Books(ISBN,Title,Author,Year)
VALUES ('978-1122334455','Cybersecurity Essentials','Alice Smith',2021);
```

**Output:**

![image](https://github.com/user-attachments/assets/1bb0b052-9176-4260-964f-5446772dc8d6)  

**Question 8**
---
Write an SQL command can to add a column named email of type TEXT to the customers table

```sql
ALTER TABLE customers
ADD email TEXT;
```

**Output:**

![image](https://github.com/user-attachments/assets/733b1b13-4677-42d2-9a04-ad7cb5c82518)  

**Question 9**
---
Insert all products from Discontinued_products into Products.

Table attributes are ProductID, ProductName, Price, Stock

```sql
INSERT INTO Products (ProductID, ProductName, Price, Stock) 
SELECT ProductID, ProductName, Price, Stock FROM Discontinued_products;
```

**Output:**

![image](https://github.com/user-attachments/assets/53786f9d-8c6c-4698-b492-dd4152147b59)  

**Question 10**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.

```sql
CREATE TABLE Products(
ProductID INTEGER PRIMARY KEY,
ProductName TEXT UNIQUE NOT NULL,
Price REAL CHECK((Price)>0),
StockQuantity INTEGER CHECK((StockQuantity)>=0)
);
```

**Output:**

![image](https://github.com/user-attachments/assets/d31f1bb4-21ee-4a0f-82a4-6aad82946cc8)


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
