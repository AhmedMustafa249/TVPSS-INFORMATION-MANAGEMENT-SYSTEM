##### Software Engineering Dept
Faculty of Computing
Universiti Teknologi Malaysia
```
Software Design Description (SDD)
```
```
Televisyen Pusat Sumber Sekolah (TVPSS)
```
Prepared by: Bit Buddies
Document No. : <<Document ID>>
WPC Ref. No. : <<Work Package Contract Ref. No.>>
```
Revision : <<Document Revision Number>>
```
Date Issued : 28 JANUARY 2025
Prepared by Reviewed by Approved by
HDaniel
```
Name(s) HAFIY DANIELBIN HASROM Name
```
MUHAMMAD
AIMAN HAIQAL
BIN
SALEHUDDIN
Name
DR. ADILA
FIRDAUS BINTI
ARBAIN
Position Design Lead Position Design Manager Position Project Director
1. Frontispiece
a. Overview
The current system documentation includes sections on the introduction, specific
requirements, system architectural design, detailed component descriptions, data
design, user interface design, and a requirements matrix. The introduction outlines
the purpose, scope, definitions, acronyms, abbreviations, and references. Specific
```
requirements cover interfaces, system features (including use cases, requirements,
```
```
constraints, and software system attributes). The detailed component descriptions
```
further elaborate on these requirements, while the data design focuses on the
database structure.
b. Issuing Organization / Project Team Members
Member Names Roles Tasks Status
Auni Najwa Binti
Alizar
Back-End Developer Design and maintain
the server-side
infrastructure,
manage databases,
secure user data,
optimize
performance, and
ensure system
scalability.
Completed
Hafiy Danial Bin
Hasrom
Project Manager,
Front-End Developer,
Accuracy Checker
Oversee project
development,
coordinate the team,
manage resources
and risks, ensure
timely delivery, and
develop a responsive
user interface. Check
and compile the
report
Completed
Muhammad Aiman
Haiqal
Back-End Developer,
Skeptic
Develop and
maintain server logic,
manage databases,
secure user data,
and ensure system
reliability and
Completed
1
scalability. Give
query and comment
on the assignment
and compile EA file.
Syed Muhammad
Naufal bin Syed
Zulkhairul Iskandar
Front-End Developer Design and
implement a
user-friendly
interface, ensuring a
seamless user
experience across
different devices.
Completed
c. Version Control History
VERSION ISSUE DATE DETAILS OF REVISION
1.0 31/12/2024 Completed Assignment 1 requirement details
2.0 22/01/2025 Completed design pattern in Assignment 2 for the system
3.0 28/01/2025 Completed Project 1
2
Table of Contents
1 Frontispiece 1
2 Introduction 5
2.1 Purpose 5
2.2 Scope 5
2.3 Context 6
2.4 Summary 6
3 References 8
4 Glossary 9
5 Design Body 10
5.1 Design Stakeholders and Their Concerns 10
5.2 Context Viewpoint 10
5.2.1 Design Concerns 10
```
5.2.2 Design View (Use Case Diagram) 12
```
```
5.3 Logical Viewpoint (Architecture Style Diagram) 49
```
5.3.1 Design Concerns 49
```
5.3.2 Design View (Class Diagram) 50
```
```
5.4 Information Viewpoint (DB Design) 52
```
5.4.1 Design Concerns 52
```
5.4.2 Design View (ERD Diagram) 53
```
5.5 Interface Viewpoint 58
5.5.1 Design Concerns 58
```
5.5.2 Design View (Interfaces Wireframe) 59
```
```
5.6 Structure Viewpoint (Behavioral + Structural Pattern) 60
```
5.6.1 Design Concerns 60
3
```
5.6.2 Design View (Class Diagram) 61
```
```
5.7 Interaction Viewpoint (Creational Pattern + Sequence) 63
```
5.7.1 Design Concerns 63
```
5.7.2 Design View (Class + Sequence Diagram) 74
```
```
5.8 Algorithm Viewpoint (Decision Table) 98
```
5.8.1 Design Concerns 98
```
5.8.2 Design View (Activity Diagram / Decision Tables) 99
```
6 User Interface Design 100
7 Appendices 107
4
2. Introduction
2.1 Purpose
This SD describes the requirements for a file and record management system
```
that will be developed for Television Pusat Sumber Sekolah (TVPSS). SD is
```
important to be completed as it will be used by the developer to describe the
entire system to the stakeholder. The details of the system will be explained
into multiple parts to enhance deliverability and clarity of understanding the
system. The requirements in this SD are elicited from the stakeholders of
TVPSS through a workshop that is being conducted online on 26 April 2024.
The intended audience for this SD are the stakeholders of TVPSS.
2.2 Scope
TVPSS Management System is an Information Management System
designed to replace the existing manual management system. Based on the
requirement of the stakeholders, TVPSS Management System will be
designed as a PWA that is primarily featured in managing all the information
flows such as information retrieval, information modification and information
validation. There are four main modules that are involved in this system which
are Dashboard and Administration Module, School Information Management
Module, School Version Management Module, Student Achievement
Management Module, Donation Management Module, and Equipment Report
Management Module. This system is designed to increase efficiency and
effectiveness of the TVPSS Management System.The TVPSS Managaement
System has 3 main objectives aligned with. The following are the significant
objectives to ensure the proposed system to be highly efficient and performs
well.
5
2.3 Context
This standard is intended for technical and managerial stakeholders who
prepare and use SDDs. It guides designer in the selection, organization, and
presentation of design information. For an organization developing its own
SDD practices, the use of this standard can help to ensure that design
descriptions are complete, concise, consistent, interchangeable, appropriate
for recording design experiences and lessons learned, well organized, and
easy to communicate…
2.4 Summary
```
This System Design Document (SDD) for the TVPSS Management
```
Information System outlines the key architectural and design aspects of the
system to ensure its development aligns with the project's requirements and
goals. The document is structured to provide a clear understanding of the
system's design and serves as a reference for all stakeholders involved.
The document begins with the architectural style and rationale, explaining the
chosen architectural approach and justifying its suitability for the system. It
also includes a component model that details the main components of the
system and their interactions. The use case diagram provides a high-level
view of system functionality, identifying the interactions between users and the
system. Additionally, a complete package diagram illustrates the logical
grouping of system components to show how they are organized and related.
The modules detailed description offers an in-depth explanation of each
module's responsibilities, functionality, and role within the overall system. The
data design section focuses on the database structure, including key data
entities and relationships that ensure efficient data storage and retrieval.
Lastly, the user interface design describes the visual and interactive elements
of the system to ensure usability and a seamless user experience.
6
This document serves as a comprehensive guide to the system's architecture
and design, providing a solid foundation for development, implementation,
and maintenance.
7
3. References
Specify complete list of references using a standardized reference format.
4. Sommerville, I. 2016. “Software Engineering”, 10th Edition, Pearson.
5. Tailwind Labs. (n.d.). Tailwind CSS. Tailwind CSS. Retrieved from
```
https://tailwindcss.com/
```
3. Facebook, Inc. (2021). React: A JavaScript library for building user interfaces.
Retrieved from https://react.dev/
4. Laravel. (n.d.). Laravel: The PHP framework for web artisans. Laravel.
Retrieved from https://laravel.com/
5. Google. (n.d.). Flutter: Beautiful native apps in record time. Flutter. Retrieved
from https://flutter.dev/
6. Oracle Corporation. (n.d.). MySQL: The world's most popular open-source
database. MySQL. Retrieved from https://www.mysql.com/
7. Axios. (n.d.). Promise based HTTP client for the browser and node.js. Axios.
Retrieved from https://axios-http.com/
8. Microsoft Corporation. (n.d.). Visual Studio Code. Visual Studio Code.
Retrieved from https://code.visualstudio.com/
8
9. Glossary
Definitions of all terms, acronyms and abbreviation used are to be defined here.
10. TVPSS - Televisyen Pusat Sumber Sekolah
11. SD - System Documentation
12. PWA - Progress Web Application
9
13. Design Body
5.1 Design Stakeholders and Their Concerns
The success of the TVPSS Management Information System depends on
addressing the needs and concerns of all design stakeholders involved. The
project sponsor is primarily concerned with ensuring that the system's
functionality aligns with the project's goals, is delivered on time and within
budget, and is scalable and reliable to support future growth. The system
administrators, including state admins, PPD admins, school admins, and
super admins, prioritize user-friendly interfaces for managing data and
processes, robust role-based access controls for secure operations, and
minimal downtime with fast issue resolution.
The TVPSS management crew focuses on having comprehensive
dashboards and real-time data insights, streamlined workflows for managing
applications, donations, and results, as well as reliable reporting features for
monitoring performance. For students, the main concerns are intuitive and
secure systems for viewing application results, safeguarding their personal
information, and ensuring efficient and error-free application submissions.
Similarly, donors require a transparent donation process, user-friendly
interfaces, and confidence in the system's security for financial transactions.
By addressing these diverse concerns, the system design ensures usability,
security, scalability, and maintainability, meeting the expectations of all
stakeholders involved.
5.2 Context Viewpoint
5.2.1 Design Concerns
The Context viewpoint provides a high-level “black box” perspective of the
TVPSS Management Information System, focusing on its offered services and
its interactions with users and other stakeholders in the system’s environment.
The primary purpose of the Context viewpoint is to identify the design
```
subject’s offered services, the actors (users and interacting stakeholders), and
```
10
to establish clear system boundaries. This ensures the effective delineation of
the system’s scope of use and operation, helping stakeholders understand
how the system fits within its broader environment.
The system provides key features such as role-based dashboards, application
management, donation tracking, and reporting tools, tailored to meet the
specific needs of different stakeholders. Actors interacting with the system
```
include administrators (state admin, PPD admin, school admin, and super
```
```
admin), students, donors, and other external users. By defining these
```
boundaries and interactions, the Context viewpoint ensures a focused and
structured design approach, enabling the system to deliver its intended
services effectively while addressing the needs and expectations of its users
and stakeholders.
5.2.2 Design View
The system features include user management for admins, school and student
information management , school version status tracking, student achievement
record-keeping, donation processing with payment integration, and equipment
damage reporting, ensuring efficient administration and streamlined operations
within the TVPSS Management Information System.
11
Figure 2.1: Use Case Diagram for TVPSS
12
5.2.2.1 UC001: Use Case View Dashboard
Use Case ID UC001
Use Case
Name
View Dashboard
Actors 1. Super admin
2. School admin
3. State admin
4. PPD admin
Description This use case allows the actors to access a centralized
dashboard that displays key information relevant to their roles.
Each actor has role-specific data presented in a user-friendly
format. The dashboard provides actionable insights and a
summary of the system's activities and metrics
Precondition The actor must be logged into the system with valid credentials
and assigned the appropriate role.
Postcondition The dashboard is displayed with the relevant information tailored
to the actor’s role.
Main Flow 1. The actor logs into the system successfully.
5. The system verifies the actor’s role and permissions.
6. The system retrieves data relevant to the actor’s role:
a. Super Admin: Overview of total users based on
roles.
b. State Admin: Summary of schools within the
state, schools’ TVPSS version summary, students’
certificates summary, students’ achievement
summary.
c. PPD Admin: Summary of schools under the
district, pending TVPSS applications, and
performance metrics.
d. School Admin: Details of the school’s activities,
including application results, donation records, and
13
version status.
7. The system displays the dashboard with role-specific
data.
Alternate flow AF1: Invalid session
8. The system redirects to the login page if the actor’s
session is invalid or expired.
```
AF2: Type of Days
```
1. The user selects their preferred view type: daily, weekly,
or monthly..
2. The system displays the data corresponding to the
selected view
```
AF3: Logout
```
1. The user clicks the logout button.
2. The system logs out the user, exits the dashboard page,
and redirects them to the Welcome Page.
14
```
UC002: Use Case Manage User Information
```
Use Case ID UC002
Use Case
Name
Manage User Information
Actors Super Admin
Description This use case enables the Super Admin to manage user
accounts within the system. This includes creating, updating, and
deleting user information, as well as assigning roles. The Super
Admin can ensure that only authorized personnel have access to
the system.
Precondition The Super Admin must be logged into the system with valid
credentials.
Postcondition User information is successfully created, updated, or deleted in
the system database.
Main Flow 1. The Super Admin logs into the system successfully.
2. The Super Admin selects the Pengurusan Pengguna
option from the main menu.
3. The system displays the user management interface,
```
including the list of users and available actions (Create,
```
```
Update, Delete).
```
4. The Super Admin performs the following actions:
a. Create User:
i. Enter the new user’s details (e.g., role,
name, email, role, password, state and
```
district).
```
ii. Submits the form, and the system saves
the new user to the database.
b. Update User:
i. Selects an existing user.
ii. Modifies the user’s details or role.
iii. Submits the changes, and the system
15
updates the information in the database.
c. Delete User:
i. Selects an existing user.
ii. Confirms the deletion.
iii. The system removes the user from the
database.
5. The system displays a confirmation message after each
action.
Alternate flow AF1: Invalid session
6. The system redirects to the login page if the actor’s
session is invalid or expired.
```
AF2: Search users
```
1. The user enters either Nama Penuh, Alamat Email,
Negeri, or Jenis Pengguna to search for a user.
2. The system displays the results based on the user's input.
```
AF3: Number of users
```
1. The user clicks the "Bilangan Data" dropdown button to
```
select the number of users to display (5, 10, or 25).
```
2. The system displays the user list based on the user's
selection.
```
AF4: Pagination
```
1. The user clicks the "Selepas" or "Sebelum" button to
navigate through the user's data when it exceeds the
display limit.
2. The system redirects to the next or previous page
accordingly.
```
AF5: Logout
```
1. The user clicks the logout button.
2. The system logs out the user, exits the Pengurusan
Pengguna page, and redirects them to the Welcome
Page.
16
5.2.2.2 UC003: Use Case Manage School Information
Use Case ID UC003
Use Case
Name
Manage School Information
Actors School Admin
Description This use case allows the School Admin to manage their school's
information within the system. This includes updating school
details, managing contact information, and maintaining relevant
data to ensure the school profile is accurate and up to date.
Precondition The School Admin must be logged into the system with valid
credentials.
Postcondition The school information is successfully created and updated in the
system database.
Main Flow 1. The School Admin logs into the system successfully.
3. The School Admin selects the Informasi Sekolah option
from the main menu.
4. The system displays the school management interface
with current school details.
5. The School Admin performs the following actions:
a. Update School Details:
i. Edits fields such as school name, address,
contact information, and other relevant
data.
ii. Submits the changes, and the system
updates the school record in the database.
6. The system displays a confirmation message after the
changes or verification is completed.
Alternate flow AF1: Logout
7. The user clicks the logout button.
8. The system logs out the user, exits the Pengurusan
Pengguna page, and redirects them to the Welcome
17
Page.
```
AF2: Cancel button
```
1. The user clicks the "Batal" button.
2. The system discards all changes made by the user.
Exception EF1: Invalid Input
3. If the School Admin enters invalid or incomplete
information, the system highlights the errors and prompts
for correction.
18
5.2.2.3 UC004: Use Case Manage Student Information
Use Case ID UC004
Use Case
Name
Manage Student Information
Actors School Admin
Description This use case allows the School Admin to manage the student
information for their school. This includes adding new students,
updating existing student records, and removing students who
have left the school. The School Admin ensures the student
database remains accurate and up-to-date.
Precondition The School Admin must be logged into the system with valid
credentials.
Postcondition The student information is successfully added, updated, or
deleted in the system database.
Main Flow 1. The School Admin logs into the system successfully.
4. The School Admin selects the Senarai Pelajar option
from the main menu.
5. The system displays the student management interface
with the list of current students.
6. The School Admin performs the following actions:
a. Add Student:
i. Enters new student details, such as name,
identification number, email and other
required data.
ii. Submits the form, and the system saves
the new student record in the database.
b. Update Student Information:
i. Selects an existing student from the list.
ii. Modifies student details, such as updated
contact information or grade level.
iii. Submits the changes, and the system
19
updates the student record.
c. Delete Student:
i. Selects a student to be removed.
ii. Confirms the deletion.
iii. The system removes the student record
from the database.
7. The system displays a confirmation message after each
action.
Alternate flow AF1: Invalid session
8. The system redirects to the login page if the actor’s
session is invalid or expired.
```
AF2: Search students
```
1. The user enters either Nama Penuh, No Kad Pengenalan
or Email to search for a student.
2. The system displays the results based on the user's input.
```
AF3: Number of students
```
1. The user clicks the "Bilangan Data" dropdown button to
```
select the number of students to display (5, 10, or 25).
```
2. The system displays the student list based on the user's
selection.
```
AF4: Pagination
```
1. The user clicks the "Selepas" or "Sebelum" button to
navigate through the student’s data when it exceeds the
display limit.
2. The system redirects to the next or previous page
accordingly.
```
AF5: Logout
```
1. The user clicks the logout button.
2. The system logs out the user, exits the Pengurusan
Pengguna page, and redirects them to the Welcome
Page.
20
5.2.2.4 UC005: Use Case Validate School Crew Application
Use Case ID UC005
Use Case
Name
Validate School Crew Application
Actors 1. School Admin
Description This use case allows the School Admin to validate and process
applications submitted by individuals applying to be part of the
school crew. The validation process includes reviewing the
application details and approving or rejecting the application
based on eligibility and criteria.
Precondition 1. The School Admin must be logged into the system with
valid credentials.
3. Applications must be submitted and available for review in
the system.
Postcondition The application is validated and marked as approved or rejected
in the system
Main Flow 1. The School Admin logs into the system successfully.
4. The School Admin selects the Permohonan Krew option
from the main menu.
5. The system displays the list of pending applications.
6. The School Admin selects an application to review.
7. The system displays the application details, including:
a. Applicant’s personal details (e.g., name, contact
```
information).
```
b. Role applied for in the school crew.
6. The School Admin performs the following actions:
a. Verify Details:
i. Ensures all provided information is
accurate and complete.
b. Approve Application:
i. Confirms the applicant meets all criteria.
21
ii. Marks the application as approved, and the
system updates the status.
c. Reject Application:
i. Identifies missing or incorrect information
or determines the applicant does not meet
criteria.
ii. Marks the application as rejected, and the
system updates the status.
Alternate flow AF1: Invalid session
7. The system redirects to the login page if the actor’s
session is invalid or expired.
```
AF2: Search students
```
1. The user enters either Nama Penuh, No Kad Pengenalan,
Jawatan or Status to search for a crew.
2. The system displays the results based on the user's input.
```
AF3: Number of students
```
1. The user clicks the "Bilangan Data" dropdown button to
```
select the number of crew to display (5, 10, or 25).
```
2. The system displays the crew list based on the user's
selection.
```
AF4: Pagination
```
1. The user clicks the "Selepas" or "Sebelum" button to
navigate through the crew’s data when it exceeds the
display limit.
2. The system redirects to the next or previous page
accordingly.
Exceptional EF1: Invalid Data
3. If the data is invalid, the system does not update the
application's status to "approved”.
22
5.2.2.5 UC006: Use Case View Application Result
Use Case ID UC006
Use Case
Name
View Application Result
Actors 1. School Admin
4. Student
Description This use case allows students to view the status and results of
their submitted applications. The School Admin can also view
and verify the results for their school’s students, ensuring
transparency and accuracy.
Precondition 1. The student must have a valid account and have
submitted an application.
5. The School Admin must be logged in with valid
credentials.
Postcondition The application result is successfully displayed to the actor.
Main Flow 1. Students:
a. The student logs into the system using an IC
number.
b. The student navigates to the Keputusan
Permohonan section.
c. The system displays a list of the student’s
submitted applications with their current status.
d. The student selects an application to view detailed
results.
6. School Admin:
a. The School Admin logs into the system.
b. The School Admin selects the Permohonan Krew
option from the main menu.
c. The system displays a list of applications
submitted by students for their school.
d. The School Admin selects an application to view
23
detailed results
Alternate flow AF1: Search result
7. The student enters either Jawatan or Status to search for
a result.
8. The system displays the results based on the student’s
input.
```
AF2: Action button
```
1. The student clicks on the Lihat button.
2. The system will display a popup message with
information, including the status of the application, which
can be "Diterima," "Dalam Proses," or "Ditolak."
Exceptional EF1: No application found
3. If no applications are found for the student or school
admin, the system displays a message indicating there
are no records.
24
5.2.2.6 UC007: Use Case Submit School Crew Application
Use Case ID UC007
Use Case
Name
Submit School Crew Application
Actors Student
Description This use case allows students to submit an application for a
school crew position. The process includes providing personal
details and selecting the desired role.
Precondition The student must have a valid account and be logged into the
system.
Postcondition The application is successfully submitted and stored in the
system for review by the School Admin.
Main Flow 1. The student logs into the system.
4. The student navigates to the Permohonan Krew section.
5. The system displays the application form, which includes
fields for:
a. Personal details (e.g., name, identification number,
```
contact information).
```
b. Desired role in the school crew.
4. The student fills in the required fields.
5. The student submits the application.
6. The system stores the application in the database and
displays a confirmation message.
Exception EF1: Data Validation
7. If the student fails to fill in all required fields, the system
highlights the missing information and prompts the
student to complete the form.
25
5.2.2.7 UC008: Use Case View School Version Status
Use Case ID UC008
Use Case
Name
View School Version Status
Actors 1. PPD Admin
8. State Admin
Description This use case allows the State Admin to view the version status
of TVPSS deployed in schools under their jurisdiction. The
version status includes information about the current version and
status of the version.
Precondition 1. The State Admin or PPD Admin must be logged into the
system with valid credentials.
9. Version information must be available in the system for
schools.
Postcondition The State Admin or PPD Admin successfully views the version
status for each school.
Main Flow PPD Admin:
10. The PPD Admin logs into the system.
11. The PPD Admin selects the Informasi TVPSS Sekolah
option from the main menu.
12. The system displays a list of schools under the PPD
Admin’s jurisdiction that needs to be verified whether it
should be Diterima or Ditolak for the version.
State Admin:
13. The State Admin logs into the system.
14. The State Admin selects the Informasi TVPSS Sekolah
option from the main menu.
15. The system displays a list of schools in the State Admin’s
jurisdiction and each schools’ version status.
Alternate flow AF1: Search result
16. The user enters either Nama Sekolah, Pegawai, Versi or
26
Status to search for a result.
17. The system displays the results based on the user’s input.
```
AF2: Pagination
```
1. The user clicks the "Selepas" or "Sebelum" button to
navigate through the school’s data when it exceeds the
display limit.
2. The system redirects to the next or previous page
accordingly.
```
AF3: Update version TVPSS
```
1. The user clicks on the pencil icon button.
2. The system displays the update school version page,
where the user can approve or reject the request from the
school.
27
5.2.2.8 UC009: Use Case Verify School Version Status
Use Case ID UC009
Use Case
Name
Verify School Version Status
Actors 1. PPD Admin
3. State Admin
Description This use case allows the PPD Admin to verify the accuracy and
completeness of the TVPSS version status information for
schools within their assigned district.
Precondition 1. The PPD Admin must be logged into the system with valid
credentials.
4. Version status information for schools must be available in
the system
Postcondition The system records the verification and confirms the current
version status for each school as reviewed.
Main Flow PPD Admin
5. The PPD Admin logs into the system.
6. The PPD Admin selects the Informasi TVPSS Sekolah
option from the main menu.
7. The system displays a list of schools within the PPD
Admin’s jurisdiction, along with their current version
statuses.
8. The PPD Admin performs the following actions for each
```
school:
```
a. Approving TVPSS version
i. Reviews the displayed version information
```
(schools’s information, TVPSS information,
```
```
current version).
```
ii. Confirms that the school version status is
accurate and up to date.
iii. Approve Application:
28
1. Confirms the TVPSS information
meets all criteria.
2. Marks the request as approved,
and the system updates the status.
iv. Reject Application:
3. Identifies missing or incorrect
information or determines the
request does not meet criteria.
4. Marks the application as rejected,
and the system updates the status.
State Admin
5. The State Admin logs into the system.
6. The State Admin selects the Informasi TVPSS Sekolah
option from the main menu.
7. The system displays a list of schools within the State
Admin’s jurisdiction, along with their current version
statuses.
8. The State Admin performs the following actions for each
```
school:
```
a. Approving TVPSS version
i. Reviews the displayed version information
```
(schools’s information, TVPSS information,
```
```
current version).
```
ii. Confirms that the school version status is
accurate and up to date.
iii. Approve Application:
1. Confirms the TVPSS information
meets all criteria.
2. Marks the request as approved,
and the system updates the status.
iv. Reject Application:
3. Identifies missing or incorrect
information or determines the
request does not meet criteria.
4. Marks the application as rejected,
29
and the system updates the status.
Exception
Flow
```
EF1: Data Validation
```
1. If the student fails to fill in all required fields, the system
highlights the missing information and prompts the
student to update version status interface.
5.2.2.9
30
5.2.2.10 UC010: Use Case Manage School Version Status
Use Case ID UC010
Use Case
Name
Manage School Version Status
Actors School Admin
Description This use case allows the school admin to manage and submit the
version status of their school's TVPSS. This includes tracking the
current version, and TVPSS information.
Precondition The School Admin must be logged into the system with valid
credentials.
Postcondition The school’s version status is successfully submitted to be
reviewed and approved from PPD Admin and State Admin.
Main Flow 1. The School Admin logs into the system.
2. The School Admin navigates to the Submit Versi TVPSS
section.
3. The system displays the school information form:
4. School Admin updates school information.
5. The system displays the school’s TVPSS information
form.
6. School Admin fills the required fields.
7. School Admin submit the form.
8. The system stores the application in the database and
displays a confirmation message.
Alternate flow AF1: Reset button
9. The user clicks the "Batal" button.
10. The system reset the field.
Exception EF1: Incomplete Application
11. If the school admin fails to fill in all required fields, the
system highlights the missing information and prompts the
student to complete the form.
31
5.2.2.11 UC011: Use Case Generate Student’s E-Cert
Use Case ID UC011
Use Case
Name
Generate Student’s E-Cert
Actors State Admin
Description This use case enables the School Admin to generate electronic
```
certificates (E-Certs) for students. These certificates may be
```
issued for academic achievements, participation in events, or
other recognized accomplishments. The process includes
uploading certificate templates, choosing the certificate template,
and confirming certificate details before generation.
Precondition 1. The School Admin must be logged into the system with
appropriate permissions.
2. Certificate templates must be pre-uploaded or available
for selection in the system.
Postcondition The customized E-Cert is successfully generated, stored in the
system, and available for download or distribution.
Main Flow 1. The School Admin logs into the system.
3. The School Admin navigates to the Jana Sijil Pelajar
section.
4. The system displays a list of schools within the State
Admin’s jurisdiction, along with certificate statuses.
5. State admin then chose the school to generate the
certificate.
6. The system displays the list of the school’s students
achievements.
7. State admin navigates to the Jana Sijil section.
8. The system displays options to Upload New Template,
Choose Existing Template or Delete Existing
Template.
32
a. Upload New Template:
i. The State Admin selects and uploads a
```
template file (e.g., PDF or image).
```
ii. Assign a name to the template.
iii. The system validates and stores the
template.
b. Choose Existing Template:
i. The State Admin previews and selects a
previously uploaded template.
c. Delete Existing Template:
i. The State Admin selects a template and
confirms the deletion.
ii. The system removes the template from the
available list and logs the action.
8. After selecting or uploading a template, the State Admin
enters the total pages of certificates wanted.
9. School admin customizes it by adding details that suits
the templates’ details.
10. The State Admin reviews and confirms the customized
certificate.
11. The E-Cert is made available for download in PDF.
33
5.2.2.12 UC012: Use Case Update Student’s E-Cert
Use Case ID UC012
Use Case
Name
Update Student’s E-Cert
Actors State Admin
```
Description This use case extends UC011 (Generate Student’s E-Cert) by
```
enabling the State Admin to update previously generated student
```
electronic certificates (E-Certs). Updates may include correcting
```
errors, updating student details, or making adjustments to
template formats.
Precondition 1. The State Admin is logged into the system with
appropriate permissions.
2. Previously generated E-Certs must be stored in the
system and accessible for modification.
Postcondition 1. The E-Cert is successfully updated and stored in the
system, replacing the previous version.
3. The updated E-Cert is available for download.
Main Flow 1. The State Admin logs into the system.
4. The State Admin navigates to the Jana Sijil Pelajar
section.
5. The system displays a list of previously generated E-Certs
within the State Admin’s jurisdiction, along with certificate
statuses.
6. State admin then chose the school to generate the
certificate.
7. The system displays the list of the school’s students
achievements.
8. The State Admin selects the E-Cert to update.
9. The system loads the selected E-Cert with current details
and template format.
10. The State Admin makes updates, such as:
34
a. Correcting student information
b. Updating certificate content
11. The State Admin reviews and confirms the changes.
12. The system generates the updated E-Cert and stores it
securely, replacing the original version.
13. A confirmation message is displayed, and the updated
E-Cert is available for download.
Alternate flow AF1: Back button
14. The user clicks on the Kembali ke Senarai Templat button.
15. The system will redirect back to the list certificate
template.
Exception EF1: No Available E-Certs to Update
16. The system displays a message indicating that no
previously generated E-Certs are available for update.
35
5.2.2.13 UC013: Use Case Submit Student Achievement
Use Case ID UC013
Use Case
Name
Submit Student Achievement
Actors School Admin
Description This use case outlines the process for school administrators to
submit individual student achievements to the state
administrative system for the generation of official certificates.
Precondition School Admin must be logged in the system.
Postcondition 1. The submitted student achievement is recorded in the
system.
17. The achievement may become visible on the student's
profile, and school profile.
Main Flow 1. The School Admin navigates to the "Student
Achievements" section of the TVPSSS system.
18. The School Admin selects the "Submit New Achievement"
option.
19. The system presents a form to the School Admin.
20. The School Admin fills in the following details:
a. Student's Name
b. Student’s Identification Number Card
c. Achievement Type (Group/Solo)
d. Achievement Date
e. Achievement Description
f. Supporting Evidence
21. The School Admin clicks the "Submit" button.
22. Upon successful validation, the system records the
achievement in the database, associating it with the
selected student's and school’s profile.
23. The system displays a confirmation message to the
School Admin, indicating successful submission.
36
Alternate flow AF1: Cancel Submission
24. The School Admin can click a "Cancel" button at any time
before submitting.
25. The system discards any entered information and returns
to the previous screen.
Exception EF1: Incomplete Information
26. If any mandatory fields are left blank, the system displays
specific error messages indicating which information is
missing.
37
5.2.2.14 UC014: Use Case Make Donation
Use Case ID UC014
Use Case
Name
Make Donation
Actors Guest
Description This use case describes the process by which a guest can
donate money to a specific school, enabling the school to
purchase equipment for the TVPSS or make necessary upgrades
to enhance its functionality and infrastructure.
Precondition Guests access the Welcome Page on the TVPSS website.
Postcondition 1. Payment has been successfully made to the school.
27. Receipt of payment is ready to be downloaded.
Main Flow 1. Guest navigates to the donation page section.
28. The system presents a donation form to the Guest.
29. Guests fill up the personal information including name, ic
number, email and phone number.
30. Guests need to select the state, district and school’s
name to donate.
31. Guests insert the total amount that they want to donate to
the school.
32. Guest clicks on the “Teruskan Pembayaran” button.
33. The system will show the payment gateway to the Guest
for them to proceed with payment.
34. Upon successful validation, the system records the
donation from guests in the database.
35. The system will display a receipt of donation to the Guest,
indicating their payment is successful.
Alternate flow AF1: Cancel Submission
36. Guests can click a "Kembali" button at any time before
submitting.
38
37. The system discards any entered information and returns
to the previous screen.
Exception EF1: Incomplete Information
38. If any mandatory fields are left blank, the system displays
specific error messages indicating which information is
missing.
```
EF2: Invalid Data
```
1. If entered data doesn't match expected formats, the
system provides clear feedback to the Guests.
39
5.2.2.15 UC015: Use Case View Donation History
Use Case ID UC015
Use Case
Name
View Donation History
Actors School Admin
Description This use case describes the process by which a school
administrator can access and review a detailed record of all
donations made by guests. This allows the school to identify
donors, track the amounts contributed, and assess the total funds
collected for improving the TVPSS.
Precondition The School Admin is logged into the system with appropriate
permissions.
Postcondition The School Admin successfully views the history of donation.
Main Flow 1. The School Admin logs into the system.
2. The School Admin selects the Sumbangan option from
the main menu.
3. The system displays a list of donations that have been
made by Guests.
Alternate flow AF1: User Export Data:
4. Users click on the export option button to view
spreadsheets.
5. System gets a response export and it will convert the data
into spreadsheets.
Exception EF1: No Data
6. The system will show “Tiada Data Ditemui”.
40
5.2.2.16 UC016: Use Case Report Damaged Equipment
Use Case ID UC016
Use Case
Name
Report Damaged Equipment
Actors 1. School Admin
7. PPD Admin
Description This use case describes the process by which a School Admin
reports damaged equipment used in the TVPSS. The report
includes detailed information about the damaged item, such as
the item's name, a description of the issue, and supporting proof
```
(e.g., images or documents). The submitted report is then
```
reviewed by the PPD Admin for further action.
Precondition The School Admin or PPD Admin must be logged into the system
with valid credentials.
Postcondition The report is successfully created and updated in the system
database.
Main Flow School Admin:
1. The School Admin logs into the system.
2. The School Admin selects the Pengurusan Peralatan
option from the main menu.
3. The system displays a list of equipment that has been
reported.
4. User clicks on “Tambah Barang” button.
5. The system will display the report form.
6. The user enters all information equipment details (e.g.,
Item’s name, Type of item, Location, Date of Report and
```
Status of Equipment).
```
7. Users enter the details of damaged equipment and upload
the proof of the damaged equipment picture
8. Users click on the “Submit” button.
9. The report will be successfully submitted to the PPD
41
Admin for them to review.
PPD Admin:
10. The PPD Admin logs into the system.
11. The PPD Admin selects the Pengurusan Peralatan
option from the main menu.
12. The system displays a list of equipment that has been
reported.
13. The system will display the report form.
Alternate flow AF1: Cancel Submission
14. The School Admin can click a "Cancel" button at any time
before submitting.
15. The system discards any entered information and returns
to the previous screen.
Exception EF1: Incomplete Information
16. If any mandatory fields are left blank, the system displays
specific error messages indicating which information is
missing.
```
EF2: Invalid Data
```
1. If entered data doesn't match expected formats, the
system provides clear feedback to the School Admin.
42
5.2.2.17 UC017: Use Case Update Damaged Equipment Report
Use Case ID UC017
Use Case
Name
Update Damaged Equipment Report
Actors 1. School Admin
2. PPD Admin
Description This use case describes the process by which a School Admin or
PPD Admin updates an existing report for damaged equipment.
The administrator can modify details such as the item's
description, damage status, location, or proof documents if new
or updated information is available. Once updated, the revised
report is saved in the system and re-submitted for review by the
State Admin.
Precondition 1. The School Admin or PPD Admin must be logged into the
system with valid credentials.
3. The damaged equipment report must already exist in the
system.
Postcondition 1. The damaged equipment report is updated successfully
and saved in the system database.
4. The PPD Admin is notified of the updated report for
review from School Admin.
Main Flow School Admin:
5. The School Admin logs into the system.
6. The School Admin navigates to the "Pengurusan
```
Peralatan" (Equipment Management) section.
```
3. The system displays a list of previously submitted
damaged equipment reports.
4. The School Admin selects the report they wish to update.
5. The system displays the report details.
6. The School Admin modifies the necessary fields, such as
the item's name, description, location, date of report,
43
status, or uploads new proof documents.
7. The School Admin clicks on the "Update" button.
8. The system validates the updated information.
9. The system saves the updated report and notifies the
State Admin for further review.
PPD Admin:
10. The PPD Admin logs into the system.
11. The PPD Admin navigates to the "Pengurusan
```
Peralatan" (Equipment Management) section.
```
3. The system displays a list of previously submitted
damaged equipment reports.
4. The PPD Admin selects the report they wish to update.
5. The system displays the report details.
6. The PPD Admin modifies the status and uploads proof
documents.
7. The PPD Admin clicks on the "Update" button.
8. The system validates the updated information.
9. The system saves the updated report and notifies the
State Admin for further review.
Alternate flow AF1: Cancel Submission
10. The School Admin or PPD Admin can click a "Cancel"
button at any time before submitting.
11. The system discards any entered information and returns
to the previous screen.
Exception EF1: Incomplete Information
12. If any mandatory fields are left blank, the system displays
specific error messages indicating which information is
missing.
44
5.2.2.18 UC018: Use Case View Damaged Equipment Report
Use Case ID UC018
Use Case
Name
View Damaged Equipment Report
Actors 1. PPD Admin
13. School Admin
Description This use case describes the process by which a PPD Admin or
School Admin views an existing report for damaged equipment.
The PPD Admin or School Admin can see the details of the
damage, including item descriptions, status, location, and proof
documents. This functionality helps in reviewing the submitted
reports and making decisions about the next steps in the
equipment management process.
Precondition 1. The PPD Admin or School Admin must be logged into the
system with valid credentials.
14. At least one damaged equipment report must already be
available in the system.
Postcondition
The damaged equipment report is successfully displayed for the
PPD Admin or School Admin.
Main Flow PPD Admin:
15. The PPD Admin logs into the system.
16. The PPD Admin navigates to the "Pengurusan Peralatan"
```
(Equipment Management) section.
```
3. The system displays a list of previously submitted
damaged equipment reports.
4. The PPD Admin selects a report they wish to view.
5. The system displays the details of the selected report,
```
including:
```
- Equipment Name
- Damage Status
45
- Location
- Proof Documents (if any)
6. The PPD Admin reviews the report and may decide on
```
further actions (e.g., review, approve, or request more
```
```
information).
```
School Admin:
1. The School Admin logs into the system.
2. The School Admin navigates to the "Pengurusan
```
Peralatan" (Equipment Management) section.
```
3. The system displays a list of previously submitted
damaged equipment reports.
4. The School Admin selects a report they wish to view.
5. The system displays the details of the selected report,
```
including:
```
- Equipment Name
- Damage Status
- Location
- Proof Documents (if any)
6. The School Admin reviews the report and may decide on
```
further actions (e.g., review, approve, or request more
```
```
information).
```
Exception EF1: Report Not Found:
1. If the report does not exist or has been deleted, the
system displays a message saying the report is
unavailable and provides options to view other reports.
46
5.2.2.19 UC019: Use Case Payment Gateway
Use Case ID UC019
Use Case
Name
Payment Gateway
Actors Guest
```
Description The Payment Gateway (UC019) in the Donation Management
```
Subsystem is an integral component that facilitates secure
payment processing whenever a guest makes a donation
```
(UC014). It acts as an intermediary between the guest’s payment
```
```
method (online banking) and the system, ensuring sensitive
```
payment information is securely handled through encryption and
compliance with industry standards like PCI-DSS.
Precondition Guests fill up the donation form including inserting the amount of
donation.
Postcondition 1. The system confirms the transaction with the guest.
2. The system will record the donation details in the
database.
Main Flow 1. The guest provides necessary details and submit the
donation request.
3. The system redirects the guest to the Payment Gateway
for payment processing.
4. The guest enters their payment details (e.g., username,
```
password) into the secure Payment Gateway interface.
```
4. The Payment Gateway validates the provided payment
```
information (e.g., checks sufficient balance, or
```
```
authentication through 3D Secure or OTP).
```
5. The Payment Gateway processes the payment by
communicating with the guest’s bank or payment service
provider.
6. The Payment Gateway returns the transaction status
```
(success or failure) to the system.
```
47
7. Handle Successful Payment:
a. The system updates the donation record with the
guest’s details and the donated amount.
b. The system displays a confirmation message and
receipt for the guest.
8. Handle Failed Payment:
a. The system notifies the guest of the failure.
b. The guest is given options to retry the payment or
cancel the donation process.
9. The guest is redirected back to the Donation Management
Subsystem with the status of the transaction and the
donation process concludes.
Alternate flow AF1: Invalid Payment Information:
10. The Payment Gateway rejects the transaction and
displays an error message "Payment authorization
failed".
```
AF2: Insufficient Funds:
```
1. The Payment Gateway notifies the system of the failure,
```
and an error message is displayed to the guest (e.g.,
```
```
"Insufficient balance in your account").
```
```
AF3: Payment Gateway Unavailable:
```
1. The system notifies the guest of the issue (e.g., "Payment
```
service is temporarily unavailable, please try again later").
```
```
AF4: Guest Cancels Payment:
```
1. The Payment Gateway cancels the transaction and
notifies the system.
Exception EF1: No Data
2. The system will show “Tiada Data Ditemui”.
48
```
5.3 Logical Viewpoint (Architecture Style Diagram (Assignment 1))
```
5.3.1 Design Concerns
The logical viewpoint defines the structural composition of the TVPSS system,
elaborating on the relationships between various classes and interfaces. It ensures a
well-structured system by specifying class dependencies and interactions. The
design is centered around controllers, models, and enumerations that handle
authentication, school and student management, equipment tracking, and donations.
```
The system follows a role-based access model, ensuring that different users (Super
```
```
Admin, State Admin, PPD Admin, and School Admin) have specific functionalities
```
and permissions. Controllers manage operations related to authentication, school
administration, student achievements, equipment tracking, and donations. The
relationships between models, such as students being linked to schools, equipment
being monitored for status updates, and donation records being processed through a
payment system, provide a clear structure for data management.
This structured approach ensures maintainability, scalability, and secure data
management by defining clear responsibilities for each entity. The logical
relationships also aid in efficient data retrieval and operations processing.
49
```
5.3.2 Design View (Class Diagram)
```
Figure 4.3: Class diagram for TVPSS Management Information System
Controllers
```
UserController: Manages user information and dashboard access.
```
```
AuthenticatedSessionController: Handles user authentication and session management.
```
```
SchoolAdminController: Oversees school functions (e.g., managing school info, student
```
```
records, equipment).
```
```
PPDAdminController: Manages TVPSS version verification and equipment damage
```
reports.
```
StateAdminController: Manages student certificate generation and school version
```
validation.
```
DonationController: Handles donation transactions and financial management.
```
```
PaymentController: Manages payment transactions.
```
50
Models
```
User: Represents users, includes fields like email, password, district, and state.
```
```
SchoolInfo: Stores school-related data (e.g., school name, code, logo).
```
```
Student: Represents student records, includes personal info and school affiliation.
```
```
Studcrew: Manages student crew applications and statuses.
```
```
StudentAchievement: Tracks student achievements (e.g., type of achievement, status).
```
```
TVPSSVersion: Handles versioning and approval of TVPSS school versions.
```
```
Equipment: Maintains records of school equipment.
```
```
EqFollowUp: Tracks follow-up actions on equipment issues.
```
```
Donation: Manages donation transactions.
```
Enumerations
```
UserRole: Defines user roles (Super Admin, State Admin, PPD Admin, School Admin).
```
```
EquipStatus: Tracks equipment status (Functional, Non-functional, Under maintenance).
```
```
Status: Check the status if the item is available or not
```
```
CrewStatus: Tracks student crew application status (Approved, Rejected, Pending).
```
51
5.4 Information Viewpoint
5.4.1 Design Concerns
Entity Name Description
donation An entity that represents the details of donations,
including the donor's identity, donation amount,
purpose, and date of contribution.
eq_follow_ups An entity that represents the follow-up records for
equipment maintenance or issue resolution
eq_locations An entity that represents the physical storage or
deployment locations of equipment for the school
equipment An entity that represents the inventory of equipment,
detailing descriptions and condition status.
schoolinfo An entity that represents the essential information
about a school, including its name, address and
contact details
schoolversion An entity that represents the versioning or
configuration records specific to schools, tracking
updates, versions, and implementation details of
TVPSS activities.
studcrew An entity that represents student’s crew of TVPSS.
students An entity that represents the personal including
identification number and contact information.
student_achievements An entity that represents the records of student
accomplishments, such as awards, recognitions, and
extracurricular achievements.
users An entity that represents all system users, tracking
login credentials, roles, permissions, and profile
details.
52
5.4.2 Design View
Data Dictionary
```
Entity: Donation
```
Attribute Name Type Description
id bigint Primary key for donation record
school_id bigint Foreign key linking to schoolinfo
name string Donor's name
email string Donor's email
phone string Donor's phone number
ic_num string Donor's identification number
amaun string Donation amount
```
Entity: eq_follow_ups
```
Attribute Name Type Description
id bigint Primary key for follow-up record
equipment_id bigint Foreign key linking to equipment
user_id bigint Foreign key linking to users
uploadBrEq json JSON data of uploaded
documents
content text Follow-up details/notes
date date Date of follow-up
timestamps datetime Created and updated timestamps
```
Entity: eq_locations
```
Attribute Name Type Description
id bigint Primary key for follow-up record
school_info_id bigint Foreign key linking to schoolinfo
eqLocName string Name of equipment location
eqLocType string Type of location
timestamps datetime Created and updated timestamps
```
Entity: equipment
```
Attribute Name Type Description
53
id bigint Primary key for follow-up record
school_info_id bigint Foreign key linking to schoolinfo
equipName string Name of equipment
equipType string Type/category of equipment
location string Current location of equipment
acquired_date date Date when equipment was
acquired
```
status enum Equipment status ('Berfungsi',
```
'Tidak Berfungsi',
```
'Penyelenggaraan')
```
level tinyint Equipment level/grade
timestamps datetime Created and updated timestamps
```
Entity: schoolinfo
```
Attribute Name Type Description
id bigint Primary key for follow-up record
user_id bigint Foreign key linking to users table
schoolOfficer string Name of school officer in charge
schoolCode string Unique school identification code
schoolName string Official name of the school
schoolEmail string Official school email address
schoolAddress1 string Primary address line
```
schoolAddress2 string Secondary address line (optional)
```
district string School's district
postcode string School's postal code
state string School's state
noPhone string School's contact number
```
noFax string School's fax number (optional)
```
schoolLogo string Path to school logo image
linkYoutube string School's YouTube channel link
timestamps datetime Created and updated timestamps
```
Entity: schoolversion
```
Attribute Name Type Description
id bigint Primary key for follow-up record
school_info_id bigint Foreign key linking to schoolinfo
54
version integer Version number
agency1_name string Type/category of equipment
agency2_name string Current location of equipment
agencyManager1_name string Name of first agency manager
agencyManager2_name string Name of second agency manager
recordEquipment tinyint Recording equipment availability
```
tvpssStudio enum('Ada','Tiada') TVPSS studio availability
```
```
recInSchool enum('Ada','Tiada') In-school recording capability
```
```
recInOutSchool enum('Ada','Tiada') Outside school recording
```
capability
```
greenScreen enum('Ada','Tiada') Green screen availability
```
timestamps datetime Created and updated timestamps
```
Entity: studcrew
```
Attribute Name Type Description
id bigint Primary key for follow-up record
student_id bigint Foreign key linking to students
jawatan string Position/role in the crew
```
status enum Application status ('Permohonan
```
Lulus', 'Permohonan Ditolak',
```
'Permohonan Belum Diproses')
```
timestamps datetime Created and updated timestamps
```
Entity: Students
```
Attribute Name Type Description
id bigint Primary key for follow-up record
name string Student's full name
ic_num string Student's identification number
```
(unique)
```
```
email string Student's email address (unique)
```
crew string Student's crew assignment
state string Student's state
district string Student's district
schoolName string Name of student's school
school_info_id bigint Foreign key linking to schoolinfo
timestamps datetime Created and updated timestamps
```
Entity: student_achievements
```
55
Attribute Name Type Description
id bigint Primary key for follow-up record
type_of_achievement string Category/type of achievement
type_of_application string Type of achievement application
date date Date of achievement
details text Detailed description of
achievement
supporting_file string Path to supporting documentation
students json JSON data of involved students
school_info_id bigint Foreign key linking to schoolinfo
status string Status of achievement record
timestamps datetime Created and updated timestamps
```
Entity: Users
```
Attribute Name Type Description
id bigint Primary key for follow-up record
name string User's full name
email string User's unique email address
state string User's state of residence
district string User's district within the state
role integer User's role/permission level in the
system
email_verified_at timestamp Timestamp when email was
verified
password string Encrypted user password
remember_token string Token for "remember me"
functionality
timestamps datetime Created and updated timestamps
```
Entity: certificate_templates
```
Attribute Name Type Description
id bigint Primary key for certificate
templates
name string name of the certificate’s template
file_path string store file in database
timestamps datetime Created and updated timestamps
56
```
Entity Relationship Diagram (ERD)
```
57
```
5.5 Interface Viewpoint (Interface Design)
```
5.5.1 Design Concerns
By focusing on describing the functionality of the TVPSS Management
Information System from the user’s perspective, outlining how users can
interact with the system to complete all expected features and the feedback
they will receive.
From a user interface perspective, the system provides intuitive and
role-based dashboards for administrators, students, and donors.
Administrators can use the interface to manage applications, monitor
donations, and view comprehensive reports, while students can view
application statuses and results. Donors are provided with a transparent and
user-friendly interface to make contributions and school admin can track the
donors' donation history. The system ensures smooth navigation with clear
feedback, such as success or error messages, and real-time updates on user
actions.
In terms of hardware interfaces, the system is designed to function
seamlessly on various devices, including desktop computers, tablets, and
smartphones, ensuring accessibility across different platforms. For software
interfaces, the system integrates with external APIs and services to enable
secure payment processing for donations, data synchronization, and email
notifications. These integrations are implemented to ensure reliable and
efficient communication between system components and external entities.
Overall, the interface viewpoint ensures a seamless and efficient interaction
between users and the system while providing comprehensive documentation
for developers and testers to maintain and enhance the system’s functionality.
58
```
5.5.2 Design View (Wireframe design)
```
User Interfaces
The system's interface will be clear and easy to use. When users log in to the
system, they will see a homepage with login choices. While to login, they may only
use the .moe domain email to login to their account. Users can get to different
menus based on their jobs once they are logged in. Super Admins will be able to
view dashboards and handle user information. School Admins will be able to
manage school information and equipment, and students will be able to see
application results and send in their own. Users will be able to change things about
their profiles, like their passwords and personal information, through the interface.
Hardware Interfaces
The TVPSS Management Information System is compatible with laptops, desktop
computers and mobile phones that have internet connectivity. The system does not
```
require additional hardware but ensures that basic input devices (keyboard and
```
```
mouse) are functional for user interaction.
```
Software Interfaces
The system will use the Database Management System and centralized TVPSS
Data to organize and store all data, including user information, school details, and
student achievements. It will interact with web browsers and mobile phone
applications for user access and may integrate with other school management
software if necessary.
Communication Interfaces
The TVPSS Management Information System will use a strong internet connection.
For data security and privacy during transmission, it will use secure HTTP/HTTPS
protocols. For alerts and notifications, the system will also connect to email services.
59
```
5.6 Structure Viewpoint (Behavioral Pattern + Structural Pattern
```
```
(Assignment 2))
```
5.6.1 Design Concerns
The Structure viewpoint is used to document the internal constituents and
organization of the TVPSS Management Information System by focusing on
the relationships and interactions between classes and packages within the
system. This viewpoint provides a recursive perspective, breaking down the
system into its components to give a detailed understanding of how they are
structured and interrelated.
For the user, the Structure viewpoint provides insight into how the system’s
components work together to deliver expected functionality. It ensures
transparency in how data flows between different modules, such as
application management, donation tracking, and user dashboards. This
enables users to trust the system’s efficiency and reliability.
For the developer, the Structure viewpoint outlines the interaction between
classes and packages, highlighting their dependencies, hierarchies, and
integration points. It details how individual modules, such as authentication,
database management, and reporting, communicate with one another,
ensuring consistency and modularity. This viewpoint helps developers
understand the organization of the codebase, enabling effective debugging,
testing, and future enhancements.
By detailing the internal structure, this viewpoint ensures that both users and
developers have a clear understanding of the system’s organization, fostering
confidence in its maintainability, scalability, and functionality.
60
```
5.6.2 Design View (Class / Package Diagram)
```
Figure 4.1: Package Diagram for TVPSS
This package diagram represents the modular structure of the TVPSS Management
Information System, dividing the system into multiple subsystems, each responsible
for different functionalities. The diagram illustrates the relationships between these
subsystems and their interactions through shared models and controllers. The
Dashboard & Administrative Subsystem manages user-related operations,
containing the User model, UserController, and multiple dashboard views for
different user roles, such as PPD Admin, School Admin, State Admin, and Super
Admin. The School Information Management Subsystem is responsible for managing
student-related data, with the StudCrew model and StudentController, along with
views for adding students, applying for crew, approving crew applications, and
61
updating school information. The Student Achievement Subsystem handles student
certificates and achievements using the CertificateTemplate and
StudentAchievement models, providing views for listing achievements, generating
certificates, and editing certificates.
The Donation Management Subsystem facilitates the donation process, containing
the Donation model and controllers like DonationController and PaymentController,
with views for donation history, receipt generation, and donation submission. The
Equipment Report Management Subsystem manages equipment tracking using the
EqFollowUp, EqLocation, and Equipment models, providing views for adding, listing,
and updating equipment and locations. The School Version Management Subsystem
ensures version control of the TVPSS system across different schools, with the
TVPSSVersion model and views for approving PPD and state versions, listing
schools, and updating school versions.
A key component of the system is the SharedModelAndControllers package, which
centralizes common models such as SchoolInfo and Student, along with
administrative controllers like PPDAdminController, SchoolAdminController, and
StateAdminController. These shared components ensure modularity, consistency,
and reusability across different subsystems. The interactions between these
packages are depicted through dependency relationships, showing how different
modules use shared models and controllers for seamless communication.
Overall, this package diagram effectively organizes the TVPSS Management
Information System into distinct yet interconnected subsystems, promoting
scalability, maintainability, and efficient development by ensuring that related
functionalities are encapsulated within their respective modules while leveraging
shared resources where necessary.
62
```
5.7 Interaction Viewpoint (Creational Pattern + Sequence Diagram
```
```
(Assignment 2+ 1))
```
5.7.1 Design Concerns
Creational
The diagram demonstrates the implementation of the Factory Method Pattern for
managing equipment and follow-up operations. The Controller serves as the abstract
creator, defining generic methods for updating equipment and saving follow-ups,
while the SchoolAdminController and PPDAdminController act as concrete creators,
implementing specific logic tailored to their respective domains. The Model functions
as the abstract product, providing a shared structure or behavior, with Equipment
and EqFollowUp as the concrete products that handle detailed operations. The
Equipment model interacts with the EqFollowUp model to manage scoped follow-up
actions based on queries and equipment IDs. This design ensures flexibility,
scalability, and adherence to the Factory Method Pattern by decoupling object
creation from the controllers, enabling easier maintenance and extension.
The Factory Method pattern allows a class to delegate the responsibility of
creating objects to its subclasses, promoting flexibility and adherence to the
open/closed principle. In this case:
63
1. Base Class (Controller):
The Controller class serves as the base class, providing a common
structure and possibly abstract methods for managing resources or
requests. It acts as a "framework" that defines generic behavior but
leaves specific details of resource management to its subclasses.
2. Subclass (SchoolAdminController):
The SchoolAdminController extends the Controller class and
implements specific functionality relevant to school administrators. It
can act as a "factory" that creates or processes resources specific to
school administrators, such as managing schools, updating
information, or handling school-related requests.
3. Subclass (PPDAdminController):
The PPDAdminController is a subclass that extends the Controller
```
class to provide functionality specific to PPD (District Education Office)
```
administrators. This class is responsible for managing operations that
pertain to the PPD admin's role, such as managing schools under their
jurisdiction, overseeing teacher data, or processing district-specific
reports.
4. Factory Behavior in Methods:
PPDAdminController and SchoolAdminController acts as a factory by
encapsulating the logic for creating or managing specific resources or
entities relevant to the PPD admin and School Admin. This includes
fetching data or instantiating models associated with PPD and School
Admin
tasks.
64656667
Behavioral
TVPSS Management System has a several dashboard that needs to display
real-time data in the form of charts and statuses. When users input data, the system
```
should immediately update the dashboard components (like charts and statuses)
```
without requiring a manual refresh. To achieve this, we use the Observer Pattern.
Automatic Synchronization Across Observers
○ When the UserInputData changes, the BroadCastService triggers the
```
notifyAllObserver() method, ensuring all registered observers are
```
automatically updated with the new data.
○ This eliminates manual synchronization and ensures consistency
across dependent components.
By this, it will provide seamless and efficient synchronization between the
model and its observers, avoiding redundant update logic.
Here, timeRange, date, and selectedRegion act as the subjects. Any update
to these states will notify the observers.
68
Observers
```
The charts (Bar, Doughnut) and summary cards are observers. When the
```
```
state changes (for instance, timeRange changes), the charts and other UI
```
components re-render to reflect the new data.
6970
Structural
This diagram illustrates the application of the Facade Pattern in a role-based
dashboard system. The AuthenticatedSessionController serves as the facade,
streamlining interactions with multiple role-specific dashboard interfaces
```
(dashboardSP, dashboardST, dashboardPP, dashboardSA). These interfaces
```
represent the entry points to the dashboards tailored for specific user roles,
```
such as super admin(SP), state admin (ST), school admin (SA), and PPD
```
```
admin (PP). The AuthenticatedSessionController centralizes functionality,
```
```
such as session management (create(), destroy(), store()), login attempt limits
```
```
(maxAttempts), and redirection (redirectTo), while the User class provides
```
```
role-specific details using the getRoleName() method. This pattern simplifies
```
the complexity of accessing role-specific dashboards by encapsulating their
details within a unified controller.
71
Role-Based Redirection: The facade hides the complexity of routing users to
the appropriate dashboard based on their role:
● Super Admin → dashboardSP
● State Admin → dashboardST
● PPD Admin → dashboardPP
● School Admin → dashboardSA
7273
```
5.7.2 Design View (Class Diagram + Sequence diagram)
```
```
a) Module Dashboard and Administration
```
74
1. SD001: Sequence diagram for View Dashboard
Figure 4.4: Sequence Diagram for View Dashboard
75
2. SD002: Sequence diagram for Manage User Information
Figure 4.4: Sequence Diagram for View Dashboard
76
```
b) Module School Information Management
```
77
3. SD003: Sequence diagram for Manage School Information
Figure 4.4: Sequence Diagram for View Dashboard
78
4. SD004: Sequence diagram for Manage Student Information
Figure 4.4: Sequence Diagram for Manage Student Information
79
5. SD005: Sequence diagram for Validate School Crew Application
Figure 4.4: Sequence Diagram for Validate School Crew Application
80
6. SD006: Sequence diagram for View Application Result
Figure 4.4: Sequence Diagram for View Application Result
7. SD007: Sequence diagram for Submit School Crew Application
Figure 4.4: Sequence Diagram for Submit School Crew Application
81
```
c) Module School Version Management
```
82
8. SD008: Sequence diagram for View School Version Status
Figure 4.4: Sequence Diagram for View School Version Status
83
9. SD009: Sequence diagram for Verify School Version Status
Figure 4.4: Sequence Diagram for Verify School Version Status
84
10. SD010: Sequence diagram for Manage School Version Status
Figure 4.4: Sequence Diagram for Manage School Version Status
85
```
d) Module Student Achievement
```
86
11. SD011: Sequence diagram for Generate Student’s E-Cert
Figure 4.4: Sequence Diagram for Generate Student’s E-Cert
87
12. SD012: Sequence diagram for Update Student’s E-Cert
Figure 4.4: Sequence Diagram for Update Student’s E-Cert
88
13. SD013: Sequence diagram for Submit Student Achievement
Figure 4.4: Sequence Diagram for Submit Student Achievement
89
```
e) Module Donation Management
```
90
14. SD014: Sequence diagram for Make Donation
Figure 4.4: Sequence Diagram for Make Donation
91
15. SD015: Sequence diagram for View Donation History
Figure 4.4: Sequence Diagram for View Donation History
92
16. SD019: Sequence diagram for Payment Gateway
Figure 4.4: Sequence Diagram for Payment Gateway
93
```
f) Module Equipment Report Management
```
94
17. SD016: Sequence diagram for Report Damaged Equipment
Figure 4.4: Sequence Diagram for Report Damaged Equipment
95
18. SD017: Sequence diagram for Update Damaged Equipment Report
Figure 4.4: Sequence Diagram for Update Damaged Equipment Report
96
19. SD018: Sequence diagram for View Damaged Equipment Report
Figure 4.4: Sequence Diagram for View Damaged Equipment Report
97
```
5.8 Algorithm Viewpoint (Construction Design)
```
5.8.1 Design Concerns
The authentication and redirection mechanism in the TVPSS system ensures secure
user validation and proper access control. Upon successful login, session
regeneration is performed to prevent session fixation attacks, enhancing security by
assigning a new session ID.
The system follows a role-based redirection approach, where Super Admins, State
Admins, PPD Admins, and School Admins are directed to their respective
dashboards. Unauthorized users are redirected to the login page with an error
message, preventing improper access.
Logging plays a crucial role in monitoring user activity. Each successful login records
the user ID, role, and email, while redirection events ensure users are routed
correctly. Unauthorized access attempts are also logged, allowing administrators to
identify security threats.
These design considerations align with the system’s access control policies,
ensuring that users only access permitted areas. Error handling mechanisms prevent
misrouting, and security measures such as session regeneration and logging protect
sensitive data while maintaining system integrity.
98
```
5.8.2 Design View (Decision Table)
```
99
User Interface Design
5.9 Overview of User Interface
When users register into the TVPSS Management System, they are directed to a
role-based dashboard where they can access capabilities based on their allocated
```
responsibilities (Super Admin, State Admin, PPD Admin, or School Admin). The
```
Super Administrator has complete authority over user administration, role
allocations, and system-wide monitoring. The State Administrator manages schools
in their state, reviews reports, and supervises school-level activities. The PPD Admin
oversees district-level school operations, whereas the School Admin administers
students, staff, and provides reports for their institution. The system features user
```
management (only for Super Admins), which allows users to be created, modified,
```
and assigned roles. Users can generate performance, attendance, and activity
reports by entering parameters such as date range and school information. School
management enables state and school administrators to keep track of student and
staff records as well as educational development.
Additionally, the system includes event/activity management, which allows users to
schedule, track, and approve school-related events. Role-based access control
ensures that each user can only conduct actions according to their role. The file
management module allows administrators to add, view, and manage files based on
classification and status, as well as open, close, borrow, and dispose of them. The
system also facilitates file borrowing authorization, damage reporting, and disposal
scheduling, resulting in more efficient administrative operations. By combining these
elements into a streamlined interface, the TVPSS Management System improves
efficiency, accessibility, and security while managing school-related data and
processes.
100
5.10 Screen Images
1.1.1.1 User Interface Prototype Login Page
3.1.1.2 User Interface Prototype Dashboard Page
101
3.1.1.3 User Interface Prototype Crew Application Submission Page
3.1.1.4 User Interface Prototype Crew Application Result Page
102
3.1.1.5 User Interface Prototype Manage Equipment Page
3.1.1.6 User Interface Prototype School Information Page
103
3.1.1.7 User Interface Prototype Submit Version Page
3.1.1.7 User Interface Prototype Validate School Crew Application Page
104
3.1.1.8 User Interface Prototype Generate E-Cert Student Page 1/2
105
6. 3.1.1.9 User Interface Prototype Prototype Generate E-Cert Student Page
2/2
106
Appendices
107