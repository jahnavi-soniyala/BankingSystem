# Banking System Backend

> A RESTful backend system built with Spring Boot and Spring Data JPA for managing users, bank accounts, and financial transactions.

---

## Table of Contents

* [About](#about)
* [Features](#features)
* [Tech Stack](#tech-stack)
* [Installation](#installation)
* [Usage](#usage)
* [API Endpoints](#api-endpoints)
* [Security](#security)
* [Validation & Error Handling](#validation--error-handling)
* [Sample Workflow](#sample-workflow)
* [Future Enhancements](#future-enhancements)
* [Contact](#contact)

---

## About

This project is a banking application backend that handles:

* User registration, update, and deletion
* Creation and management of bank accounts
* Recording deposits, withdrawals, and transfers
* Maintaining transaction history

It uses **Spring Boot** for backend development and **Spring Data JPA** for database interactions.

---

## Features

* CRUD operations for **Users**
* CRUD operations for **Accounts**
* Manage **Transactions** (DEPOSIT, WITHDRAWAL, TRANSFER)
* RESTful API design with proper validation
* UUID-based transaction IDs
* Enum-based account and transaction types
* Robust global exception handling with structured JSON error responses
* Request DTOs for clean data separation and input validation
* Centralized validation error messages

---

## Tech Stack

* **Java 21**
* **Spring Boot 3**
* **Spring Data JPA**
* **Spring Security**
* **PostgreSQL**
* **Maven**
* **Postman**

---

## Installation

### Prerequisites

* Java 17+
* Maven
* PostgreSQL
* IDE (IntelliJ IDEA / Eclipse / VSCode)

### Steps

1. Clone the repository:

```bash
git clone https://github.com/jahnavi-soniyala/BankingSystem.git
cd BankingSystem
```

2. Update `application.properties`:

```properties
spring.datasource.url=jdbc:postgresql://localhost:5432/your_database
spring.datasource.username=your_username
spring.datasource.password=your_password
spring.datasource.driver-class-name=org.postgresql.Driver
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect
```

3. Build and run the application:

```bash
mvn spring-boot:run
```

---

## Usage

You can use **Postman** or **cURL** to test the endpoints.

**Example: Creating a User**

```bash
curl -X POST http://localhost:8080/api/users \
-H "Content-Type: application/json" \
-d '{
  "username": "john",
  "email": "john@example.com",
  "password": "secret123",
  "firstName": "John",
  "lastName": "Doe"
}'
```

**Example: Creating an Account**

```bash
curl -X POST http://localhost:8080/api/accounts \
-H "Content-Type: application/json" \
-d '{
  "userId": 1,
  "accountNumber": "ACC123456",
  "balance": 1000.00,
  "type": "CHECKING"
}'
```

---

## API Endpoints

### User APIs

| Method | URL               | Description                  |
| ------ | ----------------- | ---------------------------- |
| POST   | `/api/users`      | Create a new user            |
| GET    | `/api/users`      | Get all users                |
| GET    | `/api/users/{id}` | Get a user by ID             |
| PUT    | `/api/users/{id}` | Update user info             |
| DELETE | `/api/users/{id}` | Delete user (if no accounts) |

### Account APIs

| Method | URL                  | Description          |
| ------ | -------------------- | -------------------- |
| POST   | `/api/accounts`      | Create a new account |
| GET    | `/api/accounts`      | Get all accounts     |
| GET    | `/api/accounts/{id}` | Get account by ID    |
| PUT    | `/api/accounts/{id}` | Update account info  |
| DELETE | `/api/accounts/{id}` | Delete account       |

### Transaction APIs

| Method | URL                      | Description           |
| ------ | ------------------------ | --------------------- |
| POST   | `/api/transactions`      | Create a transaction  |
| GET    | `/api/transactions`      | Get all transactions  |
| GET    | `/api/transactions/{id}` | Get transaction by ID |

---

## Security

* Uses **HTTP Basic Authentication**.

* Default users for testing:

  * **admin / admin123** (ROLE\_ADMIN)
  * **user / user123** (ROLE\_USER)

* Endpoints require authentication except `/api/users/register`.

---

## Validation & Error Handling

* All request bodies are validated using `jakarta.validation` annotations.
* Detailed error messages are returned for invalid input.
* Errors are wrapped in consistent JSON responses via a global exception handler.

**Example Validation Error Response:**

```json
{
  "timestamp": "2025-09-23T18:31:20.000",
  "status": 400,
  "error": "Bad Request",
  "message": "Validation failed",
  "errors": {
    "email": "Email is required",
    "username": "Username is required"
  }
}
```

* Handles foreign key violations (e.g., cannot delete a user with accounts)
* Generic exceptions return structured Internal Server Error responses

---

## Sample Workflow

1. Register a user → `POST /api/users`
2. Create accounts → `POST /api/accounts`
3. Perform transactions → `POST /api/transactions`
4. View accounts/transactions → `GET /api/accounts`, `GET /api/transactions`
5. Update user/account → `PUT /api/users/{id}`, `PUT /api/accounts/{id}`
6. Delete user/account → `DELETE` (with validation)

---

## Future Enhancements

* Replace Basic Auth with **JWT authentication**
* Add **role-based access control** for users/admins
* Implement **transaction rollback** for insufficient funds
* Add **pagination/filtering** for accounts and transactions
* Add **email notifications** for important transactions

---

## Contact

* **Jahnavi Soniyala**
* Email: [jahnavisonayala@gmail.com](mailto:jahnavisonayala@gmail.com)
* [LinkedIn](https://www.linkedin.com/in/jahnavi-sonayala/)

---


