```markdown
# Task Management API

A RESTful API for managing tasks, built with Node.js, Express, and MongoDB. The API supports basic CRUD operations, data validation, filtering, sorting, and pagination. Designed with proper error handling and efficient database interactions.

---

## **Features**

- **CRUD Operations**: Create, read, update, and delete tasks.
- **Data Validation**: Input validation using Joi.
- **Filtering & Sorting**: Filter by `status` and `priority`; sort by `createdAt` or `dueDate`.
- **Pagination**: Support for large datasets with `limit` and `skip` query parameters.
- **Error Handling**: Centralized error management for predictable responses.
- **Extensibility**: Designed to easily integrate with additional features like authentication.

---

## **Requirements**

- **Node.js** (v14 or higher)
- **MongoDB**
- **Dependencies**:
  - `express`
  - `mongoose`
  - `dotenv`
  - `joi`

---

## **Installation**

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/<your-username>/task-management-api.git
   cd task-management-api
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   ```

3. **Set Up Environment Variables**:
   Create a `.env` file in the project root and add the following:
   ```env
   PORT=5000
   MONGO_URI=mongodb+srv://<username>:<password>@cluster.mongodb.net/<dbname>?retryWrites=true&w=majority
   ```

4. **Start the Server**:
   ```bash
   npm start
   ```
   The API will be available at `http://localhost:5000`.

---

## **API Endpoints**

### **1. Create a Task**
**POST** `/tasks`
- **Request Body**:
  ```json
  {
    "title": "Task Title",
    "description": "Task Description",
    "status": "TODO",
    "priority": "HIGH",
    "dueDate": "2024-12-31"
  }
  ```
- **Response**:
  ```json
  {
    "_id": "unique-task-id",
    "title": "Task Title",
    "description": "Task Description",
    "status": "TODO",
    "priority": "HIGH",
    "dueDate": "2024-12-31",
    "createdAt": "2024-12-08T12:00:00.000Z",
    "updatedAt": "2024-12-08T12:00:00.000Z"
  }
  ```

---

### **2. Retrieve All Tasks**
**GET** `/tasks`
- **Query Parameters**:
  - `status`: Filter by `TODO`, `IN_PROGRESS`, or `COMPLETED`.
  - `priority`: Filter by `LOW`, `MEDIUM`, or `HIGH`.
  - `sort`: Sort by `createdAt` or `dueDate` (`asc` or `desc`).
  - `limit`: Number of tasks to return (default: 10).
  - `skip`: Offset for pagination (default: 0).

**Example Request**:
```http
GET /tasks?status=TODO&priority=HIGH&sort=createdAt&limit=5&skip=0
```

---

### **3. Retrieve a Task by ID**
**GET** `/tasks/:id`
- **Response**:
  ```json
  {
    "_id": "unique-task-id",
    "title": "Task Title",
    "description": "Task Description",
    "status": "TODO",
    "priority": "HIGH",
    "dueDate": "2024-12-31",
    "createdAt": "2024-12-08T12:00:00.000Z",
    "updatedAt": "2024-12-08T12:00:00.000Z"
  }
  ```

---

### **4. Update a Task**
**PUT** `/tasks/:id`
- **Request Body** (Partial updates allowed):
  ```json
  {
    "status": "IN_PROGRESS"
  }
  ```
- **Response**:
  ```json
  {
    "_id": "unique-task-id",
    "title": "Task Title",
    "description": "Task Description",
    "status": "IN_PROGRESS",
    "priority": "HIGH",
    "dueDate": "2024-12-31",
    "createdAt": "2024-12-08T12:00:00.000Z",
    "updatedAt": "2024-12-08T14:00:00.000Z"
  }
  ```

---

### **5. Delete a Task**
**DELETE** `/tasks/:id`
- **Response**: HTTP status `204 No Content` on success.

---

## **Error Responses**

- `400 Bad Request`: Invalid input data.
- `404 Not Found`: Resource not found.
- `500 Internal Server Error`: General server error.

**Example**:
```json
{
  "message": "Task not found"
}
```

---

## **Testing**

1. Use **Postman** to test API endpoints.
2. Import the provided Postman collection (`postman_collection.json`) from the repository.

---

## **Bonus Features**

- **Authentication Middleware** (Optional): Add user authentication with JWT.
- **Logging**: Use Winston or Morgan for logging API requests and errors.
- **Soft Deletes**: Implement soft delete functionality for tasks.

---

## **Future Enhancements**

- Add user authentication and task ownership.
- Enable notifications for upcoming due dates.
- Build a front-end interface for task management.

---

## **Contributing**

Contributions are welcome! Fork the repository, make changes, and submit a pull request.

---

## **License**

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.
```