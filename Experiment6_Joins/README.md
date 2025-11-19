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
![image](https://github.com/user-attachments/assets/5ff51a78-b6f9-4336-aa23-0aaa88cf71fb)


```sql
SELECT o.ord_no, o.purch_amt, c.cust_name, c.city
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
WHERE o.purch_amt BETWEEN 500 AND 2000;
```

**Output:**

![image](https://github.com/user-attachments/assets/7b3ef239-07da-40c8-9455-e599d436e4a5)


**Question 2**
---
![image](https://github.com/user-attachments/assets/3c1f1c71-acb6-418e-a59c-defec8739f88)


```sql
SELECT c.cust_name AS "Customer Name", 
       c.city AS "city", 
       s.name AS "Salesman", 
       s.city AS "city", 
       s.commission
FROM customer c
JOIN salesman s ON c.salesman_id = s.salesman_id
WHERE c.city <> s.city
AND s.commission > 0.12;
```

**Output:**

![image](https://github.com/user-attachments/assets/4b38188d-a771-4447-9ac4-81031b8a0717)


**Question 3**
---
![image](https://github.com/user-attachments/assets/2965a9b5-994d-49d3-80f6-2673011c97a7)

```sql
SELECT p.first_name AS patient_name, t.test_name
FROM patients p
INNER JOIN test_results t ON p.patient_id = t.patient_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/7872fcb0-e288-43aa-9eee-a13414e17840)


**Question 4**
---
![image](https://github.com/user-attachments/assets/164cc173-32d9-4f28-9120-f419b9bc7e45)


```sql
SELECT o.ord_no, 
       o.ord_date, 
       o.purch_amt, 
       c.cust_name AS "Customer Name", 
       c.grade, 
       s.name AS "Salesman", 
       s.commission
FROM orders o
JOIN customer c ON o.customer_id = c.customer_id
JOIN salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/5f8900a9-41df-43fc-8b9a-bd4c71b6511c)


**Question 5**
---

![image](https://github.com/user-attachments/assets/c18e4ff0-25e2-40c3-ba6b-6a2c94af9aff)

```sql
SELECT c.*
FROM customer c
LEFT JOIN orders o ON c.customer_id = o.customer_id
WHERE o.ord_date > '2012-08-17';
```

**Output:**

![image](https://github.com/user-attachments/assets/1426c153-d78a-4593-b1ba-2dd0ed3a9cca)


**Question 6**
---
![image](https://github.com/user-attachments/assets/80cdaaa1-c17b-4e41-aab6-48c0fa5bf79b)


```sql
SELECT p.first_name, p.last_name
FROM patients p
INNER JOIN surgeries s ON p.patient_id = s.patient_id
WHERE s.surgery_date BETWEEN '2024-01-01' AND '2024-01-31';
```

**Output:**

![image](https://github.com/user-attachments/assets/845f63c8-f46c-420f-b812-c3b7b34e4f39)

**Question 7**
---

![image](https://github.com/user-attachments/assets/05fd4637-1d7b-4c7b-9663-f80b007bb807)

```sql
SELECT p.first_name AS patient_name, d.first_name AS doctor_name
FROM patients p
INNER JOIN doctors d ON p.doctor_id = d.doctor_id
WHERE p.discharge_date IS NOT NULL;
```

**Output:**

![image](https://github.com/user-attachments/assets/d12aae86-e8a7-4bd4-a563-c3a67bc727cf)


**Question 8**
---
![Screenshot 2025-04-29 175118](https://github.com/user-attachments/assets/e2a08b21-ea87-49c3-9acd-c79161b09f96)

```sql
SELECT 
    c.cust_name,
    c.city,
    o.ord_no,
    o.ord_date,
    o.purch_amt AS "Order Amount",
    s.name AS "name",
    s.commission
FROM 
    customer c
LEFT JOIN 
    orders o ON c.customer_id = o.customer_id
LEFT JOIN 
    salesman s ON o.salesman_id = s.salesman_id;
```

**Output:**

![image](https://github.com/user-attachments/assets/1c255f68-1887-4a32-bbcb-87907aa821c0)

**Question 9**
---

![image](https://github.com/user-attachments/assets/00d22a40-251a-4de6-b89b-5dc95aa1409b)

```sql
SELECT 
    s.name AS "name",
    c.cust_name,
    c.city,
    c.grade,
    c.salesman_id
FROM 
    salesman s
LEFT JOIN 
    customer c ON s.salesman_id = c.salesman_id;
```

**Output:**
![image](https://github.com/user-attachments/assets/3c5ed61f-cc3d-4ef0-99bc-821f517fa8fd)


**Question 10**
---
![image](https://github.com/user-attachments/assets/8d1a6592-cdae-4694-925e-fc35a2d38a48)


```sql
SELECT 
    c.cust_name,
    c.city AS city,
    c.grade,
    s.name AS Salesman,
    s.city AS city
FROM 
    customer c
JOIN 
    salesman s ON c.salesman_id = s.salesman_id
ORDER BY 
    c.customer_id ASC;
```

**Output:**

![image](https://github.com/user-attachments/assets/ad83b85e-d5ed-45f1-9962-2a58bba2d230)


## RESULT
Thus, the SQL queries to implement different types of joins have been executed successfully.
