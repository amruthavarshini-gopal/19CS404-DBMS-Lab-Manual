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
Create a table named jobs including columns job_id, job_title, min_salary and max_salary, and make sure that, the default value for job_title is blank and min_salary is 8000 and max_salary is NULL will be entered automatically at the time of insertion if no value assigned for the specified columns.

```sql
create table jobs(
job_id int,
job_title default(null),
min_salary default(8000),
max_salary default(null)
)
```

**Output:**

<img width="1068" height="193" alt="Screenshot 2025-09-29 132042" src="https://github.com/user-attachments/assets/79192b39-b7bb-4ac8-bce9-1e3d19828791" />


**Question 2**
---
Write an SQL query to add two new columns, department_id and manager_id, to the table employee with datatype of INTEGER. The manager_id column should have a default value of NULL.

```sql
alter table employee add column department_id INTEGER;
alter table employee add column manager_id INTEGER default(NULL);
```

**Output:**

<img width="1256" height="290" alt="Screenshot 2025-09-29 132243" src="https://github.com/user-attachments/assets/f9c02d3b-d780-4d87-a800-410bbbc8e838" />


**Question 3**
---
Create a table named Products with the following constraints:
ProductID as INTEGER should be the primary key.
ProductName as TEXT should be unique and not NULL.
Price as REAL should be greater than 0.
StockQuantity as INTEGER should be non-negative.

```sql
create table Products(
ProductID INTEGER primary key,
ProductName TEXT UNIQUE not null,
Price REAL CHECK(Price>0),
StockQuantity INTEGER CHECK(StockQuantity>=0)
)
```

**Output:**

<img width="1206" height="354" alt="Screenshot 2025-09-29 132443" src="https://github.com/user-attachments/assets/b96c6af6-0ef3-4284-ac4d-fc025ad803c2" />

**Question 4**
---
Create a table named Employees with the following constraints:

EmployeeID should be the primary key.
FirstName and LastName should be NOT NULL.
Email should be unique.
Salary should be greater than 0.
DepartmentID should be a foreign key referencing the Departments table.

```sql
create table Employees(
EmployeeID int primary key,
FirstName varchar(100) not null,
LastName varchar(100) not null,
Email text unique,
Salary real CHECK(Salary>0),
DepartmentID int,
foreign key(DepartmentID) references Departments(DepartmentID)
)
```

**Output:**

<img width="1292" height="374" alt="Screenshot 2025-09-29 132655" src="https://github.com/user-attachments/assets/7aa980aa-b28f-468b-9aed-ce4f43eb6f7a" />


**Question 5**
---
Insert the below data into the Books table, allowing the Publisher and Year columns to take their default values.

ISBN             Title                 Author
---------------  --------------------  ---------------

978-6655443321   Big Data Analytics    Karen Adams

Note: The Publisher and Year columns will use their default values.

```sql
insert into Books(ISBN,Title,Author) values("978-6655443321","Big Data Analytics","Karen Adams");
```

**Output:**

<img width="1247" height="349" alt="Screenshot 2025-09-29 132851" src="https://github.com/user-attachments/assets/524b598f-a259-44e1-b08e-893801c7f759" />

**Question 6**
---
Write a SQL Query  to add attribute ISBN as varchar(30) and domain_dept as varchar(30) in the table 'books'

```sql
alter table books add column ISBN varchar(30);
alter table books add column domain_dept varchar(30);
```

**Output:**

<img width="1287" height="375" alt="Screenshot 2025-09-29 133015" src="https://github.com/user-attachments/assets/f90bb6b5-e86e-497a-9c93-a0797ec56f69" />


**Question 7**
---
Insert all employees from Former_employees into Employee

Table attributes are EmployeeID, Name, Department, Salary
```sql
insert into Employee(EmployeeID,Name,Department,Salary)
select EmployeeID,Name,Department,Salary from Former_employees;
```

**Output:**

<img width="1213" height="353" alt="Screenshot 2025-09-29 133132" src="https://github.com/user-attachments/assets/8be2ce4a-7236-47b1-9cdc-267398c55a56" />


**Question 8**
---
In the Products table, insert a record where some fields are NULL, another record where all fields are filled without any NULL values, and a third record where some fields are filled, and others are left as NULL.

ProductID   Name              Category    Price       Stock
----------  ---------------   ----------  ----------  ----------
106         Fitness Tracker   Wearables

107         Laptop            Electronics  999.99      50

108         Wireless Earbuds  Accessories              100
 
```sql
insert into Products(ProductID,Name,Category) values(106,"Fitness Tracker","Wearables");
insert into Products(ProductID,Name,Category,Price,Stock) values(107,"Laptop","Electronic",999.99,50);
insert into Products(ProductID,Name,Category,Stock) values(108,"Wireless Earbud","Accessorie",100);
```

**Output:**



**Question 9**
---
Create a table named Customers with the following columns:

CustomerID as INTEGER
Name as TEXT
Email as TEXT
JoinDate as DATETIME

```sql
create table Customers(
CustomerID INTEGER,
Name TEXT,
Email TEXT,
JoinDate DATETIME
)
```

**Output:**

<img width="1297" height="345" alt="Screenshot 2025-09-29 133410" src="https://github.com/user-attachments/assets/c97d68e1-1577-4798-a642-01256bb30b59" />


**Question 10**
---
Create a table named Shipments with the following constraints:
ShipmentID as INTEGER should be the primary key.
ShipmentDate as DATE.
SupplierID as INTEGER should be a foreign key referencing Suppliers(SupplierID).
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

```sql
create table Shipments(
ShipmentID INTEGER PRIMARY KEY,
ShipmentDate DATE,
SupplierID INTEGER,
OrderID INTEGER,
FOREIGN KEY(SupplierID) REFERENCES Suppliers(SupplierID),
FOREIGN KEY(OrderID) REFERENCES Orders(OrderID)
)
```

**Output:**

<img width="1243" height="275" alt="Screenshot 2025-09-29 133547" src="https://github.com/user-attachments/assets/56e02bb1-ee39-4eb0-8031-67382b82b00c" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
