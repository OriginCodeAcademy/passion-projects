# Build your own LMS

The goal of this project is to build your own custom learning management system that helps schools manage Students and Teachers, as well as Courses which both parties are scheduled to attend/teach.

## 1. Build the Backend

### 1a. Setup the Project

First, create a folder to store the back-end for this project:

```bash
$ mkdir -p ~/oca/passion-projects/vehicle-manager/backend
```

Next, navigate to that folder and initialize a new `npm` project

```bash
$ cd ~/oca/passion-projects/vehicle-manager/backend
$ git init
$ npm init
```

This will prompt you to answer some questions, such as the name of your project; a brief description; author names etc. If you don't know what to enter for a particular field, it is common practice to hit return to give a default answer.

At this point, run through the [Idiomatic Express Drill](https://gist.github.com/cameronwilby/76489153e00aaf3423abfaa2dc2d1884#method-3---idiomatic-folder-structure) to get to a good starting point for the backend.

### 1b. Setup your Model Layer

Once you have created your base Express app, you can focus on creating your models.

Choose either [Sequelize](http://docs.sequelizejs.com/) or [Mongoose](http://mongoosejs.com/) to create these tables in [MySQL](https://www.mysql.com/) or [MongoDB](https://www.mongodb.com/) respectively.

#### `Student` Entity

| Name        | Type   | Note                  |
| ------------| ------ | ----------------------|
| studentId   | int    | Primary Key / ObjectId|
| firstName   | string | Student first name    |
| lastName    | string | Student last name     |
| emailAddress| string | Student email address |
| telephone   | ?      | Student telephone     |

(Optionally, add any extra fields you think would be useful to store about a student)

#### `Teacher` Entity

| Name         | Type   | Note                  |
| ------------ | ------ | ----------------------|
| teacherId    | int    | Primary Key / ObjectId|
| firstName    | string | Teacher first name    |
| lastName     | string | Teacher last name     |
| emailAddress | string | Teacher email address |
| telephone    | ?      | Teacher telephone     |

(Optionally, add any extra fields you think would be useful to store about a teacher)

#### `Course` Entity

| Name       | Type    | Note                                              |
| -----------| --------| --------------------------------------------------|
| courseId   | int     | Primary Key / ObjectId                            |
| teacherId  | int     | Foreign Key linking a teacher to this course      |
| shortCode  | string  | Short code for the course (e.g. REACT200)         |
| description| string  | Long name for the course (e.g. Intermediate React)|
| startDate  | datetime| Start date for the course                         |
| endDate    | datetime| End date for the course                           |

(Optionally, add any extra fields you think would be useful to store about a course)

### 1c. Setup Express Routes

Once you have built your models, build out the following express routes:

#### `/api/students`

| Verb     | Route              | Description         |
| -------- | -------------------| --------------------|
| `GET`    | `/api/students/`   | Get all students    |
| `GET`    | `/api/students/:id`| Get a single student|
| `POST`   | `/api/students/`   | Create a student    |
| `PUT`    | `/api/students/:id`| Update a student    |
| `DELETE` | `/api/students/:id`| Delete a student    |

#### `/api/teachers`

| Verb     |Route              | Description        |
| -------- |-------------------| ------------------ |
| `GET`    |`/api/teachers/`   | Get all teachers   |
| `GET`    |`/api/teachers/:id`| Get single teacher |
| `POST`   |`/api/teachers/`   | Create a teacher   |
| `PUT`    |`/api/teachers/:id`| Update a teacher   |
| `DELETE` |`/api/teachers/:id`| Delete a teacher   |

#### `/api/courses`

| Verb     |Route             | Description      |
| -------- |------------------| -----------------|
| `GET`    |`/api/courses/`   | Get all courses  |
| `GET`    |`/api/courses/:id`| Get single course|
| `POST`   |`/api/courses/`   | Create a course  |
| `PUT`    |`/api/courses/:id`| Update a course  |
| `DELETE` |`/api/courses/:id`| Delete a course  |

> Use [Postman](https://www.getpostman.com/) to test your routes - it allows you to issue the four main HTTP requests (`GET`, `POST`, `PUT`, and `DELETE`) as well as see additional information such as response time and status code.

### 1d. Write Tests

Setup `mocha` and `chai` in your project, then write unit tests for every route in your express application.

### 1e. Backend Exit Criteria

- Models are created and can successfully store information in a database
- Full test coverage for your express routes
- All tests are passing

---

`DO NOT CONTINUE UNTIL YOU HAVE A WORKING BACKEND SOLUTION WITH UNIT TESTS!`

---

## 2. Build the Frontend

### 2a. Setup the project

First, create a folder to store the back-end for this project, then use [Create React App](https://github.com/facebookincubator/create-react-app) to scaffold your React app.

```bash
$ mkdir -p ~/oca/passion-projects/coffee-house/frontend
```

### 2b. Design and build required screens

#### Student List Screen
---

This screen should:

* Present the user with a list of all students within the system, using the `GET` express route at `/api/students` as the data source.
* Give users the ability to click on a student to view more information.
  * (This must be a link to the `Student Detail Screen`)
* Allow users to click a delete button for a student to remove them from the system.
* Show a confirm dialog to the user before removing a student using either the `confirm()` function or [SweetAlert](https://sweetalert.js.org/)

(Choose fields you think will make sense for the user to see on this page.)

> The simplest way to display students is to use a table with columns, but you could take some time at this point to research alternatives such as the masonry grids used by Pinterest / Google Keep.

#### Student Detail Screen
---

This screen should:
 
 * Present the user with detailed information about a single student, using the `GET` express route at `/api/students/:id` as the data source.
 * Allow users to create a student it no `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
 * Allow users to update a student if an `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
 * Display a list of courses the student is enrolled in.
   * (You can potentially re-use some of the React components you used to build the `Course List Screen` here)

#### Teacher List Screen
---

This screen should:

* Present the user with a list of all teachers within the system, using the `GET` express route at `/api/teachers` as the data source.
* Give users the ability to click on a teacher to view more information.
  * (This must be a link to the `Teacher Detail Screen`)
* Allow users to click a delete button for a teacher to remove them from the system.
* Show a confirm dialog to the user before removing a teacher using either the `confirm()` function or [SweetAlert](https://sweetalert.js.org/)

(Choose fields you think will make sense for the user to see on this page.)

#### Teacher Detail Screen
---

This screen should:
 
 * Present the user with detailed information about a single teacher, using the `GET` express route at `/api/teacher/:id` as the data source.
 * Allow users to create a teacher if no `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
 * Allow users to update a teacher if an `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
 * (Optionally) Contain a tabbed interface with the following tabs:
   * "Previous Courses": Displays courses previously taught by this teacher.
   * "Current Courses": Displays courses this teacher is currently teaching.
   * "Future Courses": Displays courses this teacher is scheduled to teach.

(Choose fields you think will make sense for the user to see on this page.)

#### Course List Screen
---

This screen should:

* Present the user with a list of all courses within the system, using the `GET` express route at `/api/courses` as the data source.
* Give users the ability to click on a course to view more information.
  * (This must be a link to the `Course Detail Screen`)
* Allow users to click a delete button for a course to remove them from the system.
* Show a confirm dialog to the user before removing a course using either the `confirm()` function or [SweetAlert](https://sweetalert.js.org/).


#### Course Detail Screen
---

This screen should:

 * Present the user with detailed information about a single course, using the `GET` express route at `/api/course/:id` as the data source.
 * Allow users to create a course if no `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
 * Allow users to update a course if an `id` [parameter](https://github.com/reactjs/react-router-tutorial/tree/master/lessons/06-params) is provided to the page.
 * Prominently display information about the teacher for this course
 * Display a list of students that are enrolled in this course.

#### Optional: Dashboard Screen
--- 

> Focus your efforts on the other screens first - it will be easier to build this screen out once those are complete.

The dashboard would be the first page that a user would see upon opening the application. It could display reports/charts to the user that show information about the school.

For this screen, research some useful information that a user could potentially want to see in this business domain, and use a library such as [ChartJS](https://www.google.com/search?q=react+chartjs&oq=react+chartjs&aqs=chrome..69i57.1202j0j4&sourceid=chrome&ie=UTF-8) to display this information. (You do not have to use ChartJS)