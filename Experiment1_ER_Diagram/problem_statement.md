# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---

# Scenario A: City Fitness Club Management

**Business Context:**  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

**Requirements:**  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.


### ER Diagram:
<img width="1243" height="580" alt="image" src="https://github.com/user-attachments/assets/6b3717f8-2788-4099-af44-91548e6240d1" />


### Entities and Attributes

| Entity           | Attributes (PK, FK)                                         | Notes                                |
| ---------------- | ----------------------------------------------------------- | ------------------------------------ |
| Member           | Member_ID (PK), Name, Membership_Type, Start_Date           | Stores details of gym members        |
| Trainer          | Trainer_ID (PK), Name, Specialization                       | Stores information of gym trainers   |
| Program          | Program_ID (PK), Program_Name, Description                  | Each program offered by gym          |
| Personal_Session | Session_ID (PK), Member_ID (FK), Trainer_ID (FK), Date/Time | For member–trainer personal sessions |
| Payment          | Payment_ID (PK), Member_ID (FK), Amount, Date, Payment_Type | Records payments made by members     |
| Attendance       | Attendance_ID (PK), Session_ID (FK), Status                 | Tracks attendance for each session   |

### Relationships and Constraints

|              |            |               |       |
| Relationship                      | Cardinality | Participation                          | Notes                                    |
| --------------------------------- | ----------- | -------------------------------------- | ---------------------------------------- |
| Member joins Program              | M:N         | Total for Member, Partial for Program  | A member can enroll in multiple programs |
| Trainer assigned to Program       | M:N         | Total for Trainer, Partial for Program | Trainers can conduct multiple programs   |
| Member books Personal_Session     | 1:M         | Partial for Member, Total for Session  | Each session belongs to one member       |
| Trainer conducts Personal_Session | 1:M         | Partial for Trainer, Total for Session | Each session led by one trainer          |
| Member makes Payment              | 1:M         | Partial for Member, Total for Payment  | Member may make several payments         |
| Session has Attendance            | 1:1         | Total for both                         | Tracks attendance per session            |


### Assumptions
- Each member has a unique Member_ID.

- A trainer can handle multiple programs simultaneously.

- Payments include both membership and session fees.

- Attendance is recorded only for scheduled sessions.

- A program can exist without assigned members initially.
---

# Scenario B: City Library Event & Book Lending System


### ER Diagram:
<img width="1246" height="738" alt="image" src="https://github.com/user-attachments/assets/ed263f94-0d85-484b-953b-0dafcb867440" />


### Entities and Attributes

| Entity  | Attributes (PK, FK)                                                       | Notes                                            |
| ------- | ------------------------------------------------------------------------- | ------------------------------------------------ |
| Member  | Member_ID (PK), Name, Membership_Type, Start_Date                         | Library members                                  |
| Book    | Book_ID (PK), Title, Author, Category                                     | Books available for lending                      |
| Loan    | Loan_ID (PK), Member_ID (FK), Book_ID (FK), Issue_Date, Return_Date, Fine | Record of borrowed books                         |
| Event   | Event_ID (PK), Event_Name, Date, Time                                     | Library-organized cultural or educational events |
| Speaker | Speaker_ID (PK), Name, Profession                                         | Guests speaking at events                        |
| Room    | Room_ID (PK), Room_Name, Capacity, Type                                   | Rooms available for study or events              |
| Payment | Payment_ID (PK), Member_ID (FK), Amount, Date, Type                       | Tracks fines and event fees                      |


### Relationships and Constraints

| Relationship               | Cardinality | Participation                        | Notes                                    |
| -------------------------- | ----------- | ------------------------------------ | ---------------------------------------- |
| Member borrows Book        | M:N         | Total for Loan, Partial for Member   | A member can borrow many books           |
| Loan issued for Book       | 1:M         | Total for Loan, Partial for Book     | Each loan tied to one book               |
| Member registers for Event | M:N         | Total for Member, Partial for Event  | Members can attend multiple events       |
| Event has Speaker          | 1:M         | Total for Event, Partial for Speaker | Each event can feature multiple speakers |
| Room booked for Event      | 1:1         | Total for both                       | Each event held in one room              |
| Member makes Payment       | 1:M         | Partial for Member                   | Payment can be for fine or event fee     |


### Assumptions

- A member can borrow multiple books but only return them after the due date is checked.

- Each event must be assigned to one room.

- Fine calculation is handled outside the ER model.

- A speaker can appear in multiple events.

- Each loan record is unique per book-member pair.

---

# Scenario C: Restaurant Table Reservation & Ordering


### ER Diagram:
<img width="1114" height="748" alt="image" src="https://github.com/user-attachments/assets/76cc7c47-04eb-4cd4-a9ed-d69386e24a80" />


### Entities and Attributes
| Entity       | Attributes (PK, FK)                                             | Notes                              |
| ------------ | --------------------------------------------------------------- | ---------------------------------- |
| Customer     | Customer_ID (PK), Name, Phone_No, Email, Address                | Stores customer details            |
| Reservation  | Reservation_ID (PK), Customer_ID (FK), Date, Time, No_Of_Guests | Booking details                    |
| Table        | Table_ID (PK), Table_No, Capacity                               | Restaurant tables                  |
| Waiter       | Waiter_ID (PK), Name, Shift_Time                                | Waiter information                 |
| Dish         | Dish_ID (PK), Dish_Name, Price, Category                        | Menu items served                  |
| Order        | Order_ID (PK), Reservation_ID (FK), Date, Total_Amount          | Orders made under a reservation    |
| Order_Detail | OrderDetail_ID (PK), Order_ID (FK), Dish_ID (FK), Quantity      | Contains multiple dishes per order |
| Bill         | Bill_ID (PK), Reservation_ID (FK), Amount, Date, Payment_Type   | Final billing record               |



### Relationships and Constraints
| Relationship                | Cardinality | Participation                               | Notes                                     |
| --------------------------- | ----------- | ------------------------------------------- | ----------------------------------------- |
| Customer makes Reservation  | 1:M         | Partial for Customer, Total for Reservation | A customer can have multiple reservations |
| Reservation assigned Table  | 1:1         | Total for both                              | Each reservation gets one table           |
| Waiter serves Reservation   | 1:M         | Partial for Waiter                          | A waiter may handle multiple reservations |
| Reservation generates Order | 1:M         | Total for Reservation                       | Each reservation can have multiple orders |
| Order contains Dish         | M:N         | Total for both                              | Each dish may appear in multiple orders   |
| Reservation produces Bill   | 1:1         | Total for both                              | One bill per reservation                  |

### Assumptions
- Each reservation is uniquely identified by Reservation_ID.

- Walk-in customers are assigned a temporary Reservation record.

- Dishes are grouped by category for menu clarity.

- A waiter can be assigned to several tables per shift.

- Bills are generated immediately after the meal.
## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
