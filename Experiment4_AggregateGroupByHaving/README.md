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
Write a SQL query to find the average length of names for people living in Chennai?

Table: customer

name        type
----------  ----------
id          INTEGER
name        TEXT   
city        TEXT
email       TEXT
phone       INTEGER


**Code:**

```sql
SELECT avg(length(name)) AS avg_name_length
FROM customer 
WHERE city = 'Chennai'; 
```

**Output:**

<img width="430" height="298" alt="image" src="https://github.com/user-attachments/assets/87d42c60-91b5-43e6-8994-da8d822d7508" />


**Question 2**
---
Write a SQL query to return the total number of rows in the 'customer' table where the city is Noida.

Sample table: customer

**Code:**

```sql
SELECT count(city) AS COUNT
FROM customer
WHERE city = 'Noida';
```

**Output:**

<img width="342" height="300" alt="image" src="https://github.com/user-attachments/assets/0258318e-c170-40a4-ae94-70fbebf5b9b7" />


**Question 3**
---
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

**Code:**

```sql
SELECT COUNT(cust_name) AS COUNT
FROM customer
WHERE grade > 1;
```

**Output:**

<img width="340" height="297" alt="image" src="https://github.com/user-attachments/assets/c4bb8c76-c7d1-42c7-93c7-fa806e52091f" />


**Question 4**
---
How many patients are there in each age group category (e.g., under 20, 20-30, 30-40, etc.)?

Sample table: Patients Table

**Code:**

```sql
SELECT 
    CASE
        WHEN age BETWEEN 20 AND 30 THEN '20-30'
        WHEN age BETWEEN 31 AND 40 THEN '31-40'
        WHEN age BETWEEN 41 AND 50 THEN '41-50'
        WHEN age > 50 THEN 'Above 50'
    END AS AgeGroup,
    COUNT(*) AS TotalPatients
FROM (
    SELECT 
        CAST(
            strftime('%Y', 'now') - 
            strftime('%Y', DateOfBirth) - 
            (strftime('%m-%d', 'now') < strftime('%m-%d', DateOfBirth))
        AS INTEGER) AS age
    FROM Patients
) AS AgeCalc
WHERE age >= 20
GROUP BY AgeGroup
ORDER BY MIN(age);
```

**Output:**

<img width="616" height="448" alt="image" src="https://github.com/user-attachments/assets/8dab9264-e7ce-4f24-98d0-8d371dcec48e" />


**Question 5**
---
What is the total number of medications prescribed for each patient?

Sample tablePrescriptions Table

**Code:**

```sql
SELECT
    PatientID,
    COUNT(*) AS TotalMedications
FROM Prescriptions
GROUP BY PatientID
ORDER BY PatientID;
```

**Output:**

<img width="672" height="740" alt="image" src="https://github.com/user-attachments/assets/e0ab6c02-e264-4fb7-864d-23885e8a9544" />


**Question 6**
---
How many male and female doctors are there in each medical specialty?

Sample table:Doctors Table

**Code:**

```sql
SELECT
    Specialty,
    Gender,
    COUNT(*) AS TotalDoctors
FROM Doctors
GROUP BY Specialty, Gender
ORDER BY Specialty, Gender;
```

**Output:**

<img width="925" height="650" alt="image" src="https://github.com/user-attachments/assets/68e5e51a-ff01-47e3-b689-06d311b90de5" />


**Question 7**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.

Sample table: customer1

**Code:**

```sql
SELECT
    address,
    SUM(salary)
FROM customer1
GROUP BY address
HAVING SUM(salary)>2000;
```

**Output:**

<img width="578" height="475" alt="image" src="https://github.com/user-attachments/assets/ab897b45-b475-4595-8588-a577ab1b1575" />


**Question 8**
---
Write the SQL query that accomplishes the selection of total number of products for each category from the "products" table, and includes only those products where the minimum category ID is less than 3.

Sample table: products

**Code:**

```sql
SELECT 
    category_id,
    count(product_name)
FROM products
GROUP BY category_id
HAVING category_id < 3;
```

**Output:**

<img width="735" height="336" alt="image" src="https://github.com/user-attachments/assets/2593685b-1e19-4755-bff1-816f936f0eda" />


**Question 9**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the average age for each group, and excludes groups where the average age is not less than 24.

Sample table: customer1

**Code:**

```sql
SELECT 
    (age / 5) * 5 AS age_group,
    AVG(age)
FROM customer1
GROUP BY age_group
HAVING AVG(age) < 24;
```

**Output:**

<img width="557" height="290" alt="image" src="https://github.com/user-attachments/assets/117d96eb-7bdd-4401-96df-509d6cbde34f" />


**Question 10**
---
Write a SQL query to identify the cities (addresses) where the average salary is greater than Rs. 5000, as per the "customer1" table.

Sample table: customer1

**Code:**

```sql
SELECT 
    address,
    AVG(salary)
FROM customer1
GROUP BY address
HAVING AVG(salary) > 5000;
```

**Output:**

<img width="577" height="426" alt="image" src="https://github.com/user-attachments/assets/3a4dc38b-7eac-4282-a75a-477915701ea2" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
