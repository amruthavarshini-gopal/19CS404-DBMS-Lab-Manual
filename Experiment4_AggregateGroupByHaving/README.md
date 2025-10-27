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
How many prescriptions were written in each frequency category (e.g., once daily, twice daily)?

Sample tablePrescriptions Table



For example:

Result

Frequency      TotalPrescriptions

-------------  ------------------

Every 3 weeks  1

Every 6 hours  1

Once           1

Once daily     4

Once daily at  1

Pending        1

Twice daily    1

**Program:**
```sql
select frequency,count(*) as TotalPrescriptions
from Prescriptions
group by frequency;
```

**Output:**

<img width="746" height="590" alt="Screenshot 2025-10-27 132324" src="https://github.com/user-attachments/assets/f85d872e-fb74-4383-ad06-f7eea83a0003" />


**Question 2**
---
How many patients have insurance coverage valid in each year?

Sample table:Insurance Table

name               type

-----------------  ----------

InsuranceID        INTEGER

PatientID          INTEGER

InsuranceCompany   TEXT

PolicyNumber       TEXT

PolicyHolder       TEXT

ValidityPeriod     TEXT

For example:

Result

ValidityYear  TotalPatients

------------  -------------

2024          3

2025          1

2027          4

2031          2

**Program:**
```sql
select strftime('%Y',ValidityPeriod) as ValidityYear,count(*) as TotalPatients
from Insurance
group by ValidityPeriod;
```

**Output:**

<img width="643" height="452" alt="Screenshot 2025-10-27 132624" src="https://github.com/user-attachments/assets/f0b75264-9501-4c62-9282-9f277f11e6af" />


**Question 3**
---
How many medical records were created in each month?

Sample table:MedicalRecords Table

<img width="961" height="146" alt="Screenshot 2025-10-27 132855" src="https://github.com/user-attachments/assets/24e40f59-226e-4134-8f22-93aff00887ff" />

For example:

Result

Month       TotalRecords

----------  ------------

2023-12     2

2024-01     6

2024-02     2


**Program:**
```sql
select strftime('%Y-%m',Date) as Month,count(*) as TotalRecords
from MedicalRecords
group by strftime('%Y-%m',Date);
```

**Output:**

<img width="580" height="486" alt="Screenshot 2025-10-27 132947" src="https://github.com/user-attachments/assets/5b3e6fa4-2500-4cde-a18b-b9fd87ffc395" />


**Question 4**
---
Write a SQL query to determine the number of customers who received at least one grade for their activity.

Sample table: customer

customer_id |   cust_name    |    city    | grade | salesman_id 

-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001

        3007 | Brad Davis     | New York   |   200 |        5001

        3005 | Graham Zusi    | California |   200 |        5002

 

For example:

Result

COUNT

----------

8

**Program:**
```sql
select count(grade>1) as 'COUNT'
from customer;
```

**Output:**

<img width="326" height="366" alt="image" src="https://github.com/user-attachments/assets/4c7b05aa-2d0f-4f84-b4e9-1183106f2070" />


**Question 5**
---
Write a SQL query to find the number of employees whose age is greater than 32.

Sample table: employee

<img width="297" height="164" alt="Screenshot 2025-10-27 133302" src="https://github.com/user-attachments/assets/0194b7dd-7d20-4b31-ada1-f2e5e1ac5c51" />

 

For example:

Result

COUNT

----------

5

**Program:**
```sql
select sum(age>32) as 'COUNT'
from employee;
```

**Output:**

<img width="344" height="377" alt="Screenshot 2025-10-27 133515" src="https://github.com/user-attachments/assets/9ef29430-7610-4ec3-b3ee-70be6ce551f0" />


**Question 6**
---
Write a SQL query to find the total income of employees aged 40 or above.

Table: employee

name        type

----------  ----------

id          INTEGER

name        TEXT

age         INTEGER

city        TEXT

income      INTEGER

For example:

Result

total_income

------------

1800000

**Program:**
```sql
select sum(income) as total_income
from employee
where age>=40;
```

**Output:**

<img width="377" height="368" alt="Screenshot 2025-10-27 133641" src="https://github.com/user-attachments/assets/18cd289c-0f53-422f-a47c-92260aaca162" />


**Question 7**
---
Write a SQL query to find the number of employees who are having the same age removing the duplicate values.

Sample table: employee

<img width="272" height="159" alt="Screenshot 2025-10-27 133721" src="https://github.com/user-attachments/assets/39e99d43-7700-4eb1-a5a8-379e41fa2c7b" />

For example:

Result

COUNT

----------

4

**Program:**
```sql
select count(distinct age) as 'COUNT'
from employee;
```

**Output:**

<img width="339" height="375" alt="Screenshot 2025-10-27 133818" src="https://github.com/user-attachments/assets/ae9355dc-f4fd-4526-9756-84787b50bdb5" />


**Question 8**
---
Which cities (addresses) in the "customer1" table have an average salary lesser than Rs. 15000
Sample table: customer1
For example:

Result

address     AVG(salary)

----------  -----------

Ahmedabad   2000.0

Bhopal      8500.0

Delhi       1500.0

Hyderabad   4500.0

Indore      10000.0

Kota        2000.0

Mumbai      6500.0

**Program:**
```sql
select address,avg(salary) as 'AVG(salary)'
from customer1
group by address
having avg(salary)<15000;
```

**Output:**

<img width="579" height="668" alt="Screenshot 2025-10-27 134156" src="https://github.com/user-attachments/assets/67ca3e23-0fb8-429c-93c1-ede5b37c7a33" />

**Question 9**
---
Write the SQL query that performs grouping by age groups and displays the maximum salary for each group, excluding groups where the maximum salary is not greater than 8000. 

Note: Calculate the age group as multiples of 5.

Eg., 20,22,23 comes in age group 20. 

25,27,29 comes in age group 25.

Sample table: customer1

For example:

Result

age_group   MAX(salary)

----------  -----------

20          10000

25          8500

**Program:**
```sql
select (age/5)*5 as age_group,max(salary) as 'MAX(salary)'
from customer1
group by (age/5)*5
having max(salary)>8000;
```

**Output:**

<img width="570" height="412" alt="Screenshot 2025-10-27 134340" src="https://github.com/user-attachments/assets/e02f7387-7507-4d88-8768-e4510d3e8f24" />


**Question 10**
---
Write the SQL query that achieves the grouping of data by age intervals using the expression (age/5)5, calculates the total salary sum for each group, and excludes groups where the total salary sum is not greater than 5000.

Sample table: customer1

For example:

Result

age_group   SUM(salary)

----------  -----------

20          16500

25          16500

**Program:**
```sql
select (age/5)*5 as age_group,sum(salary) as 'SUM(salary)'
from customer1
group by (age/5)*5
having sum(salary)>5000;
```

**Output:**

<img width="571" height="412" alt="Screenshot 2025-10-27 134455" src="https://github.com/user-attachments/assets/a1710c1c-d746-4676-8c37-f864fd226e21" />


**SEB Grade-Module 3**

<img width="1258" height="112" alt="image" src="https://github.com/user-attachments/assets/469b8b81-0348-4d46-86d3-53e6c45bbeea" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
