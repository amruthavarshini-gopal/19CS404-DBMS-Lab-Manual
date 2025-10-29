# Experiment 5: Subqueries and Views

## AIM
To study and implement subqueries and views.

## THEORY

### Subqueries
A subquery is a query inside another SQL query and is embedded in:
- WHERE clause
- HAVING clause
- FROM clause

**Types:**
- **Single-row subquery**:
  Sub queries can also return more than one value. Such results should be made use along with the operators in and any.
- **Multiple-row subquery**:
  Here more than one subquery is used. These multiple sub queries are combined by means of ‘and’ & ‘or’ keywords.
- **Correlated subquery**:
  A subquery is evaluated once for the entire parent statement whereas a correlated Sub query is evaluated once per row processed by the parent statement.

**Example:**
```sql
SELECT * FROM employees
WHERE salary > (SELECT AVG(salary) FROM employees);
```
### Views
A view is a virtual table based on the result of an SQL SELECT query.
**Create View:**
```sql
CREATE VIEW view_name AS
SELECT column1, column2 FROM table_name WHERE condition;
```
**Drop View:**
```sql
DROP VIEW view_name;
```

**Question 1**
--
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)



For example:

Result

student_name     grade

---------------  ---------------

Bob              85

Frank            85

John             85

**Program:**

```sql
select g.student_name,g.grade
from GRADES g
where grade=(select min(grade) from GRADES where subject=g.subject);
```

**Output:**

<img width="720" height="495" alt="Screenshot 2025-10-29 101456" src="https://github.com/user-attachments/assets/fc0a7159-a940-4a53-830b-89e8972dc77c" />


**Question 2**
---
From the following tables write a SQL query to find the order values greater than the average order value of 10th October 2012. Return ord_no, purch_amt, ord_date, customer_id, salesman_id.

Note: date should be yyyy-mm-dd format

ORDERS TABLE

name            type

----------     ----------

ord_no          int

purch_amt    real

ord_date       text

customer_id  int

salesman_id  int

For example:

Result

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70005       2400.6      2012-07-27  3007         5001

70008       5760.0      2012-09-10  3002         5001

70003       2480.4      2012-10-10  3009         5003

70013       3045.6      2012-04-25  3002         5001

**Program:**

```sql
select *
from ORDERS
where purch_amt>(select avg(purch_amt) from ORDERS where ord_date='2012-10-10');
```

**Output:**

<img width="1245" height="514" alt="Screenshot 2025-10-29 101647" src="https://github.com/user-attachments/assets/a62f97f8-8f6b-4dab-a877-dd41ba9c4701" />


**Question 3**
---
From the following tables, write a SQL query to determine the commission of the salespeople in Paris. Return commission.

salesman table


name             type

---------------  ---------------

salesman_id      numeric(5)

name                 varchar(30)

city                    varchar(15)

commission       decimal(5,2)

customer table

name         type

-----------  ----------

customer_id  int

cust_name    text

city         text

grade        int

salesman_id  int

For example:

Result

commission

----------
0.14

**Program:**

```sql
select commission
from salesman
where salesman_id IN(
select salesman_id
from customer
where city='Paris'
);
```

**Output:**

<img width="336" height="394" alt="Screenshot 2025-10-29 101748" src="https://github.com/user-attachments/assets/8012e5ba-a074-4a4d-aa7a-3a6c71a8d1fa" />


**Question 4**
---
Write a SQL query to Retrieve the names of customers who have a phone number that is not shared with any other customer.

SAMPLE TABLE: customer

name             type

---------------  ---------------

id               INTEGER

name             TEXT

city             TEXT

email            TEXT

phone            INTEGER

For example:

Result

name

---------------

Aarti Desai

Vivek Sharma

Nisha Patel

Rajesh Singh

Radha Iyer

**Program:**

```sql
select name
from customer
where phone IN(
select phone
from customer
group by phone
having count(*)=1
);
```

**Output:**

<img width="424" height="515" alt="Screenshot 2025-10-29 101855" src="https://github.com/user-attachments/assets/74830cb9-eb97-4a5c-82fe-c13c73052c2a" />


**Question 5**
---
Write a SQL query to retrieve all columns from the CUSTOMERS table for customers whose Address as Delhi and age below 30

Sample table: CUSTOMERS

ID          NAME         AGE       ADDRESS       SALARY

---------  ----------   --------- ----------    ----------


1          Ramesh        32          Ahmedabad      2000

2          Khilan        25          Delhi          1500

3          Kaushik       23          Kota           2000

4          Chaitali      25          Mumbai         6500

5          Hardik        27          Bhopal         8500

6          Komal         22          Hyderabad      4500

7          Muffy         24          Indore         10000

 
 

For example:

Result

ID          NAME        AGE         ADDRESS     SALARY

----------  ----------  ----------  ----------  ----------

2           Khilan      25          Delhi       1500

**Program:**

```sql
select *
from CUSTOMERS
where ADDRESS IN(select ADDRESS from CUSTOMERS where ADDRESS='Delhi' and AGE<30)
ORDER BY ID ASC;
```

**Output:**

<img width="1192" height="414" alt="Screenshot 2025-10-29 102004" src="https://github.com/user-attachments/assets/439d1213-11dd-46ea-84b0-88e1f0af6018" />


**Question 6**
---
From the following tables, write a SQL query to find all the orders generated in New York city. Return ord_no, purch_amt, ord_date, customer_id and salesman_id.

SALESMAN TABLE

name               type

-----------        ----------

salesman_id         numeric(5)

name                varchar(30)

city                varchar(15)

commission          decimal(5,2)

ORDERS TABLE

name               type

----------        ----------

ord_no              int

purch_amt           real

ord_date            text

customer_id         int

salesman_id         int

For example:

Result

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------


70002       65.26       2012-10-05  3002         5001

70005       2400.6      2012-07-27  3007         5001

70008       5760.0      2012-09-10  3002         5001

70013       3045.6      2012-04-25  3002         5001

**Program:**

```sql
select *
from ORDERS
where salesman_id IN(
select salesman_id from SALESMAN where city='New York'
);
```

**Output:**

<img width="1238" height="541" alt="Screenshot 2025-10-29 102128" src="https://github.com/user-attachments/assets/15c311fb-4c19-422a-87b3-0ab6766ab1a6" />

**Question 7**
---
Write a SQL query to List departments with names longer than the average length

Departments Table (attributes: department_id, department_name)

<img width="991" height="177" alt="Screenshot 2025-10-29 102212" src="https://github.com/user-attachments/assets/39b18a17-9086-42ee-a4da-461b19471f24" />


For example:

Result

depar  department_name

-----  ---------------

5      Anesthesiologis

**Program:**

```sql
select department_id as depar,department_name
from Departments
where LENGTH(department_name)>(select avg(LENGTH(department_name)) from Departments);
```

**Output:**

<img width="550" height="457" alt="Screenshot 2025-10-29 102256" src="https://github.com/user-attachments/assets/72445e0a-d256-4b6a-addd-6b5990605798" />


**Question 8**
---
Write a SQL query to Find employees who have an age less than the average age of employees with incomes over 2.5 Lakh

Employee Table

name             type

------------   ---------------

id                 INTEGER

name               TEXT

age                INTEGER

city               TEXT

income             INTEGER

For example:

Result

id     name             age              city             income

-----  ---------------  ---------------  ---------------  ----------

101    Peter            32               NewYork          200000

102    Mark             32               California       300000

103    Donald           25               Arizona          1000000

104    Obama            35               Florida          5000000

105    Linklon          32               Georgia          250000

107    Adam             35               California       5000000

**Program:**

```sql
select *
from Employee
where age<(select avg(age) from Employee where income>250000);
```

**Output:**

<img width="1245" height="513" alt="Screenshot 2025-10-29 102357" src="https://github.com/user-attachments/assets/949b6a12-f345-4a37-894d-c6aff2e9ee31" />


**Question 9**
---
Write a SQL query that retrieves the all the columns from the Table Grades, where the grade is equal to the minimum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="674" height="264" alt="Screenshot 2025-10-29 102457" src="https://github.com/user-attachments/assets/cff245ec-a1f5-4a18-816d-c3d5aee58271" />

For example:

Result

student_id       student_name     subject          grade

---------------  ---------------  ---------------  ---------------

2                Bob              Math             85

6                Frank            Science          85

7                John             Social           85

**Program:**

```sql
select *
from GRADES g
where grade=(select min(grade) from GRADES where subject=g.subject);
```

**Output:**

<img width="1207" height="433" alt="Screenshot 2025-10-29 102547" src="https://github.com/user-attachments/assets/a01dfe6f-221e-4075-92a1-8a09450c7e69" />

**Question 10**
---
Write a SQL query that retrieves the names of students and their corresponding grades, where the grade is equal to the maximum grade achieved in each subject.

Sample table: GRADES (attributes: student_id, student_name, subject, grade)

<img width="678" height="262" alt="Screenshot 2025-10-29 102636" src="https://github.com/user-attachments/assets/15276722-b927-4a4f-bee7-a76e42ab54fb" />

For example:

Result

student_name     grade

---------------  ---------------

Charlie          95

Emma             92

John             85

**Program:**

```sql
select student_name,grade
from GRADES g
where grade=(select max(grade) from GRADES where subject=g.subject);
```

**Output:**

<img width="728" height="489" alt="Screenshot 2025-10-29 102732" src="https://github.com/user-attachments/assets/ac034dda-1c7d-4a2d-9dfd-1d10573ee3d0" />



## RESULT
Thus, the SQL queries to implement subqueries and views have been executed successfully.
