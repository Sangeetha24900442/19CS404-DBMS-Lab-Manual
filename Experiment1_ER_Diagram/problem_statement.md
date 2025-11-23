# ER Diagram Workshop – Submission Template
## NAME : Sangeetha S
## REG NO : 212224040287
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
<img width="1039" height="681" alt="Screenshot 2025-08-25 155711" src="https://github.com/user-attachments/assets/4cb15a2f-6040-410b-b120-9b34411af697" />

### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Members| MemberID (PK), Name, MembershipType, StartDate, ContactInfo|Central entity connected to programs, trainers, payments, attendance, and sessions.       |
| Programs| ProgramID (PK), ProgramName, Description, MembersCount|Members join programs; trainers conduct them.       |
| Trainers| TrainerID (PK), TrainerName, Specialization, ContactInfo|Conduct programs and train members.       |
| Payment | PaymentID (PK), Amount, PaymentType, Date, MemberID (FK)|Payments made by members.       |
| PersonalTrainingSession| SessionID (PK), Duration, SessionDate, MemberID (FK), TrainerID (FK)| Booked sessions between member and trainer.      |
| Attendance| AttendanceID (PK), MembershipType, ContactInfo, StartDate, Programs|Tracks attendance for program sessions.       |


### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Members – Joins – Programs             |  M:N          |  Partial             | Members join many programs; programs have many members.      |
| Trainers – Conducts – Programs             |   M:N         | Partial              | Trainers may conduct many programs.      |
|  Trainers – Trains – Members            | 1:M           |  Partial             | A trainer can train multiple members.      |
|Members – Books – PersonalTrainingSession| 1:M           |  Partial             | A member may book many training sessions.      |
|  Trainers – PersonalTrainingSession            | 1:M           |  Total             | A session must be assigned to one trainer.      |
|  Members – MakesPayment – Payment            | 1:M           |  Total on Payment             | Every payment belongs to one member.      |
|  Members – Attends – Programs (Attendance)   | M:N           |  Partial             | Attendance captures member-program sessions.      |


### Assumptions
- Attendance is linked to both Member and Program entities via the “Attends” relationship.
- Payment is only related to Members (not directly to Programs or Trainers).
- Personal training sessions always have one trainer and one member.
- A trainer may conduct programs and train members, but training members is separate from conducting programs.
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
<img width="1142" height="736" alt="Screenshot 2025-08-31 203137" src="https://github.com/user-attachments/assets/7583591d-8528-473d-a9e4-a03392a96e73" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
| Members       | MemberID (PK), Name, MembershipType, Email, ContactInfo | Borrow books, pay fines, register for events.      |
| Books       | BookID (PK), Title, Author, Category, PublicationYear  | Books available for borrowing.       |
| Loans       | LoanID (PK), ReturnDate, DueDate, FineAmount, ProgramID | Represents borrowing of books.      |
| Fines       | FineID (PK), Amount, FineDate, Status, Remarks | Fines for overdue returns.  |
| Events      | EventID (PK), EventName, EventType, EventDate, Duration| Library events members can register for.      |
| Speakers  | SpeakerID (PK), Name, Email, ContactInfo, Biography | Speakers who speak at events.      |
| Rooms      | RoomID (PK), RoomName, Location, Capacity, AvailabilityStatus                   | Rooms used for events.      |


### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Members – Borrows – Books| M:N | Partial | Borrow relationship handled via “Loans”.      |
| Loans – Derived – Fines | 1:1| Partial | Fine generated only if overdue.      |
| Members – Pays – Fines | 1:M| Partial| Member can have many fines.      |
| Members – Registers – Events  | M:N |Partial | Many members register for many events.      |
| Speakers – Speaks – Events | M:N | Partial |Events have multiple speakers.       |
| Events – BookedIn – Rooms |  1:M | Total on Events | Every event must be assigned to a room.      |


### Assumptions
- Fines are directly derived from Loan data when overdue.
- Events are linked to exactly one room via “BookedIn”.
- Speakers can speak at multiple events.
- Loans represent the borrowing record connecting Member and Book.
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
<img width="1111" height="740" alt="Screenshot 2025-08-31 205928" src="https://github.com/user-attachments/assets/58285a86-4eac-47f6-9713-0e96e9564f16" />


### Entities and Attributes

| Entity | Attributes (PK, FK) | Notes |
|--------|--------------------|-------|
|  Customer   |  CustomerID (PK), Name, Email, ContactInfo   | A customer can make reservations and orders.      |
| Reservation       | ReservationID (PK), CustomerID (FK), TableID (FK), Date, Time, NumberOfGuests   | Each reservation is made by a customer and assigned to a table. |
| Table       | TableID (PK), TableNumber, Capacity, Location                   | A table can have many reservations.      |
| Waiter      | WaiterID (PK), Name, ContactInfo, Shift                   | Waiters serve reservations and take orders.      |
| Order       | OrderID (PK), ReservationID (FK), WaiterID (FK), OrderDateTime                   | Every order is linked to a reservation and handled by a waiter.      |
| Dish       | DishID (PK), Name, Category, Price                   | Menu items served in the restaurant.      |
| OrderDetails       | OrderDetailsID (PK), OrderID (FK), DishID (FK), Quantity                    | Stores items included in each order.      |


### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
| Customer – Makes – Reservation  |  1-to-M (One customer can make many reservations) | Customer (partial), Reservation (total) | Every reservation must belong to a customer.|
|Reservation – Assigned table – Table |M-to-1 (Many reservations assigned to one table)| Reservation (total), Table (partial) | A reservation must have one table.|
|Waiter – Served by – Reservation|1-to-M (One waiter serves many reservations) | Waiter (partial), Reservation (partial)|Optional assignment depending on shift.  |
|Reservation – Places – Order |1-to-M| Reservation (partial), Order (total) |Orders are linked to reservations.       |
|Order – Contains – Dish (OrderDetails)|M-to-M via OrderDetails | Both partial | One order contains multiple dishes and a dish appears in multiple orders.      |
| Waiter – Takes – Order | 1-to-M | Waiter (partial), Order (total) | Waiter must be assigned to an order.      |


### Assumptions
- A reservation must always be linked to an existing customer.
- A table can have multiple reservations but not at the same time (time conflicts handled separately). 
- Orders cannot exist without a reservation.-
- A dish must exist in the menu before it can be added to an order.
- Each order must record at least one dish in OrderDetails.

## Instructions for Students

1. Complete **all three scenarios** (A, B, C).  
2. Identify entities, relationships, and attributes for each.  
3. Draw ER diagrams using **draw.io / diagrams.net** or hand-drawn & scanned.  
4. Fill in all tables and assumptions for each scenario.  
5. Export the completed Markdown (with diagrams) as **a single PDF**
