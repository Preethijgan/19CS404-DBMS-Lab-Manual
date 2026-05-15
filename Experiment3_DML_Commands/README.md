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
Write a query to list all products that have a discounted price between $100 and $250. Return product_id, original_price, discount_percentage, and discounted_price from products table.

**Code:**

```sql
SELECT 
    product_id,
    original_price,
    discount_percentage,
    original_price - (original_price * discount_percentage) AS discounted_price
FROM products
WHERE original_price - (original_price * discount_percentage) BETWEEN 100 AND 250;
```

**Output:**
<img width="1187" height="198" alt="image" src="https://github.com/user-attachments/assets/d51ce505-eb6f-41e1-b478-6dd90e8aa2db" />


**Question 2**
---
 Write a query to fetch details of all employees excluding the employees with first names, “Sanjay” and “Sonia” from the EmployeeInfo table.

 **Code:**

```sql
SELECT * from EmployeeInfo
WHERE EmpFname NOT IN ('Sanjay','Sonia');
```

**Output:**
<img width="1197" height="202" alt="image" src="https://github.com/user-attachments/assets/c9b9fd9d-0743-4f8f-9702-f7e4223115c6" />


**Question 3**
---
Write a SQL statement to Increase the selling price by 10% for all products in the 'Bakery' category in the products table.

Products table

---------------
product_id
product_name
category
cost_price
sell_price
reorder_lvl
quantity
supplier_id

**Code:**

```sql
UPDATE products
SET sell_price = sell_price * 1.10
WHERE category = 'Bakery';
```

**Output:**
<img width="1197" height="452" alt="image" src="https://github.com/user-attachments/assets/eb6653da-b1dc-4b6c-b9e0-ebfe2d0ce1e2" />


**Question 4**
---
Write a SQL statement to display name and commission of first 5 salesmen.

table info

salesman(name,commission) 

**Code:**

```sql
SELECT name,commission
FROM salesman
LIMIT 5;
```

**Output:**

<img width="576" height="452" alt="image" src="https://github.com/user-attachments/assets/1048da0d-6480-4687-af97-7c353a36e0d6" />



**Question 5**
---
Write a SQL statement to get the EmployeeID, FirstName, BirthDate, Age from employees table whose age is older than 50.

[Note: Calculate age from BirthDate field (consider current date as '2023-12-30')]

employees table

cid         name        type        notnull     dflt_value  pk
----------  ----------  ----------  ----------  ----------  ----------
0           EmployeeID  INTEGER       0                       1
1           LastName    VARCHAR(15)   0                       0
2           FirstName   VARCHAR(15)   0                       0
3           BirthDate   DATETIME      0                       0
4           Photo       VARCHAR(25)   0                       0
5           Notes       VARCHAR(10)   0                       0

**Code:**

```sql
SELECT 
EmployeeID, 
FirstName, 
BirthDate,
(strftime('%Y','2023-12-30')-strftime('%Y',BirthDate)) AS age

FROM employees
WHERE (strftime('%Y','2023-12-30')-strftime('%Y',BirthDate)) > 50;
```

**Output:**
<img width="968" height="566" alt="image" src="https://github.com/user-attachments/assets/2937ad3b-a8a0-4770-bdd8-ea7c5e2681f9" />


**Question 6**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type
-----------------  ---------------
product_id         INT
product_name       VARCHAR(100)
category           VARCHAR(50)
cost_price         DECIMAL(10,2)
sell_price         DECIMAL(10,2)
reorder_lvl        INT
quantity           INT
supplier_id        INT

**Code:**

```sql
UPDATE PRODUCTS
SET reorder_lvl = 40
WHERE category = 'Grocery';
```

**Output:**
<img width="1197" height="382" alt="image" src="https://github.com/user-attachments/assets/6e222bf9-f8b2-4878-ac36-4319cbe5b2f9" />


**Question 7**
---
Write a SQL query to delete a doctor from Doctors table whos specialization is 'Cardiology'

Sample table: Doctors

attributes: doctor_id, first_name, last_name, specialization

**Code:**

```sql
DELETE
FROM Doctors
WHERE specialization IN ('Cardiology');
```

**Output:**
<img width="993" height="311" alt="image" src="https://github.com/user-attachments/assets/5eadad7a-b7d7-40d0-82a5-1253fda99bdc" />


**Question 8**
---
Find Products with a Discounted Price Greater than a Given Amount:

Write a query to list all products that have a discounted price greater than $100. Return product_id, original_price, discount_percentage, and discounted_price.

Sample table: Products

product_id | original_price | discount_percentage

-----------------------------------------------------------

"101" "50" "0.1"

"102" "150" "0.15"

"103" "200" "0.2"

"104" "300" "0.25"
**Code:**

```sql
SELECT
    product_id,
    original_price,
    discount_percentage,
    original_price - (original_price*discount_percentage) AS discounted_price
FROM products
WHERE original_price - (original_price*discount_percentage) > 100;
```

**Output:**
<img width="1183" height="281" alt="image" src="https://github.com/user-attachments/assets/fe3a0635-503f-40a1-91f3-f1aed6a1d270" />


**Question 9**
---
write a SQL query to identify customers who do not belong to the city of 'New York' or have a grade value that exceeds 100. Return customer_id, cust_name, city, grade, and salesman_id.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------
        3002 | Nick Rimando   | New York   |   100 |        5001
        3007 | Brad Davis     | New York   |   200 |        5001
        3005 | Graham Zusi    | California |   200 |        5002

**Code:**

```sql
SELECT 
    customer_id,
    cust_name,
    city,
    grade,
    salesman_id
FROM customer
WHERE city <> 'New York'
  AND grade = 100;
```

**Output:**
<img width="1168" height="322" alt="image" src="https://github.com/user-attachments/assets/ebda8939-5089-48cd-a977-68bbc5782a5c" />


**Question 10**
---
Write a SQL query to Get the employees whose name starts and ends with the same two characters:

Table name: emp

name        type
----------  ----------
empno       INT
ename       VARCHAR(100)
job         VARCHAR(50)
mgr         INT
hiredate    DATE
sal         DECIMAL(10,2)
comm        DECIMAL(10,2)
deptno      INT

**Code:**

```sql
SELECT ename
FROM emp
WHERE LOWER(SUBSTR(ename, 1, 2)) = LOWER(SUBSTR(ename, -2, 2));
```

**Output:**

<img width="422" height="288" alt="image" src="https://github.com/user-attachments/assets/432679fb-2c4a-43c1-965f-94eb27e72f16" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
