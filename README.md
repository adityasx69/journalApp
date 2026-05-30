# Journal App

A personal journal management backend built with Spring Boot and MongoDB

> **Status:** Active development  
> Core functionality is complete. Spring Security with BCrypt password encoding is implemented.

---

## Features

- User registration with **BCrypt password hashing**
- **Spring Security** with HTTP Basic auth and stateless sessions
- **Role-based access control** (`USER` role assigned on registration)
- Journal entry **CRUD** operations scoped to the authenticated user
- **MongoDB transactions** (`@Transactional`) for atomic journal + user updates
- RESTful backend with a clean controller → service → repository layering
- Public endpoint for health checks and user registration (no auth required)

---

## Tech Stack

| Layer | Technology |
|---|---|
| Language | Java 8 |
| Framework | Spring Boot 2.7.16 |
| Security | Spring Security · BCryptPasswordEncoder |
| Persistence | Spring Data MongoDB |
| Build tool | Maven |
| Boilerplate reduction | Lombok |
| Database | MongoDB |

---

## Project Architecture



---

## API Reference

### Public endpoints (no auth required)

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/public/health-check` | Returns `"Ok"` |
| `POST` | `/public/create-user` | Register a new user |

### User endpoints (HTTP Basic auth required)

| Method | Endpoint | Description |
|---|---|---|
| `PUT` | `/user` | Update username and/or password |
| `DELETE` | `/user` | Delete the authenticated user |

### Journal endpoints (HTTP Basic auth required)

| Method | Endpoint | Description |
|---|---|---|
| `GET` | `/journal` | Get all entries for the authenticated user |
| `POST` | `/journal` | Create a new journal entry |
| `GET` | `/journal/id/{id}` | Get a specific entry by ID |
| `PUT` | `/journal/id/{username}/{id}` | Update an entry by ID |
| `DELETE` | `/journal/id/{username}/{id}` | Delete an entry by ID |

> All `/journal/**` and `/user/**` routes are protected. Any unauthenticated request returns `401`.

---

## Getting Started

### Prerequisites

- Java 8+
- Maven 3.6+
- MongoDB (local or Atlas)

### Running locally

```bash
git clone https://github.com/your-username/journalApp.git
cd journalApp
mvn spring-boot:run
```

Make sure MongoDB is running on the default port (`27017`). Configure the connection in `src/main/resources/application.properties`:

```properties
spring.data.mongodb.uri=mongodb://localhost:27017/journaldb
```

---

## MongoDB Collections

### `users`

| Field | Type | Notes |
|---|---|---|
| `_id` | ObjectId | Primary key |
| `userName` | String | Unique index |
| `password` | String | BCrypt hashed |
| `journalEntries` | DBRef[] | References to `journal_entries` |
| `roles` | String[] | Defaults to `["USER"]` |

### `journal_entries`

| Field | Type | Notes |
|---|---|---|
| `_id` | ObjectId | Primary key |
| `title` | String | Required |
| `content` | String | Optional |
| `date` | LocalDateTime | Set automatically on creation |

---

## Planned Enhancements

- [ ] JWT authentication (replace HTTP Basic)
- [ ] Swagger / OpenAPI documentation
- [ ] Search and filtering on journal entries
- [ ] Tags and categories
- [ ] File and image attachments
- [ ] Dockerisation
- [ ] CI/CD pipeline (GitHub Actions)
- [ ] Cloud deployment (AWS / GCP)
- [ ] Automated testing (JUnit 5, Mockito)
- [ ] Frontend — React + TypeScript + Tailwind CSS

---

## Author

**Aditya Saraswat**

---

⭐ If you found this project interesting, consider starring the repository.
