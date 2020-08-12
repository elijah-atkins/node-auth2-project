# Authentication using JSON Web Tokens (JWTs)

## Topics

- Authentication.
- Express Middleware.
- JSON Web Tokens (JWTs).
- Hashing Passwords.

## Description

In this project we'll implement a full authentication workflow (register/login/logout/restrict endpoint) using `Node.js`, `Express`, `SQLite` and `JSON Web Tokens` on the server.

### Download Project Files

- **Fork** and **Clone** this repository.
- **CD into the folder** where you cloned the repository.
- Do your magic!

## Assignment

Use Node.js, Express and Knex to build an API that provides _Authentication_ functionality using SQLite to store _User_ information.

use `npm init` to generate `package.json` file. Add dependiencies and run `npm i` to get project initialized

use `knex init` to generate `knexfile.js` and set 

use `knex migrate:make users` to make migration file()

set up schema in generated js file run `knex migrate:latest` to generate db file (`knex migrate:rollback` to undo)

The user schema should include: `username`, `password` and `department`. The `department` should be a string used to group the users. No need for a `departments` table or setting up relationships.
//set up departments table with relationships

generate seeds with `knex seed:make <seed_name>`
run seeds with `knex seed:run`

Use **JSON Web Tokens** to keep users authenticated across requests.

### Design and build the following endpoints.

| Method | Endpoint      | Description                                                                                                                                                                                                                                                            |
| ------ | ------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| POST   | /api/register | Creates a `user` using the information sent inside the `body` of the request. **Hash the password** before saving the user to the database.                                                                                                                            |
| POST   | /api/login    | Use the credentials sent inside the `body` to authenticate the user. On successful login, create a new JWT with the user id as the subject and send it back to the client. If login fails, respond with the correct status code and the message: 'You shall not pass!' |
| GET    | /api/users    | If the user is logged in, respond with an array of all the users contained in the database from the same department as the user. If the user is not logged in respond with the correct status code and the message: 'You shall not pass!'.                                                                  |
| GET    | /api/users/all    | If the user is logged in and is from department 1 Admin, respond with an array of all the users contained in the database. If the user is not logged in respond with the correct status code and the message: 'You shall not pass!'.            

## Stretch Problem

- [x] add the code necessary so that when a client makes a `GET` request to `/api/users` the server only returns documents with the `same department` as the logged in user. For example if the logged in user belongs to the finance department, then only users with the _finance_ department should be returned; if the logged in user is in _sales_ only users on the sales department should be returned.
- [x] implement a React client:
  - [x] use `create-react-app` to generate a application to server as the client for the Web API.
  - [x] inside the React application add **client-side routes** and components for `signup`, `signin` and showing the `list of users` stored in the database.
  - [x] the `/signup` route should provide a form to gather `username`, `password` and `department` for the user and make a `POST` request to the `/api/register` route on the API. If the user is created successfully, take the returned token, save it to the browser's local storage and redirect the user to the `/users` route, where they should see the list of users.
  - [x] the `/signin` route should provide a form to gather `username` and `password` for the user and make a `POST` request to the `/api/login` route on the API. Upon successful login, persist the returned token to the browser's local storage and redirect the user to the `/users` route.
  - [x] the `/users` route should read the token from local storage and make a `GET` request to the `/api/users` route on the API attaching the token as the value of the `Authorization` header.
  - [x] provide a button to `sign out` that will remove the token from local storage.
- [x] add any extra functionality to make the application more user friendly like showing a message and redirecting to `/signin` if an unauthenticated user tries to access the list of users in the `/users` route.
