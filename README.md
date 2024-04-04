# SQL-Project-1
MIST 4610 - SQL Project 1
1. Shana Sah (https://github.com/shana-sah/SQL-Project-1-) 
2. Maya Patel (https://github.com/mayapatel47488/SQL-Project-1-)
3. Sofia Slavov (https://github.com/sophiaslavovv/SQL-PROJ-1)
4. Cade Mayfield (https://github.com/CaMay999/sql-project-1-)
5. Chris Vitucci (https://github.com/chrisvitucci/SQL-Project-1)


<u>Problem Description:</u>
Pretend you are the owner/operator of a RUNNING association (club)
needing to build a relational database. You hired some students from the MIST 4610 class at
the University of Georgia to create the database for you. They need to know more about your
organization to identify which entities, attributes, and relationships are important for you.
Start by describing your business as a real client.

<u>CHATGPT Response:</u>
As the owner/operator of a running club, our organization is dedicated to promoting health, fitness, and community through the sport of running. We provide a variety of services and activities tailored to runners of all ages and abilities, fostering a supportive environment where individuals can pursue their running goals and connect with like-minded enthusiasts.

Here's a snapshot of our running club:

Group Runs: We organize regular group runs at various locations, including trails, parks, and urban routes, catering to different distances and paces. These group runs serve as opportunities for members to train together, socialize, and enjoy the camaraderie of fellow runners.

Coaching and Training Programs: Our club offers coaching services and structured training programs led by experienced coaches and trainers. These programs are designed to help runners improve their performance, set and achieve personal goals, and stay motivated through structured workouts and personalized guidance.

Events and Races: We host and participate in various running events and races throughout the year, including fun runs, charity races, and competitive events. These events provide members with opportunities to challenge themselves, showcase their skills, and engage in friendly competition within the running community.

Workshops and Seminars: We organize educational workshops, seminars, and guest speaker events covering topics such as nutrition, injury prevention, race strategy, and mental preparation. These events offer valuable insights and resources to help runners enhance their training and overall well-being.

Community Engagement: Our club actively engages with the local community through outreach initiatives, volunteer opportunities, and partnerships with schools, businesses, and other organizations. We seek to promote the benefits of running, encourage participation in physical activity, and support charitable causes aligned with our mission.

Membership: We offer membership options with various benefits, including access to club resources, discounts on coaching services and merchandise, priority registration for events, and exclusive member-only activities.

Equipment and Gear: Our club may provide access to equipment and gear, such as running apparel, shoes, hydration packs, and safety accessories, either through partnerships with vendors or through a club-owned inventory.

Given this overview, the database should encompass key entities such as Members, Coaches, Events, Races, Training Programs, Workshops, Community Partnerships, Equipment, and Transactions, along with their associated attributes and relationships to effectively manage club operations, member registrations, event planning, coaching services, and inventory tracking.

Question 1  asked to CHATGPT: 

What are the relationships? 

Members - Events: Many-to-Many - Recorded via a junction table (e.g., Attendance).

Members - Races: Many-to-Many - Utilizing a junction table (e.g., RaceRegistration).

Members - Training Programs: Many-to-Many - Managed through a junction table (e.g., ProgramEnrollment).

Coaches - Training Programs: One-to-Many - Coach ID foreign key in the Training Programs table.

Members - Feedback: One-to-Many - Feedback table contains Member ID foreign key.

Members - Volunteers: One-to-Many - Volunteers table links to Member ID.

Members - Medical Information: One-to-One - Medical info stored in Members table or separate with one-to-one relationship.

Members - Transactions: One-to-Many - Transactions table includes Member ID foreign key.

Q2: What are the attributes within each entity? 

CHATGPT RESPONSE: Sure! Let's outline the attributes for each of the entities mentioned earlier:

1.Runners:

Runner ID (Primary Key)
First Name
Last Name
Email
Phone Number
Address
Date of Birth
Gender
Emergency Contact Information

2.Coaches:

Coach ID (Primary Key)
First Name
Last Name
Email
Phone Number
Coaching Certification(s)
Specialties/Expertise
Availability (Days/Time)
Bio/Description

3.Events:
Event ID (Primary Key)
Event Name
Event Type (e.g., Group Run, Workshop, Race)
Date
Time
Location
Description
Registration Deadline
Maximum Capacity

4.Races:
Race ID (Primary Key)
Race Name
Date
Location
Distance
Registration Fee
Registration Deadline
Course Map
Sponsors

5.Training Programs:
Program ID (Primary Key)
Program Name
Duration
Focus Areas
Schedule (Days/Time)
Coach ID (Foreign Key)
Description
Enrollment Capacity

6.Community Partnerships:
Partnership ID (Primary Key)
Partner Name
Contact Person
Contact Email
Contact Phone
Partnership Type
Description
Start Date
End Date

7.Workshops/Seminars:
Workshop ID (Primary Key)
Workshop Name
Date
Time
Location
Presenter(s)
Description
Registration Deadline
Maximum Capacity

8.Equipment/Gear:
Item ID (Primary Key)
Item Name
Description
Size/Specification
Quantity Available
Rental Price
Purchase Price
Supplier
Date Acquired

9.Transactions:
Transaction ID (Primary Key)
Member ID (Foreign Key)
Transaction Date
Transaction Type (e.g., Membership Fee, Event Registration, Merchandise Purchase)
Amount
Payment Method


10. Stores
Associative entity
11. Clubs
12. Attendance


-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Data Model:
![Runner Data Model](proj.png)

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Data Model Description:

Runners

The Runners table identifies the ID of the runners, their first and last names, their email, their phone number, and their coach. Each runner has one ID as the primary key of the table. Each runner has one coach, and coach ID is the foreign key that connects runners to the coaches table.

Coaches

The Coaches table is related to the Runners table through the Coach ID(primary key). The Coaches table contains the Coach ID, Coach first and last name, Coach email, and Coaching certification. One coach can have multiple runners and training programs, making it a one-to-many relationship.

Training Programs

The primary key for the training programs table is the Program ID. This table contains the program name, duration, schedule, and focus areas. Coaches ID is the foreign key that references the Coaches table. Coaches can have multiple training programs. Each program has one coach, which makes it a one-to-many relationship.

Recordings

The recordings program is an associative entity between training programs and runners. Runner ID and Program ID are the foreign keys of the table that reference the Runners and Training Program tables. The recordings table identifies training completion and location of the training. Runners can have multiple training programs, and each training program can have multiple recorded entries.

Equipment

This table is used for identifying the equipment ID, the equipment type, and the equipment year. The equipment table’s primary key is the equipment ID. The runner ID is used as a foreign key that references the runner’s table. Each runner can have multiple pieces of equipment.

Medical Information

The medical information table identifies the name of the doctors and the location the doctors were at. The medical ID is the primary key of the table, and runner ID is the foreign key that references the runners table. Each runner has one doctor, making it a one-to-one relationship.

Attendance

Attendance is an associative entity that references the runners and the events tables. Runner ID and event ID are the foreign keys. The attendance table identifies the guest count for each runner as well as the club check-in.

Events

The events table identifies the ID of the event as the primary key, the name of the event, the event type, the event date, and the location of the event.

Races

The races table identifies the race ID as the primary key, the race name, location, date, and distance. The events ID is the foreign key that references the Events table.

Race Registration

The race registration table is an associative entity that references the races and runners tables. Races ID and Runner ID are the foreign keys that reference their respective tables.
Race registration also identifies the race place and race time. Runners can register for multiple races and each race has multiple registrations, making it a many-to-many relationship.

Transactions

The transactions table has a primary key of transaction ID. The Runners ID foreign key references the runners table, and the stores ID references the stores table. Runners can have multiple transactions. Transactions acts as an associative entity between stores and runners.

Stores

Store ID is the primary key of the stores table. The stores table contains the store location and the store products. Each store has multiple transactions, making it a one-to-many relationship.

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Queries:
#1 Show me runners participated in races between january and february:

USE al_Group_21482_G1;
SELECT r.RunnerFirstName, r.RunnerLastName
FROM Runners r
JOIN RaceRegistration rr ON r.idRunners = rr.Runners_idRunners
JOIN Races ra ON rr.Races_idRaces = ra.idRaces
WHERE ra.rDate BETWEEN '2024-01-01' AND '2024-04-28';


Tracking runners who participated in races during a specific time period can help in monitoring their performance over time. Coaches, athletes, and enthusiasts can gain insights into the progress of individual runners by analyzing their race times, improvements, and consistency.

#2 How many runners does each coach have?

SELECT Coaches.CoachFN, Coaches.CoachLN, COUNT(Runners.idRunners) AS NumberOfRunners
FROM Coaches
LEFT JOIN Runners ON Coaches.idCoaches = Runners.Coaches_idCoaches
GROUP BY Coaches.CoachFN, Coaches.CoachLN;

Shows which coaches have the most runners in descending order; used for determining popularity of coaches.The number of runners under each coach allows the company to monitor the performance of coaches in terms of their ability to attract and retain runners.

#3 How many transactions were made at each individual store?

Select sLocation, COUNT(Transactions.TransactionID) AS NumberOfTransactions
FROM Transactions
JOIN Stores on Stores.StoreID=Transactions.Stores_StoreID
GROUP BY sLocation
ORDER BY NumberOfTransactions DESC;


The transaction data from each store can tell how popular each store was,it  identifies where the most purchases are being made and where the least purchases are made.Transaction data can be used to forecast future sales and plan inventory levels accordingly. The data can provide information to plan for customer behavior and preferences towards products.


#4 Report the names of a runner who have a distance higher than their own average distance.


Select RunnerFirstName, RunnerLastName, Distance
From Runners
JOIN RaceRegistration ON Runners.idRunners= RaceRegistration.Runners_idRunners
JOIN Races ON RaceRegistration.Races_idRaces= Races.idRaces
WHERE Distance > (
Select AVG(Distance) FROM 
Races);

Identifying runners who have exceeded their own average distance can provide insights into their performance capabilities and potential for growth. It allows coaches and athletes to recognize achievements, as well as areas where development may be needed.


#5 Find the name of the training program and the number of runners who have completed it, sort the number of completions in descending order

SELECT programName,COUNT(Recordings.Runners_idRunners) AS NumberOfCompletions
FROM Recordings
JOIN TrainingPrograms ON TrainingPrograms.ProgramID = Recordings.TrainingPrograms_ProgramID
Join Runners on Runners.idRunners= Recordings.Runners_idRunners
GROUP BY TrainingPrograms.programName
ORDER BY NumberofCompletions DESC;


This query keeps track of which people have completed which races. Analyzing completion rates can also provide insights into areas for improvement in training programs. Adjustments and enhancements can be displayed to meet the needs of runners/participants.

#6 list and count the names and contact information of the runners who have a guest count greater than 4. Sort in alphabetical order of runner last name

SELECT RunnerFirstName, RunnerLastName, email, PhoneNumber
FROM Runners
WHERE idRunners IN (
    SELECT Runners_idRunners
    FROM Attendance
    GROUP BY Runners_idRunners
    HAVING COUNT(*) > 0
)
ORDER BY RunnerLastName ASC;


This query is useful for retrieving  the names of the guests and attempting to increase participation. Listing the total number of participants who brought lots of guests encourages them to return. Knowing names and contact information of runners who plan to bring more than four guests to an event can help the company or event organizer anticipate attendance numbers accurately. 

#7 What is the total number of races each runner has participated in?

USE al_Group_21482_G1;
SELECT r.idRunners, r.RunnerFirstName, r.RunnerLastName, COUNT(rr.Runners_idRunners) AS TotalRaces
FROM Runners r
LEFT JOIN RaceRegistration rr ON r.idRunners = rr.Runners_idRunners
GROUP BY r.idRunners
ORDER BY TotalRaces DESC;


Understanding the race participation history of each runner helps in tailoring training plans and schedules. Runners with more race experience might require different training approaches compared to those who are relatively new to racing.

#8 List members who participated in both events and races.

USE al_Group_21482_G1;
SELECT RunnerFirstName, RunnerLastName
FROM Runners
WHERE idRunners IN (
 SELECT Runners_idRunners
 FROM RaceRegistration
 )
AND 
 idRunners IN (
 SELECT Runners_idRunners
 FROM `Attendance`
 WHERE guestCount > 0
 );

 
Members who participate in both events and races may demonstrate higher levels of loyalty and commitment to the company.Using this information to understand what motivates these individuals to participate in multiple activities can help the company create programs/events to keep customer loyalty.

#9 Find the event type and event name off all events with the number of attendees listed

SELECT EventName,EventType,guestCount
FROM Events 
JOIN Attendance ON Events.idEvents = Attendance.Events_idEvents;


This query is useful to identify which types of events are most popular and successful in terms of attendance. It allows them to focus on organizing events that resonate with their participants and align with their interests.It helps the company make informed decisions about future event planning

#10 Which runners finished in the top ten and at what event?

 Select RunnerFirstName, RunnerLastName, RacerPlace, idEvents, EventName
 From Runners
 join RaceRegistration on Runners.idRunners= RaceRegistration.Runners_idRunners
 Join Races on Races.idRaces=RaceRegistration.Races_idRaces
 join Events on Events.idEvents=Races.Events_idEvents
 where RacerPlace<11;

This query is useful because the best runners attract the most viewers. By tracking top finishers, we are able to better advertise for future events.




--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Table: Runners

| Column Name        | Description                                                      | Data Type | Size | Format         | Key? |
|--------------------|------------------------------------------------------------------|-----------|------|----------------|------|
| idRunners          | Unique sequential number indicating the runner identification    | INT      | 20   |                | PK   |
| RunnerFirst Name  | The first name of the runner corresponding to a specific ID       | VARCHAR      | 45   |      Text          |      |
| RunnerLast Name   | The last name of the runner corresponding to a specific ID        | VARCHAR     | 45   |      Text          |      |
| email              | The contact email corresponding to a specific ID                  | VARCHAR     | 45   |       Text         |      |
| phoneNumber        | Phone number of runner in question                               | INT     | 10   | (999)999-9999 |      |
| Coaches_idCoaches | The ID of each runner's coach                                     |  INT         |      |                | FK(Reference_Coaches)  |

### Table: Coaches

| Column Name         | Description                                                             | Data Type | Size | Format         | Key? |
|---------------------|-------------------------------------------------------------------------|-----------|------|----------------|------|
| idCoaches           | Unique sequential number indicating the identification number of a coach | INT      | 18   |                | PK   |
| CoachFN             | The first name of the coach corresponding to a specific ID              | VARCHAR     | 45   |           Text     |      |
| CoachLN             | The last name of the coach corresponding to a specific ID               | VARCHAR      | 45   |       Text         |      |
| Coachemail          | The contact email corresponding to a specific Coaches ID                 | VARCHAR      | 45   |      Text          |      |
| CoachingCertification | Document identifying the coach as a legally responsible instructor of athletics | VARCHAR | 45 |  |   |

### Table: Equipment

| Column Name   | Description                                                                   | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------------|-----------|------|--------|------|
| equipmentID   | Unique sequential number indicating the serial number of a piece of equipment | INT      | 20   |        | PK   |
| equipmentType | Identifies what form of equipment the item is.                                | VARCHAR    | 45   |   Text     |      |
| EquipmentYear | The year a piece of equipment was produced                                    | DATE   | 4    | 9999   |      |
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |


### Table: Medical Information

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| MedicalID     | Unique sequential number indicating the identification number of a medical professional | INT | 25 |        | PK   |
| DoctorName    | Name corresponding to each doctor                                       | VARCHAR      | 45   |   Text     |      |
| Doctorlocation| Where the medical practitioner is located                               | VARCHAR     | 45   |   Text     |      |
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |

### Table: Attendance

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |
| Events_idEvents | Unique number corresponding to a specific event                         | INT      | 15   |        | FK (refrence_Events) |
| guestCount    | Number of guests per event                                             | INT    | 3    |        |      |
| Club Check-in | How many of each club attended                                         | VARCHAR     | 45    |    Text    |      |

### Table: Events

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Events_idEvents | Unique number corresponding to a specific event                         | INT      | 15   |        | PK   |
| EventName     | Name of an event                                                        | VARCHAR      | 45   |  Text      |      |
| EventType     | The purpose of the event                                                | VARCHAR      | 45  |  Text      |      |
| date          | When the event is going to occur                                        | DATE   | 8    | 99-99-9999 |    |
| location      | Where the event is going to occur                                       | VARCHAR     | 45   |    Text    |      |

### Table: Races

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| idRaces       | Identification number of a specific race                                | INT     | 20   |        | PK   |
| RaceName      | Name of race                                                            | VARCHAR     | 45  |  Text      |      |
| rLocation     | Location of the race                                                    | VARCHAR     | 45   |  Text      |      |
| rDate         | Race date                                                               | DATE   | 8    | 99-99-9999 |    |
| Distance      | How far is the race                                                     | INT      | 3    | 9.99     |      |
| Events_idEvents | Unique number corresponding to a specific event                         | INT      | 15   |        | FK (Reference_Events) |

### Table: Race Registration

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |
| idRaces       | Identification number of a specific race                                | INT     | 20   |        | FK (reference_Races) |
| RacerPlace    | The finishing position of a runner in a race                            | INT     | 3    |        |      |
| RacerTime     | The time a runner finishes the race in                                  | TIME   | 4    | 99:99  |      |

### Table: Training Programs

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| ProgramID     | The identification number corresponding to a specific training program  | INT     | 20   |        | PK   |
| programName   | The Name of a training program                                          | VARCHAR     | 45   |   Text     |      |
| Date      | When the session is occuring                                                | DATE   | 4    | 99-99-9999  |      |
| FocusAreas    | What is the focus of the workout                                        | VARCHAR     | 45   |  Text      |      |
| Tschedule     | When are these programs available                                        | VARCHAR   | 45   | Text |    |
| Coaches_idCoaches | Unique sequential number indicating the identification number of a coach | INT | 18 | | FK(reference_Coaches) |

### Table: Recordings

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |
| Training Programs_ProgramID | The identification number corresponding to a specific training program  | INT | 20 | | FK(reference_Training Programs) |
| Training Completed | Was the training completed, yes or no?                                  | VARCHAR      | 45    |  Text      |      |
| TrainingLocation | Where do the training sessions                                          | VARCHAR      | 45   |     Text   |      |

### Table: Transactions

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| TransactionID | ID connected to the purchase and transaction of a product               | INT     | 20   |        |      |
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |
| Stores_StoreID | The identification number corresponding to a specific Store             | INT      | 20   |        | FK(reference_Stores) |

### Table: Stores

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Stores_StoreID | The identification number corresponding to a specific Store             | INT      | 20   |        | FK(reference_Stores) |
| sLocation     | Location of a store                                                     | VARCHAR      | 45   |    Text    |      |
| StoreProducts    | Inventory that a store sells                                        | VARCHAR   | 45   | Text |   |

### MATRIX TABLE:

| Query Feature | 1 | 2 | 3 | 4 | 5 | 6 | 7 | 8 | 9 | 10 |
|---------------|---|---|---|---|---|---|---|---|---|----|
| HAVING        |  |   |   |   |   | x  |   |   |   |    |
| WHERE         | x |   |   |  x |   |   |   | x  |   | x   |
| GROUP BY      |   | x | x |   | x | x | x |   |   |    |
| ASC           |   |   |   |   | x |   |   |   |   |    |
| DESC          |   |   | x  |   | x  |  |  |   |   |    |
| COUNT         |  | x | x | x | x | x | x  |   |   |    |
| BETWEEN       | x |   |   |   |   |   |   |   |   |    |
| ORDER BY      |   | x | x |   | x | x |   |  |  |    |
| JOIN          |  | x | x | x | x | x | x |   | x  |   |
| DOUBLE JOIN   | x  |   |   |   |   |   |   |   |   |   |
| TRIPLE JOIN   |   |   |   |   |   |   |   |   |   |  X |
| SUBQUERY      |   |   |  |   |   |  |   | x |   |   |
