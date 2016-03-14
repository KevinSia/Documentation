# Admin Guide to the NEXT Learning Portal (pun intended)

Table of Contents
---
* [Learning Portal Information](#learning-portal-infomation)
* [Admin Usage](#admin-user-settings)
  * [Navigation Bar](#navigation-bar) 
    * [Courses](#courses) 
    * [Assessments](#assessments)
    * [Settings](#settings)
  * [Managing Courses](#managing-courses)
  * [Managing Topics](#managing-topics)
  * [Managing Challenges](#managing-challenges)
  * [Managing Users](#managing-users)
  * [The Dashboard](#dashboard)
  * [Challenge Attempts](#attempts-for-individual-challenge)
* [Pair Programming](#pair-programming)
* [Gitlab Repository](#gitlab-repository)
* [Code Review](#code-review)
* [Issues](#issue-discovered)

## Learning Portal Infomation
Structure of the syllabus:
> User 

> -> Courses (Full Stack Bootcamp, iOS Bootcamp etc.)

> ---> Topics (Ruby, SQL, Sinatra, Rails etc.)

> -----> Challenges (RubyRacer, DeafAunty, Sudoku etc.)


|    Role    | Create Course     | Create Topic/Challenges   |     Create user        | See all student's progress   | 
|------------|:-----------------:|:-------------------------:|------------------------|:----------------------------:|
| Superadmin |       Yes         |          Yes              |   Admin, Mentor, Student |          Yes                 |
|   Admin    |       No          |          Yes              |   Mentor, Student       |          Yes                 |
|   Mentor   |       No          |          No               |   None                 |          Yes                 |
|   Student  |       No          |          No               |   None                 |          No                  |


## Admin User settings
## First-time log in
---
- **Log in** with your given credentials
- You will then be prompt to do a **one-time update** for your:
 - Username
 - A new password

## Navigation Bar
---
- Courses 
 - Clicking a course will redirect you to the courses dashboard
- Assessments
 - See students submitted attempt
- Settings
 - **Manage courses**   -> Course dashboard
 - **Manage users**     -> List of students, mentors and admins
 - **My profile**       -> Shows your profile and achievements
 - **Add SSH key**      -> add SSH key for your machine ( password-less authentication for GitLab )
 - **Edit my account**  -> Edit your details and password


## Managing _Courses_
----
- To **Manage Courses**/**Edit a Course**:
 - Settings -> Manage courses
- The Course index page will have a **list of courses** 
- Each of the Courses has 4 options:
    - **Preview** page of the Course (Eye open icon).
    - **Stats** for the progress of the Course's student (Graph icon)
     - Student's current attempting Challenge
     - Student's progess on the Topic
    - **Edit** Course. (Pencil icon)
    - **Delete** Course. (Trash bin icon)
- To **add a new course** press the _yellow Add new course_ button on top-right.


## Managing _Topics_
--------
- To **Manage Topic**
  - Enter the [Edit Course page](#managing-courses) that the Topic belongs to
- To **Add a topic**
  - Press the _yellow Add a topic_ button at the bottom.
- To **Remove a topic**
  - Press the _red Remove topic_ button in the Topic itself.
- **Order** will determine the _order of the topic_. The Topics will be sorted according to it's order.
- Topics shall not have the same **order**. 
  - Topics with duplicate orders will prevent from the Course to be updated.
- **Title** and *description* for each Topic and the Course itself shall not be left *empty*.
  - An _error message_ 'Unable to update course' will appear if form submitted with empty fields. 


## Managing _Challenges_
---
- To **Manage Challenges**:
  - 1. Edit Course page -> Manage Topics & Challenges (located at top-right)
  - 2. Accessing from [Dashboard](#dashboard) and go into the Challenge you want to manage
- To **Add a Challenge**:
  - Press challenge under the topic -> Add new Challenges
  - **_Labels_** A Challenge will have one of the three _labels_:
    - **_Lecture_**     -> Will contain lecture notes and theories
    - **_Core_**        -> Will be the Challenge that students _must complete_
    - **_Optional_**    -> Tough Challenges for students who aren't afraid of losing
  - **_Order_**         -> Order of the Challenge. The Challenges will be sorted according to it's Order.
  - **_Video URL_**     -> link for the introductory video (can be blank)
  - **_Gitlab Repo_**   -> link for the link of the repo that contains the Challenge's code
  - **_Description_**   -> Description / short introduction / guidance / insights for that Challenge
- To **Edit a challenge** :
  - Go to the Topic that the Challenge belongs to -> Click on the Challenge name
- To **Delete a challenge** :
  - Go to Edit Challenge page -> Click on the _Red trash bin icon_


  
## Managing _Users_
---
- To **Manage Users**:
  - [Settings](#navigation-bar) -> Manage Users
  - A list of Users will appear with the following options:
    - **Profile**          -> shows the User's profile and achievements
    - **Edit**             -> edits the User's profile and **reset User's password**
    - **Authorize GitLab** -> authorize User in GitLab to be able to fork repo
    - **Delete**           -> deletes a User
- To **Add a user**
  - Press **+ Add New User** located on top-right
  - **Course**       -> Assigning the User to the course
  - **Role**         -> Sets the role for the User (admin, mentor, student)
  - **First name**   -> User's first name
  - **Last name**    -> User's last name (will be combined with first name and become username before User edits)
  - **Email**        -> User's email address

## Dashboard
---
- It's a dashboard for students to access NEXT Academy's syllabus :)
- To access **Dashboard**:
  - Nav Bar -> Courses -> choose your Course 
- **Current Progress** will show the latest challenge you are attempting.
- **Start Challenge** button / **Continue Challenge** button:
  - You can start the available Challenge (and create an **Attempt**) with this button.
  - You can continue where they left off. 
- **Timeline** 
  - Each **Green Dot** represents a **Topic** 
  - Pressing it with open a list of **Challenges**
  - You will not be able to access to the next Topic if you have not complete the Challenges for previous Topic

## Attempts for individual challenge
---
- Upon pressing **Start challenge** (in dashboard), an attempt will be created for that Student on that Challenge
- In GitLab, the Challenge's repository in git.nextacademy.com will be forked to the Student's repository

## Pair programming
---
- In the early phase of the bootcamp, students are encouraged to practice _Pair Programming_
  - There will be a second user log into the account of the other pair
- To _log in_ a second user
  - Go to Settings -> **Log In Second User**

## GitLab Repository
---
- When creating a Challenge repository, access permission for GitLab repository should be `internal`

## Code Review
---
- Students will be redirected to _Code Review_ section after they clicked _Complete Challenge_
- Must comment? or Review and click to return to Dashboard? (to be confirmed)


## Issue discovered
- After pressing update challenge, redirects back to edit challenge page (intended?)
- Create new user page header is still create new **student** (should be create new **user**)
- Lets replace _student_ with a ~~freaking~~ cool name?
- Unique username error not clear in update page (change flash message)
- Duplicated challenge order error more user-friendly? (show what order has been taken)

