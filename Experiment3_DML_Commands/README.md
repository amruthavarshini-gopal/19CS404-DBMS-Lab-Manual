
# Experiment 3: DML Commands

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
For products with a profit % less than 30% of selling price, update the selling price to provide a profit margin of 35% over cost price of the product in the products table.

PRODUCTS TABLE

name               type

-----------------  ---------------

product_id         INT

product_name       VARCHAR(100)

category           VARCHAR(50)

cost_price         DECIMAL(10,2)

sell_price         DECIMAL(10,2)

reorder_lvl        INT

quantity           INT

supplier_id        INT

**Program:**
```sql
update Products
set sell_price=CAST(cost_price*1.35 AS INTEGER)
where ((sell_price-cost_price)/sell_price)*100<30;
```

**Output:**

<img width="1283" height="465" alt="Screenshot 2025-10-15 103441" src="https://github.com/user-attachments/assets/eee1638b-5db5-492a-b0e0-7b643bc6d635" />


**Question 2**
---
Update the reorder level to 40 pieces for all products belonging to the 'Grocery' category in the products table.

PRODUCTS TABLE

name               type

-----------------  ---------------

product_id         INT

product_name       VARCHAR(100)

category           VARCHAR(50)

cost_price         DECIMAL(10,2)

sell_price         DECIMAL(10,2)

reorder_lvl        INT

quantity           INT

supplier_id        INT

**Program:**
```sql
update PRODUCTS
set reorder_lvl=40
where category='Grocery';
```

**Output:**
<img width="1278" height="388" alt="Screenshot 2025-10-15 103611" src="https://github.com/user-attachments/assets/be095130-ea35-4ebe-9508-c1c093e3f0d5" />


**Question 3**
---
Write a SQL statement to Increase the selling price per unit by 5% for product ID 15 who's sale is on '2023-01-31'.
sales(sale_id,sale_date,product_id,quantity,sell_price,total_sell_price)

**Program:**
```sql
update sales
set sell_price=sell_price*1.05
where product_id=15 and sale_date='2023-01-31';
```

**Output:**

<img width="1266" height="414" alt="Screenshot 2025-10-15 103809" src="https://github.com/user-attachments/assets/363fdb85-b91e-4fe0-994d-f5539b39e27a" />


**Question 4**
---
Write a SQL statement to Increase quantity of all products by 10% to adjust for surplus stock counted

Products table

---------------
product_id

product_name

category

cost_price

sell_price

reorder_lvl

quantity

supplier_id

**Program:**
```sql
update Products
set quantity=quantity*1.10;
```

**Output:**

<img width="1262" height="556" alt="Screenshot 2025-10-15 103949" src="https://github.com/user-attachments/assets/6b86f81e-70c2-494c-ac1b-c3f05693db09" />


**Question 5**
---
Increase the reorder level by 30% for products from 'Food' category having quantity in stock less than 50% of existing reorder level in the products table

name               type

--------------  ----------

product_id         INT

product_name       VARCHAR(10)

category           VARCHAR(50)

cost_price         DECIMAL(10)

sell_price         DECIMAL(10)

reorder_lvl        INT

quantity              INT

supplier_id           INT

**Program:**
```sql
update products
set reorder_lvl=reorder_lvl*1.30
where category='Food' and quantity<(reorder_lvl*0.50);
```

**Output:**
<img width="1271" height="379" alt="Screenshot 2025-10-15 104156" src="https://github.com/user-attachments/assets/3effdfca-fd3b-4014-9aab-7da839da3e90" />


**Question 6**
---
Write a SQL query to Delete customers with 'GRADE' 2 and 'CUST_NAME' starting with 'M', and whose 'PAYMENT_AMT' is less than 3000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

**Program:**
```sql
delete from Customer
where GRADE=2 and CUST_NAME LIKE 'M%' and PAYMENT_AMT<3000;
```

**Output:**

<img width="1262" height="382" alt="Screenshot 2025-10-15 104400" src="https://github.com/user-attachments/assets/62923938-97ba-4799-a730-c400979bdf0c" />


**Question 7**
---
Write a SQL query to Delete customers with 'GRADE' 3 or 'AGENT_CODE' 'A008' whose 'OUTSTANDING_AMT' is less than 5000

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

**Program:**
```sql
delete from Customer
where (GRADE=3 or AGENT_CODE='A008') and OUTSTANDING_AMT<5000;
```

**Output:**

<img width="1261" height="371" alt="Screenshot 2025-10-15 104905" src="https://github.com/user-attachments/assets/2fb9d1e2-b7da-42b8-b0dd-b9c5aeda874a" />


**Question 8**
---
Write a SQL query to Delete all Doctors whose Specialization is either 'Pediatrics' or 'Cardiology' and Last Name is Brown.

Sample table: Doctors

attributes : doctor_id, first_name, last_name, specialization

**Program:**
```sql
delete from Doctors
where specialization IN('Pediatrics','Cardiology') and last_name='Brown';
```

**Output:**
<img width="1057" height="806" alt="Screenshot 2025-10-15 105055" src="https://github.com/user-attachments/assets/2ca4d776-d141-45e4-a46a-54ccb6ff4427" />


**Question 9**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is odd.

Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

**Program:**
```sql
delete from Customer
where GRADE%2!=0
```

**Output:**
<img width="1268" height="403" alt="Screenshot 2025-10-15 105208" src="https://github.com/user-attachments/assets/88d9b173-620c-4c8c-a1ca-65b7ae035b8b" />


**Question 10**
---
Write a SQL query to Delete customers from 'customer' table where 'GRADE' is greater than or equal to 2.

 
Sample table: Customer

+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+  
|CUST_CODE  | CUST_NAME   | CUST_CITY   | WORKING_AREA | CUST_COUNTRY | GRADE | OPENING_AMT | RECEIVE_AMT | PAYMENT_AMT |OUTSTANDING_AMT| PHONE_NO     | AGENT_CODE |
+-----------+-------------+-------------+--------------+--------------+-------+-------------+-------------+-------------+---------------+--------------+------------+
| C00013    | Holmes      | London      | London       | UK           |     2 |     6000.00 |     5000.00 |     7000.00 |       4000.00 | BBBBBBB      | A003       |
| C00001    | Micheal     | New York    | New York     | USA          |     2 |     3000.00 |     5000.00 |     2000.00 |       6000.00 | CCCCCCC      | A008       |
| C00020    | Albert      | New York    | New York     | USA          |     3 |     5000.00 |     7000.00 |     6000.00 |       6000.00 | BBBBSBB      | A008       |

**Program:**
```sql
delete from Customer
where GRADE>=2;
```


**Output:**

<img width="701" height="622" alt="Screenshot 2025-10-15 105400" src="https://github.com/user-attachments/assets/d1149c93-d596-4897-aa84-b52210c77c04" />


## RESULT
Thus, the SQL queries to implement DML commands have been executed successfully.
