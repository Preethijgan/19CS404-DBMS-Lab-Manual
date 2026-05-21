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
Write the SQL query that accomplishes the selection of all columns from the "patients" table and the first name of doctors from the "doctors" table, with an inner join on the "doctor_id" column.

PATIENTS TABLE:
| name            |  type            |
| --------------- |  --------------- |
| patient_id |      INT |
|first_name    |   VARCHAR(50) |
| last_name    |    VARCHAR(50) |
|date_of_birth |   DATE |
| admission_date |  DATE |
| discharge_date |  DATE |
| doctor_id     |   INT |

DOCTORS TABLE:

|name            | type             |
|--------------- |  --------------- |
|doctor_id  |      INT|
| first_name    |   VARCHAR(50) |
| last_name   |     VARCHAR(50) |
| specialization |  VARCHAR(100) |

```sql
SELECT 
    P.*,
    d.first_name AS doctor_name
FROM PATIENTS AS p
INNER JOIN DOCTORS AS d
    ON  p.doctor_id = d.doctor_id;

```

**Output:**

<img width="1187" height="552" alt="image" src="https://github.com/user-attachments/assets/f0d4be8f-4404-466f-86f8-03df66e31a1e" />


**Question 2**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

CUSTOMER TABLE:

<img width="1021" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/f51f31d3-cf0e-4519-85af-68fc3bf3acc6" />


ORDERS TABLE:
<img width="1094" height="166" alt="unnamed" src="https://github.com/user-attachments/assets/d8b473da-3f1a-4958-8090-95632286a527" />


```sql
SELECT
    c.cust_name
FROM CUSTOMER AS c
LEFT JOIN ORDERS AS o
    ON c.customer_id = o.customer_id
WHERE purch_amt < 100;
```

**Output:**

<img width="522" height="475" alt="image" src="https://github.com/user-attachments/assets/5608542d-2297-4216-a9c9-e82d5aa67ec3" />


**Question 3**
---
Write the SQL query that achieves the selection of all columns from the "nurses" table (aliased as "n") and the "department_name" column from the "departments" table, with an inner join on the "department_id" column.

NURSES TABLE:
<img width="1002" height="166" alt="unnamed" src="https://github.com/user-attachments/assets/b47579c0-e6c8-4a45-a508-e200d026305b" />



DEPARTMENTS TABLE:

<img width="1017" height="173" alt="unnamed" src="https://github.com/user-attachments/assets/721082a6-1744-4ff5-b270-3e1366eea7a6" />


```sql
SELECT
    n.*,
    d.department_name
FROM NURSES AS n
INNER JOIN DEPARTMENTS AS d
    ON n.department_id = d.department_id;
```

**Output:**
<img width="1191" height="556" alt="image" src="https://github.com/user-attachments/assets/4801d272-a4ee-4483-8973-5456c9e61120" />


**Question 4**
---
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

| name            | type            |
| --------------- |  ---------------|
| patient_id |      INT |
| first_name   |    VARCHAR(50) |
| last_name   |     VARCHAR(50) |
| date_of_birth |   DATE |
| admission_date |   DATE |
| discharge_date  | DATE |
| doctor_id    |    INT |

SURGERIES TABLE:

| name            | type             |
| --------------- |  --------------- |
| surgery_id   |    INT |
| patient_id  |     INT |
| surgeon_id   |    INT |
| surgery_date   |  DATE |

```sql
SELECT
    p.first_name,
    p.last_name
FROM PATIENTS AS p
INNER JOIN SURGERIES AS s
    ON p.patient_id = s.patient_id
WHERE surgery_date BETWEEN '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="785" height="388" alt="image" src="https://github.com/user-attachments/assets/0eec2854-5b21-4c02-97aa-37bbc23aa7ca" />


**Question 5**
---
Write the SQL query that accomplishes the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column and a condition filtering for patients with the first name 'Alice'.

PATIENTS TABLE:
| name            | type            |
| --------------- |  ---------------|
| patient_id |      INT |
| first_name   |    VARCHAR(50) |
| last_name   |     VARCHAR(50) |
| date_of_birth |   DATE |
| admission_date |   DATE |
| discharge_date  | DATE |
| doctor_id    |    INT |

SURGERIES TABLE:

| name            | type             |
| --------------- |  --------------- |
| surgery_id   |    INT |
| patient_id  |     INT |
| surgeon_id   |    INT |
| surgery_date   |  DATE |




For example:

```sql
SELECT 
    p.first_name,
    s.*
FROM PATIENTS p
INNER JOIN SURGERIES s
    ON p.patient_id = s.patient_id
WHERE first_name = 'Alice';
```

**Output:**
<img width="1198" height="401" alt="image" src="https://github.com/user-attachments/assets/11bc1a97-52a4-435a-a872-7d0a29857568" />


**Question 6**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'New York'.

Customer Table:
<img width="1021" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/47e76c5d-5165-40a3-8960-d2aed012d710" />



Salesmen Table:
<img width="1046" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/69c56d6a-264a-4b65-af83-cd25638efc34" />



```sql
SELECT
    name
FROM Salesman AS s
LEFT JOIN Customer AS c
    ON s.salesman_id = c.salesman_id
WHERE c.city = 'New York';
```

**Output:**

<img width="535" height="381" alt="image" src="https://github.com/user-attachments/assets/d2997933-2092-4732-9af9-c40eee186dd6" />


**Question 7**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and the test name from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

<img width="1052" height="172" alt="unnamed" src="https://github.com/user-attachments/assets/0305c3b2-11a2-410e-8a51-acde4cd1d60c" />


TEST_RESULT TABLES:
<img width="1060" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/b253f280-1c8f-480d-a27b-5d1424e604cd" />



```sql
SELECT 
    p.first_name AS patient_name,
    t.test_name
FROM PATIENTS AS p
INNER JOIN TEST_RESULTS AS t
    ON P.patient_id = t.patient_id;
    
```

**Output:**

<img width="801" height="546" alt="image" src="https://github.com/user-attachments/assets/b51e42d0-abce-45c1-9881-05629b526734" />


**Question 8**
---
Write the SQL query that achieves the selection of the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the city 'London'.

Customer Table:
<img width="1021" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/c15208f8-d057-4d4d-8435-41b71d4bfcb7" />



Salesmen Table:

<img width="1046" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/557febe0-842a-4949-95ba-39afbe6ac744" />


```sql
SELECT 
    s.name
FROM Salesman AS s
LEFT JOIN Customer AS c
    ON s.salesman_id = c.salesman_id
WHERE c.city = 'London';
```

**Output:**

<img width="497" height="480" alt="image" src="https://github.com/user-attachments/assets/312281ba-b640-4f2d-bbaa-853679c2a6f5" />


**Question 9**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column and a condition filtering for test results with the test name 'Blood Pressure'.

PATIENTS TABLE:

<img width="1052" height="172" alt="unnamed" src="https://github.com/user-attachments/assets/6114bbd3-8fec-4632-8b8e-e5bc713cb42b" />


TEST_RESULT TABLES:
<img width="1060" height="171" alt="unnamed" src="https://github.com/user-attachments/assets/0194c046-0857-430b-806b-714477bf8b41" />



```sql
SELECT
    p.first_name AS patient_name,
    t.*
FROM PATIENTS AS p
INNER JOIN TEST_RESULTS AS t
    ON p.patient_id = t.patient_id
WHERE test_name = 'Blood Pressure';
```

**Output:**

<img width="1197" height="393" alt="image" src="https://github.com/user-attachments/assets/429dc56f-9910-4e4e-8598-eb02ea5c7377" />


**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table and all columns from the "surgeries" table, with an inner join on the "patient_id" column. Include conditions to filter for patients discharged between '2024-03-01' and '2024-03-31' but not admitted during the same period.
PATIENTS TABLE:
| name            | type            |
| --------------- |  ---------------|
| patient_id |      INT |
| first_name   |    VARCHAR(50) |
| last_name   |     VARCHAR(50) |
| date_of_birth |   DATE |
| admission_date |   DATE |
| discharge_date  | DATE |
| doctor_id    |    INT |

SURGERIES TABLE:

| name            | type             |
| --------------- |  --------------- |
| surgery_id   |    INT |
| patient_id  |     INT |
| surgeon_id   |    INT |
| surgery_date   |  DATE |



```sql
SELECT 
    p.first_name,
    s.*
FROM PATIENTS AS p
INNER JOIN SURGERIES AS s
    ON p.patient_id = s.patient_id
WHERE discharge_date BETWEEN '2024-03-01' and '2024-03-31'
    AND admission_date <> '2024-03-01' and '2024-03-31';
```

**Output:**

<img width="1172" height="412" alt="image" src="https://github.com/user-attachments/assets/b3dd42d9-aec1-454b-af2d-89e18e9d0a65" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
