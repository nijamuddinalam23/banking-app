# Banking App

A backend banking application built with **Spring Boot**, **Spring Data JPA**, and **MySQL**. It provides REST APIs for account management, deposits, withdrawals, and fund transfers, with pagination, sorting, Bean Validation, DTOs, and global exception handling.

## Features

- Create and manage bank accounts
- Deposit money into an account
- Withdraw money from an account
- Transfer funds between accounts
- Pagination and sorting for account listings
- Input validation using **Bean Validation**
- DTO-based design, so entities are never exposed directly
- Centralized error handling with `@RestControllerAdvice`
- APIs tested with **Postman**

## Tech Stack

| Layer       | Technology                  |
|-------------|-----------------------------|
| Language    | Java                        |
| Framework   | Spring Boot                 |
| Persistence | Spring Data JPA (Hibernate) |
| Database    | MySQL                       |
| Validation  | Jakarta Bean Validation     |
| Build Tool  | Maven                       |
| API Testing | Postman                     |

## Project Structure

```
banking-app/                     <- repository root
└── banking-app/                 <- Spring Boot project
    └── src/main/java/...
        ├── controller           # REST controllers
        ├── dto                  # Request/response DTOs
        ├── entity               # JPA entities
        ├── exception            # Custom exceptions + global handler
        ├── repository           # Spring Data JPA repositories
        └── service              # Business logic
```

## Getting Started

### Prerequisites

- JDK 17 or higher
- Maven 3.8+
- MySQL 8+
- Git

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/nijamuddinalam23/banking-app.git
   cd banking-app/banking-app
   ```

2. **Create the database**
   ```sql
   CREATE DATABASE banking_db;
   ```

3. **Configure the database** in `src/main/resources/application.properties`
   ```properties
   spring.datasource.url=jdbc:mysql://localhost:3306/banking_db
   spring.datasource.username=your_username
   spring.datasource.password=your_password

   spring.jpa.hibernate.ddl-auto=update
   spring.jpa.show-sql=true
   ```

4. **Run the application**
   ```bash
   mvn spring-boot:run
   ```

The server starts at `http://localhost:8080`.

## API Endpoints

> Update the paths below to match your controller.

| Method | Endpoint                          | Description                          |
|--------|-----------------------------------|--------------------------------------|
| POST   | `/api/accounts`                   | Create a new account                 |
| GET    | `/api/accounts/{id}`              | Get account details by ID            |
| GET    | `/api/accounts`                   | List accounts (paginated and sorted) |
| POST   | `/api/accounts/{id}/deposit`      | Deposit money                        |
| POST   | `/api/accounts/{id}/withdraw`     | Withdraw money                       |
| POST   | `/api/accounts/transfer`          | Transfer funds between accounts      |

### Pagination and Sorting

| Query Param | Default | Description                     |
|-------------|---------|---------------------------------|
| `page`      | `0`     | Page number (starts at 0)       |
| `size`      | `10`    | Records per page                |
| `sortBy`    | `id`    | Field to sort by                |
| `sortDir`   | `asc`   | Sort direction: `asc` or `desc` |

Example:
```
GET /api/accounts?page=0&size=5&sortBy=balance&sortDir=desc
```

## Validation and Error Handling

Request bodies are validated with Bean Validation annotations (such as `@NotBlank`, `@NotNull`, `@Positive`). All errors are handled in one place by a `@RestControllerAdvice` class, which returns clear, consistent responses for cases like:

- Invalid input (validation failures)
- Account not found
- Insufficient balance
- Invalid transfer requests

Example error response:
```json
{
  "status": 400,
  "message": "Insufficient balance",
  "timestamp": "2026-10-21T10:30:00"
}
```

## Testing with Postman

1. Start the application.
2. Open Postman and create requests for each endpoint above.
3. Set the `Content-Type` header to `application/json` for POST requests.
4. Try both valid and invalid inputs to see validation and error responses.



## Author

**Nijamuddin Alam**
GitHub: [@nijamuddinalam23](https://github.com/nijamuddinalam23)
