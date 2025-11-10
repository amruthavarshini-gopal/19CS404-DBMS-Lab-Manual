# Experiment 6: Joins

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
Write the SQL query that achieves the selection of all columns from the "patients" table, with an inner join on the "doctor_id" column, and includes a condition filtering for patients whose doctors have the first name 'John' and last name 'Smith'.

PATIENTS TABLE:

name             type

---------------  ---------------

patient_id       INT

first_name       VARCHAR(50)

last_name        VARCHAR(50)

date_of_birth    DATE

admission_date   DATE

discharge_date   DATE

doctor_id        INT


DOCTORS TABLE:

name             type

---------------  ---------------

doctor_id        INT

first_name       VARCHAR(50)

last_name        VARCHAR(50)

specialization   VARCHAR(100)

For example:

Result

patient_id       first_name       last_name        date_of_birth    admission_date  discharge_date  doctor_id

---------------  ---------------  ---------------  ---------------  --------------  --------------  ----------

1                Alice            Williams         1980-05-12       2024-01-10                      1

**Program:**
```sql
select p.*
from patients p
inner join doctors d on p.doctor_id=d.doctor_id
where d.first_name="John" and d.last_name="Smith";
```

**Output:**

<img width="1308" height="391" alt="Screenshot 2025-11-10 131758" src="https://github.com/user-attachments/assets/7281673c-afc5-4a14-86ec-bb644f982bad" />


**Question 2**
---
Write the SQL query that achieves the selection of the "cust_name" and "city" columns from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column and a condition filtering for customers in the city 'London'.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

 

For example:

Result

cust_name        city             ord_no           ord_date         purch_amt

---------------  ---------------  ---------------  ---------------  ----------

Brad Guzan       London           70009            2012-09-10       270.65

Julian Green     London           70012            2012-06-27       250.45

**Program:**
```sql
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt
from customer c
left join orders o on c.customer_id=o.customer_id
where c.city='London';
```

**Output:**

<img width="1247" height="431" alt="Screenshot 2025-11-10 131928" src="https://github.com/user-attachments/assets/5be4cdad-0ef4-47a9-baa3-0135b3fc9135" />


**Question 3**
---
Write the SQL query that accomplishes the selection of the first name and last name from the "patients" table, with an inner join on the "patient_id" column and a condition filtering for surgeries with a surgery date between '2024-01-01' and '2024-01-31'.

PATIENTS TABLE:

name             type

---------------  ---------------

patient_id       INT

first_name       VARCHAR(50)

last_name        VARCHAR(50)

date_of_birth    DATE

admission_date   DATE

discharge_date   DATE

doctor_id        INT

SURGERIES TABLE:

name             type

---------------  ---------------

surgery_id       INT

patient_id       INT

surgeon_id       INT

surgery_date     DATE

For example:

Result

first_name       last_name

---------------  ---------------

Alice            Williams

**Program:**
```sql
select p.first_name,p.last_name
from patients p
inner join surgeries s on p.patient_id=s.patient_id
where s.surgery_date BETWEEN  '2024-01-01' and '2024-01-31';
```

**Output:**

<img width="729" height="455" alt="Screenshot 2025-11-10 132036" src="https://github.com/user-attachments/assets/7a5680d2-5810-49ab-b2a3-64f189d3c2c6" />


**Question 4**
---
write a SQL query to find the salesperson and customer who reside in the same city. Return Salesman, cust_name and city.

Sample table: salesman

 salesman_id |    name    |   city   | commission 

-------------+------------+----------+------------

        5001 | James Hoog | New York |       0.15
        
        5002 | Nail Knite | Paris    |       0.13
        
        5005 | Pit Alex   | London   |       0.11
        
        5006 | Mc Lyon    | Paris    |       0.14
        
        5007 | Paul Adam  | Rome     |       0.13
        
        5003 | Lauson Hen | San Jose |       0.12

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001
        
        3007 | Brad Davis     | New York   |   200 |        5001
        
        3005 | Graham Zusi    | California |   200 |        5002
        
        3008 | Julian Green   | London     |   300 |        5002
        
        3004 | Fabian Johnson | Paris      |   300 |        5006
        
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        
        3001 | Brad Guzan     | London     |       |        5005


For example:


Result

Salesman         cust_name        city

---------------  ---------------  ---------------

Bob Emily        Brad Davis       New York

Nail Knite       Fabian Johns     Paris

Pit Alex         Brad Guzan       London

Pit Alex         Julian Green     London

Mc Lyon          Fabian Johns     Paris

**Program:**
```sql
select s.name as Salesman,c.cust_name,c.city
from salesman s
join customer c on s.city=c.city;
```

**Output:**

<img width="1030" height="757" alt="Screenshot 2025-11-10 132136" src="https://github.com/user-attachments/assets/26ff9d81-163f-4778-89bd-b298d4f204ac" />


**Question 5**
---
From the following tables write a SQL query to find those customers with a grade less than 300. Return cust_name, customer city, grade, Salesman, salesmancity. The result should be ordered by ascending customer_id. 

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001
        
        3007 | Brad Davis     | New York   |   200 |        5001
        
        3005 | Graham Zusi    | California |   200 |        5002
        
        3008 | Julian Green   | London     |   300 |        5002
        
        3004 | Fabian Johnson | Paris      |   300 |        5006
        
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 
-------------+------------+----------+------------

        5001 | James Hoog | New York |       0.15
        
        5002 | Nail Knite | Paris    |       0.13
        
        5005 | Pit Alex   | London   |       0.11
        
        5006 | Mc Lyon    | Paris    |       0.14
        
        5007 | Paul Adam  | Rome     |       0.13
        
        5003 | Lauson Hen | San Jose |       0.12

For example:

Result

cust_name        city             grade            Salesman         city
---------------  ---------------  ---------------  ---------------  ----------

Brad Guzan       London           100              Pit Alex         London

Nick Rimando     Chennai          100              Bob Emily        New York

Jozy Altidore    Moscow           200              Paul Adam        Rome

Graham Zusi      California       200              Nail Knite       Paris

Brad Davis       New York         200              Bob Emily        New York

Geoff Cameron    Berlin           100              Lauson Hen       San Jose

**Program:**
```sql
select c.cust_name,c.city,c.grade,s.name as Salesman,s.city
from customer c
join salesman s on c.salesman_id=s.salesman_id
where c.grade<300
order by c.customer_id asc;
```

**Output:**

<img width="1247" height="666" alt="Screenshot 2025-11-10 132257" src="https://github.com/user-attachments/assets/469d43b2-5a07-4928-aef6-0b1d7012b90a" />


**Question 6**
---
From the following tables write a SQL query to display the customer name, customer city, grade, salesman, salesman city. The results should be sorted by ascending customer_id.  

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
 
-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001
        
        3007 | Brad Davis     | New York   |   200 |        5001
        
        3005 | Graham Zusi    | California |   200 |        5002
        
        3008 | Julian Green   | London     |   300 |        5002
        
        3004 | Fabian Johnson | Paris      |   300 |        5006
        
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        
        3001 | Brad Guzan     | London     |       |        5005

Sample table: salesman

 salesman_id |    name    |   city   | commission 
 
-------------+------------+----------+------------

        5001 | James Hoog | New York |       0.15
        
        5002 | Nail Knite | Paris    |       0.13
        
        5005 | Pit Alex   | London   |       0.11
        
        5006 | Mc Lyon    | Paris    |       0.14
        
        5007 | Paul Adam  | Rome     |       0.13
        
        5003 | Lauson Hen | San Jose |       0.12

For example:

Result

cust_name        city             grade            Salesman         city

---------------  ---------------  ---------------  ---------------  ----------

Brad Guzan       London           100              Pit Alex         London

Nick Rimando     Chennai          100              Bob Emily        New York

Jozy Altidore    Moscow           200              Paul Adam        Rome

Fabian Johns     Paris            300              Mc Lyon          Paris

Graham Zusi      California       200              Nail Knite       Paris

Brad Davis       New York         200              Bob Emily        New York

Julian Green     London           300              Nail Knite       Paris

Geoff Cameron    Berlin           100              Lauson Hen       San Jose

**Program:**
```sql
select c.cust_name,c.city,c.grade,s.name as Salesman,s.city
from customer c
inner join salesman s on c.salesman_id=s.salesman_id
order by c.customer_id asc;
```

**Output:**

<img width="1248" height="783" alt="Screenshot 2025-11-10 132400" src="https://github.com/user-attachments/assets/78383b28-4bf6-4b89-b5f0-1ed0221fd5c1" />


**Question 7**
---
SQL statement to generate a report with customer name, city, order number, order date, order amount, salesperson name, and commission to determine if any of the existing customers have not placed orders or if they have placed orders through their salesman or by themselves.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id
 
-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001
        
        3007 | Brad Davis     | New York   |   200 |        5001
        
        3005 | Graham Zusi    | California |   200 |        5002
        
        3008 | Julian Green   | London     |   300 |        5002

        3004 | Fabian Johnson | Paris      |   300 |        5006
        
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        
        3001 | Brad Guzan     | London     |       |        5005

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

70004       110.5       2012-08-17  3009         5003

70007       948.5       2012-09-10  3005         5002

70005       2400.6      2012-07-27  3007         5001

70008       5760        2012-09-10  3002         5001

70010       1983.43     2012-10-10  3004         5006

70003       2480.4      2012-10-10  3009         5003

70012       250.45      2012-06-27  3008         5002

70011       75.29       2012-08-17  3003         5007

70013       3045.6      2012-04-25  3002         5001


Sample table: salesman

 salesman_id |    name    |   city   | commission 
 
-------------+------------+----------+------------

        5001 | James Hoog | New York |       0.15
        
        5002 | Nail Knite | Paris    |       0.13
        
        5005 | Pit Alex   | London   |       0.11
        
        5006 | Mc Lyon    | Paris    |       0.14
        
        5007 | Paul Adam  | Rome     |       0.13
        
        5003 | Lauson Hen | San Jose |       0.12

For example:


Result

cust_name        city             ord_no           ord_date         Order Amount  name        commission

---------------  ---------------  ---------------  ---------------  ------------  ----------  ----------

Nick Rimando     Chennai          70002            2012-10-05       65.26         Bob Emily   0.15

Nick Rimando     Chennai          70008            2012-09-10       5760.0        Bob Emily   0.15

Nick Rimando     Chennai          70013            2012-04-25       3045.6        Bob Emily   0.15

Graham Zusi      California       70001            2012-10-05       150.5         Nail Knite  0.13

Graham Zusi      California       70007            2012-09-10       948.5         Nail Knite  0.13

Brad Guzan       London           70009            2012-09-10       270.65        Pit Alex    0.11

Fabian Johns     Paris            70010            2012-10-10       1983.43       Mc Lyon     0.14

Brad Davis       New York         70005            2012-07-27       2400.6        Bob Emily   0.15

Geoff Cameron    Berlin           70003            2012-10-10       2480.4        Lauson Hen  0.12

Geoff Cameron    Berlin           70004            2012-08-17       110.5         Lauson Hen  0.12

Julian Green     London           70012            2012-06-27       250.45        Nail Knite  0.13

Jozy Altidore    Moscow           70011            2012-08-17       75.29         Paul Adam   0.13

**Program:**
```sql
select c.cust_name,c.city,o.ord_no,o.ord_date,o.purch_amt as 'Order Amount',s.name,s.commission
from customer c
left join orders o on c.customer_id=o.customer_id
left join salesman s on c.salesman_id=s.salesman_id;
```

**Output:**

<img width="1339" height="850" alt="Screenshot 2025-11-10 132545" src="https://github.com/user-attachments/assets/db47dd72-49c1-4f80-950f-317ac5598ab6" />


**Question 8**
---
Write the SQL query that achieves the selection of the "cust_name" column from the "customer" table (aliased as "c"), and the "ord_no," "ord_date," and "purch_amt" columns from the "orders" table (aliased as "o"), with a left join on the "customer_id" column.

'customer' Table: (customer_id, cust_name, city, grade, salesman_id)

'orders' Table: (ord_no, purch_amt, ord_date, customer_id, salesman_id)

 

For example:

Result

cust_name        ord_no           ord_date         purch_amt

---------------  ---------------  ---------------  ---------------

Nick Rimando     70002            2012-10-05       65.26

Nick Rimando     70008            2012-09-10       5760.0

Nick Rimando     70013            2012-04-25       3045.6

Graham Zusi      70001            2012-10-05       150.5

Graham Zusi      70007            2012-09-10       948.5

Brad Guzan       70009            2012-09-10       270.65

Fabian Johns     70010            2012-10-10       1983.43

Brad Davis       70005            2012-07-27       2400.6

Geoff Cameron    70003            2012-10-10       2480.4

Geoff Cameron    70004            2012-08-17       110.5

Julian Green     70012            2012-06-27       250.45

Jozy Altidore    70011            2012-08-17       75.29


**Program:**
```sql
select c.cust_name,o.ord_no,o.ord_date,o.purch_amt
from customer c
left join orders o on c.customer_id=o.customer_id;
```

**Output:**

<img width="888" height="851" alt="Screenshot 2025-11-10 132706" src="https://github.com/user-attachments/assets/d1137e86-f984-4629-9d8b-db55374a37af" />


**Question 9**
---
From the following tables write a SQL query to find those orders where the order amount exists between 500 and 2000. Return ord_no, purch_amt, cust_name, city.

Sample table: customer

 customer_id |   cust_name    |    city    | grade | salesman_id 
 
-------------+----------------+------------+-------+-------------

        3002 | Nick Rimando   | New York   |   100 |        5001
        
        3007 | Brad Davis     | New York   |   200 |        5001
        
        3005 | Graham Zusi    | California |   200 |        5002
        
        3008 | Julian Green   | London     |   300 |        5002
        
        3004 | Fabian Johnson | Paris      |   300 |        5006
        
        3009 | Geoff Cameron  | Berlin     |   100 |        5003
        
        3003 | Jozy Altidor   | Moscow     |   200 |        5007
        
        3001 | Brad Guzan     | London     |       |        5005

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

70004       110.5       2012-08-17  3009         5003

70007       948.5       2012-09-10  3005         5002

70005       2400.6      2012-07-27  3007         5001

70008       5760        2012-09-10  3002         5001

70010       1983.43     2012-10-10  3004         5006

70003       2480.4      2012-10-10  3009         5003

70012       250.45      2012-06-27  3008         5002


70011       75.29       2012-08-17  3003         5007

70013       3045.6      2012-04-25  3002         5001


For example:

Result

ord_no           purch_amt        cust_name        city

---------------  ---------------  ---------------  ---------------

70007            948.5            Graham Zusi      California

70010            1983.43          Fabian Johns     Paris

**Program:**
```sql
select o.ord_no,o.purch_amt,c.cust_name,c.city
from customer c
join orders o on o.customer_id=c.customer_id
where o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

<img width="1238" height="554" alt="Screenshot 2025-11-10 132839" src="https://github.com/user-attachments/assets/31ec02d9-205a-457a-bfa9-eec9a7b8f254" />


**Question 10**
---
Write the SQL query that achieves the selection of the first name from the "patients" table (aliased as "patient_name") and all columns from the "appointments" table (aliased as "a"), with an inner join on the "patient_id" column.

PATIENTS TABLE:

ATTRIBUTES - patient_id, first_name, last_name, date_of_birth, admission_date, discharge_date, doctor_id

<img width="777" height="126" alt="Screenshot 2025-11-10 132923" src="https://github.com/user-attachments/assets/166ca58d-a437-4db9-bce1-dae6c4225986" />

APPOINTMENTS TABLE:

ATTRIBUTES - appointment_id, patient_id, doctor_id, appointment_date

<img width="815" height="370" alt="Screenshot 2025-11-10 133014" src="https://github.com/user-attachments/assets/5a7de46e-33cb-4eb9-b13c-ea96d5b9c909" />

**Program:**
```sql
select p.first_name as patient_name,a.appointment_id,a.patient_id,a.doctor_id,a.appointment_date
from patients p
inner join appointments a on p.patient_id=a.patient_id;
```

**Output:**

<img width="1305" height="457" alt="Screenshot 2025-11-10 133103" src="https://github.com/user-attachments/assets/acf50c18-1c1c-430f-8a15-fe619369de56" />

**SEB Grade-Module 5**
<img width="1167" height="81" alt="image" src="https://github.com/user-attachments/assets/563997f2-f5f8-4b1d-a87d-1c187525703b" />

## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
