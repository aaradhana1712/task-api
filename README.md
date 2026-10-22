# Task Management RESTful API & Database Integration

A production-ready RESTful CRUD API built with **Node.js**, **Express.js**, and **MongoDB Atlas** with **Mongoose**. Developed as part of the **Time To Future - Full Stack Web Development Internship (Week 2: TASK-WD-201)**.

---

## 🌟 Key Features

- **Standard RESTful API Architecture**: Strict adherence to HTTP methods (`GET`, `POST`, `PUT`, `PATCH`, `DELETE`) with standardized JSON responses.
- **Database Persistence**: Connected to MongoDB Atlas cloud database via Mongoose ODM.
- **Schema Validation & Constraints**: Robust field validations for title, description, enum checks on status and priority, and automatic timestamps.
- **Pagination, Search & Filtering**:
  - Pagination (`page`, `limit`) with metadata (`total`, `totalPages`, `hasNextPage`, `hasPrevPage`).
  - Filter by `status` (`pending`, `in-progress`, `completed`) and `priority` (`low`, `medium`, `high`).
  - Case-insensitive search on title.
  - Dynamic sorting (`sort=-createdAt`).
- **Centralized Error Handling**: Custom error middlewares handling Mongoose `ValidationError`, `CastError` (invalid ObjectId), JSON parse errors, and standard 404 route handlers.
- **CORS Enabled**: Cross-Origin Resource Sharing supported for frontend integration.
- **Postman Collection Included**: Complete Postman collection with test cases and pre-configured requests included in the repository (`Task_API.postman_collection.json`).

---

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js (v5)
- **Database**: MongoDB Atlas
- **ODM**: Mongoose (v9)
- **Environment Management**: dotenv
- **Testing**: Postman, Thunder Client

---

## 📁 Project Structure

```text
task-api/
├── src/
│   ├── config/
│   │   └── db.js                 # MongoDB connection logic
│   ├── controllers/
│   │   └── taskController.js     # CRUD handler functions with pagination & filtering
│   ├── middleware/
│   │   └── errorHandler.js       # Centralized 404 and error handling
│   ├── models/
│   │   └── Task.js               # Mongoose Task schema & data validation
│   └── routes/
│       └── taskRoutes.js         # API route definitions
├── .env.example                  # Template for environment variables
├── .gitignore                    # Ignored files (node_modules, .env)
├── package.json                  # Dependencies & scripts
├── server.js                     # Server entry point
├── Task_API.postman_collection.json # Exported Postman collection
└── README.md                     # Documentation
```

---

## ⚙️ Setup and Installation

### 1. Clone the Repository
```bash
git clone https://github.com/aaradhana1712/task-api.git
cd task-api
```

### 2. Install Dependencies
```bash
npm install
```

### 3. Configure Environment Variables
Create a `.env` file in the root directory:
```env
PORT=5000
MONGO_URI=your_mongodb_atlas_connection_string
```

### 4. Run the Server
- **Development Mode** (with Nodemon):
  ```bash
  npm run dev
  ```
- **Production Mode**:
  ```bash
  npm start
  ```

Server will run on `http://localhost:5000`.

---

## 🚀 API Endpoints & Documentation

### Base URL: `http://localhost:5000/api/tasks`

| Method | Endpoint | Description | Query Parameters |
| :--- | :--- | :--- | :--- |
| **GET** | `/` | Health check route | None |
| **POST** | `/api/tasks` | Create a new task | None |
| **GET** | `/api/tasks` | Get all tasks (paginated) | `page`, `limit`, `status`, `priority`, `search`, `sort` |
| **GET** | `/api/tasks/:id` | Get single task by ID | None |
| **PUT/PATCH** | `/api/tasks/:id` | Update task by ID | None |
| **DELETE** | `/api/tasks/:id` | Delete task by ID | None |

---

### Request & Response Examples

#### 1. Create Task
**`POST /api/tasks`**
```json
// Request Body
{
  "title": "Build RESTful API",
  "description": "Implement CRUD with MongoDB and Express",
  "status": "in-progress",
  "priority": "high",
  "dueDate": "2026-10-31T00:00:00.000Z"
}
```
**Response (`201 Created`):**
```json
{
  "success": true,
  "data": {
    "_id": "67b8d4f012e4...",
    "title": "Build RESTful API",
    "description": "Implement CRUD with MongoDB and Express",
    "status": "in-progress",
    "priority": "high",
    "dueDate": "2026-10-31T00:00:00.000Z",
    "createdAt": "2026-10-22T10:00:00.000Z",
    "updatedAt": "2026-10-22T10:00:00.000Z",
    "__v": 0
  }
}
```

---

#### 2. Get All Tasks (with Pagination, Search & Filter)
**`GET /api/tasks?page=1&limit=5&status=in-progress&priority=high&search=API`**

**Response (`200 OK`):**
```json
{
  "success": true,
  "data": [
    {
      "_id": "67b8d4f012e4...",
      "title": "Build RESTful API",
      "description": "Implement CRUD with MongoDB and Express",
      "status": "in-progress",
      "priority": "high",
      "createdAt": "2026-10-22T10:00:00.000Z",
      "updatedAt": "2026-10-22T10:00:00.000Z"
    }
  ],
  "pagination": {
    "total": 1,
    "page": 1,
    "limit": 5,
    "totalPages": 1,
    "hasNextPage": false,
    "hasPrevPage": false
  }
}
```

---

#### 3. Error Response (Validation Failure)
**`POST /api/tasks`** (Missing required `title`)

**Response (`400 Bad Request`):**
```json
{
  "success": false,
  "message": "Validation failed",
  "errors": [
    "Title is required"
  ]
}
```

---

## 📮 Postman Documentation & Collection

- **Live Public Documentation**: [View API Documentation on Postman](https://documenter.getpostman.com/view/48133336/2sBYHUSKs5)
- **Exported Collection File**: [`Task_API.postman_collection.json`](./Task_API.postman_collection.json)

### How to use in Postman:
1. Open **Postman**.
2. Click **Import** in the top left.
3. Select or drag-and-drop the file `Task_API.postman_collection.json`.
4. Ensure your server is running (`http://localhost:5000`).
5. Run the requests to test all CRUD and edge cases!

---

## 👤 Author
- **Intern**: Aaradhana Mewade
- **Internship**: Full Stack Web Development (Time To Future)
- **Task ID**: TASK-WD-201
