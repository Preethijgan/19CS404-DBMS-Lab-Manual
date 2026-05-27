# Experiment 10: PL/SQL – Triggers

## AIM
To write and execute PL/SQL trigger programs for automating actions in response to specific table events like INSERT, UPDATE, or DELETE.

---

## THEORY

A **trigger** is a stored PL/SQL block that is automatically executed or fired when a specified event occurs on a table or view. Triggers can be used for enforcing business rules, auditing changes, or automatic updates.

### Types of Triggers:
- **Before Trigger**: Executes before the operation (INSERT, UPDATE, DELETE).
- **After Trigger**: Executes after the operation.
- **Row-level Trigger**: Executes for each affected row.
- **Statement-level Trigger**: Executes once for the triggering statement.

**Basic Syntax:**
```sql
CREATE OR REPLACE TRIGGER trigger_name
BEFORE|AFTER INSERT|UPDATE|DELETE ON table_name
[FOR EACH ROW]
BEGIN
   -- trigger logic
END;
```

## 1. Write a trigger to log every insertion into a table.
**Steps:**
- Create two tables: `employees` (for storing data) and `employee_log` (for logging the inserts).
- Write an **AFTER INSERT** trigger on the `employees` table to log the new data into the `employee_log` table.


**Program:**

```sql

CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE TABLE employee_log (
    log_id NUMBER GENERATED ALWAYS AS IDENTITY,
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER,
    log_date DATE
);

CREATE OR REPLACE TRIGGER trg_employee_log
AFTER INSERT ON employees
FOR EACH ROW
BEGIN
    INSERT INTO employee_log(emp_id, emp_name, salary, log_date)
    VALUES(:NEW.emp_id, :NEW.emp_name, :NEW.salary, SYSDATE);
END;
/

INSERT INTO employees VALUES (101, 'John', 50000);

COMMIT;

SELECT * FROM employee_log;
```
**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

---

**Output:**

<img width="1042" height="777" alt="image" src="https://github.com/user-attachments/assets/e163406c-9f59-4bbc-9fcb-ab0fdbfc70ec" />


## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Program:**

```sql
CREATE TABLE sensitive_data (
    id NUMBER,
    data VARCHAR2(100)
);

INSERT INTO sensitive_data VALUES (1, 'Confidential Record');
COMMIT;

CREATE OR REPLACE TRIGGER trg_prevent_delete
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(
        -20001,
        'ERROR: Deletion not allowed on this table.'
    );
END;
/

DELETE FROM sensitive_data WHERE id = 1;


```

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

---

**Output:**

<img width="1020" height="700" alt="image" src="https://github.com/user-attachments/assets/916762d8-368b-469c-b521-045647f0434e" />


## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program:**

```sql
CREATE TABLE products (
    product_id NUMBER,
    product_name VARCHAR2(50),
    price NUMBER,
    last_modified TIMESTAMP
);

INSERT INTO products
VALUES (1, 'Laptop', 50000, SYSTIMESTAMP);

COMMIT;

CREATE OR REPLACE TRIGGER trg_update_timestamp
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/

UPDATE products
SET price = 55000
WHERE product_id = 1;

COMMIT;

SELECT * FROM products;


```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.

---

**Output:**

<img width="1016" height="621" alt="Screenshot 2026-05-27 205440" src="https://github.com/user-attachments/assets/f61ab6e0-1f50-4df9-995b-0b39b2245138" />






## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program:**

```sql
CREATE TABLE customer_orders (
    order_id NUMBER,
    customer_name VARCHAR2(50),
    amount NUMBER
);

CREATE TABLE audit_log (
    update_count NUMBER
);

INSERT INTO audit_log VALUES (0);

INSERT INTO customer_orders VALUES (1, 'Preethi', 2500);

COMMIT;

CREATE OR REPLACE TRIGGER trg_update_counter
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1;
END;
/

UPDATE customer_orders
SET amount = 3000
WHERE order_id = 1;

COMMIT;

SELECT * FROM audit_log;

```
**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.

---

**Output:**

<img width="1038" height="636" alt="image" src="https://github.com/user-attachments/assets/cb2592b3-b0ce-4f5c-9e4f-752d53066ef0" />


## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program:**

```sql

CREATE TABLE employees (
    emp_id NUMBER,
    emp_name VARCHAR2(50),
    salary NUMBER
);

CREATE OR REPLACE TRIGGER trg_check_salary
BEFORE INSERT ON employees
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(
            -20002,
            'ERROR: Salary below minimum threshold.'
        );
    END IF;
END;
/

INSERT INTO employees VALUES (1, 'John', 5000);

COMMIT;

INSERT INTO employees VALUES (2, 'Sam', 2000);

SELECT * FROM employees;
```

**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`

**Output:**

<img width="1041" height="673" alt="image" src="https://github.com/user-attachments/assets/c0a6c5d2-6f0a-4252-9e04-c11114e54c6f" />


## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
