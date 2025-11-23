# Experiment 10: PL/SQL – Triggers
### NAME : Sangeetha S
### REG NO : 212224040287
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

**Program**
```
CREATE TABLE employees (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR(100),
    department VARCHAR(50),
    hire_date DATE
);
CREATE TABLE employee_log (
    log_id INT PRIMARY KEY,
    emp_id INT,
    emp_name VARCHAR(100),
    department VARCHAR(50),
    hire_date DATE,
    inserted_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
CREATE OR REPLACE TRIGGER after_employee_insert
AFTER INSERT ON employees
FOR EACH ROW
DECLARE
    new_log_id INT;
BEGIN
    SELECT NVL(MAX(log_id), 0) + 1 INTO new_log_id FROM employee_log;

    INSERT INTO employee_log (
        log_id,
        emp_id,
        emp_name,
        department,
        hire_date,
        inserted_at
    ) VALUES (
        new_log_id,
        :NEW.emp_id,
        :NEW.emp_name,
        :NEW.department,
        :NEW.hire_date,
        SYSTIMESTAMP
    );
END;
/
INSERT INTO employees (emp_id, emp_name, department, hire_date)
VALUES (102, 'Mushafina', 'Information Technology', DATE '2025-05-21');

SELECT * FROM EMPLOYEE_LOG;
```

**Expected Output:**
- A new entry is added to the `employee_log` table each time a new record is inserted into the `employees` table.

![image](https://github.com/user-attachments/assets/35235c08-4d4b-4340-81ad-95cf82093dd7)


## 2. Write a trigger to prevent deletion of records from a sensitive table.
**Steps:**
- Write a **BEFORE DELETE** trigger on the `sensitive_data` table.
- Use `RAISE_APPLICATION_ERROR` to prevent deletion and issue a custom error message.

**Expected Output:**
- If an attempt is made to delete a record from `sensitive_data`, an error message is raised, e.g., `ERROR: Deletion not allowed on this table.`

![image](https://github.com/user-attachments/assets/c258e6a0-c804-47df-b66e-4f11bb6f3fe6)

**Program**
```
CREATE TABLE sensitive_data (
    record_id INT PRIMARY KEY,
    info VARCHAR2(100)
);
INSERT INTO sensitive_data (record_id, info)
VALUES (3, 'Secured'),
       (4, 'COnfidential');

CREATE OR REPLACE TRIGGER prevent_sensitive_deletion
BEFORE DELETE ON sensitive_data
FOR EACH ROW
BEGIN
    RAISE_APPLICATION_ERROR(-20001, 'ERROR: Deletion not allowed on this table.');
END;
/

DELETE FROM sensitive_data WHERE record_id=3;
```

## 3. Write a trigger to automatically update a `last_modified` timestamp.
**Steps:**
- Add a `last_modified` column to the `products` table.
- Write a **BEFORE UPDATE** trigger on the `products` table to set the `last_modified` column to the current timestamp whenever an update occurs.

**Program**
```
CREATE TABLE products (
    product_id INT PRIMARY KEY,
    product_name VARCHAR2(100),
    price NUMBER(10, 2),
    last_modified TIMESTAMP
);
INSERT INTO products (product_id, product_name, price)
VALUES (4, 'Tab', 30000),(5,'HP Laptop',60000),(6,'Smartphone',35000);
CREATE OR REPLACE TRIGGER update_last_modified
BEFORE UPDATE ON products
FOR EACH ROW
BEGIN
    :NEW.last_modified := SYSTIMESTAMP;
END;
/

UPDATE products
SET price = 46000
WHERE product_id = 5;
SELECT * FROM products;
```

**Expected Output:**
- The `last_modified` column in the `products` table is updated automatically to the current date and time when any record is updated.
- 
![image](https://github.com/user-attachments/assets/f03ba488-94ca-476b-bc98-ac97e0c6f099)


## 4. Write a trigger to keep track of the number of updates made to a table.
**Steps:**
- Create an `audit_log` table with a counter column.
- Write an **AFTER UPDATE** trigger on the `customer_orders` table to increment the counter in the `audit_log` table every time a record is updated.

**Program**
```
CREATE TABLE customer_orders (
    order_id INT PRIMARY KEY,
    customer_name VARCHAR2(100),
    product_name VARCHAR2(100),
    quantity INT
);
INSERT INTO customer_orders (order_id, customer_name, product_name, quantity)
VALUES (10, 'Kshira', 'Samsung S23', 5),(11,'Thanushree','HP Laptop',2);
CREATE TABLE audit_log (
    table_name VARCHAR2(50) PRIMARY KEY,
    update_count INT
);
INSERT INTO audit_log (table_name, update_count)
VALUES ('CUSTOMER_ORDERS', 10);
CREATE OR REPLACE TRIGGER track_order_updates
AFTER UPDATE ON customer_orders
FOR EACH ROW
BEGIN
    UPDATE audit_log
    SET update_count = update_count + 1
    WHERE table_name = 'CUSTOMER_ORDERS';
END;
/

UPDATE customer_orders
SET quantity = 3
WHERE order_id = 11;
SELECT * FROM audit_log;
```
**Expected Output:**
- The `audit_log` table will maintain a count of how many updates have been made to the `customer_orders` table.
![image](https://github.com/user-attachments/assets/d5f806eb-3892-4748-b4ef-36e5b0ddf612)


## 5. Write a trigger that checks a condition before allowing insertion into a table.
**Steps:**
- Write a **BEFORE INSERT** trigger on the `employees` table to check if the inserted salary meets a specific condition (e.g., salary must be greater than 3000).
- If the condition is not met, raise an error to prevent the insert.

**Program**
```
CREATE TABLE employeesfor5th (
    emp_id INT PRIMARY KEY,
    emp_name VARCHAR2(100),
    salary NUMBER(10, 2)
);
CREATE OR REPLACE TRIGGER check_salary_before_insert
BEFORE INSERT ON employeesfor5th
FOR EACH ROW
BEGIN
    IF :NEW.salary < 3000 THEN
        RAISE_APPLICATION_ERROR(-20002, 'ERROR: Salary below minimum threshold.');
    END IF;
END;
/
INSERT INTO employeesfor5th (emp_id, emp_name, salary)
VALUES (5, 'Nakshathira', 5000),(7,'Kaavya',7000);
```
**Expected Output:**
- If the inserted salary in the `employees` table is below the condition (e.g., salary < 3000), the insert operation is blocked, and an error message is raised, such as: `ERROR: Salary below minimum threshold.`
![image](https://github.com/user-attachments/assets/987fd423-33de-43d5-8efd-28ab5efe2ca1)

## RESULT
Thus, the PL/SQL trigger programs were written and executed successfully.
