#### **Gruve Backend API Development Test with Authentication and Task Management**

### **Description**:
The goal of this task is to assess your ability to design, implement, and secure a backend API with proper authentication mechanisms. You will be required to develop a RESTful API that handles the management of **events** and **tasks** associated with each event. The API must support CRUD operations (Create, Read, Update, Delete) for both events and tasks, along with the ability to assign tasks to specific members with due dates.

Additionally, the API must be secured with **JWT authentication** to ensure only authorized users can access and manipulate the data.

The system should also include unit tests to ensure API functionality, and test coverage should exceed **90%**.




### **Specific Requirements**:
1. **Event CRUD**:
   - Ability to create, retrieve, update, and delete events.
   - Events should include attributes like name, location, start time, and end time.

2. **Task CRUD under Events**:
   - Ability to create, retrieve, update, and delete tasks for a specific event.
   - Each task should have attributes like title, description, due time, and a list of assigned members.

3. **Authentication**:
   - Use **JWT tokens** to authenticate users for all API endpoints.
   - Implement **login** and **register** endpoints for user authentication and token generation.

4. **Test Coverage**:
   - Achieve a test coverage of at least **90%**, ensuring all core functionality and edge cases are tested.
   - Use **unit tests** and **integration tests** for API endpoints and business logic.

This task will evaluate your skills in backend development, API security, testing, and overall system design.



### **API Requirements:**

**1. Event CRUD API:**
- **Endpoint 1: POST /events**
  - **Create an event**
  - Request Body:
    ```json
    {
      "name": "Sample Event",
      "location": "Venue A",
      "start_time": "2025-02-10T10:00:00Z",
      "end_time": "2025-02-10T12:00:00Z"
    }
    ```
  - **Response:**
    ```json
    {
      "id": 1,
      "name": "Sample Event",
      "location": "Venue A",
      "start_time": "2025-02-10T10:00:00Z",
      "end_time": "2025-02-10T12:00:00Z"
    }
    ```
  
- **Endpoint 2: GET /events**
  - **Get a list of events**
  - **Response:**
    ```json
    [
      {
        "id": 1,
        "name": "Sample Event",
        "location": "Venue A",
        "start_time": "2025-02-10T10:00:00Z",
        "end_time": "2025-02-10T12:00:00Z"
      }
    ]
    ```

- **Endpoint 3: GET /events/{eventId}**
  - **Get event details by ID**
  - **Response:**
    ```json
    {
      "id": 1,
      "name": "Sample Event",
      "location": "Venue A",
      "start_time": "2025-02-10T10:00:00Z",
      "end_time": "2025-02-10T12:00:00Z"
    }
    ```

- **Endpoint 4: PUT /events/{eventId}**
  - **Update an event**
  - Request Body:
    ```json
    {
      "name": "Updated Event Name",
      "location": "Updated Venue",
      "start_time": "2025-02-12T10:00:00Z",
      "end_time": "2025-02-12T12:00:00Z"
    }
    ```
  - **Response:**
    ```json
    {
      "id": 1,
      "name": "Updated Event Name",
      "location": "Updated Venue",
      "start_time": "2025-02-12T10:00:00Z",
      "end_time": "2025-02-12T12:00:00Z"
    }
    ```

- **Endpoint 5: DELETE /events/{eventId}**
  - **Delete an event**
  - **Response:**
    ```json
    {
      "message": "Event deleted successfully"
    }
    ```

---

**2. Task CRUD API under Event (with time and member assignments):**

- **Endpoint 1: POST /events/{eventId}/tasks**
  - **Create a task for an event**
  - Request Body:
    ```json
    {
      "title": "Task 1",
      "description": "Task description here",
      "assigned_to": [1, 2],  // Member IDs
      "due_time": "2025-02-10T11:00:00Z"
    }
    ```
  - **Response:**
    ```json
    {
      "id": 1,
      "title": "Task 1",
      "assigned_to": [1, 2],
      "due_time": "2025-02-10T11:00:00Z",
      "description": "Task description here",
      "event_id": 1
    }
    ```

- **Endpoint 2: GET /events/{eventId}/tasks**
  - **Get all tasks for an event**
  - **Response:**
    ```json
    [
      {
        "id": 1,
        "title": "Task 1",
        "assigned_to": [1, 2],
        "due_time": "2025-02-10T11:00:00Z",
        "description": "Task description here"
      }
    ]
    ```

- **Endpoint 3: GET /events/{eventId}/tasks/{taskId}**
  - **Get details of a specific task**
  - **Response:**
    ```json
    {
      "id": 1,
      "title": "Task 1",
      "assigned_to": [1, 2],
      "due_time": "2025-02-10T11:00:00Z",
      "description": "Task description here",
      "event_id": 1
    }
    ```

- **Endpoint 4: PUT /events/{eventId}/tasks/{taskId}**
  - **Update task details**
  - Request Body:
    ```json
    {
      "title": "Updated Task 1",
      "description": "Updated description",
      "assigned_to": [1],  // Update assigned members
      "due_time": "2025-02-12T12:00:00Z"
    }
    ```
  - **Response:**
    ```json
    {
      "id": 1,
      "title": "Updated Task 1",
      "assigned_to": [1],
      "due_time": "2025-02-12T12:00:00Z",
      "description": "Updated description"
    }
    ```

- **Endpoint 5: DELETE /events/{eventId}/tasks/{taskId}**
  - **Delete a task**
  - **Response:**
    ```json
    {
      "message": "Task deleted successfully"
    }
    ```

---

### **Authentication:**
- **JWT Authentication**:
  - Protect all the above endpoints with **JWT-based authentication**.
  - The candidate should implement token-based authentication, where the user must send a valid JWT in the `Authorization` header for access.
  - Example Authorization header:
    ```text
    Authorization: Bearer <jwt_token>
    ```

- **User login & registration**:
  - You can have a login route to authenticate and issue a JWT token:
    - **POST /auth/login**: Returns JWT after validating username/password
    - **POST /auth/register**: Allows a new user to create an account

---

### **Testing Requirements:**

- **Test coverage**:
  - The candidate should write unit and integration tests for the API using a framework such as **Jest**, **Mocha**, or **Jasmine**.
  - The tests should cover at least the following scenarios:
    - Successful and failed user authentication
    - CRUD operations for events (create, read, update, delete)
    - CRUD operations for tasks under events (create, read, update, delete)
    - Validation errors (e.g., missing fields, incorrect data types)
    - Permissions (e.g., ensuring tasks are only accessible to authenticated users)
    - Edge cases (e.g., deleting an event with tasks, or tasks with no assigned members)
  - The overall test coverage should be above **90%**.

---

### **Additional Requirements:**

- **Database**: Use any ORM (e.g., Sequelize, TypeORM) with a relational database (e.g., PostgreSQL, MySQL) for data management.
- **Validation**: Use input validation for the data (e.g., using **Joi**, **express-validator**, or similar libraries).
- **Code quality**: The code should be well-structured, readable, and maintainable.
- **Error handling**: Proper error messages with appropriate HTTP status codes (e.g., `400`, `404`, `500`).

---

### **Evaluation Criteria**:
- Ability to follow specifications and implement a secure API
- Code organization and use of best practices (e.g., modular code, clean architecture)
- Authentication and authorization implementation
- Test coverage and effective handling of edge cases
- Attention to detail (e.g., input validation, meaningful error messages)

