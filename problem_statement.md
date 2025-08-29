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

| Entity    | Attributes (PK, FK)                                   | Notes                                  |
| --------- | ----------------------------------------------------- | -------------------------------------- |
| Customer  | CustomerID (PK), Name, Phone, Email                   | Stores details of customers            |
| MenuItem  | ItemID (PK), Name, Price, Category                    | Food and drinks offered                |
| Order     | OrderID (PK), OrderDate, CustomerID (FK), TotalAmount | Represents a customer’s order          |
| OrderItem | OrderItemID (PK), OrderID (FK), ItemID (FK), Quantity | Junction table for M\:N Order–MenuItem |
| Staff     | StaffID (PK), Name, Role                              | Waiter, Chef, Cashier, etc.            |
| Payment   | PaymentID (PK), OrderID (FK), Amount, Date, Mode      | Payment for the order                  |


### Relationships and Constraints

| Relationship | Entities                         | Cardinality | Participation       | Notes                                     |
| ------------ | -------------------------------- | ----------- | ------------------- | ----------------------------------------- |
| Places       | Customer ↔ Order                 | 1\:M        | Total on Order side | Each customer can place many orders       |
| Contains     | Order ↔ MenuItem (via OrderItem) | M\:N        | Total on OrderItem  | Orders include multiple menu items        |
| ServedBy     | Order ↔ Staff                    | M\:N        | Partial             | An order may be handled by multiple staff |
| Pays         | Customer ↔ Payment               | 1\:M        | Total on Payment    | Customers make payments for orders        |


### Assumptions

1. A customer must place at least one order to exist in the system.

2. Each order is linked to one customer but can include many items.

3. Staff roles may overlap (e.g., same staff can serve and also prepare).

4. Payments are always tied to an order.

5. Menu items may exist without being ordered yet.

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

| Entity     | Attributes (PK, FK)                                     | Notes                              |
| ---------- | ------------------------------------------------------- | ---------------------------------- |
| Student    | StudentID (PK), Name, Major, Year                       | Stores student info                |
| Course     | CourseID (PK), CourseName, Credits                      | Courses offered by the university  |
| Professor  | ProfessorID (PK), Name, Department                      | Professors who teach courses       |
| Enrollment | EnrollmentID (PK), StudentID (FK), CourseID (FK), Grade | Junction entity for Student–Course |
| Department | DeptID (PK), DeptName                                   | University departments             |


### Relationships and Constraints

| Relationship | Entities                          | Cardinality | Participation       | Notes                                                        |
| ------------ | --------------------------------- | ----------- | ------------------- | ------------------------------------------------------------ |
| EnrollsIn    | Student ↔ Course (via Enrollment) | M\:N        | Total on Enrollment | Students can enroll in multiple courses                      |
| Teaches      | Professor ↔ Course                | 1\:M        | Total on Course     | A professor can teach many courses, one professor per course |
| BelongsTo    | Professor ↔ Department            | M\:N        | Partial             | Professors can belong to multiple departments                |
| OfferedBy    | Course ↔ Department               | 1\:M        | Total on Course     | A course belongs to exactly one department                   |

### Assumptions

1. Every student must be enrolled in at least one course.

2. Each course has exactly one primary professor.

3. Grades are assigned only after course completion.

4. A professor may belong to multiple departments (e.g., interdisciplinary roles).

5. Departments may exist even if they don’t currently offer courses.

---

## RESULT

Thus the ER Diagram for each scenario has been drawn and explained successfully.
