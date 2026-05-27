# Experiment 9: PL/SQL – Procedures and Functions

## AIM
To understand and implement procedures and functions in PL/SQL for performing various operations such as calculations, decision-making, and looping.

---

## THEORY

PL/SQL (Procedural Language/SQL) extends SQL by adding procedural constructs like variables, conditions, loops, procedures, and functions. Procedures and functions are subprograms that help modularize the code and improve reusability.

### **Procedure**
A PL/SQL **procedure** is a subprogram that performs a specific action. It does not return a value directly but can return values using `OUT` parameters.

**Syntax:**
```sql
CREATE OR REPLACE PROCEDURE procedure_name (parameters)
IS
BEGIN
   -- statements
END;
```

To call the procedure

```sql
EXEC procedure_name(arguments);
```

### **Function**
A PL/SQL **function** is a subprogram that returns a single value using the RETURN keyword.

```sql
CREATE OR REPLACE FUNCTION function_name (parameters)
RETURN datatype
IS
BEGIN
   -- statements
   RETURN value;
END;
```

To call the function:

```sql
SELECT function_name(arguments) FROM DUAL;
```

Key Differences:

-A procedure does not return a value, whereas a function must return a value.
-Functions can be called from SQL queries, procedures cannot (in most cases).

## 1. Write a PL/SQL Procedure to Find the Square of a Number

### Steps:
- Create a procedure named `find_square`.
- Declare a parameter to accept a number.
- Inside the procedure, compute the square of the input number.
- Use `DBMS_OUTPUT.PUT_LINE` to display the result.
- Call the procedure with a number as input.

**Program:**
```sql

SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE find_square(p_number IN NUMBER) IS
    v_square NUMBER;
BEGIN
    v_square := p_number * p_number;
    DBMS_OUTPUT.PUT_LINE('Square of ' || p_number || ' is ' || v_square);
END;
/
BEGIN
    find_square(6);
END;
/

```

**Expected Output:**  
Square of 6 is 36

**Output:**
<img width="945" height="162" alt="image" src="https://github.com/user-attachments/assets/6cd5249b-0f42-4b7f-8932-ba1f8bb43aa8" />

---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.


**Program:**

```sql

CREATE OR REPLACE FUNCTION get_factorial(p_number IN NUMBER)
RETURN NUMBER
IS
   v_result NUMBER := 1;
BEGIN
   IF p_number < 0 THEN
      RETURN NULL;  
   END IF;

   FOR i IN 1..p_number LOOP
      v_result := v_result * i;
   END LOOP;

   RETURN v_result;
END;
/

DECLARE
   v_input NUMBER := 5;
   v_output NUMBER;
BEGIN
   v_output := get_factorial(v_input);
   DBMS_OUTPUT.PUT_LINE('Factorial of ' || v_input || ' is ' || v_output);
END;
/

```
**Expected Output:**  
Factorial of 5 is 120

**Output:**
<img width="1919" height="874" alt="image" src="https://github.com/user-attachments/assets/1b298332-00fa-469c-8cec-01a0aa20af8d" />


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Program:**
```sql

CREATE OR REPLACE PROCEDURE check_even_odd(p_number IN NUMBER) IS
BEGIN
  
   IF MOD(p_number, 2) = 0 THEN
      DBMS_OUTPUT.PUT_LINE(p_number || ' is Even');
   ELSE
      DBMS_OUTPUT.PUT_LINE(p_number || ' is Odd');
   END IF;
END;
/

BEGIN
   check_even_odd(12);  
END;
/


```

**Expected Output:**  
12 is Even

---

**Output:**







## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

---

## 5. Write a PL/SQL Procedure to Display the Multiplication Table of a Number

### Steps:
- Create a procedure named `print_table`.
- Accept an input number.
- Use a loop from 1 to 10 to multiply the input number.
- Display the multiplication results using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Multiplication table of 5:  
5 x 1 = 5  
5 x 2 = 10  
5 x 3 = 15  
...  
5 x 10 = 50

## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
