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
<img width="948" height="556" alt="Screenshot 2025-08-29 161648" src="https://github.com/user-attachments/assets/7637a23c-6bce-4891-ab93-20d0a86dee1f" />


### Entities and Attributes

| Entity | Attributes (PK, FK)                         | Notes |
|--------|---------------------------------------------|-------|                         
| Member |MemberID (PK), Name,MembershipType, StartDate| Stores gym members’ details         |
| Program     | ProgramID (PK), ProgramName, Type                   | Yoga, Zumba, Weight Training, etc.      |
| Trainer        |   TrainerID (PK), Name, Specialization                 |Each trainer may handle multiple programs       |
|  Session      |    SessionID (PK), Date, Time, TrainerID (FK), ProgramID (FK)                |   Personal training or group sessions    |
|Payment        |  PaymentID (PK), MemberID (FK), Amount, PaymentDate, Type                  |     Tracks membership & session payments  |

### Relationships and Constraints

| Relationship | Cardinality | Participation | Notes |
|--------------|------------|---------------|-------|
|  Registers (Member–Program)            | M:N           |  Partial (not all members join all programs)             | A member may join many programs      |
|  AssignedTo (Trainer–Program)            |  M:N          | Total for Program              |   Programs must have at least one trainer    |
|   Books (Member–Trainer–Session)           |  M:N          |  Partial             |  Members may book multiple trainers; sessions linked     |
|Attends (Member–Session)|M:N|Partial|Records attendance|
|PaysFor (Member–Payment)|1:M|Total for Payment|Each payment belongs to one member|
|Covers (Payment–Session/Membership)|1:M|Optional|A payment can cover membership fee or personal session|

### Assumptions

1. Each member must have at least one active membership.

2. A program may have multiple trainers, but at least one is mandatory.

3. Members can attend multiple sessions; attendance is recorded separately.

4. Personal training sessions are modeled as “Session” with specific trainer and member.

5. Payments can be for either membership fees or personal sessions.

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

![WhatsApp Image 2025-08-29 at 18 58 42_b5a3ad44](https://github.com/user-attachments/assets/9d92d91d-842a-4d43-a3c6-f33e8744d90e)

### Entities and Attributes

| Entity       | Attributes (PK, FK)                                                 | Notes                             |
| ------------ | ------------------------------------------------------------------- | --------------------------------- |
| Member       | MemberID (PK), Name, Email, Phone                                   | Library members                   |
| Book         | BookID (PK), Title, Author, Category                                | Books available in the library    |
| Loan         | LoanID (PK), MemberID (FK), BookID (FK), LoanDate, ReturnDate, Fine | Tracks lending/return of books    |
| Event        | EventID (PK), Title, Date, RoomID (FK)                              | Library cultural events           |
| Speaker      | SpeakerID (PK), Name, Topic                                         | Guest speakers/authors for events |
| Room         | RoomID (PK), RoomName, Capacity                                     | Rooms for events and study        |
| Registration | RegID (PK), EventID (FK), MemberID (FK)                             | Members registering for events    |



### Relationships and Constraints

| Relationship | Entities                          | Cardinality | Participation         | Notes                                              |
| ------------ | --------------------------------- | ----------- | --------------------- | -------------------------------------------------- |
| Borrows      | Member ↔ Book (via Loan)          | M\:N        | Total on Loan         | A member can borrow many books; tracked with dates |
| RegistersFor | Member ↔ Event (via Registration) | M\:N        | Total on Registration | Members can register for multiple events           |
| HostedIn     | Event ↔ Room                      | M:1         | Total on Event        | Each event must be held in one room                |
| HasSpeaker   | Event ↔ Speaker                   | M\:N        | Partial               | Events may have multiple speakers                  |
| FineApplied  | Loan ↔ Member                     | 1\:M        | Partial               | Overdue fines applied to member if late return     |



### Assumptions

1. A member must exist before borrowing a book or registering for an event.

2. A book can only be borrowed by one member at a time.

3. Every event must be hosted in exactly one room.

4. Events may have zero or multiple speakers.

5. Overdue fines are calculated and stored in Loan.

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
![WhatsApp Image 2025-08-29 at 18 33 27_1528602a](https://github.com/user-attachments/assets/4ef9001e-8e60-44a9-bf61-af061ac7ae05)

### Entities and Attributes

| Entity      | Attributes (PK, FK)                                           | Notes                               |
| ----------- | ------------------------------------------------------------- | ----------------------------------- |
| Customer    | CustomerID (PK), Name, Phone, Email                           | Restaurant customers                |
| Reservation | ResID (PK), CustomerID (FK), Date, Time, Guests, TableID (FK) | Reservations or walk-ins            |
| Table       | TableID (PK), Capacity                                        | Physical tables available           |
| Order       | OrderID (PK), ResID (FK), OrderTime                           | Orders linked to reservations       |
| Dish        | DishID (PK), Name, Category, Price                            | Menu items (starter, main, dessert) |
| OrderItem   | OrderItemID (PK), OrderID (FK), DishID (FK), Quantity         | Tracks multiple dishes per order    |
| Bill        | BillID (PK), ResID (FK), TotalAmount, ServiceCharge, Date     | Bill generated per reservation      |
| Waiter      | WaiterID (PK), Name, Shift                                    | Waiters assigned to reservations    |



### Relationships and Constraints

| Relationship | Entities                     | Cardinality | Participation        | Notes                                           |
| ------------ | ---------------------------- | ----------- | -------------------- | ----------------------------------------------- |
| Makes        | Customer ↔ Reservation       | 1\:M        | Total on Reservation | Customer can have multiple reservations         |
| AssignedTo   | Reservation ↔ Table          | M:1         | Total on Reservation | Each reservation linked to one table            |
| Places       | Reservation ↔ Order          | 1\:M        | Total on Order       | A reservation can have multiple orders          |
| Contains     | Order ↔ Dish (via OrderItem) | M\:N        | Total on OrderItem   | Orders can contain multiple dishes              |
| Generates    | Reservation ↔ Bill           | 1:1         | Total on Bill        | Each reservation produces one bill              |
| ServedBy     | Reservation ↔ Waiter         | M\:N        | Partial              | A reservation can be served by multiple waiters |

### Assumptions

1. A customer must exist before making a reservation.

2. Walk-in customers are treated as reservations with immediate booking.

3. Each reservation is linked to exactly one table.

4. An order can only be placed after a reservation exists.

5. One bill is generated per reservation (covers food + service).

6. A reservation can be served by one or more waiters.

---

## RESULT

Thus the ER Diagram for each scenario has been drawn and explained successfully.
