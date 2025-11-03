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
How many patients are there in each city?

Sample table: Patients Table



For example:

Result
Address     TotalPatients
----------  -------------
Berlin      3
Chicago     4
Mexico      3

```sql
select Address, count(*) as TotalPatients from Patients
group by Address;
```

**Output:**

<img width="778" height="491" alt="image" src="https://github.com/user-attachments/assets/b47ed5bc-a9e5-4d0d-aabc-33b53d93ee0d" />


**Question 2**
---
Write SQL query to extract the email domain from each patient's email address and count the number of patients with the same email domain.

Sample table: Patients Table



For example:

Result
EmailDomain  TotalPatients
-----------  -------------
example.com  10

```sql
select substr(Email, instr(Email,'@')+1)as EmailDomain,
count(*) as TotalPatients From Patients
group by EmailDomain;
```

**Output:**


**Question 3**
---
How many appointments are scheduled in each hour of the day?

Sample table:Appointments Table

name                              type
--------------------          ----------
AppointmentID               INTEGER
PatientID                         INTEGER
DoctorID                         INTEGER
AppointmentDateTime   DATETIME
Purpose                           TEXT
Status                              TEXT     

For example:

Result
HourOfDay   TotalAppointments
----------  -----------------
09          2
10          5
11          1
14          1
16          1

```sql
select strftime("%H",AppointmentDateTime) as HourOfDay,
count(*) as TotalAppointments from Appointments group by HourOfDay
order by HourOfDay;
```

**Output:**

<img width="817" height="632" alt="image" src="https://github.com/user-attachments/assets/1f588929-0ba1-41fc-b16e-546ad652c635" />

**Question 4**
---
Write a SQL query to find the total amount of fruits with a unit type of 'LB'.

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
total
----------
225

```sql
select sum(inventory) as total
from fruits where unit ='LB';
```

**Output:**

<img width="805" height="386" alt="image" src="https://github.com/user-attachments/assets/6f245509-cfa2-408c-99f1-b44572a3c1b6" />

**Question 5**
---
Write a SQL query to calculate total available amount of fruits that has a price greater than 0.5 . Return total Count. 

Note: Inventory attribute contains amount of fruits

Table: fruits

name        type
----------  ----------
id          INTEGER
name        TEXT
unit        TEXT
inventory   INTEGER
price       REAL
 

For example:

Result
total_available_amount
----------------------
160

```sql
select sum(inventory) as total_available_amount from fruits where price>0.5;
```

**Output:**

<img width="802" height="396" alt="image" src="https://github.com/user-attachments/assets/8ee5cafb-e64d-4b59-b2ec-b39ea3657a22" />

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

```sql
select sum(income) as total_income from employee where age>=40;
```

**Output:**

<img width="779" height="387" alt="image" src="https://github.com/user-attachments/assets/271f60d0-764a-4cde-937c-1f1df80ae0c0" />

**Question 7**
---
Write a SQL query to find the maximum purchase amount.

Sample table: orders

ord_no      purch_amt   ord_date    customer_id  salesman_id

----------  ----------  ----------  -----------  -----------

70001       150.5       2012-10-05  3005         5002

70009       270.65      2012-09-10  3001         5005

70002       65.26       2012-10-05  3002         5001

 

For example:

Result
MAXIMUM
----------
5760.0

```sql
select max(purch_amt) as MAXIMUM from orders;
```

**Output:**

<img width="726" height="386" alt="image" src="https://github.com/user-attachments/assets/e0c87df6-3923-4580-af79-9f91b6af045f" />

**Question 8**
---
Write the SQL query that achieves the selection of category and calculates the sum of the product of price and category ID as Revenue for each category from the "products" table, and includes only those products where the total revenue is greater than 25.

Sample table: products



For example:

Result
category_id  Revenue
-----------  ----------
1            49.5
2            126
3            79.44

```sql
select category_id, sum(price*category_id) as Revenue
from products
group by category_id having Revenue>25;
```

**Output:**

<img width="764" height="536" alt="image" src="https://github.com/user-attachments/assets/9bededa0-eb82-424e-a50d-a8d46b91b4c6" />

**Question 9**
---
Write the SQL query that achieves the grouping of data by city, calculates the average income for each city, and includes only those cities where the average income is greater than 500,000.

Sample table: employee



For example:

Result
city        AVG(income)
----------  -----------
Arizona     1000000.0
California  2650000.0
Florida     2675000.0

```sql
select city, AVG(income) from employee group by city having avg(income)>500000;
```

**Output:**

<img width="725" height="489" alt="image" src="https://github.com/user-attachments/assets/b2b5e7d5-ad63-46f9-a6f3-067024c87aa5" />

**Question 10**
---
Write the SQL query that accomplishes the grouping of data by joining date (jdate), calculates the minimum work hours for each date, and excludes dates where the minimum work hour is not less than 10.

Sample table: employee1



For example:

Result
jdate       MIN(workhour)
----------  -------------
2002.0      9
2004.0      9
2006.0      9

```sql
select jdate,MIN(workhour) from employee1 group by jdate having min(workhour)<10;
```

**Output:**

<img width="792" height="509" alt="image" src="https://github.com/user-attachments/assets/a6ecbed9-4df1-4e08-83ff-41e7d381ea7f" />


## RESULT
Thus, the SQL queries to implement aggregate functions, GROUP BY, and HAVING clause have been executed successfully.
