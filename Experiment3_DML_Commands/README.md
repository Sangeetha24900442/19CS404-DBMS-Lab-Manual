# Experiment 3: DML Commands
### NAME : Sangeetha S
### REG NO : 212224040287
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
Write a SQL statement to Update the per_unit_price to 25 and total_price accordingly in purchases table where purchase_date is '2022-08-15' and product_id is 12.



```
Update purchases
set per_unit_price=25,total_price=25*quantity
where purchase_date ='2022-08-15' and product_id=12;
```

**Output:**

<img width="1849" height="434" alt="Screenshot 2025-11-20 214416" src="https://github.com/user-attachments/assets/2e7b55aa-0cf4-46af-aad9-5e3e24df9f3d" />


**Question 2**
---
Write a SQL statement to Update the hire_date of employees in department 50 to 2024-01-24.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```
update Employees
set hire_date ='2024-01-24'
where department_id='50';

```

**Output:**


<img width="1069" height="230" alt="Screenshot 2025-11-20 214457" src="https://github.com/user-attachments/assets/5d77b671-7ee0-4122-b327-b4b988c504df" />

**Question 3**
---
Write a SQL statement to change the first_name column of employees table with 'John' for those employees whose department_id is 80 and gets a commission_pct below 0.35.

Employees table

---------------
employee_id
first_name
last_name
email
phone_number
hire_date
job_id
salary
commission_pct
manager_id
department_id

```
update employees
set  first_name='John';

```

**Output:**

<img width="1211" height="204" alt="Screenshot 2025-11-20 214510" src="https://github.com/user-attachments/assets/23ecd8a5-a7da-424a-b9fd-b8df6b3c8e5c" />


**Question 4**
---
Write a SQL statement to Update the address to '58 Lakeview, Magnolia' where supplier ID is 5 in the suppliers table.



```
Update Suppliers 
set address ='58 Lakeview, Magnolia'
where supplier_id=5;

```

**Output:**

<img width="970" height="172" alt="Screenshot 2025-11-20 214517" src="https://github.com/user-attachments/assets/5c686085-eb97-4fc1-bbbf-effeb8e778c9" />


**Question 5**
---
Write a SQL query to remove rows from the table 'customer' with the following condition -

1. 'cust_city' should begin with the letter 'L',

Sample table: Customer


```
delete from customer where cust_city like 'L%';

```

**Output:**

<img width="1587" height="456" alt="Screenshot 2025-11-20 214528" src="https://github.com/user-attachments/assets/2a4ae551-ebc5-48fa-a841-ab66ec7279dd" />


**Question 6**
---
Write a SQL query to Delete All Doctors whose ID ranges from 2 to 4.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

```
Delete FROM Doctors
where doctor_id BETWEEN 2 and 4;

```

**Output:**

<img width="1103" height="685" alt="Screenshot 2025-11-20 214538" src="https://github.com/user-attachments/assets/960e4f68-69e3-4f9d-abb9-a395b14114a9" />


**Question 7**
---
Write a SQL query to Delete customers from 'customer' table where 'CUST_NAME' contains the substring 'Holmes'.

```
delete from customer where CUST_NAME LIKE '%Holmes%';

```

**Output:**

<img width="1438" height="277" alt="Screenshot 2025-11-20 214550" src="https://github.com/user-attachments/assets/d1f27b5e-4b9c-44dc-a664-ef77d701b82a" />


**Question 8**
---

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is exactly 2.

```
delete from customer where GRADE=2;
```

**Output:**

<img width="619" height="276" alt="Screenshot 2025-11-20 214556" src="https://github.com/user-attachments/assets/a41e4d50-6efe-411e-acc0-3e77145c6eed" />


**Question 9**
---

Write a SQL query to Delete customers from 'customer' table where 'GRADE' is greater than or equal to 2.
```

Delete from customer where grade >=2;

```

**Output:**

<img width="716" height="262" alt="Screenshot 2025-11-20 214601" src="https://github.com/user-attachments/assets/982a09c2-73d6-4a4b-8a76-d3aa82eb1aaa" />


**Question 10**
---
Write a query to Select all the records from the EmployeeInfo table, where the departments are either HR or Account.
```
select * from Employeeinfo
where department in ('HR','Account');

```

**Output:**


<img width="1444" height="252" alt="Screenshot 2025-11-20 220337" src="https://github.com/user-attachments/assets/7e4bda94-41d6-4482-b505-8eb19da9746a" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
