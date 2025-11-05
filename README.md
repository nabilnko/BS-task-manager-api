# 📋 Task Manager API

A robust RESTful API built with Spring Boot for efficient task management operations. This application provides a complete backend solution with CRUD functionality, exception handling, and interactive API documentation.

![Spring Boot](https://img.shields.io/badge/Spring_Boot-6DB33F?style=for-the-badge&logo=spring-boot&logoColor=white)
![Java](https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white)
![Maven](https://img.shields.io/badge/Maven-C71A36?style=for-the-badge&logo=apache-maven&logoColor=white)
![REST API](https://img.shields.io/badge/REST-02569B?style=for-the-badge&logo=rest&logoColor=white)

---

## ✨ Features

### 🎯 Core Functionality
- **Complete CRUD Operations**: Create, Read, Update, and Delete tasks
- **RESTful Architecture**: Clean and intuitive API endpoints
- **Data Validation**: Input validation for task creation and updates
- **Exception Handling**: Global exception handler with meaningful error responses
- **Status Management**: Track task completion status

### 📚 Documentation & Testing
- **OpenAPI/Swagger Integration**: Interactive API documentation
- **Swagger UI**: Test endpoints directly from the browser
- **API Specification**: Auto-generated OpenAPI 3.0 documentation

### 🏗️ Technical Features
- **Layered Architecture**: Separation of concerns (Controller, Service, Repository, Entity)
- **Repository Pattern**: JPA-based data access layer
- **Dependency Injection**: Spring's IoC container for loose coupling
- **Maven Build System**: Simplified dependency management

---


## 🛠️ Technology Stack

| Technology | Version | Purpose |
|------------|---------|---------|
| **Java** | 17+ | Programming language |
| **Spring Boot** | 3.x | Application framework |
| **Spring Web** | - | REST API development |
| **Spring Data JPA** | - | Database abstraction |
| **H2 Database** | - | In-memory database |
| **Maven** | 3.8+ | Build and dependency management |
| **SpringDoc OpenAPI** | 2.x | API documentation |
| **Lombok** | (optional) | Reduce boilerplate code |

---

## 🚀 Getting Started

### Prerequisites

Ensure you have the following installed:

- **Java Development Kit (JDK)** 17 or higher
- **Maven** 3.8+ (or use included Maven wrapper)
- **IntelliJ IDEA** / **Eclipse** / **VS Code** with Java extensions
- **Git** for version control
- **Postman** (optional, for API testing)

### Installation & Setup

1. **Clone the repository**
   git clone https://github.com/nabilnko/BS-task-manager-api.git
   cd task-manager-api
2. **Build the project**
   Using Maven wrapper (recommended)
   ./mvnw clean install

Or using system Maven
mvn clean install
3. **Run the application**
   Using Maven wrapper
   ./mvnw spring-boot:run

Or using system Maven
mvn spring-boot:run
4. **Access the application**
- **API Base URL**: `http://localhost:8080`
- **Swagger UI**: `http://localhost:8080/swagger-ui.html`
- **H2 Console**: `http://localhost:8080/h2-console` (if enabled)

---

## 📖 API Endpoints

### Task Management

| Method | Endpoint | Description | Request Body |
|--------|----------|-------------|--------------|
| `GET` | `/api/tasks` | Retrieve all tasks | - |
| `GET` | `/api/tasks/{id}` | Get task by ID | - |
| `POST` | `/api/tasks` | Create new task | Task JSON |
| `PUT` | `/api/tasks/{id}` | Update existing task | Task JSON |
| `DELETE` | `/api/tasks/{id}` | Delete task | - |

### Request/Response Examples

#### Create Task
POST /api/tasks
Content-Type: application/json

{
"title": "Complete project documentation",
"description": "Write comprehensive README for GitHub",
"completed": false
}
**Response (201 Created):**
{
"id": 1,
"title": "Complete project documentation",
"description": "Write comprehensive README for GitHub",
"completed": false,
"createdAt": "2025-11-05T13:30:00"
}
#### Get All Tasks
GET /api/tasks
**Response (200 OK):**
[
{
"id": 1,
"title": "Complete project documentation",
"description": "Write comprehensive README for GitHub",
"completed": false
},
{
"id": 2,
"title": "Review pull requests",
"description": "Check pending PRs on GitHub",
"completed": true
}
]
#### Update Task
PUT /api/tasks/1
Content-Type: application/json

{
"title": "Complete project documentation",
"description": "Write comprehensive README for GitHub",
"completed": true
}
#### Delete Task
DELETE /api/tasks/1
**Response (204 No Content)**

---

## 🗃️ Database Configuration

By default, the application uses **H2 in-memory database**. Configuration in `application.properties`:

H2 Database
spring.datasource.url=jdbc:h2:mem:taskdb
spring.datasource.driverClassName=org.h2.Driver
spring.datasource.username=sa
spring.datasource.password=

JPA/Hibernate
spring.jpa.database-platform=org.hibernate.dialect.H2Dialect
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true

H2 Console
spring.h2.console.enabled=true
spring.h2.console.path=/h2-console
### Switching to MySQL (Production)

Update `pom.xml`:
<dependency> <groupId>mysql</groupId> <artifactId>mysql-connector-java</artifactId> <scope>runtime</scope> </dependency> ```spring.datasource.url=jdbc:mysql://localhost:3306/taskmanager

Update application.properties:
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.hibernate.ddl-auto=update
spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL8Dialect

🧪 Testing
Run Tests
# Using Maven wrapper
./mvnw test

# Using system Maven
mvn test
Test with Postman
Import the collection from postman-collection.json (if available)

Set base URL: http://localhost:8080

Test all CRUD operations

Test with Swagger UI
Navigate to: http://localhost:8080/swagger-ui.html

Expand endpoint sections

Click "Try it out"

Fill in request body

Execute and view response

📦 Build & Deployment
Package as JAR
./mvnw clean package
The JAR file will be created in target/taskmanager-0.0.1-SNAPSHOT.jar

Run JAR
java -jar target/taskmanager-0.0.1-SNAPSHOT.jar
Docker Deployment (Optional)
Create Dockerfile:
FROM openjdk:17-jdk-slim
WORKDIR /app
COPY target/taskmanager-0.0.1-SNAPSHOT.jar app.jar
EXPOSE 8080
ENTRYPOINT ["java", "-jar", "app.jar"]
Build and run:
docker build -t task-manager-api .
docker run -p 8080:8080 task-manager-api
🎯 Project Structure Explained
Entity Layer (Task.java)
Defines the data model

JPA annotations for database mapping

Includes fields: id, title, description, completed

Repository Layer (TaskRepository.java)
Extends JpaRepository

Provides CRUD methods

Custom queries (if needed)

Service Layer (TaskService.java)
Business logic implementation

Transaction management

Data transformation

Controller Layer (TaskController.java)
REST endpoint definitions

Request/response handling

HTTP status codes

Exception Handling (GlobalExceptionHandler.java)
Centralized error handling

Custom exception responses

Consistent error format

Configuration (OpenAPIConfig.java)
Swagger/OpenAPI setup

API metadata

Documentation customization

🔮 Future Enhancements
User Authentication: Add JWT-based security

Task Categories: Organize tasks by categories/tags

Due Dates: Add deadline tracking with reminders

Priority Levels: Implement task prioritization

Search & Filter: Advanced query capabilities

Pagination: Handle large datasets efficiently

Task Sharing: Multi-user collaboration

Email Notifications: Automated reminders

File Attachments: Add documents to tasks

Activity Logs: Track task history and changes

Docker Compose: Multi-container setup

CI/CD Pipeline: Automated testing and deployment

🤝 Contributing
Contributions are welcome! To contribute:

Fork the repository

Create a feature branch: git checkout -b feature/your-feature-name

Commit your changes: git commit -m 'Add some amazing feature'

Push to the branch: git push origin feature/your-feature-name

Open a Pull Request

Code Style Guidelines
Follow Java naming conventions

Write meaningful commit messages

Add comments for complex logic

Include unit tests for new features
👨‍💻 Author
Your Name

GitHub:https://github.com/nabilnko

Email: nabilnko11@gmail.com.com

🙏 Acknowledgments
Spring Boot team for the excellent framework

Spring community for tutorials and support

OpenAPI/Swagger for API documentation tools

All contributors and supporters
