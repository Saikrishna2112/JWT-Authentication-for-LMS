# JWT-Authentication-for-LMS
# Secure RESTful API Authentication with Spring Boot and JWT

This project demonstrates a robust and secure authentication system for RESTful APIs using Spring Boot and JSON Web Tokens (JWT). It provides a foundational boilerplate for implementing user management and secure access control in your microservices or web applications.

## ✨ Features

* **User Registration:** Allows new users to create an account.
* **User Login:** Authenticates users with their credentials.
* **JWT Generation:** Issues a stateless JWT upon successful login.
* **Protected Endpoints:** Secures API endpoints, requiring a valid JWT for access.
* **Stateless Authentication:** Leverages JWTs for efficient and scalable authentication without server-side sessions.
* **Password Hashing:** Securely stores user passwords using BCrypt.

## 🚀 Technologies Used

* **Spring Boot:** Framework for building robust, stand-alone, production-grade Spring applications.
* **Spring Security:** Comprehensive security framework for Spring applications.
* **JWT (JSON Web Tokens):** For secure, stateless authentication.
* **Spring Data JPA:** Simplifies data access layer development.
* **PostgreSQL:** Relational database for storing user data.
* **Lombok:** Reduces boilerplate code (getters, setters, constructors).

## 🛠️ Setup and Run

### Prerequisites

* Java Development Kit (JDK) 22 or higher
* Maven 3.6+
* PostgreSQL database server

### Database Configuration

1.  **Create PostgreSQL Database:**
    Open your PostgreSQL client (e.g., `psql`, pgAdmin) and create a new database:
    ```sql
    CREATE DATABASE jwt_auth_db;
    ```
2.  **Update `application.properties`:**
    In `src/main/resources/application.properties`, configure your database connection details:

    ```properties
    spring.datasource.url=jdbc:postgresql://localhost:5432/jwt_auth_db
    spring.datasource.username=your_postgresql_username
    spring.datasource.password=your_postgresql_password
    spring.datasource.driver-class-name=org.postgresql.Driver

    # JPA and Hibernate Configuration
    spring.jpa.hibernate.ddl-auto=update
    spring.jpa.show-sql=true
    spring.jpa.properties.hibernate.format_sql=true
    spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.PostgreSQLDialect

    # JWT Configuration
    jwt.secret=your_super_secret_jwt_key_that_is_at_least_256_bits_long_and_base64_encoded
    jwt.expiration=300000 # 5 minutes in milliseconds
    ```
    **Important:**
    * Replace `your_postgresql_username` and `your_postgresql_password` with your actual PostgreSQL credentials.
    * Replace `your_super_secret_jwt_key...` with a strong, random, Base64-encoded secret key. You can generate one online or use a tool like `openssl rand -base64 32` for a 256-bit key.

### Build and Run

1.  **Clone the Repository:**
    ```bash
    git clone <your-repository-url>
    cd springboot-jwt-auth
    ```
2.  **Build the Project:**
    ```bash
    mvn clean install
    ```
3.  **Run the Application:**
    ```bash
    mvn spring-boot:run
    ```
    The application will start on `http://localhost:8080`.

## 🧪 API Endpoints

You can use a tool like Postman, Insomnia, or curl to test the API endpoints.

### 1. Register a New User (Public)

* **Endpoint:** `POST http://localhost:8080/auth/register`
* **Headers:**
    * `Content-Type: application/json`
* **Request Body (JSON):**
    ```json
    {
        "username": "testuser",
        "password": "password123"
    }
    ```
* **Success Response (Example):**
    ```json
    {
        "message": "User registered successfully!"
    }
    ```

### 2. User Login (Public)

* **Endpoint:** `POST http://localhost:8080/auth/login`
* **Headers:**
    * `Content-Type: application/json`
* **Request Body (JSON):**
    ```json
    {
        "username": "testuser",
        "password": "password123"
    }
    ```
* **Success Response (Example):**
    ```json
    {
        "token": "eyJhbGciOiJIUzI1NiJ9.eyJzdWIiOiJ0ZXN0dXNlciIsImlhdCI6MTcwMDAwMDAwMCwiZXhwIjoxNzAwMDAzNjAwfQ...."
    }
    ```
    *Copy this `token` for accessing protected resources.*

### 3. Access Protected Resource (Requires JWT)

* **Endpoint:** `GET http://localhost:8080/api/hello` (or any other protected endpoint you define)
* **Headers:**
    * `Authorization: Bearer YOUR_JWT_TOKEN_HERE`
* **Success Response (Example):**
    ```json
    {
        "message": "Hello from a protected endpoint!"
    }
    ```
    *If the token is missing, invalid, or expired, you will receive a 401 Unauthorized or 403 Forbidden response.*

## 🤝 Contributing

Feel free to fork the repository, open issues, and submit pull requests.

