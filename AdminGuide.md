# Admin Guide to the NEXT Learning Portal (pun intended)

Table of Contents
---

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

Structure of the syllabus:
> User 

> -> Courses (Full Stack Bootcamp, iOS Bootcamp etc.)

> ---> Topics (Ruby, SQL, Sinatra, Rails etc.)

> -----> Challenges (RubyRacer, DeafAunty, Sudoku etc.)


|    Role    | Create Course     | Create Topic/Challenges   |     Create user        | See student's progress   | 
|------------|:-----------------:|:-------------------------:|------------------------|:------------------------:|
| Superadmin |       Yes         |          Yes              |   Admin,Mentor,Student |          Yes             |
|   Admin    |       No          |          Yes              |   Mentor,Student       |          Yes             |
|   Mentor   |       No          |          Yes              |   None                 |          Yes             |
|   Student  |       No          |          Yes              |   None                 |          Yes             |


# Admin User settings
## First-time log in
---
- **Log in** with your given credentials
- You will then be prompt to do a **one-time update** for your:
 - Username
 - A new password

## Navigation Bar
---
### NEXT Academy Learning Portal Logo :)
### Courses 
- Clicking a course will redirect you to the courses dashboard

### Assessments
- See students submitted attempt

### Settings
- **Manage courses**   -> Course dashboard
- **Manage users**     -> List of students and admins
- **My profile**      -> Shows your profile and achievements
- **Add SSH key**     -> add SSH key for your device ( not needed for admins )
- **Edit my account** -> Edit your details and password


## Managing _Courses_
----
- To **Manage Courses**:
 - Settings -> Manage courses
- The Course index page will have a **list of courses** 
- Each of the Courses has 4 options:
    - **Preview** page of the Course (Eye open icon).
    - **Stats** for the progress of the Course's student (Graph icon)
    - **Edit** Course. (Pencil icon)
    - **Delete** Course. (Trash bin icon)
- To **add a new course** press the _yellow Add new course_ button on top-right.


## Managing _Topics_
--------
- To **Manage Topic**
  - Press the edit course button for the Course that the Topic belongs to
- To **Add a topic**
  - Press the _yellow Add a topic_ button at the bottom.
- To **Remove a topic**
  - Press the _red Remove topic_ button in the Topic itself.
- **Order** will determine the _order of the topic_. The Topics will be sorted according to it's order.
- Topics shall not have the same **order**. 
  - Topics with duplicate orders will prevent from the Course to be updated.
- **Title** and *description* for each Topic and the Course itself shall not be left *empty*.
  - An _error message_ 'Unable to update course' will appear if submit with empty fields  . 


## Managing _Challenges_
___
- To **Manage Challenges**:
  - Edit Course -> Manage Topics & Challenges (top-right position)
- To **Add a Challenge**:
  - Press challenge under the topic -> Add new Challenges
  - **Labels** A Challenge will have one of the three _labels_:
    - **_Lecture_**     -> Will contain lecture notes and theories
    - **_Core_**        -> Will be the challenge that students _must complete_
    - **_Optional_**    -> Tough Challenges for students who aren't afraid of losing
  - **_Order_**         -> order of the challenge. The Challenges will be sorted according to it's order.
  - **_Video URL_**     -> link for the introductory video (can be blank)
  - **_Gitlab Repo_**   -> link for the link of the repo that contains the Challenge's code
  - **_Description_**   -> description / short introduction / guidance for the Challenge
- To **Edit a challenge** :
  - Go to the Topic that the Challenge belongs to -> Click on the Challenge name
- To **Delete a challenge** :
  - Go to edit Challenge -> Click on the _Red trash bin icon_


  
## Managing _Users_
- To **Manage Users**:
  - Settings -> Manage Users
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
- It's a dashboard for students to access NEXT Academy's syllabus :)
- To access **Dashboard**:
  - Nav Bar -> Courses -> choose your Course 
- **Current Progress** will show the latest challenge you has attemtped
- **Start Challenge** button / **Continue Challenge** button:
  - You can start the available Challenge (and create an **Attempt**) with this button.
  - You can continue where they left off. 
- **Timeline** 
  - Each _Green Dot_ represents a **Topic** 
  - Pressing it with open a list of **Challenges**
  - You will not be able to access to the next Topic if you have not complete the Challenges for previous Topic

## Attempts for individual challenge
- Upon pressing _start challenge_, an attempt will be created for that Student on that Challenge
- In GitLab, the Challenge's repository in git.nextacademy.com will be forked to the Student's repository

## Pair programming
- In the early phase of the bootcamp, students are encouraged to practice **Pair Programming**
- To log in a second user
  - Go to Settings -> Log In Second User

## GitLab Repository
- Access permission for GitLab repository should be `internal`

## Code Review
- Students will be redirected to **Code Review** section after they clicked _Complete Challenge_
- Must comment? or Review and click to return to Dashboard?


## Issue discovered
- After pressing update challenge, redirects back to edit challenge page (should return back to topics index)
- Create new user page header is still create new student (instead of create new user)
- Shall we give the student a ~~freakin~~ cool name?

