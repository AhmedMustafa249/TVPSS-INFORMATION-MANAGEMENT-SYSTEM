




co

SECJ 2253: Software Modeling and
## Requirements Engineering

## Software Requirements Specification

TVPSS Management Information System
## 1.0
## 12/6/2024

Prepared by: Softwork.Net

## Team Members:
1 Adam Imran bin Alwi B23CS0017
2 Elvis Chang Feng Jie  A22EC9157
3 Jessie Chang A22EC0054
4 Muhammad Aiman Haiqal bin Salehuddin B23CS0050






## Revision Page
a. Overview
A description of the overall requirements, a list of specific terms, and an introduction are
included  in  this  most  recent  version  of  the Software  Requirement  Specification. This
document will describe how the three requirements modelling perspectives data, functional,
and behavioral for our proposed system were used to build the software that we obtained
from  our  stakeholders. Each section in  the  Software Requirements  Specification is
discussed specifically and follows the learning concepts of Requirements Engineering and
Software Modeling and the IEEE Guideline.
b. Target Audience
## - KPM
## - PPD
## - Sekolah
## - Student
- TVPSS Management Team
## - Development Team
c. Project Team Members
## Team Member Name Module Name
Adam Imran bin Alwi Module Dashboard and Administration
## Elvis Chang Feng Jie  Module School Information Management
## Jessie Chang Module School Version Managements
Muhammad Aiman Haiqal bin
## Salehuddin
## Module Student Achievement Management




iii
P3 SRS-Template-v2.0-ForSECJ2253-RESM@UTM-ByNI-27June2021
d. Version Control History
Version  Primary Author(s) Description of Version Date Completed
## 1.0 Muhammad Aiman Haiqal User Requirements
## Definition
## 12/5/2024
## 1.0 Muhammad Aiman Haiqal Requirements Model
Document (Functional, Data,
## Behavioral Perspectives)
## 31/5/2024
## 1.0 Elvis Chang Feng Jie Software Requirements
Specification of TVPSS
## Management System
## 12/6/2024
























iv

Table of Contents
## 1 Introduction  1
## 1.1 Purpose 1
## 1.2  Scope 1
1.3  Definitions, Acronyms and Abbreviations 2
## 1.4 References 2
## 1.5 Overview 3
## 2 Overall Description 4
## 2.1  Product Perspective 6
## 2.1.1 System Interfaces 8
## 2.1.2 User Interfaces 8
## 2.1.3 Hardware Interfaces 8
## 2.1.4 Software Interfaces 8
## 2.1.5 Communication Interfaces 8
## 2.1.6 Memory 8
## 2.1.7 Operations 8
## 2.1.8 Site Adaptations Requirements 9
## 2.2 Product Functions 9
## 2.3 User Characteristic 9
## 2.4 Constraints 9
2.5 Assumption and Dependencies 10
2.6 Apportioning of Requirements 10
## 3 Specific Requirements 11
## 3.1  External Interface Requirements 16
## 3.1.1 User Interfaces 16


v

## 3.1.2 Hardware Interfaces 24
## 3.1.3 Software Interfaces 25
## 3.1.4 Communication Interfaces 26
## 3.2  System Features 27
3.2.1 Module Dashboard and Administration 27
3.2.1.1 UC001: Use Case View Dashboard 27
3.2.1.2 UC002: Use Case Manage User Information   31
## 3.2.2 Module School Information Management 37
3.2.2.1 UC006: Use Case Manage School Information 37
3.2.2.2 UC008: Use Case Manage Equipment Number 42
3.2.2.3 UC009: Validate School Crew Application 48
3.2.2.4 UC011: View Application Result 55
3.2.2.5 UC012: Submit School Crew Application 58
## 3.2.3 Module School Version Managements 62
3.2.3.1       UC003: Use Case View School Version Status 62
3.2.3.2       UC007: Use Case Manage School Version Status 65
3.2.3.2       UC005: Use Case Verify School Version Status 71
## 3.2.4 Module Student Achievement Management 75
3.2.4.1       UC004: Generate E-Cert Student 75
3.2.4.2       UC010: Submit Student Achievement  80
## 3.3  Performance Requirements 85
## 3.4  Design Constraints 85
## 3.5 Software System Attributes 86
## 3.6 Other Requirements
## Appendices
## 87
## 88



## 1


## 1. Introduction
## 1.1 Purpose
This  Software  Requirements Specification  (SRS)  details  the  proposed  TVPSS  management
system, outlining its functionality for various stakeholders (Super Admin, State Admin, District
Admin, School Admin, and Students). The SRS is organized into four distinct modules within
the System Features section according to the stakeholders’ requirements, each accompanied by
use  case  diagrams  and  specifications  for  clarity.  This  structured  approach  ensures  that  all
stakeholders have a comprehensive understanding of the system's capabilities and intended use.

## 1.2 Scope
TVPSS Management System is an Information Management System designed to replace the
existing manual management system. Based on the requirement of the stakeholders, TVPSS
Management System will be designed as a PWA that is primarily featured in managing all the
information  flows  such  as information retrieval,  information  modification  and information
validation. There are four main modules that are involved in this system which are Dashboard
and  Administration  Module, School  Information  Management  Module,  School  Version
Management Module and Student Achievement Management Module. This system is designed
to increase efficiency and effectiveness of the TVPSS Management System.

The TVPSS Managaement System has 3 main objectives aligned with. The following are the
significant objectives to ensure the proposed system to be highly efficient and performs well.

- Support the effective implementation of TVPSS programs.
- Improve the efficiency and effectiveness of TVPSS administration
- Provide   a   high   usability   and   well-coordinated   system   platform   for  information
management of TVPSS program.





## 2

1.3 Definitions, Acronyms and Abbreviation
Acronyms and
## Abbreviation
Full-Form
## Definition
## SRS
## Software Requirements
## Specification

A document that details
the features and
functionality of a system.
## TVPSS
## Televisyen Pusat Sumber
## Sekolah

A school program for
students to showcase their
talents in journalism, media
and hosting.
## PWA
## Progressive Web
## Application
A type of web app that can
operate both as a web page
and mobile app on any
device.
## Stakeholder
A person, group of people
or an organisation who has
directly or indirectly
influence the requirements
of the regarded system.

## 1.4 References
Tailwind Labs. (n.d.). Tailwind CSS. Tailwind CSS. Retrieved from https://tailwindcss.com/
Facebook, Inc. (2021). React: A JavaScript library for building user interfaces. Retrieved
from https://react.dev/
Laravel. (n.d.). Laravel: The PHP framework for web artisans. Laravel. Retrieved from
https://laravel.com/
Google. (n.d.). Flutter: Beautiful native apps in record time. Flutter. Retrieved from
https://flutter.dev/
Oracle Corporation. (n.d.). MySQL: The world's most popular open-source database. MySQL.
Retrieved from https://www.mysql.com/


## 3

Axios. (n.d.). Promise based HTTP client for the browser and node.js. Axios. Retrieved from
https://axios-http.com/
Microsoft Corporation. (n.d.). Visual Studio Code. Visual Studio Code. Retrieved from
https://code.visualstudio.com/

## 1.5 Overview
In  this  SRS, the  purpose,  scope,  definition,  reference  and  overview  of  the  document  is
available in the introduction section followed by the overall description which briefly explains
the  actors  and  system  features  along  with a  use case  diagram  attached.  Under  that  section,
product   functions,   product   perspectives, user   characteristics,   constraints,   assumptions,
dependencies and apportioning of requirements are included. The product perspective describes
the  system  from  various  aspects  besides  showing  how  the  system  performs  under  various
constraints and conditions while the products functions explain the features of the system based
on the use case proposed.
On the other hand, under the specific requirements section, the user, hardware, software
and communications  interfaces  are illustrated  and listed specifically  along  with  definitions.
Besides, the use cases are grouped into modules that represent a subsystem each representing
one of the major features of the system. Each module is also clearly explained through use case
specifications  and  activity  diagram. Lastly, this  document ends  with the  statement of
performance requirements, design constraints, software system attributes  and other needed
requirements.









## 4




## 2. Overall Description
Figure 2.1 shows the Use Case Diagram (UCD) for the TVPSS Management Information
System. There are a total of six actors, including Super Admin, School Admin, State Admin,
PPD Admin, TVPSS Management Crew, and Student, along with 12 use cases. The Dashboard
&  Administration  Subsystem  includes  UC001  for  viewing  the  dashboard  and  UC002  for
managing user information by the Super Admin. The Module School Information Management
Subsystem  consists  of  UC006  for  managing  school  information,  UC008  for  managing
equipment  numbers,  UC009  for  validating  school  crew  applications,  UC011  for  viewing
application  results,  and  UC012  for  submitting  school crew applications.  The  School  Version
Management  Subsystem  includes  UC003  for  viewing  school  version  status,  UC005  for
verifying  school version  status,  and  UC007  for  managing  school  version  status.  The  Student
Achievement Management Subsystem includes UC004 for generating e-certificates for students
and UC010 for submitting student achievements.



## 5


Figure 2.1: Use Case Diagram of TVPSS Management Information System


## 6

## 2.1 Product Perspective
The  TVPSS  Management  Information  System  is  a  highly  efficient  and  automated  web-
based and mobile application. Based on Figure 2.1, there are 4 sub-goals which are Dashboard
&  Administration Subsystem,  School  Information  Management  Subsystem,  School  Version
Management and School Achievement Management.
The  Dashboard  and  Administration  Subsystem  is  the  first  sub-goal  of  the TVPSS
Management Information System. This subsystem is primarily concerned with the provision of
a centralized and  effective  method  for  monitoring  the  entire  system.  There  are  features  for
monitoring the dashboard, which enable administrators to monitor key metrics and the status of
the system in real time. Additionally, it includes functionalities for managing user information,
which ensures that user accounts are handled in the appropriate manner. These responsibilities
fall mostly in the hands of the Super Admin, who is able to take control of the administrative
activities of  the  system  and  make  certain  that  the  management  process  is  both  efficient  and
streamlined.
The second  sub-goal  of  the  TVPSS  Management  Information  System is  the  School
Information  Management  Subsystem.  Efficient  handling  of  school  data  is  the  goal  of  this
subsystem. It has features for keeping track of school data, making sure that all information is
correct  and up  to  date.  In  addition  to  validating  school crew  applications  and  managing
equipment  numbers  for  resource  tracking,  it  ensures  that  applications  are  examined  and
authorized in  a  proper  manner.  The  application  process  is  made  visible  and  expedited  for
everyone involved by allowing users to monitor application outcomes and submit school crew
applications through this subsystem. The School Admin and the TVPSS Management Crew all
work  together  within  this  subsystem  to  ensure  that  school  operations  run  smoothly  and
efficiently for the student’s ease.
The School Version Management Subsystem is the third part of the TVPSS Management
Information System's main goal. This part of the system oversees keeping track of and checking
the different versions of school information. It has features for watching the statuses of school
versions, which makes it easy for administrators to keep track of and keep an eye on the status
of  school  data.  It  also  includes  checking  these  statuses  to  make  sure  they  are  correct  and
consistent across the system. Updating and maintaining records is made possible by managing
school version states, which is very important for keeping the school's information correct and


## 7

up  to  date. The  School  Administrator,  the  State  Administrator,  and the TVPSS  Management
Crew oversee these jobs.
Finally, the Student Achievement Management Subsystem is the fourth sub-goal. This part
of  the  system  is  for recognizing and  keeping  track  of  what  students  have  done  well.  It  has
features that let you make e-certificates for the students, which are official proof of what they've
done. It also lets students submit their successes, making sure that all their hard work is recorded
and recognized. The School Admin and State Admin are mostly in charge of these tasks and
make sure that student accomplishments are properly recorded and recognized in the system.
This part of the system is very important for helping students do well because it gives them an
official, organized way to be recognized for their hard work.

Figure 2.2: Goal Model of TVPSS Management Information System















## 8


## 2.1.1 System Interfaces
a) A Database Management System (DBMS) is built into the system interfaces to make
sure that school and student data is always available and safe.
b) A centralized TVPSS Database will hold all the information about the school, the users,
and the accomplishments of the students.
## 2.1.2 User Interfaces
The system's interface will be clear and easy to use. When users log in to the system, they will
see a homepage with login choices. While to login, they may only use the .moe domain email
to  login  to their account. Users  can  get  to  different menus  based  on  their jobs  once  they are
logged in. Super Admins will be able to view dashboards and handle user information. School
Admins will be able to manage school information and equipment, and students will be able to
see application results and send in their own. Users will be able to change things about their
profiles, like their passwords and personal information, through the interface.
## 2.1.3 Hardware Interfaces
The TVPSS Management Information System is compatible with laptops, desktop computers
and  mobile phones that  have  internet  connectivity.  The  system  does  not  require  additional
hardware  but  ensures  that  basic  input  devices  (keyboard  and  mouse)  are  functional  for  user
interaction.
## 2.1.4 Software Interfaces
The system will use the Database Management System and centralized TVPSS Data to organize
and store all data, including user information, school details, and student achievements. It will
interact with web browsers and mobile phone applications for user access and may integrate
with other school management software if necessary.
## 2.1.5 Communication Interfaces


## 9

The TVPSS Management Information System will use a strong internet connection. For data
security and privacy during transmission, it will use secure HTTP/HTTPS protocols. For alerts
and notifications, the system will also connect to email services.
## 2.1.6 Memory
The TVPSS Management Information System is based on data and needs a lot of space to store
that data. Cloud storage is the best option which will be used to store all school and student data
in a way that is both flexible and safe.
## 2.1.7 Operations
The TVPSS Management Information System will help the Super Admin, School Admin, State
Admin, TVPSS  Management Crew, and students do their jobs. It will process data and keep
track   of   things   like   user   information,   school   data,   equipment   records,   and   student
accomplishments. The system will also be able to do managerial tasks like reporting, updating,
and deleting data.
## 2.1.8 Site Adaptation Requirements
The system has been designed so that it can be used from anywhere with an internet connection.
A stable and fast internet connection is preferred for the best performance. The design of the
system makes sure that it works with popular web browsers, mobile applications and operating
systems.
## 2.2 Product Functions
The use case diagram in Figure 2.1 shows that the TVPSS Management Information System
has several important tasks that are coordinated with its subsystems. The super administrator
view  dashboard (UC001)  and manage user  information (UC002)  in  the  dashboard  and
administration subsystem. The School Admin can handle school information (UC006), manage
equipment  numbers  (UC008),  and validate school  crew  applications  (UC009)  in  the  School
Information Management Subsystem. Students can see the results of their applications (UC011)
and submit school crew application (UC012). The School Version Management Subsystem lets
users except student view school version status (UC003), verify school version status (UC005),
and manage school version status (UC007). This includes the School Admin, the State Admin,


## 10

and  the  TVPSS  Management  Crew.  The  School  Admin  and  State  Admin  can generate e-
certificates  for  students  (UC004)  and  send  in  student achievement (UC010)  in  the  Student
Achievement  Management  Subsystem.  These  features  make  sure  that  all  of  the  students'
accomplishments are recorded and recognized correctly in the system. Together, they help make
management across the school network more efficient and effective.
## 2.3 User Characteristics
There are six types of users that the system will connect to which are the Students, Super Admin,
School  Admin,  State  Admin,  PPD  Admin,  and  the  TVPSS  Management  Crew.  There  are
different jobs and permissions for each type of user. Overall system administration is handled
by   Super   Admins,   school-specific   tasks   are   handled   by   School   Admins,   state-level
administration is handled by State Admins, regional operations are supported by PPD Admins,
applications are checked by the TVPSS Management Crew, and students use the system to view
and send applications.

## 2.4 Constraints
a) The system is available only in Malaysia.
b) Login verification should be completed within five seconds with “.moe” domain   email.
c) The system interface supports Malay and English languages.
d) Only authorized admins can access comprehensive user data.
e) The user interface should load within 10 seconds.
f) Development technologies include JS, PHP, Laravel, React JS, Dart and MySQL.
g) TCP/IP protocol will be used for network communication.
h) Maximum system downtime should not exceed 1 hour.
i)      All user data will be encrypted before storage to ensure confidentiality.
2.5 Assumption and Dependencies
1) Some  people  think  that  the  system  will  mostly  be  web-based,  but  it  will  also  have  a
mobile app that can be used on computers, tablets, and smartphones and should work
pretty well. The system could not work if the devices do not have enough hardware tools
available.


## 11

2) The  system  is  designed  to  be  compatible  with  various  operating  systems,  including
macOS, Windows, Linux, iOS, and Android, ensuring broad accessibility.
3) There is an assumption that users with outdated devices or older versions of operating
systems may experience display issues, or a different interface appearance compared to
the intended design of the TVPSS Management Information System.
4) For the system to work at its best, it needs a stable and reliable internet link. When users
are  in  places  with  bad  connectivity,  they  may  see  slower  reaction  times  or  service
interruptions, which could make it harder for them to use the system.
2.6 Apportioning of Requirements
The main features of the TVPSS Management Information System are prioritized for both
web and mobile devices in the first version to make it easy for many people to access and use.
In  later  versions,  more  advanced  features  will  be  added,  such as  game-like elements  to  keep
students and staff interested, AI-powered insights for predicting success and resource use, and
VR  integration  for  more  immersive  learning  experiences.  Advanced  security  features  like
biometric identification and end-to-end encryption will be added, along with tools for working
together as a team in real time and a parent portal for keeping an eye on their child progress.
With cloud-based  document  storage, users can easily  view  school  documents  on  any  device,
and API integration, users can connect to other educational platforms without any problems.
More advanced reporting tools and user screens that can be changed will make the system even
easier to use and make sure it adapts to users' changing needs.

## 3. Specific Requirements


## 12


DM001 - Domain Model of TVPSS Management Information System

Based on Figure 3.0, the Domain Class Diagram (DCD) for the TVPSS Management
Information System consists of 19 classes: User, Role Type, Superadmin, State Admin, PPD
Admin, School Admin, TVPSS Management Crew, Equipment, Equipment Status, Application
Crew, Status  Type,  Student,  School,  School  Version,  Certificate,  Generate,  Version  Type,
Address, and School Information. The User class serves as the superclass, with Superadmin,
State Admin, PPD Admin, and School Admin as its subclasses, inheriting its properties.
The  User  class  is  associated  with  the  Role  Type  enumeration  class,  defining  the
roleType variable. The State Admin can generate certificates, while the School Admin validates
applications   submitted   by   students.   The   Application   Crew   class,   which   views these
submissions, has a status attribute linked to the Status Type enumeration class.



## 13

Moreover,  both  the  School  Admin  and  TVPSS  Management  Crew  manage  the
Equipment class, whose status is linked to the Equipment Status enumeration class. The school
class  aggregates  the  School  Admin  and  students  who  submit  applications.  It  also  has  a
composite relationship with the Address class and includes School Information.
Lastly,  the  School  Admin  can  submit  the  School  Version,  which  the  PPD  Admin
validates and the State Admin views. The School Version class is associated with the Version
Type enumeration class, detailing different version levels. This structured organization ensures
clear  role-based  access  and  efficient  management  of  school-related  data  within  the  TVPSS
system.



STD001 - State Transition Diagram for User Class
Based  on STD001,  the  state  transition  diagram  (STD)  outlines  how  the  User  and  its
subclasses process within the system. It begins at the login page, where users enter their email
and  password.  Upon  submission,  the  transition  submitLogin(email,  password)  will  validate
these credentials within the parameters. If the credentials are invalid, the system redirects to the
transition invalidCredential(), which then leads to the state redirecting to the login page with a
message. This transition leads to redirectWithError(), which redirects the user back to the login


## 14

page with an error message. If the credentials are valid, the system proceeds to check the user's
role. Next, the state will be based on the user's role, the system retrieves the appropriate data
according to the user role for the dashboard. Finally, the user is redirected to their respective
dashboard page according to their role type using getDataBasedOnRole.


STD002 - State Transition Diagram for Certificate Class
Based  on  STD002, the  state  transition  diagram  (STD)  outlines  how  the  flow  for
generating  and  sending  a  certificate  involving  the  Certificate,  Generate  and  State  Admin,
School Admin Class. The process begins when data is received, indicated by the isReceived()
function.  Upon  receiving  the  data,  the  submitData()  function  is  called,  which  transitions  the
process to the generate state. Here, the generateCert() function attempts to create a certificate.
If  the  certificate  generation  fails  it  will  then  transition  to  the  (failToGenerate()),  the  process
returns  to  the  generate  state  for  another  attempt.  However,  if  the  certificate  generation  is
successful it will then transition to the (isSucced()), the process moves to the automate state.
From  here,  two  parallel  actions  occur:  the creation  of  a  file  which  is  the  certificate  file
(createdFile()) which transitions to the send state, and the notification via email to the School


## 15

Admin Class  (notifyEmail(User.email)) which transitions to the send notification state. Finally,
both actions lead to the sent state, indicating the completion of the process.



STD003 - State Transition Diagram for Application Crew Class

Based on STD003, the state transition diagram (STD) outlines the flow for handling an
application submission, which includes validating the data and updating the application status
based on certain conditions. The process starts with the submitApplication() function, initiating
the flow with the data reception (data). Once the data is received (isReceived()), it undergoes
validation through the validate data function. After the data validation, the process moves to
submitData(),  followed  by  the  transition  to  the  application  data  state.  At  this  point,  the
application status is updated based on specific criteria. Then it will have a condition which if
the application is approved the updateStatus(Approved) function transitions the process to the
approvedStatus state. If the application is rejected, the updateStatus(Reject) function transitions
the process to the rejectStatus state. Then finally both paths converge at the successUpdate()
function,  leading  to  the  Notify  state,  where  a  notification  is  sent  to  the  user  regarding  the
application status.



## 16


STD004 - State Transition Diagram for School Version Class
Based on STD004, the state transition diagram (STD) outlines the process of handling
and validating school information, including submission version level, and sending notification.
The process begins with the getSchoolInfo() function, which retrieves the necessary data (data).
The  initial  data  submission  is  managed  by  the  submitVersion()  function,  transitioning  the
process to the versionData state. Once the version data is submitted, the PPD Admin is notified
through  the  notifyAdmin()  function.  This  leads  to  another  state  of  versionData,  where  the
version  is checked  (checkVersion()).  Following  this, the  data  undergoes  a  validation  process
(validate)  through  the  validateInfo()  function.  Then  it  will  determine  if  the  data  is  approved
(approved()). If the data is approved, the process moves to the Notify state, where notifications
are sent regarding the approval. If the version is rejected (versionReject()), the process loops
back to the data state, allowing for necessary corrections or resubmissions.



## 17

## 3.1 External Interface Requirements
## 3.1.1 User Interfaces
For the user interfaces, we will focus on both the user interface and user experience. We will
provide all user interfaces designed in the proposed system. We will follow the Google Material
system, a design system created and supported by Google designers and developers. This design
system includes detailed UX guidance and UI components for Android, Flutter, and the Web,
meeting  the  needs  of  stakeholders.  Additionally,  we  will  use  Nielsen's  heuristic  rules,  which
include ten principles such as usability, consistency, and standards. These rules match well with
the Google Material design system, making it easy to follow since they are quite similar.

## 3.1.1.1 User Interface Prototype Login Page


## 18


## 3.1.1.2 User Interface Prototype Dashboard Page

## 3.1.1.3 User Interface Prototype Crew Application Submission Page


## 19


## 3.1.1.4 User Interface Prototype Crew Application Result Page

## 3.1.1.5 User Interface Prototype Manage Equipment Page


## 20


## 3.1.1.6 User Interface Prototype School Information Page

## 3.1.1.7 User Interface Prototype Submit Version Page



## 21


## 3.1.1.7 User Interface Prototype Validate School Crew Application Page



## 22


3.1.1.8 User Interface Prototype Generate E-Cert Student Page 1/2



## 23


3.1.1.9 User Interface Prototype Prototype Generate E-Cert Student Page 2/2




## 24

## 3.1.2 Hardware Interfaces
These  are  the minimum  requirement  of  hardware details  that  the  TVPSS  Management
Information System will interact with:
For servers’ hardware:
## Processor Ram Storage Bandwidth
Intel Xeon E3 (4 Core) 16 GB 2’s 500 NVME SSD 100mbps
PC and Laptop Devices:
Operating System Processor RAM Storage Browser Internet
Windows 10 or
above / Mac OS /
## Linux
## Intel Core
i3 6
th
gen /
## AMD
## Ryzen 3
At least
## 4GB
## 120GB
of
storages
Browser such as
Google Chrome that
supports HTML5,
CSS grid and
flexbox.
## Equipped
with Wi-Fi
connection
or Lan port
## Phone Devices:
Operating System RAM Storage Browser Internet
## Android 8.0 /
HarmonyOS / IOS
At least
## 2GB
64 GB of
storages
Browser such as Google
Chrome that supports HTML5,
CSS grid and flexbox.
Equipped with
Wi-Fi
connection



## 25

## 3.1.3 Software Interfaces
These are the software details that the TVPSS Management Information System will interact
with:
## Software Interfaces Details
## Operating System Linux Ubuntu 24.04
Tailwind CSS Tailwind  CSS  is  an  open-source  CSS  framework that uses utility
classes  to  control  the  layout,  color,  spacing,  typography,  shadows,
and  more  to create  a completely  custom component  design  without
leaving the HTML or writing a single line of custom CSS.
React 18 React  is  a  front-end  JavaScript  library  that  is  free  and open  source
that is used to create user interfaces using components.
Laravel 11 A  free  and  open-source  web  framework  for  creating  powerful
applications for the web, Laravel is based on PHP.
Flutter Flutter  is  an  open-source  UI  software  development  kit  created  by
Google. Dart,  another  language  created  by  Google,  was  the  one
utilized  for  development.  With  Flutter,  cross-platform  applications
for the web, Fuchsia, Android, iOS, Linux, and macOS can be created
from a single codebase.
MySQL MySQL  is  an  open-source  relational  database  management  system
(RDBMS)  that  is  widely  used  for  managing  and  manipulating
structured data. It manages the data using structured query language.
MySQL  is  renowned  for  its  dependability,  user-friendliness,  and
efficiency.
Composer 2.7.7 Composer is an application-level dependency manager that offers a
common   format   for   handling   PHP   software   dependencies   and
necessary libraries.
NodeJS 22 Node.js   is   a   cross-platform,   open-source   JavaScript   runtime
environment that executes JavaScript code outside a web browser. It
let  developers  use  JavaScript  to  write  command  line  tools  and  for
server-side scripting.


## 26

Node package
manager (NPM)
NPM is a package manager for the JavaScript programming language
it is also the  default  package  manager  for  the  JavaScript  runtime
environment Node.js
Axios HTTP Axios HTTP is used to send HTTP requests from Node.js apps and
browsers. It makes managing responds and sending asynchronous
HTTP queries to web servers easier.
Visual Studio Code Visual Studio Code (VS Code), a small, free source code editor. It
gives programmers a strong and adaptable environment for writing,
modifying, and debugging code on Windows, macOS, and Linux,
among other platforms.
GitHub GitHub is an online platform that uses Git for version management.
It has functions including code review, issue tracking, repository
hosting, collaborative project management tools, and integration
with other services and tools for developers.
Git  Git is a distributed version control system that allows users to track
changes in source code during software development.
Git CLI The Git Command Line Interface (CLI) provides a set of commands
for interacting with Git repositories from the terminal or command
prompt. It enables users to perform tasks using text-based
commands.

## 3.1.4 Communication Interfaces
For the TVPSS Management Information System to function properly and always be accessible,
a  robust  internet  connection  is  required.  Secure  HTTP/HTTPS  protocols  with  SSL/TLS
encryption will be used to protect sensitive data during transmission. The system will employ
SSH to provide secure file transfers and server access. It will establish an SMTP connection
with email providers to send notifications and alerts.



## 27

## 3.2 System Features
3.2.1 Module Dashboard and Administration
The  Dashboard  and  Administration  Module  is  where  the  five  main  users  can  view  their
dashboard and where the Super Admin can manage users. This module lets users see a summary
of their data and allows the Super Admin to manage who can log in to the system. The functional
requirements are UC001 View Dashboard and UC002 Manage User Information.


Figure 3.2 Dashboard and Administration Module

3.2.1.1 UC001: Use Case View Dashboard
Table 3.2.1.1: Use Case Specification for View Dashboard
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-001
## Use Case Name: View Dashboard
## Created By: Adam Imran Bin Alwi Last Updated By:   Adam Imran Bin Alwi


## 28

## Date Created: 30 May 2024 Last Revision Date:  8 June 2024
Actors: Super Admin, State Admin, PPD Admin, School Admin TVPSS Management
Description: This use case describes how users with different roles such as Super Admin, State
Admin, PPD Admin, School Admin and TVPSS Management Crew can view the
dashboard, where each role having access to different data and functionalities
based on their roles and permission.
## Pre-conditions:
- The user must be logged into the system.
- The user must have the assigned roles.
Normal Flow: NF1 Success Login:
1.1. The session starts with data which is retrieved from the database.
1.2. The system checks for the roles based on the session.
1.3. The user will be redirected to the dashboard.
1.4. The system loads the dashboard with data and functionalities based on the
user's role.
NF2 User navigates to Dashboard:
2.1. The user selects the dashboard link from the navigation bar.
2.2. The system loads the dashboard with data and functionalities based on the
user's role
## Alternative
## Flow:
AF1: User Filters Dashboard Data:
1.1. User selects filter options such as date to view data.
1.2. System gets response filter and return XMLHttpRequest with filtered data.
Exception: EF1: Invalid User Role:
1.1. System fails to recognize the user's role.
1.2. System displays error page with response code: "403 Invalid user role."
EF2: Data Server Response Failure:
2.1. System encounters an error while loading the dashboard data.
2.2. System  displays  an  error  message:  "Something  went  wrong.  Please  try
again later."
EF3: Session Timeout:
3.1. User's session times out due to inactivity.
3.2. System redirects the user to the login page with an error message:  "Current
session timed out. Kindly log in."
3.3. User logs in again to access the dashboard.
EF4: Unauthorized Access:
4.1. System detects that the user does not have the necessary roles   to view   the
dashboard.


## 29

4.2. System displays an error message: "Error Code 403: Unauthorized"
## Post-conditions: S1 Success Login:
The system loads the dashboard with data and functionalities based on the user's
role.
## S2 Invalid User Role:
System displays error page with response code: "403 Invalid user role."
## S3 Data Server Response Failure:
System displays an error message: "Something went wrong. Please try again
later."
## S4 Session Timeout:
System redirects the user to the login page with an error message:  "Current
session timed out. Kindly log in."
## S5 Unauthorized Access:
System displays an error message: "Error Code 403: Unauthorized”.
## Related
## Requirement:
ID Requirement Priority
FR UC-001-01 The system shall allow users with different roles
(Super Admin, State Admin, PPD Admin, School
Admin, TVPSS Management) to view the
dashboard.
## Basic
FR UC-001-02 The system shall retrieve data from the database
based on the user's role and permissions to
populate the dashboard.
## Basic
FR UC-001-03 The system shall provide different functionalities
on the dashboard based on the user's role and
permissions.
## Basic
QR UC-001-01 The system shall ensure seamless navigation to
the dashboard from the login page without any
interruptions.
## Performance
QR UC-001-02 The system shall provide responsive and timely
data loading on the dashboard to ensure a smooth
user experience.
## Performance
QR UC-001-03 The system shall handle session timeouts
gracefully, redirecting users to the login page
with appropriate error messages.
## Performance


## 30

CR UC-001-01 The system shall detect and handle cases of
invalid user roles, displaying an error page with a
response code "403: Invalid user role."
## Performance
CR UC-001-02 The system shall detect unauthorized access
attempts and display an error message "Error
## Code 403: Unauthorized."
## Basic




Figure 3.2.1.1: Activity Diagram of View Dashboard





## 31

3.2.1.2 UC002: Manage User Information
Table 3.2: Use Case Specification for Manage User Information
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-002
## Use Case Name: Manage User Information
## Created By: Jessie Chang Last Updated By:  Adam Imran Bin Alwi
## Date Created: 30 May 2024 Last Revision Date:  8 June 2024
## Actors: Super Admin
Description: This use case allows the Super Admin to manage user information within the
system, including creating new user profiles, updating existing user details,
viewing user information, and deleting user accounts.
Pre-conditions: 1. The Super Admin must be logged into the system.
- The system must have access to the user database and necessary permissions to
modify user data.
- UC001 is performed by Super Admin
Normal Flow: 1. Super Admin chooses to manage user information.
- Super Admin chooses to perform the operation (AF1, AF2, AF3, AF4, AF5)
- Use case ends.
## Alternative
## Flow:
AF1. Create User:
1.1 The system displays a form for creating a new user.
1.2 The Super Admin enters the required user information such as name, email
and role.
1.3 The system validates the entered information. (EF1)
1.4 The system saves the new user information to the database.
1.5 The system displays a confirmation message indicating successful creation
of the user.
AF2. Update User:
2.1 The system retrieves and displays the user list. (EF2)
2.2 The Super Admin selects a user to update from the user list.
2.3 The system displays the current information of the selected user.
2.4 The Super Admin modifies the necessary information.


## 32

2.5 The system validates the updated information. (EF1)
2.6 The system updates the user information in the database.
2.7 The system displays a confirmation message indicating successful update
of the user information.
AF3. Delete User:
3.1 The system retrieves and displays the user list. (EF2)
3.2 The Super Admin selects a user to delete from the user list.
3.3 The system prompts the Super Admin to confirm the deletion.
3.4 The Super Admin confirms the deletion. (EF1)
3.5 The system removes the user information from the database.
3.6 The system displays a confirmation message indicating successful deletion
of the user.
AF4. View User:
4.1 The system retrieves and displays the user list. (EF2)
4.2 The Super Admin selects a user view.
4.3 The system displays the selected user information. (EF3)
AF5. Cancel Operation:
5.1 The Super Admin can choose to cancel the operation at any point.
5.2 The Super Admin clicks the “Cancel” button.
5.3 The system cancels the current operation and discards any unsaved
changes.
5.4 The system returns the Super Admin to the user management section
without making any changes.
Exception: EF1. Validation Failure:
1.1 The system detects invalid or incomplete information.
1.2 The system displays an error message indicating the issue.
1.3 The Super Admin corrects the information and resubmits the form.
EF2. Data Retrieval Failure:
2.1 The system encounters an error while retrieving the user list.
2.2 The system logs the error and displays an error message to the Super
Admin indicating a failure to retrieve the data.
2.3 The Super Admin can retry the operation or contact technical support.
EF3. Database Error:
3.1 The system encounters an error while accessing the database.
3.2 The  system  displays  an  error  message  to  the  Super  Admin  indicating  a
failure to process the request.


## 33

3.3 The Super Admin can retry the operation or contact technical support.

Post-conditions: 1. The  user  information  is  successfully  created,  updated,  or  deleted  in  the
system database.
- The system reflects the changes immediately in the user webpage, ensuring
up-to-date information for all system users
## Related
## Requirement:
ID Requirement Priority
FR UC-002-01 The system shall allow the Super Admin to
manage user information within the system.
## Basic
FR UC-002-02 The system shall provide functionality for
creating new user profiles.
## Basic
FR UC-002-03 The system shall provide functionality for
updating existing user details.
## Basic
FR UC-002-04 The system shall provide functionality for
viewing user information.
## Basic
FR UC-002-05 The system shall provide functionality for
deleting user accounts.
## Basic
QR UC-002-01 The system shall display a list of created users in
the system database.
## Performance
QR UC-002-02 The system shall display the list of created users. Basic
QR UC-002-03 The system shall retrieve and display the user
list.
## Basic
QR UC-002-04 The system shall display a confirmation message
indicating successful creation of the user.
## Basic
CR UC-002-01 The system shall validate the entered user
information.
## Performance




## 34



Figure 3.2.1.2: Activity Diagram of Manage User Information



## 35

## 3.2.2 Module School Information Management
The School Information Management module is a subsystem that includes all the features to manage or
retrieve school  information by  the  school  internal stakeholders such  as  student,  school  admin  and
TVPSS Management Crew.  School admin and TVPSS management crew can always update and modify
the information as well  as the  equipment inventory. Students can apply to become one of the TVPSS
crew  and view  the  application  result  on  their  dashboard  whereas  the  application  will  be  validate  by
school admin. Functional requirements for this modules includes UC006: Manage School Information,
UC008:  Manage  Equipment  Number,  UC009:  Validate  School  Crew  Application,  UC011:  View
Application Result and UC012: Submit School Crew Application.

## Figure 3.2.2: School Information Management Module


3.2.2.1 UC006: Manage School Information


## 36

Table 3.2.2.1: Use Case Specification for UC006 Manage School Information
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-006
## Use Case Name: Manage School Information
## Created By: Muhammad Aiman Haiqal
bin Salehuddin
## Last Updated By:  Elvis Chang Feng Jie
## Date Created: 30 May 2024 Last Revision Date:  12 May 2024
Actors: School Admin  ,TVPSS Management Crew
Description: This use case allows the School Admin and TVPSS Management Crew to manage
and update school information, including name, address, contact details, and other
relevant data to ensure that the school information is in real-time data and accurate
in the system

Pre-conditions: 1. Both actor must be logged into the system using .MOE domain email.
- The   actor   must   have   the necessary   permissions   to   update   school
information.
Normal Flow: 1. The  actor  selects  the  "Manage  School  Information"  option  from  the
dashboard.verify
- The system displays the current school information in an editable form.
- The actor updates the necessary fields with new information.
- The actor submits the changes.
- The system validates the inputs and updates the school information in the
database.
- The system confirms the update with a success message.


## 37

## Alternative
## Flow:
AF1. Invalid data input
1.1. The actor enters invalid data.
1.2. The  system  displays  an  error  message  indicating  the  invalid  data  and
prompts the actor to correct it.
1.3. The actor corrects the data and resubmits.
1.4. The system validates the inputs and updates the school information in the
database.
1.5. The system confirms the update with a success message.
Exception: EF1. System failure to update database
1.1. The system encounters an error while trying to update the database.
1.2. The  system  displays  an  error  message  indicating  that  the  update
failed.
1.3. The actor is prompted to retry the operation later or contact support.

Post-conditions: 1. The school information is updated and stored in the system database.
- The  system  logs  the  changes  made  to  the  school  information  for  audit
purposes.

## Related
## Requirement:
ID Requirement Priority
## FR UC-006-
## 01
The system shall be allow school admin and
TVPSS management crew to manage school
information.
## Basic
## FR UC-006-
## 02
The system shall be able to retrieve the existing
school information from the database and display
it in an editable form.
## Basic
## FR UC-006-
## 03
The system shall validate the updated school
information before saving it to the database.
## Basic
## FR UC-006-
## 04
The system shall provide clear error messages for
invalid data input during school information
update.
## Basic
## QR UC-006-
## 01
The system shall display a confirmation message
upon successful update of school information.
## Usability
## QR UC-006-
## 02
The system shall log all changes made to school
information, including the user who made the
## Security


## 38

changes and the timestamp, for auditing
purposes.
## CR UC-006-
## 01
The system shall be able to handle concurrent
updates to school information by multiple users
without causing data inconsistencies.
## Performance




## 39



Figure 3.2.2.1: Activity Diagram of UC006 Manage School Information



## 40



3.2.2.2 UC008: Manage Equipment Number
Table 3.2.2.2: Use Case Specification for UC008 Manage Equipment Number
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-008
## Use Case Name: Manage Equipment Number
## Created By: Adam Imran Bin Alwi

## Last Updated By: Elvis Chang Feng Jie
## Date Created: 30 May 2024 Last Revision Date:  12 June 2024
Actors: School Admin  ,TVPSS Management Crew

Description: This  use  case  describes  how  the school and management  team  can manage the
number  of  equipment  available.  The  user  can list  the  names  and  their  quantities
based on its category.

Pre-conditions: 1. The user must be logged into the system.
- The   user   must   have   the   assigned   roles   (School  Admin  or   TVPSS
## Management Crew).

Normal Flow: NF1: View Equipment List
The user navigates to the equipment management section.
The system retrieves and displays a list of all equipment categorized by
their category.
NF2: Update Equipment Number
## 1.
## 2.
The user selects an equipment item to update.
The system displays the current number of the equipment and its name.
The user enters the new number for the selected equipment or name.
The user confirms the update.
The system updates the quantity or name of the selected equipment in
the database.
The system displays a success message to the user.


## 41

NF3: Add New Equipment
## 1.
## 2.
## 3.
The user selects the option to add new equipment.
The system prompts the user to enter the details of the new equipment
such as name and quantity.
The user enters the details and confirms the addition.
The system adds the new equipment to the database.
The system displays a success message to the user.
NF4: Delete Equipment
## 1.
## 2.
## 3.
## 4.
The user selects an equipment item to remove.
The system prompts the user to confirm the removal.
The user confirms the removal.
The system removes the equipment from the database.
The system displays a success message to the user.

Alternative Flow: AF1: User Filters Equipment List
The user selects filter options (e.g. by name, type, quantity).
The system filters the equipment list based on the selected criteria and
displays the filtered list.
AF2: User Search Equipment
## 1.
## 2.
The  user  searches  for  equipment  filter  options  (e.g.,  by  name,  type,
quantity).
The system returns the equipment data based on the user search.

Exception: EF1: Invalid User Role
The system fails to recognize the user's role.
The system displays an error page with response code: "403 Invalid user
role."


## 42

EF2: Data Server Response Failure
## 1.
## 2.
The system encounters an error while retrieving, updating, or deleting
the equipment data.
The system displays an error message: "Something went wrong. Please
try again later."
EF3: Unauthorized Access
## 1.
## 2.
## 3.
The  system  detects  that  the  user  does  not  have  the  necessary  roles  to
manage the equipment.
The system displays an error message: "Error Code 403: Unauthorized."


## Post-conditions: S1: Success Update
The system successfully updates the number of the selected equipment.
## S2: Success Addition
The system successfully adds the new equipment to the database.
## S3: Success Deletion
The system successfully deletes the selected equipment from the database.
## S4: Invalid User Role
The system displays an error page with response code: "403 Invalid user role."
## S5: Data Server Response Failure
The  system  displays  an  error  message:  "Something  went  wrong.  Please  try
again later."
## S7: Unauthorized Access
The system displays an error message: "Error Code 403: Unauthorized."

## Related
## Requirement:
ID Requirement Priority
## FR UC-008-
## 01
The system shall allow School Admin and
TVPSS Management Crew to view a list of all
equipment.
## Basic
## FR UC-008-
## 02
The system shall allow School Admin and
TVPSS Management Crew to update the quantity
and name of existing equipment.
## Basic


## 43

## FR UC-008-
## 03
The system shall allow School Admin and
TVPSS Management Crew to add new
equipment with details such as name, type, and
quantity.
## Basic
## FR UC-008-
## 04
The system shall allow School Admin and
TVPSS Management Crew to delete existing
equipment.
## Basic
## QR UC-008-
## 01

The system shall display a confirmation message
before deleting equipment to prevent accidental
deletions.
## Usability
## QR UC-008-
## 02
The system shall display an error message if the
user does not have the necessary permissions to
manage equipment (Error Code 403:
## Unauthorized).
## Security
## QR UC-008-
## 03
The system shall display an error message if
there is a failure retrieving, updating, or deleting
equipment data ("Something went wrong. Please
try again later.").
## Reliability
## QR UC-008-
## 04
The system shall maintain a log of all equipment
management activities (view, update, add, delete)
with timestamps and user information.
## Security
## CR UC-008-
## 01
The system should only allow one user to update
equipment list at time to ensure data consistency
## Performance



## 44



Figure 3.2.2.2: Activity Diagram of UC008 Manage Equipment Number




## 45

3.2.2.3 UC009: Validate School Crew Application
Table 3.2.2.3: Use Case Specification for UC009 Validate School Crew Application
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-009
## Use Case Name: Validate School Crew Application

## Created By: Adam Imran Bin Alwi Last Updated By:  Elvis Chang Feng Jie
## Date Created: 30 May 2024 Last Revision Date:  12 June 224
## Actors: School Admin
Description: This use case describes how the Admin School validates applications from students
who apply to join the system as TVPSS Management Crew. The School Admin can
approve or reject applications based on user criteria.

Pre-conditions: 1. The user must be logged into the system.
- The user must have the assigned roles which is Admin School
Normal Flow: NF1: View Pending Applications
The Admin School navigates to the application management section.
The   system   retrieves   and   displays   a   list   of   all   pending   student
applications.
NF2: Review Application
## 1.
## 2.
The School Admin selects a student application to review.
The system displays the details of the selected application, including the
student's information and application criteria.
NF3: Approve Application
## 1.
## 2.
## 3.
The School Admin decides to approve the application.
The School Admin clicks on the "Approve" button.
The system updates the application status to "Approved" in the database.
The system displays a success message to the School Admin.


## 46

NF4: Reject Application
## 1.
## 2.
## 3.
## 4.
The School Admin decides to reject the application.
The School Admin clicks on the "Reject" button.
The  system  prompts  the  School  Admin  to  provide  a  reason  for  the
rejection.
The School Admin enters the rejection reason and confirms the action.
The system updates the application status to "Rejected" in the database.
The system displays a success message to the School Admin.

## Alternative
## Flow:
AF1: Filter Applications
The  Admin  School  selects  filter  options  (e.g.,  by  date,  by application
status).
The system filters the application list based on the selected criteria and
displays the filtered list.
AF2: Search Applications
## 1.
## 2.
The Admin School type on the search box such as application name
The system filters the application list based on the search.

Exception: EF1: Invalid User Role
The system fails to recognize the School Admin's role.
The system displays an error page with response code: "403 Invalid user
role."
EF2: Data Server Response Failure
## 1.
## 2.
The system encounters an error while retrieving or updating application
data.
The system displays an error message: "Something went wrong. Please
try again later."
EF3: Unauthorized Access


## 47

## 1.
## 2.
## 3.
The  system  detects  that  the  user  does  not  have  the  necessary  roles  to
access the page.
The system displays an error message: "Error Code 403: Unauthorized."

## Post-conditions: S1: Application Approved
The  system  successfully  updates  the  application  status  to  "Approved"  and
notifies the student.
## S2: Application Rejected
The system successfully updates the application status to "Rejected," records
the rejection reason, and notifies the student.
## S3: Invalid User Role
The  system  displays  an  error  page  with  response  code:  "403  Invalid  user
role."
## S4: Data Server Response Failure
The system displays an error message: "Something went wrong. Please try
again later."
## S6: Unauthorized Access
The system displays an error message: "Error Code 403: Unauthorized."

## Related
## Requirement:
ID Requirement Priority
## FR UC-009-
## 01
The system shall allow the School Admin to
view a list of all pending student applications for
the TVPSS Management Crew role
## Basic
## FR UC-009-
## 02
The system shall display the details of each
student application, including student
information and application criteria
## Basic
## FR UC-009-
## 03
The system shall allow the School Admin to
approve student applications, updating the
application status to "Approved" and notifying
the student.
## Basic
## FR UC-009-
## 04
The system shall allow the School Admin to
reject student applications, prompting for a
reason, updating the application status to
"Rejected," recording the reason, and notifying
the student.
## Basic


## 48

## QR UC-009-
## 01
The system shall provide filtering and search
options for the application list based on criteria
like date and application status.
## Usability
## QR UC-009-
## 02
The system shall display an error message if the
user does not have the necessary permissions to
manage applications (Error Code 403:
## Unauthorized).
## Security
## QR UC-009-
## 03
The system shall display an error message if
there is a failure retrieving or updating
application data ("Something went wrong. Please
try again later.").
## Reliability
## QR UC-009-
## 04
The system shall maintain a log of all application
validation activities (view, approve, reject) with
timestamps, user information, and rejection
reasons.
## Security

## QR UC-009-
## 05
The system shall allow for approving or rejecting
multiple applications at once.
## Usability

## QR UC-009-
## 06

The system shall notify the School Admin of new
student applications via email or in-app
notifications.
## Usability




## 49



Figure 3.2.2.3: Activity Diagram of UC009 Validate School Crew Application



## 50

3.2.2.4 UC011: View Application Result

Table 3.2.2.4: Use Case Specification for UC011 View Application Result
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-0011
## Use Case Name: View Application Result
## Created By: Elvis Chang Feng Jie Last Updated By:  Elvis Chang Feng Jie
## Date Created: 30 May 2024 Last Revision Date:  12 June 2024
## Actors: Student
Description: This use case shows the flow of students that intend to check for their TVPSS crew
application result.

Pre-conditions: 1. The student must be logged into the TVPSSS system.
- The  student  must  have  previously  submitted  an  application  to  join  a
TVPSSS crew.
- The  student  must  have  previously  participated  in  the  test  and interview
session.
Normal Flow: NF1: View Application Result
- The  student  navigates  to  the  "My  Application"  section  of  the  TVPSS
student system.
- The  system  displays  the  details  of  the  student's  current  application,
including:
## 2.1. Student Name
## 2.2. Application Position
## 2.3. Application Date
## 2.4. Application Status
## 2.4.1. Accepted
2.4.1.1. The   system   will   provide   confirmation
steps    and    acceptance    letters    to    accepted
applicants.
## 2.4.2. Rejected


## 51

2.4.2.1. The  system  will  provide  brief  feedback
and comments by evaluator.
## 2.4.3. Pending


Alternative Flow: AF1: Application Details
- The  student  may  have  the  option  to  view  more  details  about  their
application test results at any point in the process.
Exception: EF1: No Current Application
- If  the  student  does  not  have  a  pending application,  the  system  displays  a
message indicating this.
Post-conditions: 1. The student is informed of their current application status and any relevant
details.
- If accepted, the student may be prompted to complete further onboarding
steps.
- Student information and school crew list is updated.

## Related
## Requirement:
ID Requirement Priority
## FR UC-011-
## 01
The system shall allow students to view the
details of their current TVPSS crew application,
including student name, application position,
application date, and application status.
## Basic
## FR UC-011-
## 02
The system shall display the application status as
"Accepted," "Rejected," or "Pending."
## Basic
## FR UC-011-
## 03
For accepted applications, the system shall
provide confirmation steps and an acceptance
letter to the student.
## Basic
## FR UC-011-
## 04
For rejected applications, the system shall
provide brief feedback and comments from the
evaluator.
## Basic
## QR UC-011-
## 01
The system shall update the student information
and school crew list upon acceptance of an
application.
## Performance
## QR UC-011-
## 02
The system shall allow the student to view more
details about their application and test results.
## Usability


## 52

## CR UC-011-
## 01
The system must display a clear message if the
student does not have a current application.

## Usability




Figure 3.2.2.4: Activity Diagram of UC011 View Application Result







## 53



3.2.2.5 UC012: Submit School Crew Application

Table 3.2.2.5: Use Case Specification for UC012 Submit School Crew Application
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-0012
## Use Case Name: Submit School Crew Application
## Created By: Elvis Chang Feng Jie Last Updated By:  Elvis Chang Feng Jie
## Date Created: 30 May 2024 Last Revision Date:  12 June 2024
## Actors: Student
Description: This use case shows the process of a student that submit the application for a specific
position in the TVPSS management crew.

Pre-conditions: 1. The student must be logged into the TVPSSS system.
- The   student   must   not   have   any   pending   or   active   TVPSSS   crew
applications.
Normal Flow: NF1: Submit School Crew Application
- The  student  navigates  to  the  "Crew  Applications"  of  the  TVPSS  student
system.
- The system displays a list of available crew positions with descriptions.
- The student selects the desired position and clicks "Apply."
- The system validates the application data based on eligibility.
- If valid, the system records the application, marking it as "Pending "
- The   system   displays   a   confirmation   message   indicating   successful
submission.
## Alternative
## Flow:
AF1: Cancel Application
- The student can cancel the application process before submitting.


## 54

Exception: EF1: Existing Application
-  If the student already has a pending application, the system displays an
error message and prevents them from applying again.
EF2: No Open Positions
- If there are positions are currently not open for application, the system
excludes them from the application list.

Post-conditions: 1. The student's application is recorded in the system with "Pending Review"
status.
- The system schedules the student's test and interview based on the dates set
by School Admin.
- The student is notified about the test and interview date.
## Related
## Requirement:
ID Requirement Priority
## FR UC-012-
## 01
The system shall allow students to view and
select from a list of available TVPSS crew
positions with descriptions.
## Basic
## FR UC-012-
## 02
The system shall validate student application data
based on eligibility criteria.
## Basic
## FR UC-012-
## 03
The system shall record valid applications with a
"Pending Review" status.
## Basic
## FR UC-012-
## 04
The system shall allow students to cancel their
application before submission.
## Basic
## QR UC-012-
## 01
The system shall display a confirmation message
upon successful application submission.
## Usability
## QR UC-012-
## 02
The system shall schedule the student's test and
interview based on dates set by the School
Admin upon successful application submission.
## Efficiency
## QR UC-012-
## 03
The system shall notify the student about the
scheduled test and interview date.
## Usability
## CR UC-012-
## 01
The system shall display an error message if the
student has a pending application.
## Usability
## CR UC-012-
## 02

The system must exclude positions that are not
open for application from the list presented to
students.
## Performance




## 55



Figure 3.2.2.5: Activity Diagram of UC012 Submit School Crew Application









## 56

## 3.2.3 Module School Version Management
The  School  Version module is  a  module that encompasses the entire process from
viewing to managing the status of the school's version system. It begins with the State Admin,
who reviews and checks if the system needs an update. If an update is necessary, the School
Admin  or  TVPSS  Management is notified  to manage their current school’s version details.
Then,  the PPD  Admin will verify and  approve the updates of the school’s version  status,
ensuring  they  meet the  criteria. The  functional requirements include UC003:  View  School
Version  Status,  UC005:  Verify  School  Version  Status, and UC007:  Manage  School  Version
## Status.

Figure 3.2: School Version Module/Sub-System

3.2.3.1 UC003: View School Version Status
Table 3.2.3.1: Use Case Specification for View School Version Status
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC003
## Use Case Name: View School Version Status


## 57

## Created By: Jessie Chang Last Updated By:  Jessie Chang
## Date Created: 27 May 2024 Last Revision Date:  10 June 2024
## Actors: State Admin
Description: This use case allows the State Admin to view the current version status of the
school’s information system. The version status includes details such as the current
school version, latest or any pending of school’s information updates.
Pre-conditions: 1. The State Admin must be logged into the system.
- The system must have available school’s version status information for
viewing.
- UC001 is performed by State Admin.
Normal Flow: 1. The use case starts when the State Damin has carried out UC001.
- State Admin can choose to perform the operation (AF1, AF2)
- Use case ends.
## Alternative
## Flow:
AF1. View School Version Status:
1.1 The State Admin selects the option to view the school version status from
the dashboard.
1.2 The system retrieves the version status data of the school. (EF1)
1.3 The system displays the current version status to the State Admin.
AF2. Check for updates:
2.1 The State Admin decides on school version status needs to be update.
2.2 The system sends and notifies relevant users on information updates.
AF3. Cancel Operation:
3.1 The State Admin decides to cancel the viewing operation.
3.2 The State Admin clicks the “Cancel” button.
3.3 The system cancels the operation and returns to the previous section.
Exception: EF1. Data Retrieval Failure:
1.1 The system encounters an error while retrieving the school version status
data.
1.2 The system logs the error and displays an error message to the State Admin
indicating a failure to retrieve the data.
1.3 The State Admin can retry the operation or contact technical support.
Post-conditions: 1. The current version status information is successfully displayed to the State
## Admin.
## Related
## Requirement:
ID Requirement Priority
FR UC003-01 The system shall allow the State Admin to view
the version status of all schools.
## Basic


## 58

FR UC003-02 The system shall be able to display the current
version status information for each school.
## Basic
QR UC003-01 The system shall retrieve and display the school
version status information within 5 seconds.
## Performance
QR UC003-02 The system shall provide a user-friendly interface
for viewing the school version status.
## Excitement
QR UC003-03 The system shall notify the school that their
school version status needs to be updated.
## Performance
CR UC003-01 The system shall ensure that the displayed school
version status data is accurate, consistency and
up-to-date.
## Performance
CR UC003-02 The system shall prompt confirmation by
clicking ‘Cancel’ option for cancel viewing.
## Performance



Figure 3.2.3.1: Activity Diagram of UC003 View School Version Status


## 59


3.2.3.2 UC005: Verify School Version Status
Table 3.2.3.2: Use Case Specification for Verify School Version Status
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC005
## Use Case Name: Verify School Version Status
## Created By: Muhammad Aiman Haiqal
bin Salehuddin
## Last Updated By:  Jessie Chang
## Date Created: 27 May 2024 Last Revision Date:  10 June 2024
Actors: Pejabat Pendidikan Daerah (PPD) / District Admin
Description: This use case describes the process by which a Pejabat Pendidikan Daerah (PPD)
Admin verifies the version status of a school's TV PSS (Television Pusat Sumber
Sekolah) based on predefined criteria. The PPD Admin ensures that each school
has met the necessary equipment and setup requirements to achieve a specific
version status. Each version has specific criteria that must be fulfilled, and the PPD
Admin is responsible for verifying that these criteria are met before confirming the
school's version status. After the school has submitted their version status, the PPD
Admin has about 2 weeks to verify the status through an email notification.
Pre-conditions: 1. The school has submitted a request for verification of their TV PSS version
status.
- The  PPD  Admin  has  access  to  the  verification  system  and  the necessary
information about the school's equipment and setup.
- The  predefined  criteria  for  each  version  status  are  clearly  defined  and
accessible to both the school and the PPD Admin.
Normal Flow: 1. School  Submission:    The  school  admin  a  request  to  the PPD  Admin  for
verification of the TVPSS program version status.
- Login: The  PPD  Admin  logs  into  the  verification  system  using  their
credentials.
- Retrieve  Submission:  The  system  displays  the  list  of  schools  that  have
requested verification.


## 60

- Select School : The PPD Admin selects a school from the list to review their
submission.
- Review Criteria : The system displays the criteria for each TV PSS version.
The PPD Admin reviews the school's submission against the criteria.
- Verify Compliance : The PPD Admin checks if the school has fulfilled the
requirements for the requested version (e.g., presence of a name/brand, logo,
corner/mini studio, in-school recording, YouTube uploads, recording inside
and  outside  the  school,  collaboration  with  external  agencies,  using  'Green
Screen' technology).
- Update Status : If the school meets all the criteria for the requested version,
the  PPD  Admin  updates  the  school's  version  status  in  the  system.  If  the
school  does  not meet  the  criteria,  the  PPD  Admin  records  the deficiencies
and notifies the school.
- Confirmation : The system confirms the update and notifies the school of
their verified version status.
- Email  Notification:  The  system  sends  an  email  notification  to  the  PPD
Admin, reminding them that they have about 2 weeks to verify the school's
version status.
## Alternative
## Flow:
AF1. Cancel operation
1.1 At any point, the PPD Admin can cancel the verification process.
1.2 The system will save the current state and allow the PPD Admin to resume
later.
Exception: EF1. System failure to update database
1.1 If the system fails to update the school’s version status due to a technical
issue, the PPD Admin is notified.
1.2 The  PPD  Admin  can  retry  the  update  or  escalate  the  issue  to  technical
support.
EF2. Incomplete submission
2.1 If the school’s submission is incomplete, the system alerts the PPD Admin.
2.2 The  PPD   Admin   notifies   the   School   Admin   to  provide   the   mission
information before verification can proceed.
Post-conditions: 1. The school’s version status is updated in the system if all criteria are met.
- The school is notified of their verified version status or the deficiencies that
need to be addressed.
ID Requirement Priority


## 61

## Related
## Requirement:
FR UC005-01 The system shall automatically send reminders to
PPD Admins for pending verifications.
## Performance
FR UC005-02 The system shall allow the PPD Admin to verify
if the school meets the criteria for the requested
version.
## Basic
FR UC005-03 The system shall allow PPD Admin to view
historical version status and verification records
of the selected schools.
## Basic
FR UC005-04 The system shall be able to display the criteria
list for each TVPSS version before updating the
school’s version status in the system.
## Basic
FR UC005-05 The system shall allow the PPD Admin to update
the school’s version status in the system.
## Performance
QR UC005-01 The system shall provide reminders to the PPD
Admin about pending verifications within 2
weeks.
## Excitement
CR UC005-02 The system shall prompt confirmation by
clicking ‘Cancel’ option for cancel viewing the
displayed list of school pending verifications.
## Performance
CR UC005-03 The system shall be able to send email
notification to school after the school’s version
status has been successfully updated in system
database
## Performance



## 62


Figure 3.2.3.2: Activity Diagram of UC005 Verify School Version Status



## 63

3.2.3.3 UC007: Manage School Version Status
Table 3.2.3.3: Use Case Specification for Manage School Version Status
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC007
## Use Case Name: Manage School Version Status
## Created By: Jessie Chang Last Updated By:  Jessie Chang
## Date Created: 30 May 2024 Last Revision Date:  10 June 2024
Actors: School Admin, TVPSS Management Crew
Description: This use case allows users, such as School Admin and TVPSS Management Crew,
to manage different versions of the school version system. This includes updating
the system to new versions, verifying the current version, and ensuring that the
school’s version system is running the latest updates and security patches.
Pre-conditions: 1. The users must be logged into the system.
- The system must have access to the version control database.
- UC001 is performed by School Admin or TVPSS Management Crew.
Normal Flow: 1. Users such as School Admin and TVPSS Management Crew chooses to
manage school version status from UC001.
- System displays school current version information.
- User chooses to perform the operation. (AF1, AF2, AF3)
- Use case ends.
## Alternative
## Flow:
AF1. Update School Version:
1.1 The system displays the current version information along with an option
to update the version.
1.2 The user selects the option to update the version.
1.3 The system displays a form to enter new school’s status details for new
version updates.
1.4 The user enters the new school’s status details and submits the form.
1.5 The system validates the entered information. (EF1)
1.6 The system updates the school version information in the database.
1.7 The system displays a confirmation message indicating successful
verification of the version status.


## 64

AF2. Verify School Version:
2.1 The system retrieves and displays the current version status.
2.2 The user verifies the version information.
2.3 The system displays the school’s version status is up-to-date. (EF2)
2.4 The user views and confirms that the school’s version status is up-to-date.
2.5 The system records the verification status in the database.
2.6 The system displays a confirmation message indicating successful
verification of the version status.
AF3. Cancel Operation:
3.1 The user decides to cancel the operation at any point.
3.2 The user clicks the “Cancel” button.
3.3 The system cancels the current operation and returns to the previous section
without making any changes.
Exception: EF1. Validation Failure:
1.1 The system detects invalid or incomplete version information.
1.2 The system displays an error message indicating the issue.
1.3 The user corrects the information and resubmits the form.
EF2. Database Error:
1.1 The system encounters an error while accessing the database.
1.2 The system logs the error and displays an error message to the user.
1.3 The user can retry the operation or contact technical support.
Post-conditions: 2. The  school  version  information  is  successfully  updated  or  verified  in  the
system database.
## Related
## Requirement:
ID Requirement Priority
FR UC007-01 The system shall allow the School Admin and
TVPSS Management crew to manage the current
version status of the school's information system.
## Basic
FR UC007-02 The system shall be able to display the list of
school’s current version information
## Basic
FR UC007-03 The system shall be able to allow School Admin
and TVPSS Management Crew to enter new
school details into the School Version form.
## Basic
FR UC007-04 The system shall notify relevant users about
information updates and manage their version
details.
## Basic


## 65

QR UC007-01 The system shall validate the school crew
application within 3 seconds.
## Performance
QR UC007-02 The system shall be able to display error message
if validation fails
## Performance
QR UC007-03 The system shall ensure that all updates are
backed up in real-time to prevent data loss.
## Performance
CR UC007-01 The system shall prompt confirmation for
submission before submitting the school’s
version form.
## Performance












## 66



Figure 3.2.3.3: Activity Diagram of UC007 Manage School Version Status




## 67

## 3.2.4 Module Student Achievement Management
Administrators  at  the  school  and  state  level  can  use  the  Student  Achievement
Management   module   to   keep   track   of   students'   accomplishments   and   make digitized
recognition for them. This module's main tasks are to send student achievements and make e-
certificates for students. These modules must be completed in order to work which are UC004
Generate E-Cert Student and UC010 Submit Student Achievement. The activities in the Student
Achievement Management Module are shown in Figure 3.2. The State Administrator can make
e-certificates  for  students,  while  the  School  Administrator is  in  charge  of  reporting  students'
accomplishments. These steps are very important for keeping correct records of what students
have accomplished and giving them official recognition through e-certificates.


Figure 3.2: Student Achievement Management Module/Subsystem

3.2.4.1 UC004: Generate E-Certificate Student
Table 3.2.4.1: Use Case Specification for Generate E-Certificate Student
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC-004


## 68

Use Case Name: Generate E-Certificate Student
## Created By: Muhammad Aiman Haiqal
bin Salehuddin
## Last Updated By:  Muhammad Aiman Haiqal
bin Salehuddin
## Date Created: 1 June 2024 Last Revision Date:  11 June 2024
## Actors: State Admin
Description: This  use  case  allows  an authorized user,  such  as  School  Admin  or  TVPSS
Management Crew member, to generate and electronic certificate for a student. The
e-certificate  is  a  digital  document  that  confirms  the  student’s  achievement  or
completion of a program or course
Pre-conditions: 1. Both school admin and TVPSS management crew must be logged into the
TVPSS Management Information System with .moe domain email.
- The student’s achievement or completion data must be available and verified
in the system.
- The template  for  the  e-certificate  must  be  predefined  and  stored  in  the
system.
## Normal Flow:
- The  state  admin  selects  the  “Generate  E-Certificate”  option  from  the
dashboard.
- The  system  displays  a  form  to  enter  the  necessary  student  information.
(Student ID, Name, Year)
- The  state  admin  enters  the  required  student  information  and  submits  the
form.
- The system validates the entered information.
- The system retrieves the student’s achievement or completion data.
- The system generates the e-certificate using the predefined template and the
retrieved data.
- The system saves the e-certificate in the database.
- The system provides a confirmation message to the state admin and an
option to download or email the e-certificate.


## 69

## Alternative
## Flow:
AF1. Invalid student information

1.1 If the system detects invalid or incomplete student information during
validation.
1.2 The system displays an error message indicating the issue.
1.3 The actor corrects the information and resubmits the form.

AF2. Cancel operation

2.1. The actor decides to cancel the generation process at any step before
submission.
2.2. The actor clicks the “Cancel” button.
2.3. The system discards any entered data and returns the actor to the
dashboard.
Exception: EF1. System failure to retrieve data
1.1 If the system fails to retrieve the student’s achievement data due to a
database error, the system logs the error and displays an error message to the actor.
1.2 The actor can retry the operation or contact technical support

EF2. System failure to generate e-certificate
2.1. If the system encounters an error while generating the e-certificate, the
system logs the error and displays an error message to the actor.
2.2. The actor can retry the operation or contact technical support.
Post-conditions: 1. The e-certificate is generated and stored in the system database.
- The actor receives a confirmation message indicating successful generation
of the e-certificate.
- The e-certificate is available for download or email as specified by the
actor.
## Related
## Requirement:
ID Requirement Priority
FR UC-004-01 The system shall allow the State Admin to
generate an e-certificate for students based on
predefined templates.
## Basic


## 70

FR UC-004-02 The system shall validate student information
before generating the e-certificate.
## Basic
FR UC-004-03 The system shall retrieve the student's
achievement or completion data for e-certificate
generation.
## Basic
FR UC-004-04 The system shall store the generated e-certificate
in the database.
## Basic
FR UC-004-05 The system shall provide a confirmation message
and options to download or email the e-certificate
to the State Admin.
## Basic
FR UC-004-06 The system shall allow customization of the e-
certificate template to include different designs
and logos.
## Excitement
QR UC-004-01 The system shall display an error message when
no student achievement data is found in the
system database.
## Performance
QR UC-004-02 The system shall display an error message if the
e-certificate generation process fails due to
system errors.
## Performance
CR UC-004-01 The system shall prompt the State Admin for
confirmation before canceling the e-certificate
generation process.
## Performance
CR UC-004-02 The system shall allow retrying the e-certificate
generation process in case of failures.
## Performance



## 71


Figure 3.2.4.1: Activity Diagram of UC004 Generate E-Certificate Student


## 72




3.2.4.2 UC010: Submit Student Achievement
Table 3.2.4.2: Use Case Specification for Submit Student Achievement
## History Log: 1.0
## 1.1
## 1.2
## 2.0
Create initial use case
Fixed pre-conditions
Fixed normal flow
Added related requirements
## Version: 2.0
Use Case ID: UC010
## Use Case Name: Submit Student Achievement
## Created By: Muhammad Aiman Haiqal
bin Salehuddin
## Last Updated By:  Muhammad Aiman Haiqal
bin Salehuddin
## Date Created: 1 June 2024 Last Revision Date:  11 June 2024
## Actors: School Admin
Description: This use case describes how the Plantation OC and Marketing OC manage DO.
Pre-conditions: 1. School Admin must be logged in the system.
Normal Flow: NF1: Submit Student Achievement
- The  School  Admin  navigates  to  the  "Student  Achievements"  section  of  the
TVPSSS system.
- The School Admin selects the "Submit New Achievement" option.
- The system presents a form to the School Admin.
- The School Admin fills in the following details:
## 4.1 Student's Name
## 4.2 Achievement Type
## 4.3 Achievement Date
## 4.4 Achievement Description
## 4.5 Supporting Evidence
- The School Admin clicks the "Submit" button.
- Upon successful validation, the system records the achievement in the database,
associating it with the selected student's and school’s profile.
- The  system  displays  a  confirmation  message  to  the  School  Admin,  indicating
successful submission.



## 73

## Alternative
## Flow:
AF1: Saved Draft
- As  the  School  Admin  fills  out  the  form,  the  system  automatically  saves  the
entered data at regular intervals.
- If the School Admin accidentally closes the browser or loses connectivity, their
progress is not lost. They can return to the form later and resume from where they
left off.

AF2: Cancel Submission
- The School Admin can click a "Cancel" button at any time before submitting.
- The system discards any entered information and returns to the previous screen.

Exception: EF1: Incomplete Information
- If  any  mandatory  fields  are  left  blank,  the  system  displays  specific  error
messages indicating which information is missing.
EF2: Invalid Data
- If  entered  data  doesn't  match  expected formats,  the  system  provides  clear
feedback to the School Admin.
EF3: Duplicate Submission
- If the system detects that the achievement being submitted is a duplicate of
an existing record, an error message is displayed.
- The  School  Admin  can  review  the  existing  record  and  decide  whether  to
proceed with the submission or cancel.
Post-conditions: 1. The submitted student achievement is recorded in the system.
- The  achievement  may  become  visible  on  the  student's  profile,  and  school
profile.
## Related
## Requirement:
ID Requirement Priority
FR UC-010-01 The system shall allow the School Admin to
submit student achievements with detailed
information.
## Basic
FR UC-010-02 The system shall validate the entered student
achievement information before recording it in
the database.
## Basic
FR UC-010-03 The system shall automatically save the progress
of form filling at regular intervals.
## Basic


## 74

FR UC-010-04 The system shall display a confirmation message
upon successful submission of student
achievement.
## Basic
QR UC-010-01 The system shall display error messages for any
missing mandatory fields or invalid data formats.
## Performance
CR UC-010-01 The system shall prompt the School Admin for
confirmation before canceling the submission
process.
## Performance
CR UC-010-02 The system shall allow the School Admin to
resume filling out the form from the last saved
point in case of disruption.
## Performance
CR UC-010-03 The system shall detect and alert the School
Admin in case of duplicate submissions.
## Performance



## 75


Figure 3.2.4.2: Activity Diagram of UC010 Submit Student Achievement




## 76

## 3.3 Performance Requirements
- Dashboard and Administration Module:
The system shall provide responsive and timely data loading on the dashboard within 3
seconds to  ensure  a  smooth  user  experience. The  system  should  seamlessly  navigate
users from the login page to the dashboard without interruptions.

## • School Information Module:
This module requires quick data retrieval and processing to provide timely information
to users. Besides, the system should perform validation checks on the submitted school
crew application data within 3 seconds for a responsive user experience. Additionally,
it  must  handle  concurrent access  by  multiple  users  without  performance  degradation,
ensuring that updates to school information are promptly reflected across the system.

## • School Version Module:
The  system should  fetch and  display the school version  status  information from  the
database within 5 seconds to maintain a smooth user experience. Moreover, it should
efficiently manage  notifications  and  updates,  ensuring  that  any  changes  are  promptly
notified to relevant users. The module should also support the verification and approval
process for updates without causing delays or system slowdowns.uc

## • Student Achievement Module:
The   system   should   allow   for   real-time   submission   and   validation   of   student
achievements, preventing duplicate entries and ensuring data integrity. In case of system
errors  during  e-certificate  generation,  the  system  should  display  the  error  message
within 2 seconds to provide timely feedback to the user.

## 3.4 Design Constraints
## • Style Guidelines
The user interface design should follow the guidelines and standards set by the Ministry
of  Education  (MOE)  to  ensure  consistency  across  all the webpage in  the  TVPSS
Management system, including the logo and colour theme of blue and black, as well as
other aspects like fonts.



## 77

## • Compatibility
The system should be compatible with various web browsers and operating systems to
ensure accessibility for users across different platforms. For instance, it should integrate
seamlessly with  existing  school management  systems  and  databases  to  prevent  data
duplication,  minimize  additional  costs and  ensure  smooth  information  exchange.
Whereas, the system must operate on specific platforms, such as Windows, macOS, or
Linux,  which  can  limit  design options.  Additionally,  it  may  need  to  support  mobile
platforms like iOS and Android.

- Security and Privacy
The  system should implement  robust  security  measures,  including  data  encryption,
secure  communication  protocols  (HTTPS),  and  user  authentication  mechanisms  to
prevent  unauthorized  access. The  system  should also comply  with  the  Personal  Data
Protection  Act  (PDPA)  and  other  relevant  data  privacy  regulations  to  ensure  proper
handling and protection of user data.

## • User Accessibility
The system should comply with accessibility guidelines and standards, such as the Web
Content  Accessibility  Guidelines  (WCAG),  to  ensure  usability  for  users  like  students
with  disabilities. The  system  should also support  multiple  languages  and  localization
options to meet the diverse linguistic needs of users across different regions.

## • Scalability
The system will be designed to be scalable to accommodate future growth in the number
of users, schools, and data quantities without affecting the system performance.

## 3.5 Software System Attributes
The TVPSS Management System should feature an intuitive, user-friendly interface that
is easy to navigate, especially for users with less technical knowledge. The interface should be
visually appealing and consistent across all modules, incorporating UX/UI design principles to
ensure functionality and engagement. This includes using clear icons, uniform color schemes,
and logical layouts, as well as usability testing to improve the interface. Furthermore, the system
must  have  a  responsive  design  to  ensure  optimal usability and  functionality across various


## 78

devices,  including desktops,  laptops,  tablets,  and  mobile  devices.  The  interface  should  adapt
seamlessly to different screen sizes and resolutions too to provide a consistent user experience
across all devices.

To keep users informed and engaged, the system should provide real-time notifications
and alerts for important events, updates, or required actions. These can be delivered via email
or in-app notifications based on user preferences, ensuring users stay informed and can respond
quickly to  any  changes  or  issues  within  the  system.  This  feature  enhances  the  overall
responsiveness  and  user  experience  of  the  system. In  addition, The  TVPSS  Management
System needs to have strong data management capabilities for efficient data storage, retrieval,
and data backup. This  includes  implementing  strong  data  validation  and  integrity  checks  to
ensure  that  all  information  stored  in  the  database  is  accurate  and  consistent.  Efficient  data
management  is vital for  maintaining the system reliability  and  performance,  especially with
large amounts of data. Besides, regular backups and secure storage solutions are necessary to
prevent data loss and allow for quick recovery in case of any issues.

## 3.6 Other Requirements
## • Maintainability
The TVPSS Management System  should prioritise maintainability by ensuring  that
ongoing  maintenance,  bug  fixes,  and  updates  can  be  performed  efficiently and with
minimal downtime.

## • Portability
The TVPSS management System should be able to run on different hardware platforms
and operating systems. For instance, Windows, macOS, or Linux for laptops, whereas
iOS and Android for smartphones.

## • Reliability
The  TVPSS  Management  System  should  be  highly  reliable,  with  minimal  downtime
and disruptions,  to  ensure  continuous  availability  for  users. This  can  be  achieved
through  the  implementation  of  redundancy  measures,  such  as  load  balancing  and
failover mechanisms, to ensure uninterrupted service and data availability.



## 79

## • Reusability
System components should be designed for reuse on other components in the system to
reduce development time,  cost  and  human  resources. For  instance, reusable existing
code components and data library that can be accessed and utilized by developers across
different modules.

## • Usability
The system should focus on making it easy for users to navigate and understand, with
clear instructions and resources like tutorials and guidelines. It should also include tools
like FAQs and chatbots to help users with common problems.

## • Scalability
The  system  should  be  scalable  to  accommodate  growth  in  the  number  of  users  and
amount of data without affecting the performance.

## Appendices

- Appendix A: Originality/Similarity Report
