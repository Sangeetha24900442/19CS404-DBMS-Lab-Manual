# PL/SQL PROGRAMS
### NAME : Sangeetha S
### REG NO : 212224040287
## AIM
To write and execute simple PL/SQL programs using variables, loops, and conditional statements.


## THEORY

PL/SQL, which stands for Procedural Language extensions to the Structured Query Language (SQL). It is a combination of SQL along with the procedural features of programming languages.

**Syntax:**
```sql
DECLARE 
   <declarations section> 
BEGIN 
   <executable command(s)>
EXCEPTION 
   <exception handling> 
END;
```

### Basic Components of PL/SQL Block:
- DECLARE: Section to declare variables and constants.
- BEGIN: The execution section that contains PL/SQL statements.
- EXCEPTION: Handles errors or exceptions that occur in the program.
- END: Marks the end of the PL/SQL block.

# PL/SQL Programs – Steps and Expected Output

## 1. Write a PL/SQL program to find the Greatest of Two Numbers

### Steps:
- Declare two numeric variables and initialize them.
- Use an `IF` statement to compare the values.
- Display the greater number using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Greater number is: 80
```

DECLARE
    a NUMBER := 40;
    b NUMBER := 80;
BEGIN
    IF a > b THEN
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || a);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Greater number is: ' || b);
    END IF;
END;
/

```
**RESULT:**  


<img width="576" height="104" alt="Screenshot 2025-11-21 184717" src="https://github.com/user-attachments/assets/debecf1c-5f3d-4016-a496-c8e0f345919a" />

---


## 2. Write a PL/SQL program to Calculate Sum of First N Natural Numbers

### Steps:
- Declare a variable `n` and assign a value (e.g., 10).
- Initialize a `sum` variable to 0.
- Use a `WHILE` loop to iterate from 1 to `n`, adding each number to the sum.
- Display the result using `DBMS_OUTPUT.PUT_LINE`.

**Expected Output:**  
Sum of first 10 natural numbers is: 55

```
DECLARE
    n NUMBER := 10;
    i NUMBER := 1;
    total NUMBER := 0;
BEGIN
    WHILE i <= n LOOP
        total := total + i;
        i := i + 1;
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Sum of first ' || n || ' natural numbers is: ' || total);
END;
/

```
**RESULT:**

<img width="552" height="91" alt="Screenshot 2025-11-21 184814" src="https://github.com/user-attachments/assets/18556360-39f8-4a89-ace2-0e4c0507e890" />

---

## 3. Write a PL/SQL program to generate Fibonacci series

### Steps:
- Declare the variable `n` to indicate how many terms to generate.
- Initialize the first two Fibonacci numbers (0 and 1).
- Use a loop to generate the next terms using the formula `c = a + b`.
- Print each term in the series.

**Expected Output:**  
n = 7  
Fibonacci sequence: 0, 1, 1, 2, 3, 5, 8
```
DECLARE
    n NUMBER := 7;
    a NUMBER := 0;
    b NUMBER := 1;
    c NUMBER;
    i NUMBER := 3;
BEGIN
    DBMS_OUTPUT.PUT_LINE(a);
    DBMS_OUTPUT.PUT_LINE(b);

    WHILE i <= n LOOP
        c := a + b;
        DBMS_OUTPUT.PUT_LINE(c);
        a := b;
        b := c;
        i := i + 1;
    END LOOP;
END;
/
```
**RESULT:**

<img width="259" height="249" alt="Screenshot 2025-11-21 185020" src="https://github.com/user-attachments/assets/edae5fb9-ffc4-457a-9932-b90519e8ee8b" />


---

## 4. Write a PL/SQL Program to display the number in Reverse Order

### Steps:
- Declare a variable `n` and assign a value (e.g., 1535).
- Use a loop to extract each digit using modulo and reverse the number.
- Display the reversed number.

**Expected Output:**  
n = 1535  
Reversed number is 5351

```
DECLARE
    n NUMBER := 1535;
    rev NUMBER := 0;
    digit NUMBER;
    temp NUMBER := n;
BEGIN
    WHILE temp > 0 LOOP
        digit := MOD(temp, 10);
        rev := rev * 10 + digit;
        temp := FLOOR(temp / 10);
    END LOOP;

    DBMS_OUTPUT.PUT_LINE('Original number = ' || n);
    DBMS_OUTPUT.PUT_LINE('Reversed number is ' || rev);
END;
/

```
**RESULT:**


<img width="608" height="107" alt="Screenshot 2025-11-21 185152" src="https://github.com/user-attachments/assets/f9f4f4e6-a84d-4edc-a163-24784fd0f91e" />

---

## 5. Write a PL/SQL program to find the largest of three numbers

### Steps:
- Declare three numeric variables `a`, `b`, and `c`.
- Use nested `IF-ELSIF-ELSE` conditions to find the largest among the three.
- Display the largest number.

**Expected Output:**  
a = 10, b = 9, c = 15  
Largest of three number is 15

```
DECLARE
    a NUMBER := 10;
    b NUMBER := 9;
    c NUMBER := 15;
BEGIN
    IF a > b AND a > c THEN
        DBMS_OUTPUT.PUT_LINE('Largest number is ' || a);
    ELSIF b > c THEN
        DBMS_OUTPUT.PUT_LINE('Largest number is ' || b);
    ELSE
        DBMS_OUTPUT.PUT_LINE('Largest number is ' || c);
    END IF;
END;
/
```
**RESULT:**

<img width="302" height="99" alt="Screenshot 2025-11-21 185400" src="https://github.com/user-attachments/assets/f306e245-3134-4411-94d4-48951e47009e" />


## RESULT
Thus, the PL/SQL programs using variables, conditionals, and loops were executed successfully.
