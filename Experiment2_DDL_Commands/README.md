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
Insert all students from Archived_students table into the Student_details table.

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           RollNo      INT           0                       1
1           Name        VARCHAR(100)  0                       0
2           Gender      VARCHAR(10)   0                       0
3           Subject     VARCHAR(50)   0                       0
4           MARKS       INT           0                       0


Test	Result
select * from student_details;
RollNo      Name           Gender      Subject     MARKS
----------  -------------  ----------  ----------  ----------
1           Alice Johnson  Female      Math        85
2           Bob Smith      Male        Science     90
3           Charlie Brown  Male        English     78
```sql
Insert into student_details(RollNo,Name,Gender,Subject,MARKS)
Select RollNo,Name,Gender,Subject,MARKS from Archived_students
```

**Output:**
<img width="818" height="274" alt="image" src="https://github.com/user-attachments/assets/9f435678-92b5-4a3c-a04d-945d9da3a2ca" />


**Question 2**
---
Create a table named Department with the following constraints:
DepartmentID as INTEGER should be the primary key.
DepartmentName as TEXT should be unique and not NULL.
Location as TEXT.
For example:

Test	Result
INSERT INTO Department (DepartmentID, DepartmentName, Location) VALUES (1, 'Human Resources', 'New York');
select * from Department;

```sql
Create table Department(
    DepartmentID INTEGER  primary key,
    DepartmentName  TEXT  unique not NULL,
    Location  TEXT
);
```

**Output:**

<img width="828" height="267" alt="image" src="https://github.com/user-attachments/assets/bc8484e2-2b00-4dcb-a946-002f4b360ac0" />


**Question 3**
---
Insert the below data into the Customers table, allowing the City and ZipCode columns to take their default values.

CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St      

Note: The City and ZipCode columns will use their default values.
 
For example:

Test	Result
SELECT CustomerID, Name, Address
FROM Customers;
CustomerID  Name          Address
----------  ------------  ----------
304         Peter Parker  Spider St


```sql
insert into Customers( CustomerID, Name, Address)
Values(304,"Peter Parker","Spider St")
```

**Output:**

<img width="1195" height="404" alt="image" src="https://github.com/user-attachments/assets/488a954c-a7b7-4919-acaa-87e95e38b2e5" />

**Question 4**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).
For example:

Test	Result
INSERT INTO Orders (OrderID, OrderDate, CustomerID) VALUES (1, '2024-08-01', 1);
INSERT INTO Invoices (InvoiceID, InvoiceDate, Amount, DueDate, OrderID) VALUES (1, '2024-08-01', 100.0, '2024-09-01', 1);
SELECT * FROM Invoices;

```sql
create table Invoices(
InvoiceID INTEGER primary key,
InvoiceDate DATE,
Amount REAL check(Amount>0),
DueDate DATE check(DueDate >InvoiceDate),
OrderID INTEGER,
FOREIGN KEY  (OrderID)  References Orders(OrderID));
```

**Output:**

<img width="1238" height="385" alt="image" src="https://github.com/user-attachments/assets/4bfaaaf5-655d-4499-bd4a-d5c912627558" />

**Question 5**
---
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300
For example:

Test	Result
SELECT Name, Category, Price, Stock FROM Products;

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300


```sql
INSERT INTO products(Name, Category, Price, Stock)
VALUES ("Smartphone","Electronics",800,150),
("Headphones","Accessories",200,300);
```

**Output:**

<img width="1262" height="428" alt="image" src="https://github.com/user-attachments/assets/2a31a14d-f84c-46a9-afd0-f751536a2c1c" />

**Question 6**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.
For example:

Test	Result
-- Attempt to insert a record with NULL FirstName
INSERT INTO Employees (EmployeeID, FirstName, LastName, Email, Salary, DepartmentID)
VALUES (1, NULL, 'Doe', 'john.doe@example.com', 50000, 1);
Error: NOT NULL constraint failed: Employees.FirstName

```sql
CREATE TABLE Employees(
EmployeeID Integer primary key,
FirstName text NOT NULL,
LastName text  NOT NULL,
Email text unique,
Salary number check(Salary>0),
DepartmentID INTEGER,
foreign key (DepartmentID) references Departments(DepartmentID));
```

**Output:**

<img width="1217" height="523" alt="image" src="https://github.com/user-attachments/assets/48c36355-1a71-4397-8046-e2d237fb8ce2" />

**Question 7**
---
Write an SQL query to add a new column email of type TEXT to the Student_details table, and ensure that this column cannot contain NULL values and make default value as 'Invalid'

 

 

For example:

Test	Result
INSERT INTO Student_details (RollNo, Name, Gender, Subject, email) 
VALUES (1, 'John Doe', 'M', 'Math', 'john@example.com');
select * from Student_details;
RollN  Name   Gen  Subject     email
-----  -----  ---  ----------  ----------------
1      John   M    Math        john@example.com

```sql
ALTER TABLE Student_details ADD COLUMN email TEXT NOT NULL DEFAULT 'Invalid';
```

**Output:**

<img width="1236" height="332" alt="image" src="https://github.com/user-attachments/assets/0f96d431-19b6-4699-a13d-eddeea96f5d7" />

**Question 8**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.
For example:

Test	Result
INSERT INTO Products (ProductID, ProductName, Price, StockQuantity) VALUES (1, 'Laptop', 999.99, 10);
select * from Products;
```sql
CREATE TABLE Products(
ProductID INTEGER primary key,
ProductName TEXT  unique not NULL,
Price REAL check(Price>0),
StockQuantity INTEGER check(StockQuantity>0)
);
```

**Output:**

<img width="1198" height="368" alt="image" src="https://github.com/user-attachments/assets/3d845afe-9c9b-49d7-9e8b-8a6107cf048d" />

**Question 9**
---
Create a table named Departments with the following columns:

DepartmentID as INTEGER
DepartmentName as TEXT
For example:

Test	Result
pragma table_info('Departments');
cid    name             type        notnull     dflt_value  pk
-----  ---------------  ----------  ----------  ----------  ----------
0      DepartmentID     INTEGER     0                       0
1      DepartmentName   TEXT        0                     
```sql
create table Departments(
    DepartmentID INTEGER,
DepartmentName TEXT
);
```

**Output:**

<img width="1236" height="440" alt="image" src="https://github.com/user-attachments/assets/b07f9abe-b019-4f78-b1b7-7144ff918907" />

**Question 10**
---
Write an SQL query to change the name of the column id to employee_id in the table employee.

 

 

 

 

For example:

Test	Result
pragma table_info('employee');
cid         name         type        notnull     dflt_value  pk
----------  -----------  ----------  ----------  ----------  ----------
0           employee_id  integer     0                       0
1           salary       number      0                       0

```sql
alter table employee Rename column id to employee_id;
```

**Output:**
<img width="1230" height="352" alt="image" src="https://github.com/user-attachments/assets/9dbc8f69-0e77-4238-8366-aa1125a101fa" />


## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
