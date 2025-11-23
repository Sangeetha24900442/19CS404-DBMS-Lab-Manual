# Experiment 6: Joins
### NAME : Sangeetha S
### REG NO : 212224040287
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
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

```
SELECT p.first_name, p.last_name
FROM patients p
INNER JOIN surgeries s
ON p.patient_id = s.patient_id
WHERE s.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';

```

**Output:**

<img width="814" height="430" alt="Screenshot 2025-11-21 173322" src="https://github.com/user-attachments/assets/7d4ad4de-2cbb-4592-930c-b635e9f435e2" />


**Question 2**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.


```

SELECT 
    o.ord_no,
    o.purch_amt,
    c.cust_name,
    c.city
FROM 
    orders o
JOIN 
    customer c
ON 
    o.customer_id = c.customer_id
WHERE 
    o.purch_amt BETWEEN 500 AND 2000;

```

**Output:**

<img width="1289" height="507" alt="Screenshot 2025-11-21 173333" src="https://github.com/user-attachments/assets/01018ebb-5203-4987-a95d-59751b3ec6c0" />


**Question 3**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), with a left join on the "customer_id" column and a condition filtering for orders with a purchase amount less than 100.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

```

SELECT c.cust_name
FROM customer c
LEFT JOIN orders o
ON c.customer_id = o.customer_id
WHERE o.purch_amt < 100;

```

**Output:**

<img width="751" height="410" alt="Screenshot 2025-11-21 173340" src="https://github.com/user-attachments/assets/443189bf-9c8f-43d0-af76-1996af746d14" />


**Question 4**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "test_results" table (aliased as "t"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

```
SELECT p.first_name AS patient_name, 
       t.result_id, 
       t.patient_id, 
       t.test_name, 
       t.result, 
       t.test_date
FROM patients p
INNER JOIN test_results t
ON p.patient_id = t.patient_id;

```

**Output:**

<img width="1340" height="484" alt="Screenshot 2025-11-21 173411" src="https://github.com/user-attachments/assets/e3b4d839-f4b2-4b9a-b45b-18550e547a09" />


**Question 5**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c") and the "name" column from the "salesman" table (aliased as "s"), with a left join on the "salesman_id" column and a condition filtering for customers in the same city as the salesman.

Customer Table: (customer_id, cust_name, city, grade, salesman_id)

Salesman Table: (salesman_id, name, city, commission)

```
SELECT c.cust_name, 
       s.name
FROM customer c
LEFT JOIN salesman s
ON c.salesman_id = s.salesman_id
WHERE c.city = s.city;

```

**Output:**

<img width="672" height="466" alt="Screenshot 2025-11-21 173422" src="https://github.com/user-attachments/assets/d0db61a1-a28e-44e0-b0f7-c908dc537491" />


**Question 6**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

```
SELECT p.first_name AS patient_name,
       a.appointment_id,
       a.patient_id,
       a.doctor_id,
       a.appointment_date
FROM patients p
INNER JOIN appointments a
ON p.patient_id = a.patient_id;

```

**Output:**

<img width="1351" height="473" alt="Screenshot 2025-11-21 173432" src="https://github.com/user-attachments/assets/7094f8aa-6c06-4e14-8bc5-931f241905f6" />

**Question 7**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  



```
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM customer c
INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;

```

**Output:**

<img width="1283" height="740" alt="Screenshot 2025-11-21 173444" src="https://github.com/user-attachments/assets/6f86b3a5-9227-4f4e-b7a8-c75b1bf50253" />

**Question 8**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

```
SELECT 
    c.cust_name,
    c.city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM customer c
INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
WHERE c.grade < 300 OR c.grade IS NULL
ORDER BY c.customer_id ASC;

```

**Output:**

<img width="1301" height="620" alt="Screenshot 2025-11-21 173453" src="https://github.com/user-attachments/assets/bc9f2b10-0a83-4dca-925d-45964544259a" />


**Question 9**
---
Write a SQL statement to join the tables salesman, customer and orders so that the same column of each table appears once and only the relational rows are returned. 



```
SELECT 
    o.ord_no,
    o.purch_amt,
    o.ord_date,
    c.cust_name,
    c.city AS customer_city,
    c.grade,
    s.name AS salesman_name,
    s.city AS salesman_city,
    s.commission
FROM orders o
JOIN customer c
    ON o.customer_id = c.customer_id
JOIN salesman s
    ON o.salesman_id = s.salesman_id;

```

**Output:**

<img width="1329" height="649" alt="Screenshot 2025-11-21 173509" src="https://github.com/user-attachments/assets/876908f0-d12c-4f55-81fc-89f101657c9d" />



**Question 10**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  


```
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM customer c
INNER JOIN salesman s
    ON c.salesman_id = s.salesman_id
ORDER BY c.customer_id ASC;
```

**Output:**

<img width="1283" height="740" alt="Screenshot 2025-11-21 173444" src="https://github.com/user-attachments/assets/f3ef810a-2a20-403c-bdab-c13db2f7aa93" />



## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
