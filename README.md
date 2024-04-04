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

Data Model: 
![Runner Data Model](/path/to/DM.png)

Queries:
#1 Show me runners participated in races between january and february
SELECT RunnerFirstName,RunnerLastName
FROM Runners
JOIN Race Registration ON Runners.idRunners = Race Registration.idRunners
JOIN Race ON Race Registration.idRaces = Races.idRaces
WHERE rDate BETWEEN ‘01-01-2023 AND 02-28-2023’
-Tracking runners who participated in races during a specific time period can help in monitoring their performance over time. Coaches, athletes, and enthusiasts can gain insights into the progress of individual runners by analyzing their race times, improvements, and consistency. 

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

#11 Report the names of a runner who have a distance higher than their own 
average distance.
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


