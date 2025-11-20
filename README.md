# 🚀 Spark REST API

A lightweight REST API built with **Spark Java**, **Hibernate**, **PostgreSQL**, and **JWT authentication**.
The project demonstrates clean backend architecture suitable for learning and teaching Java backend development.

---

## 📌 Why this repository exists

This project was built as an educational REST API to teach:

- Routing with Spark Java
- Service → Facade → DAO architecture
- Hibernate JPA + HikariCP
- JWT authentication
- Integration testing using Testcontainers
- Docker-based backend development
- Clean separation of concerns

Everything is designed to be as easy to understand as possible.

---

# 🧰 Technologies Used

Taken from your real `pom.xml`.

- Spark Java
- Gson
- Hibernate ORM
- PostgreSQL JDBC
- HikariCP
- bcrypt (password hashing)
- Nimbus JOSE JWT
- dotenv-java
- Logback + SLF4J
- Testcontainers
- Mockito
- Rest-Assured

---

# 📂 Project Structure

```
src/main/java/dk/lyngby/
│
├── config/                → EMF, ApplicationConfig
├── controller/            → Routes
├── exceptions/            → API exception handling
├── model/
│   ├── entities/          → JPA entities
│   ├── facade/            → DB logic
│   └── security/          → JWT, auth middleware
├── service/               → Business logic
│   ├── dto/
│   ├── AuthenticationService
│   ├── PersonService
│   └── Main               → Application entry point
```

---

# 🔐 **Authentication Endpoints**

_(public)_

| Method | Endpoint           | Description            | Body                                             |
| ------ | ------------------ | ---------------------- | ------------------------------------------------ |
| POST   | `/api/v1/login`    | Login & receive JWT    | `{ "username": "", "password": "" }`             |
| POST   | `/api/v1/register` | Register & receive JWT | `{ "username": "", "password": "", "role": "" }` |

---

# 👥 **Person Endpoints (JWT protected)**

Middleware: `before("/*", authentication::authenticate);`

| Method | Endpoint              | Description     | Auth | Body        |
| ------ | --------------------- | --------------- | ---- | ----------- |
| POST   | `/api/v1/persons/`    | Create person   | Yes  | Person JSON |
| GET    | `/api/v1/persons/`    | Get all persons | Yes  | —           |
| GET    | `/api/v1/persons/:id` | Get person      | Yes  | —           |
| PATCH  | `/api/v1/persons/:id` | Update person   | Yes  | Person JSON |
| DELETE | `/api/v1/persons/:id` | Delete person   | Yes  | —           |

(Directly extracted from your Routes.java.)

---

# 🗺️ Architecture Overview

```
 Client → Routes → Services → Facades → Hibernate/JPA → PostgreSQL
```

JWT middleware wraps all `/persons` routes.

---

# 📫 Postman Collection

A full Postman collection is included:

```
postman_collection.json
```

Features:

- Login and store token automatically
- Auto-injected Bearer tokens for protected routes
- Sample request bodies
- Full CRUD suite

Import it in Postman and start testing immediately.

---

# 🐳 Running with Docker

### 1. Build the JAR

```
mvn clean package
```

Your JAR will be:

```
target/app.jar
```

### 2. Run with Dockerfile

```
docker build -t spark-api .
docker run -p 8080:8080 spark-api
```

### 3. Run with docker-compose

```
docker compose up --build
```

This starts:

- Backend
- PostgreSQL
- Environment variables injected automatically

---

# 🧪 Testing

Integration tests use **Testcontainers** for PostgreSQL.

Run all tests:

```
mvn test
```

---

# 📝 Example cURL

Login:

```bash
curl -X POST http://localhost:8080/api/v1/login \
  -H "Content-Type: application/json" \
  -d '{"username":"john","password":"test123"}'
```

---

# 📜 License

MIT License.
