# Experiment 4: Aggregate Functions, Group By and Having Clause
### Name : Sangeetha S
### Reg No : 212224040287
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
---
What is the average dosage prescribed for each medication?
```
select Medication,avg(Dosage) as AvgDosage
from Prescriptions
group by Medication;

```

**Output:**

<img width="494" height="554" alt="Screenshot 2025-11-20 222644" src="https://github.com/user-attachments/assets/c2c19f4d-fdb2-49a4-a493-4c89ea6fd5af" />


**Question 2**
---
How many appointments are scheduled in each hour of the day?

```
select Strftime('%H',APPointmentDateTime) as HourOfDay , 
count(*)as TotalAppointments
from Appointments
group by HourOfDay
order by HourOfDay;

```

**Output:**

<img width="532" height="419" alt="Screenshot 2025-11-20 222637" src="https://github.com/user-attachments/assets/e7337a2e-fb08-4f69-9ac6-32b7776f94b8" />



**Question 3**
---
How many doctors specialize in each medical specialty?

```
select Specialty,count(*) as TotalDocto
from Doctors
group by Specialty ;

```

**Output:**


<img width="502" height="520" alt="Screenshot 2025-11-20 222630" src="https://github.com/user-attachments/assets/3125cd9c-88eb-489e-b9be-00e605dd9ac2" />

**Question 4**
---

Write a SQL query that counts the number of unique salespeople. Return number of salespeople.


```
select count(DISTINCT salesman_id) as COUNT
from orders;

```

**Output:**

<img width="453" height="264" alt="Screenshot 2025-11-20 222620" src="https://github.com/user-attachments/assets/0c621d41-60b9-4829-8e4d-546bbdcf0fe3" />


**Question 5**
---
Write a SQL query to find  how many employees work in California?

```
select count(id) as employees_in_california
from employee
where city = 'California';

```

**Output:**

<img width="481" height="256" alt="Screenshot 2025-11-20 222614" src="https://github.com/user-attachments/assets/4618421f-658d-4c02-b64b-51e258521958" />


**Question 6**
---
Write a SQL query to Calculate the average email length (in characters) for people who lives in Mumbai city

```
select avg(length(email)) as avg_email_length_below_30
from customer
where city = 'Mumbai';
```

**Output:**

<img width="476" height="266" alt="Screenshot 2025-11-20 222608" src="https://github.com/user-attachments/assets/ec647183-6d03-43d3-884d-a762a76f0207" />


**Question 7**
---
Write a SQL query to find the Fruit with the lowest available quantity.

Note: Inventory attribute contains amount of fruits

```
select name as fruit_name,min(inventory) as lowest_quantity
from fruits
order by inventory Asc
Limit 1;

```

**Output:**

<img width="509" height="261" alt="Screenshot 2025-11-20 222601" src="https://github.com/user-attachments/assets/30e96680-1ed2-4491-a1eb-be9351783502" />



**Question 8**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the average work hours for each occupation, and includes only those occupations where the average work hour falls between 10 and 12.

```
select occupation,AVG(workhour)
from employee1
group by occupation
having avg(workhour) between 10 and 12;

```

**Output:**

<img width="517" height="319" alt="Screenshot 2025-11-20 222554" src="https://github.com/user-attachments/assets/bf2f2caf-0f31-43f4-a892-60bce94eda83" />



**Question 9**
---
Write the SQL query that accomplishes the grouping of data by addresses, calculates the sum of salaries for each address, and excludes addresses where the total salary sum is not greater than 2000.



```
select address,sum(salary) as 'SUM(salary)'
from customer1
group by address
having sum(salary) > 2000;

```

**Output:**

<img width="497" height="379" alt="Screenshot 2025-11-20 222545" src="https://github.com/user-attachments/assets/3f1d032e-17da-4622-93a0-52aa2a21c82b" />



**Question 10**
---
Write the SQL query that achieves the grouping of data by occupation, calculates the total work hours for each occupation, and excludes occupations where the total work hour sum is not greater than 20.

```
select occupation,SUM(workhour)
from employee1
group by occupation
having SUM(workhour) >20;

```

**Output:**

<img width="503" height="356" alt="Screenshot 2025-11-20 222536" src="https://github.com/user-attachments/assets/1a4992a4-4ca0-49d6-955f-513047a1d42a" />



## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
