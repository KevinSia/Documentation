# Guide to the NEXT Learning Portal (pun intended)

Index
---

Structure of the learning portal

User 

-> Courses (Full Stack Bootcamp, iOS Bootcamp etc.)

---> Topics (Ruby, SQL, Sinatra, Rails etc.)

-----> Challenges (RubyRacer, DeafAunty, Sudoku etc.)

Permissions (table form):
Superadmin : Can create any type of user, courses, topics, challenges, see students progress
Admin      : Can create mentor and student user, courses, topics, challenges, see students progress
Mentor     : Can see students progress
Student    : Can suffer

# Admin User settings
## First-time sign in
- **Log in** with your credentials
- You will then be prompt to do a **one-time update** for your:
  - Username
  - Make a new password
- You will then be then be redirected to Managing Courses page 
- 
-------------

## Navigation Bar
### Courses 
- Clicking a course will redirect you to the courses dashboard

### Assessments
- See students submitted attempt

### Settings
- Manage course   -> Course index page
- Manage user     -> List of students and admins
- My profile      -> Shows your profile
- Add SSH key     ->  #
- Edit my account -> Edit your details and password


### Managing _Course_
- To **Manage Courses**
- The Course index page will have a **list of courses** 
- Each of the Courses has 4 options:
    - **Preview** page of the Course (Eye open icon).
    - **Stats** for the progress of the Course's student
    - **Edit** Course.
    - **Delete** Course.
- To **add a new course** press the _yellow button_ on top-right.
--------

### Managing _Topics_
- To **Manage Topic**
  - Press the edit course button for the Course that the Topic belongs to
- To **Add a topic**
  - Press the _yellow_ button at the bottom.
- To **Remove a topic**
  - Press the _red_ button in the Topic itself.
- **Order** will determine the _order of the topic_. The Topics will be sorted according to it's order.
- Topics shall not have the same **order**. 
  - Topics with duplicate orders will prevent from the Course to be updated.
- **Title** and *description* for each Topic and the Course itself shall not be left *empty*.
  - An _error message_ 'Unable to update course' will appear if submit with empty fields  . 
--------

### Managing _Challenges_
- To **Manage Challenges**:
  - Edit Course -> Manage Topics & Challenges (top-right position)
- To **Add a Challenge**:
  - Press challenge under the topic -> Add new Challenges
  - **Labels** A Challenge will have one of the three _labels_:
    - **_Lecture_**  -> Will contain lecture notes and theories
    - **_Core_**     -> Will be the challenge that students _must complete_
    - **_Optional_** -> Tough challenges for students who are willing to take on
  - **_Order_** is the order of the challenge. The Challenges will be sorted according to it's order.
  - **_Video URL_** is the link for the introductory video (can be blank)
  - **_Gitlab Repo_** is the link for the link of the repo that contains the Challenge's code
  - **_Description_** is the description / short introduction / guidance for the Challenge
- To **Edit a challenge** :
  - Go to the Topic that the Challenge belongs to -> Click on the Challenge name
- To **Delete a challenge** :
  - Go to edit Challenge -> Click on the red trash bin icon
- To **Update instructions** :
  - ????

  
### Managing _Users (Mentor, Admin, Student)_
- To **Manage Users*:
  - Settings -> Manage Users
- To **Add a user*
  - Press the yellow button on top-right
  - 
### Pair programming
### Dashboard


### UX problem/issue discovered
- After pressing update challenge, redirects back to edit challenge page (should return back to topics index)
- Create new user page h1 is still create new studentd
- After create new user error, password reset field is shown

