# SQL-Project-1
MIST 4610 - SQL Project 1

Problem Description:
Pretend you are the owner/operator of a RUNNING association (club)
needing to build a relational database. You hired some students from the MIST 4610 class at
the University of Georgia to create the database for you. They need to know more about your
organization to identify which entities, attributes, and relationships are important for you.
Start by describing your business as a real client.

CHATGPT Response:
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

-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

Data Model:
![Runner Data Model](DataM.png)

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

SELECT RunnerFirstName,RunnerLastName
FROM Runners
JOIN Race Registration ON Runners.idRunners = Race Registration.idRunners
JOIN Race ON Race Registration.idRaces = Races.idRaces
WHERE rDate BETWEEN ‘01-01-2023 AND 02-28-2023’

Tracking runners who participated in races during a specific time period can help in monitoring their performance over time. Coaches, athletes, and enthusiasts can gain insights into the progress of individual runners by analyzing their race times, improvements, and consistency.

#2 How many runners does each coach have

Select CoachFN, CoachLN, COUNT(Runners.idRunners) AS NumberOfRunners
FROM Coaches
JOIN Runners ON Coaches.idCoaches=Runners.idCoaches
GROUP BY CoachFN, CoachLN
ORDER BY NumberOfRunners DESC;

Shows which coaches have the most runners in descending order; used for determining popularity of coaches.The number of runners under each coach allows the company to monitor the performance of coaches in terms of their ability to attract and retain runners.

#3 How many transactions were made at each individual store?

Select sLocation, COUNT(Transactions.TransactionID) AS NumberOfTransactions
FROM Transactions
JOIN Stores on Stores.StoreID=Transactions.StoreID
GROUP BY sLocation
ORDER BY NumberOfTransactions DESC, Stores.StoreID

The transaction data from each store can tell how popular each store was,it  identifies where the most purchases are being made and where the least purchases are made.Transaction data can be used to forecast future sales and plan inventory levels accordingly. The data can provide information to plan for customer behavior and preferences towards products.


#4 Display the number of runners having completed training programs

SELECT COUNT(idRunners)
FROM Runners r
JOIN Recordings rc ON r.idRunners=rc.idRunners
WHERE rc.TrainingCompleted = 'Yes';

By displaying the number of runners who complete training programs, the company can assess the effectiveness of the programs they offer. A high completion rate may indicate that the training programs are well-designed and meeting the needs of the runners.

#5 find the name of the training program and the number of runners who have completed it, sort the number of completions in descending order

SELECT programName
COUNT Runner_idRunners AS NumberOfCompletions
FROM Training Programs
JOIN Recordings ON Training Programs.ProgramID = Recordings.Training ProgramsID
GROUP BY Training Programs.programName
ORDER BY NumberofCompletions DESC;

This query keeps track of which people have completed which races. Analyzing completion rates can also provide insights into areas for improvement in training programs. Adjustments and enhancements can be displayed to meet the needs of runners/participants.

#6 list and count the names and contact information of the runners who have a guest count greater than 4. Sort in alphabetical order of runner last name

Select RunnerFirstName, RunnerLastName, email, phoneNumber,
COUNT (*) AS guestCount
FROM Runners
JOIN Attendance ON Runners.idRunners=Attendance.idRunners
GROUP BY RunnerFirstName, RunnerLastName, email, phoneNumber
HAVING guestCount > 4
ORDER BY RunnerLastName ASC;

Retrieving  the names of the guests can increase participation. Listing the total number of participants who brought lots of guests encourages them to return.Knowing names/contact information of runners who plan to bring more than four guests to an event can help the company or event organizer anticipate attendance numbers accurately.

#7 What is the total number of races each runner has participated in

SELECT
    RunnerFirstName,
    RunnerLastName,
    COUNT(rr.idRaces) AS TotalRacesParticipated
FROM Runners
JOIN `Race Registration` rr ON Runners.idRunners = rr.Runners_idRunners
GROUP BY RunnerFirstName, RunnerLastName;

Understanding the race participation history of each runner helps in tailoring training plans and schedules. Runners with more race experience might require different training approaches compared to those who are relatively new to racing.

#8 List members who participated in both events and races

SELECT RunnerFirstName, RunnerLastName
FROM Runners
WHERE idRunners IN (
 SELECT
 Runners_idRunners
 FROM
 `Race Registration`
 )
AND
 idRunners IN (
 SELECT
 Runners_idRunners
 FROM
 `Attendance`
 WHERE
 guestCount > 0
 );
 
Members who participate in both events and races may demonstrate higher levels of loyalty and commitment to the company.Using this information to understand what motivates these individuals to participate in multiple activities can help the company create programs/events to keep customer loyalty.

#9 find the event type and event name off all events with the number of attendees listed

SELECT EventName,EventType,guestCount
FROM Events
JOIN Attendance ON Events.idEvents = attendance.idEvents

They can identify which types of events are most popular and successful in terms of attendance. It allows them to focus on organizing events that resonate with their participants and align with their interests.It helps the company make informed decisions about future event planning

#10 List the runners who have not attended and registered for a race

SELECT RunnerFirstName, RunnerLast Name, Runners.idRunners FROM Runners WHERE NOT EXISTS  (SELECT * FROM Attendance WHERE Attendance.idRunners = Runners.idRunners);
The company  can reach out to these runners to understand their reasons for not participating and address any concerns or obstacles they may have. The company can use this information to develop new race formats, training programs, or other offerings that better cater to the needs of their participants.

#11 Report the names of a runner who have a distance higher than their own average distance.

Select RunnerFirstName, RunnerLastName
From Races r
JOIN Race Registration rr ON r.idRaces=rr.idRaces
JOIN Runners rn ON rn.idRunners=rr.idRunners
WHERE Distance > (
Select AVG(Distance) FROM
Races)

Identifying runners who have exceeded their own average distance can provide insights into their performance capabilities and potential for growth. It allows coaches and athletes to recognize achievements, as well as areas where development may be needed.


#12 Display all personal information of each runner

Select RunnerFirstName, RunnerLastName, email, phoneNumber
FROM Runners

The company can maintain a record of each runner's personal information, enabling personalized communication and improved customer service.They can access relevant customer data to quickly address issues and provide valuable customer care.

--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

### Table: Runners

| Column Name        | Description                                                      | Data Type | Size | Format         | Key? |
|--------------------|------------------------------------------------------------------|-----------|------|----------------|------|
| idRunners          | Unique sequential number indicating the runner identification    | INT      | 20   |                | PK   |
| RunnerFirst Name  | The first name of the runner corresponding to a specific ID       | VARCHAR      | 14   |      Text          |      |
| RunnerLast Name   | The last name of the runner corresponding to a specific ID        | VARCHAR     | 12   |      Text          |      |
| email              | The contact email corresponding to a specific ID                  | VARCHAR     | 20   |       Text         |      |
| phoneNumber        | Phone number of runner in question                               | INT     | 10   | (999)999-9999 |      |
| Coaches_idCoaches | The ID of each runner's coach                                     |  INT         |      |                | FK(Reference_Coaches)  |

### Table: Coaches

| Column Name         | Description                                                             | Data Type | Size | Format         | Key? |
|---------------------|-------------------------------------------------------------------------|-----------|------|----------------|------|
| idCoaches           | Unique sequential number indicating the identification number of a coach | INT      | 18   |                | PK   |
| CoachFN             | The first name of the coach corresponding to a specific ID              | VARCHAR     | 14   |           Text     |      |
| CoachLN             | The last name of the coach corresponding to a specific ID               | VARCHAR      | 12   |       Text         |      |
| Coachemail          | The contact email corresponding to a specific Coaches ID                 | VARCHAR      | 20   |      Text          |      |
| CoachingCertification | Document identifying the coach as a legally responsible instructor of athletics | VARCHAR | 45 |  |   |

### Table: Equipment

| Column Name   | Description                                                                   | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------------|-----------|------|--------|------|
| equipmentID   | Unique sequential number indicating the serial number of a piece of equipment | INT      | 20   |        | PK   |
| equipmentType | Identifies what form of equipment the item is.                                | VARCHAR    | 15   |   Text     |      |
| EquipmentYear | The year a piece of equipment was produced                                    | DATE   | 4    | 9999   |      |
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |


### Table: Medical Information

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| MedicalID     | Unique sequential number indicating the identification number of a medical professional | INT | 25 |        | PK   |
| DoctorName    | Name corresponding to each doctor                                       | VARCHAR      | 30   |   Text     |      |
| Doctorlocation| Where the medical practitioner is located                               | VARCHAR     | 45   |   Text     |      |
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |

### Table: Attendance

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |
| Events_idEvents | Unique number corresponding to a specific event                         | INT      | 15   |        | FK (refrence_Events) |
| guestCount    | Number of guests per event                                             | INT    | 3    |        |      |
| Club Check-in | How many of each club attended                                         | VARCHAR     | 3    |    Text    |      |

### Table: Events

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Events_idEvents | Unique number corresponding to a specific event                         | INT      | 15   |        | PK   |
| EventName     | Name of an event                                                        | VARCHAR      | 25   |  Text      |      |
| EventType     | The purpose of the event                                                | VARCHAR      | 20   |  Text      |      |
| date          | When the event is going to occur                                        | DATE   | 8    | 99-99-9999 |    |
| location      | Where the event is going to occur                                       | VARCHAR     | 45   |    Text    |      |

### Table: Races

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| idRaces       | Identification number of a specific race                                | INT     | 20   |        | PK   |
| RaceName      | Name of race                                                            | VARCHAR     | 25   |  Text      |      |
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
| programName   | The Name of a training program                                          | VARCHAR     | 25   |   Text     |      |
| Date      | When the session is occuring                                                | DATE   | 4    | 99-99-9999  |      |
| FocusAreas    | What is the focus of the workout                                        | VARCHAR     | 15   |  Text      |      |
| Tschedule     | When are these programs available                                        | VARCHAR   | 8    | Text |    |
| Coaches_idCoaches | Unique sequential number indicating the identification number of a coach | INT | 18 | | FK(reference_Coaches) |

### Table: Recordings

| Column Name   | Description                                                             | Data Type | Size | Format | Key? |
|---------------|-------------------------------------------------------------------------|-----------|------|--------|------|
| Runners_idRunners | Unique sequential number indicating the runner identification number of the athlete | INT | 20 | | FK (refrence_Runners) |
| Training Programs_ProgramID | The identification number corresponding to a specific training program  | INT | 20 | | FK(reference_Training Programs) |
| Training Completed | Was the training completed, yes or no?                                  | VARCHAR      | 3    |  Text      |      |
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
| NOT EXISTS    |   |   |   |   |   |   |   |   |   |  x  |
| SUBQUERY      |   |   |  |   |   |  |   | x |   | x   |
