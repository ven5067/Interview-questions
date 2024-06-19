
## Fullstack Coding Questions

### 1. Create a To-Do List Application

**Task:**

Build a simple To-Do list application with the following features:
- Display a list of tasks.
- Add a new task.
- Mark a task as complete.
- Delete a task.

**Approach:**

**Front-end (Angular/React/Vue):**
- Create components for displaying tasks, adding tasks, and task item.
- Implement services to communicate with the backend API.
- Use forms for adding tasks and buttons for marking tasks as complete and deleting tasks.

**Back-end (Node.js/Java Spring Boot/.NET Core):**
- Design RESTful APIs for CRUD operations (GET, POST, PUT, DELETE) on tasks.
- Implement controllers to handle these APIs.
- Use a database (e.g., MySQL, MongoDB) to store tasks.
- Ensure proper error handling and validation in API endpoints.

**Integration:**
- Connect front-end components to back-end APIs using HTTP requests (fetch API, Axios, etc.).
- Implement error handling and data validation on both client-side and server-side.

### 2. Build a Weather Forecast Application

**Task:**

Develop a weather forecast application that displays weather information for a given location.
Users should be able to enter a city or ZIP code and view current weather conditions along with a 5-day forecast.

**Approach:**

**Front-end (React/Vue/Angular):**
- Design a form to accept user input for city or ZIP code.
- Display current weather conditions (temperature, description, icon) and 5-day forecast using weather APIs (e.g., OpenWeatherMap, Weatherstack).
- Use responsive design for a good user experience on both desktop and mobile devices.

**Back-end (Node.js/Java/.NET Core):**
- Implement a proxy server or server-side API to fetch weather data from the external weather API.
- Handle requests from the front-end, fetch data from the weather API, and send it back to the client.
- Cache weather data to improve performance and reduce API calls.

**Integration:**
- Integrate with a third-party weather API to fetch weather data based on user input.
- Validate user input and handle errors gracefully (e.g., invalid city/ZIP code).

### 3. Implement Authentication and Authorization in a Web Application

**Task:**

Create a web application with user authentication and authorization.
Implement user registration, login, and access control to secure certain parts of the application.

**Approach:**

**Front-end (React/Angular/Vue):**
- Design forms for user registration and login.
- Implement authentication flows using tokens (JWT) stored in local storage or cookies.
- Manage user sessions and display authenticated content based on user roles and permissions.

**Back-end (Node.js/Java Spring Boot/.NET Core):**
- Develop APIs for user registration, login, and token management (generate, validate tokens).
- Store user credentials securely (hashed passwords).
- Implement middleware or filters to check authentication and authorization for protected routes.

**Integration:**
- Secure API endpoints with authentication middleware or decorators to validate JWT tokens.
- Handle expired tokens, token refresh, and logout functionality.
- Implement role-based access control (RBAC) to restrict access to certain routes or resources.

