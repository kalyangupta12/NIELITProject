# Added a high level backend

Tech stack: 'mongodb' for the db, 'zod' for the schemas, 'express' for the backend server, and 'node' for the runtime, 'jwts' for authentication. Also if possible use typescript for better types and ultimately more secure data entry as well as scalability

What I have done here is that I have added a high level backend for the first parent tree of the ER diagram for the starting point

### Description

- I have introduced the signgin and dashboard endpoints for both users and admins.
- For this one, in every authenticated requests, you need to send the jwt in headers (Authorization : "Bearer <actual token>").
- You need to use mongodb to store all the data persistently.
- You'll need mongodb compass and postman to test out the stuff, I guess you know that already
- Also please figure out that 'config' file which is an environment variable that stores the token separately in the server, so as to provide more security. It shouldn't be exposed anywhere when deployed. My one didn't work but the rest of the stuff works properly.
- If you have any problems I have a working small backend where the data, schema, jwt, authentication, middleware, every logic has been written in one single file here [link](https://github.com/LegioN2004/Programs/blob/main/WebDev-stuff/Kirat-cohort-0-1/3.1-Middlewares-Global_Catches-Database-%26-Auth/mongooseIntro.js). It has everything implemented but not in the way of course selling thing in mind

## Routes

### Admin Routes

- POST /admin/signup
  Description: Creates a new admin account.
  Input Body: { username: 'admin', password: 'pass' }
  Output: { message: 'Admin created successfully' }
- POST /admin/signin
  Description: Logs in an admin account.
  Input Body: { username: 'admin', password: 'pass' }
  Output: { token: 'your-token' }
- POST /admin/courses
  Description: Creates a new course.
  Input: Headers: { 'Authorization': 'Bearer <your-token>' }, Body: { title: 'course title', description: 'course description', price: 100, imageLink: '<https://linktoimage.com>' }
  Output: { message: 'Course created successfully', courseId: "new course id" }
- GET /admin/courses
  Description: Returns all the courses.
  Input: Headers: { 'Authorization': 'Bearer <your-token>' }
  Output: { courses: [ { id: 1, title: 'course title', description: 'course description', price: 100, imageLink: 'https://linktoimage.com', published: true }, ... ] }

### User routes

- POST /user/signup
  Description: Creates a new user account.
  Input: { username: 'user', password: 'pass' }
  Output: { message: 'User created successfully' }
- POST /user/signin
  Description: Logs in a user account.
  Input: { username: 'user', password: 'pass' }
  Output: { token: 'your-token' }
- GET /user/courses
  Description: Lists all the courses.
  Input: Headers: { 'Authorization': 'Bearer <your-token>' }
  Output: { courses: [ { id: 1, title: 'course title', description: 'course description', price: 100, imageLink: 'https://linktoimage.com', published: true }, ... ] }
- POST /user/courses/:courseId
  Description: Purchases a course. courseId in the URL path should be replaced with the ID of the course to be purchased.
  Input: Headers: { 'Authorization': 'Bearer <your-token>' }
  Output: { message: 'Course purchased successfully' }
- GET /user/purchasedCourses
  Description: Lists all the courses purchased by the user.
  Input: Headers: { 'Authorization': 'Bearer <your-token>' }
  Output: { purchasedCourses: [ { id: 1, title: 'course title', description: 'course description', price: 100, imageLink: 'https://linktoimage.com', published: true }, ... ] }
