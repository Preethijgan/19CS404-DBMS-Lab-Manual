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
Insert the following products into the Products table:

Name        Category     Price       Stock
----------  -----------  ----------  ----------
Smartphone  Electronics  800         150
Headphones  Accessories  200         300

**Code:**
```sql
INSERT into Products(Name, Category, Price, Stock)
Values
('Smartphone', 'Electronics', 800, 150),
('Headphones', 'Accessories', 200, 300); 
```

**Output:**

<img width="945" height="253" alt="image" src="https://github.com/user-attachments/assets/e8bf4e43-8ae9-4fa5-8d1e-552b34eff391" />


**Question 2**
---
Create a table named Tasks with the following columns:

TaskID as INTEGER
TaskName as TEXT
DueDate as DATE

**Code:**

```sql
CREATE table Tasks(
TaskID INTEGER,
TaskName TEXT,
DueDate DATE
);
```

**Output:**

<img width="1195" height="300" alt="image" src="https://github.com/user-attachments/assets/d15ae2a8-adb5-404e-bbac-da35d43e63a7" />


**Question 3**
---
Create a table named Orders with the following columns:

OrderID as INTEGER
OrderDate as TEXT
CustomerID as INTEGER

**Code:**

```sql
CREATE table Orders(
OrderID INTEGER,
OrderDate TEXT,
CustomerID INTEGER
);
```

**Output:**

<img width="1193" height="292" alt="image" src="https://github.com/user-attachments/assets/fce8722f-dd3c-49d5-a708-7fa7782bbb6c" />


**Question 4**
---
Insert a customer with CustomerID 301, Name Michael Jordan, Address 123 Maple St, City Chicago, and ZipCode 60616 into the Customers table.

**Code:**

```sql
SELECT * FROM Customers WHERE CustomerId = 301;
INSERT INTO Customers(CustomerId, Name, Address, City, ZipCode)
VALUES(301, 'Michael Jordan', '123 Maple St', 'Chicago', '60616');
```

**Output:**

<img width="1197" height="156" alt="image" src="https://github.com/user-attachments/assets/c86eeb49-903c-4efb-b81c-db9c3a8c56be" />


**Question 5**
---
Insert the following students into the Student_details table:
RollNo      Name        Gender      Subject     MARKS
----------  ----------  ----------  ----------  ----------
202            Ella King         F           Chemistry   87
203            James Bond   M          Literature    78

**Code:**

```sql
INSERT into Student_Details(RollNo, Name, Gender, Subject, MARKS)
VALUES
(202,'Ella King','F','Chemistry',87),
(203,'James Bond', 'M','Literature', 78);
```

**Output:**

<img width="1130" height="172" alt="image" src="https://github.com/user-attachments/assets/28356dda-8948-4c1b-b4bb-362fc0cc694b" />


**Question 6**
---
Create a table named Invoices with the following constraints:
InvoiceID as INTEGER should be the primary key.
InvoiceDate as DATE.
Amount as REAL should be greater than 0.
DueDate as DATE should be greater than the InvoiceDate.
OrderID as INTEGER should be a foreign key referencing Orders(OrderID).

**Code:**

```sql
CREATE table Invoices(
InvoiceID INTEGER PRIMARY KEY,
InvoiceDate DATE,
Amount REAL CHECK(Amount > 0),
DueDate DATE CHECK(DueDate > InvoiceDate),
OrderID INTEGER,
FOREIGN KEY (OrderID) REFERENCES Orders(OrderID)
);
```

**Output:**

<img width="1162" height="200" alt="image" src="https://github.com/user-attachments/assets/be5578c4-438f-4c88-8e1f-6658932f272a" />


**Question 7**
---
Write an SQL query to add two new columns, first_name and last_name, to the table employee. Both columns should have a data type of varchar(50).

**Code:**
```sql
ALTER table employee ADD COLUMN first_name varchar(50);
ALTER table employee ADD COLUMN last_name varchar(50);
```

**Output:**
<img width="1195" height="227" alt="image" src="https://github.com/user-attachments/assets/0d920ff7-9a20-4ce2-9ea6-3016f4c59ebd" />


**Question 8**
---
Write an SQL Query to add the attributes designation, net_salary, and dob to the Companies table with the following data types:
designation as VARCHAR(50)
net_salary as NUMBER
dob as DATE
 
**Code:**
```sql
ALTER TABLE Companies add column designation varchar(50);
ALTER TABLE Companies add column net_salary number;
ALTER TABLE Companies add column dob date;
```

**Output:**

<img width="1203" height="327" alt="image" src="https://github.com/user-attachments/assets/2b27d480-8aa2-4dd9-877f-d5d03d66b491" />


**Question 9**
---
Create a table named Locations with the following columns:

LocationID as INTEGER
LocationName as TEXT
Address as TEXT

**Code:**

```sql
CREATE table Locations(
LocationID INTEGER,
LocationName TEXT,
Address TEXT
);
```

**Output:**
<img width="1205" height="298" alt="image" src="https://github.com/user-attachments/assets/0b96e51d-55d4-4bf9-92ea-7f55358e5e97" />


**Question 10**
---
Create a table named Employees with the following columns:

EmployeeID as INTEGER
FirstName as TEXT
LastName as TEXT
HireDate as DATE

**Code:**

```sql
CREATE TABLE Employees(
EmployeeID INTEGER,
FirstName TEXT,
LastName TEXT,
HireDate DATE
);
```

**Output:**
<img width="1193" height="227" alt="image" src="https://github.com/user-attachments/assets/972ca3fa-47c7-45c9-b191-a4a122da066e" />



## RESULT
Thus, the SQL queries to implement different types of constraints and DDL commands have been executed successfully.
