
# User Authentication Foundations - Password Hashing & JWT Setup

A secure Node.js & Express backend application built as part of the MERN Stack specialization. This update (Update 2) focuses on production-grade user authentication foundations, enforcing cryptographic password hashing using `bcryptjs`, and preparing the system for stateful token-based authorization via `jsonwebtoken`.

---

## 🚀 Features

- **Secure User Registration:** Registers new users with strict model-level validation criteria.
- **Cryptographic Password Hashing:** Utilizes `bcryptjs` with a recommended workload factor (10 salt rounds) to encrypt user credentials before database storage, avoiding plain-text vulnerability.
- **Pre-emptive Duplicate Auditing:** Validates incoming registration requests against existing database records to prevent duplicate email accounts (`unique: true`).
- **Decoupled Data Architecture:** Manages data objects seamlessly across multiple isolated collections (`users` and `tasks`) inside MongoDB.

---

## 🛠️ Tech Stack

- **Runtime Environment:** Node.js
- **Backend Framework:** Express.js (v5.2.1)
- **Object Data Modeling (ODM):** Mongoose (v9.7.3)
- **Security Utilities:** Bcryptjs (v3.0.3), JsonWebToken (v9.0.3)
- **Environment Management:** Dotenv

---

## 📁 Project Structure

```text
├── config/
│   └── dbconnection.config.js   # Asynchronous MongoDB Atlas connection configuration
├── controllers/
│   └── tasks.controller.js      # Task CRUD operations & logic
├── models/
│   ├── tasks.model.js           # Mongoose Task Schema with enum validation
│   └── users.model.js           # Mongoose User Schema with security constraints
├── routes/
│   ├── task.route.js            # Routing architecture for task operations
│   └── user.route.js            # Routing architecture for user auth operations
├── security/
│   └── authentication.security.js # Cryptographic hashing & user creation logic
├── .env                         # Local environment variables (Port & DB Port)
├── .gitignore                   # Dependency exclusions
├── main.js                      # Central application driver & Express lifecycle
├── package.json                 # Manifest file & project metadata
└── README.md                    # Technical documentation

```

---

## ⚙️ Setup & Installation

### 1. Clone the Project Directory

```bash
git clone https://github.com/gunasekaran006-alt/day75-jwt-authentication-----day70-update2.git
cd day75-jwt-authentication-----day70-update2
```

### 2. Download Project Dependencies

```bash
npm install

```

### 3. Establish Local Environment Context

Create a `.env` file in the root structure and declare the target port and secure connection endpoints:

```env
port=8080
atlasport=mongodb+srv://<username>:<password>@cluster.mongodb.net/your-db-name

```

### 4. Execute Server Infrastructure

To initialize the backend environment under nodemon active monitoring:

```bash
npm run dev

```

---

## 🔌 API Endpoints Documentation

### User Authentication (`/user`)

| Method | Endpoint | Description | Expected Payload (JSON) | HTTP Status |
| --- | --- | --- | --- | --- |
| **POST** | `/user/register` | Audits email uniqueness, hashes credential, and commits user to DB | `{ "username", "email", "password" }` | `201 Created` / `400 Bad Request` |

> 🔒 **Security Notice:** The registration pipeline automatically enforces a minimum password length of **6 characters** (`minlength: 6`) at the schema boundary layer.

### Task Management (`/tasks`)

| Method | Endpoint | Description | Payload / URL Parameter | Success Status |
| --- | --- | --- | --- | --- |
| **GET** | `/tasks` | Fetches all relational task objects | None | `200 OK` |
| **POST** | `/tasks` | Appends a single new task instance | `{ "title", "description", "status" }` | `201 Created` |
| **PUT** | `/tasks/:id` | Alters existing parameters of a specific task | Target `id` as parameter + `req.body` | `200 OK` |
| **DELETE** | `/tasks/:id` | Purges an item permanently from collection | Target `id` as parameter | `200 OK` |

---
