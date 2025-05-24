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

**Expected Output:**  
Square of 6 is 36

## CODE:
```sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE find_square (
    num IN NUMBER,
    square_result OUT NUMBER
) AS
BEGIN
    square_result := num * num;
END;
/
DECLARE
    input_number    NUMBER := 6;
    output_square   NUMBER;
BEGIN
    find_square(input_number, output_square);
    DBMS_OUTPUT.PUT_LINE('Square of ' || input_number || ' is ' || output_square);
END;
/
```
![image](https://github.com/user-attachments/assets/5ff73dc0-33f9-46ed-beba-8883c01a107e)


---

## 2. Write a PL/SQL Function to Return the Factorial of a Number

### Steps:
- Create a function named `get_factorial`.
- Declare a parameter to accept a number.
- Use a loop to calculate the factorial.
- Return the result using the `RETURN` statement.
- Call the function using a `SELECT` statement or in an anonymous block.

**Expected Output:**  
Factorial of 5 is 120

## CODE:
```sql

SET SERVEROUTPUT ON;

CREATE OR REPLACE FUNCTION get_factorial (num IN NUMBER)
RETURN NUMBER
AS
    result NUMBER := 1;
    i      NUMBER;
BEGIN
    IF num < 0 THEN
        RETURN NULL;
    END IF;

    FOR i IN 1..num LOOP
        result := result * i;
    END LOOP;

    RETURN result;
END;
/

DECLARE
    input_number NUMBER := 5;
    output_result NUMBER;
BEGIN
    output_result := get_factorial(input_number);
    DBMS_OUTPUT.PUT_LINE('Factorial of ' || input_number || ' is ' || output_result);
END;
/
```

![image](https://github.com/user-attachments/assets/cd0a3fef-b576-4d56-9df7-b215c5c3e5ed)


---

## 3. Write a PL/SQL Procedure to Check Whether a Number is Even or Odd

### Steps:
- Create a procedure named `check_even_odd`.
- Accept an input parameter.
- Use the `MOD` function to check if the number is divisible by 2.
- Display whether it is Even or Odd using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
12 is Even

## CODE:
```sql
-- Enable output
SET SERVEROUTPUT ON;

-- Create the procedure
CREATE OR REPLACE PROCEDURE check_even_odd (num IN NUMBER) AS
BEGIN
    IF MOD(num, 2) = 0 THEN
        DBMS_OUTPUT.PUT_LINE(num || ' is Even');
    ELSE
        DBMS_OUTPUT.PUT_LINE(num || ' is Odd');
    END IF;
END;
/

-- Call the procedure
BEGIN
    check_even_odd(12);
END;
/
```
![image](https://github.com/user-attachments/assets/bd3ed451-4cbe-4bce-9d0d-c782da3ab825)

---

## 4. Write a PL/SQL Function to Return the Reverse of a Number

### Steps:
- Create a function named `reverse_number`.
- Accept an input number as parameter.
- Use a loop to reverse the digits of the number.
- Return the reversed number.
- Call the function and display the output.

**Expected Output:**  
Reversed number of 1234 is 4321

## CODE:
```sql
SET SERVEROUTPUT ON;
CREATE OR REPLACE FUNCTION reverse_number (num IN NUMBER)
RETURN NUMBER
AS
    reversed NUMBER := 0;
    n        NUMBER := num;
    digit    NUMBER;
BEGIN
    WHILE n > 0 LOOP
        digit := MOD(n, 10);
        reversed := (reversed * 10) + digit;
        n := TRUNC(n / 10);
    END LOOP;

    RETURN reversed;
END;
/

DECLARE
    input_number   NUMBER := 1234;
    output_reverse NUMBER;
BEGIN
    output_reverse := reverse_number(input_number);
    DBMS_OUTPUT.PUT_LINE('Reversed number of ' || input_number || ' is ' || output_reverse);
END;
/
```
![image](https://github.com/user-attachments/assets/24a20139-9076-4f53-82e5-fe02cc6ad50c)


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

## CODE:
```sql
SET SERVEROUTPUT ON;

CREATE OR REPLACE PROCEDURE print_table (num IN NUMBER) AS
BEGIN
    DBMS_OUTPUT.PUT_LINE('Multiplication table of ' || num || ':');
    FOR i IN 1..10 LOOP
        DBMS_OUTPUT.PUT_LINE(num || ' x ' || i || ' = ' || (num * i));
    END LOOP;
END;
/

BEGIN
    print_table(5);
END;
/
```
![image](https://github.com/user-attachments/assets/b7a3c9b4-04d8-46af-9d2a-e7f8b4920599)


## RESULT
Thus, the PL/SQL programs using procedures and functions were written, compiled, and executed successfully.
