# ER Diagram Workshop – Submission Template

## Objective
To understand and apply ER modeling concepts by creating ER diagrams for real-world applications.

## Purpose
Gain hands-on experience in designing ER diagrams that represent database structure including entities, relationships, attributes, and constraints.

---
# Scenario A: City Fitness Club Management

*Business Context:*  
FlexiFit Gym wants a database to manage its members, trainers, and fitness programs.

*Requirements:*  
- Members register with name, membership type, and start date.  
- Each member can join multiple programs (Yoga, Zumba, Weight Training).  
- Trainers assigned to programs; a program may have multiple trainers.  
- Members may book personal training sessions with trainers.  
- Attendance recorded for each session.  
- Payments tracked for memberships and sessions.

### ER Diagram:
Paste or attach your diagram here  
![ER Diagram](er_diagram_fitness.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

# Scenario B: City Library Event & Book Lending System

**Business Context:**  
The Central Library wants to manage book lending and cultural events.

**Requirements:**  
- Members borrow books, with loan and return dates tracked.  
- Each book has title, author, and category.  
- Library organizes events; members can register.  
- Each event has one or more speakers/authors.  
- Rooms are booked for events and study.  
- Overdue fines apply for late returns.

### ER Diagram:
*Paste or attach your diagram here*  
<img width="904" height="386" alt="Screenshot 2025-09-22 132453" src="https://github.com/user-attachments/assets/406cd8ec-3c94-4e85-8df5-a9437ad19b34" />


### Entities and Attributes

| Entity           |                     Attributes (PK, FK)                              | Notes                                                         |
|------------------|------------------------------------------------------------          |---------------------------------------------------------------|
|Customer          | Customer ID(PK),Customer Phone No.,Customer Email,Customer Name      |Stores details of people who register or participate in events.|
|Event Registration| Registration ID (PK),Customer ID (FK),Event ID (FK),Registration Date|Captures customer registrations for events                     |
|Event             | Event ID(PK),Event Name,Event Date,Event Type                        |Represents different events organized                          |
|Speaker           | Speaker ID(PK),Event ID(FK),Speaker Name,Expertise                   |Stores details of speakers                                     |
|Loan              | Loan ID(PK),Customer ID(FK),Loan Date,Return Date,Fine Amount        |Records borrowed items fines if returned late.                 |

### Relationships and Constraints

|Relationship|Cardinality| Participation | Notes |
|------------|-----------|---------------|-------                                                                                                          |
|Registers   |1:M        |Total for Customer,Total for Event Registration|Customer can register for many events,and each registration has one customer.    |
|Is For      |M:1        |Total for Event Registration,Total for Event   |Each registration is linked to exactly one event,but event has many registrations|
|Takes       |1:M        |Total for Loan, Partial for Customer           |A customer may take multiple loans, each loan belongs to exactly one customer.   |
|Has         |M:M        |Total for Event, Total for Speaker             |An event can have many speakers, and a speaker can be invited to many events.    |

### Assumptions
1)Customer

Each customer has a unique Customer ID.

A customer can register for multiple events but must register separately for each event.

A customer may or may not take loans.

2)Event Registration

Acts as a bridge entity between Customer and Event (resolving many-to-many).

A registration must belong to one customer and one event.

Registration ID is unique for each record.

3)Event

Each event has a unique Event ID.

An event can have multiple customers registered.

An event can have multiple speakers, and each speaker can speak at multiple events.

4)Speaker

Each speaker has a unique Speaker ID.

A speaker may be linked to multiple events (many-to-many).

5)Loan

Each loan is uniquely identified by Loan ID.

A loan must be taken by one customer only.

Fine amount is applied only when the return date is later than the due date.

---

# Scenario C: Restaurant Table Reservation & Ordering

**Business Context:**  
A popular restaurant wants to manage reservations, orders, and billing.

**Requirements:**  
- Customers can reserve tables or walk in.  
- Each reservation includes date, time, and number of guests.  
- Customers place food orders linked to reservations.  
- Each order contains multiple dishes; dishes belong to categories (starter, main, dessert).  
- Bills generated per reservation, including food and service charges.  
- Waiters assigned to serve reservations.

### ER Diagram:
*Paste or attach your diagram here*  
![ER Diagram](er_diagram_restaurant.png)

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |
|        |                    |       |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|              |            |               |       |
|              |            |               |       |
|              |            |               |       |

### Assumptions
- 
- 
- 

---

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
