# OOAD Mini Project - Exam Management System

> A comprehensive full-stack web application demonstrating Object-Oriented Analysis and Design principles using Spring Boot and React.

[![Java](https://img.shields.io/badge/Java-17-orange.svg)](https://www.oracle.com/java/)
[![Spring Boot](https://img.shields.io/badge/Spring%20Boot-3.4.4-brightgreen.svg)](https://spring.io/projects/spring-boot)
[![React](https://img.shields.io/badge/React-19.0.0-blue.svg)](https://reactjs.org/)
[![MySQL](https://img.shields.io/badge/MySQL-8.0+-blue.svg)](https://www.mysql.com/)

## 📋 Project Overview

The Exam Management System is a modern web application designed for educational institutions to manage exam registrations, student enrollment, and payment processing. This project showcases enterprise-level software development practices and design patterns.

### 🎯 Key Features
- **Student Management**: Registration, login, profile management
- **Exam Administration**: Create, schedule, and manage exams
- **Registration System**: Students can register for exams based on eligibility
- **Payment Processing**: Handle exam fees and payment tracking
- **Admin Dashboard**: Comprehensive management interface

## 🏗️ Architecture

### System Design
```
Frontend (React) ↔ REST API ↔ Spring Boot Backend ↔ MySQL Database
```

The application follows a **3-tier architecture** with clear separation of concerns:

1. **Presentation Layer** - React components and pages
2. **Business Logic Layer** - Spring Boot services and controllers  
3. **Data Access Layer** - JPA repositories and MySQL database

### Design Patterns Implemented
- **MVC (Model-View-Controller)**
- **Repository Pattern**
- **Data Transfer Object (DTO)**
- **Service Layer Pattern**
- **Mapper Pattern**
- **Dependency Injection**

## 💻 Technology Stack

### Backend
- **Framework**: Spring Boot 3.4.4
- **Language**: Java 17
- **Database**: MySQL 8.0+
- **ORM**: Hibernate/JPA
- **Build Tool**: Maven
- **Architecture**: RESTful Web Services

### Frontend
- **Framework**: React 19.0.0
- **Build Tool**: Vite
- **Routing**: React Router DOM 7.5.0
- **HTTP Client**: Axios 1.8.4
- **Styling**: Tailwind CSS
- **State Management**: React Context API

## 🚀 Getting Started

### Prerequisites
- Java 17 or higher
- Node.js 16+ and npm
- MySQL 8.0+
- Maven 3.6+

### Installation

1. **Clone the repository**
   ```bash
   git clone https://github.com/MMG159/OOAD_Mini_Project.git
   cd OOAD_Mini_Project
   ```

2. **Setup Database**
   ```sql
   CREATE DATABASE userdb;
   ```
   Update `src/main/resources/application.properties` with your MySQL credentials.

3. **Backend Setup**
   ```bash
   # Install dependencies and compile
   mvn clean install
   
   # Run the application
   mvn spring-boot:run
   ```
   Backend server will start on `http://localhost:8080`

4. **Frontend Setup**
   ```bash
   # Navigate to frontend directory
   cd frontend
   
   # Install dependencies
   npm install
   
   # Start development server
   npm run dev
   ```
   Frontend will be available on `http://localhost:5173`

## 📚 Documentation

Comprehensive documentation is available in the following files:

- **[📖 PROJECT_DOCUMENTATION.md](./PROJECT_DOCUMENTATION.md)** - Complete project explanation for interviews
- **[🏛️ ARCHITECTURE_DIAGRAM.md](./ARCHITECTURE_DIAGRAM.md)** - Visual system architecture
- **[🎬 INTERVIEW_DEMO_SCRIPT.md](./INTERVIEW_DEMO_SCRIPT.md)** - Step-by-step demo guide
- **[📋 TECHNICAL_REFERENCE.md](./TECHNICAL_REFERENCE.md)** - Quick reference for technical concepts

## 🗃️ Database Schema

### Core Entities
- **Student** - Student information and authentication
- **Exam** - Exam details and scheduling  
- **Registration** - Links students to exams
- **Payment** - Payment processing and tracking
- **Admin** - Administrative user management

### Entity Relationships
```
Student (1:N) Registration (N:1) Exam
            (1:1) Payment
```

## 🔗 API Endpoints

### Student Endpoints
- `GET /students` - Get all students
- `POST /students/register` - Register new student
- `POST /students/login` - Student authentication

### Exam Endpoints  
- `GET /exams` - Get all exams
- `POST /exams/add` - Create new exam
- `DELETE /exams/{id}` - Delete exam

### Registration Endpoints
- `POST /registrations/register` - Register for exam
- `GET /registrations/student/{email}` - Get student registrations

### Payment Endpoints
- `POST /payments/process` - Process payment
- `GET /payments/{id}` - Get payment details

## 🎯 OOAD Principles Demonstrated

### Four Pillars of OOP
1. **Encapsulation** - Private fields with public accessors
2. **Inheritance** - Repository interfaces extending JpaRepository
3. **Polymorphism** - Service implementations and method overriding
4. **Abstraction** - Abstract interfaces and DTO pattern

### Design Principles
- **Single Responsibility** - Each class has one clear purpose
- **Open/Closed** - Extensible design through interfaces
- **Liskov Substitution** - Proper inheritance hierarchies
- **Interface Segregation** - Focused, cohesive interfaces
- **Dependency Inversion** - Depend on abstractions, not concretions

## 🧪 Testing

### Backend Testing
```bash
# Run all tests
mvn test

# Run with coverage
mvn test jacoco:report
```

### Frontend Testing
```bash
# Run tests
npm test

# Run with coverage
npm run test:coverage
```

## 📊 Project Structure

```
OOAD_Mini_Project/
├── src/
│   ├── main/java/com/ooad/demo/
│   │   ├── controller/          # REST Controllers
│   │   ├── service/            # Business Logic
│   │   ├── repository/         # Data Access
│   │   ├── model/              # Entity Models
│   │   ├── dto/                # Data Transfer Objects
│   │   ├── mapper/             # Entity-DTO Mappers
│   │   └── config/             # Configuration
│   └── main/resources/
│       └── application.properties
├── frontend/
│   ├── src/
│   │   ├── components/         # React Components
│   │   ├── pages/              # Application Pages
│   │   ├── context/            # State Management
│   │   └── services/           # API Services
│   └── package.json
├── PROJECT_DOCUMENTATION.md    # Comprehensive documentation
├── ARCHITECTURE_DIAGRAM.md     # System architecture
├── INTERVIEW_DEMO_SCRIPT.md    # Demo guide
├── TECHNICAL_REFERENCE.md      # Quick reference
└── pom.xml                     # Maven configuration
```

## 🏆 Features Showcase

### For Students
- ✅ User registration and authentication
- ✅ Browse available exams by branch/semester
- ✅ Register for eligible exams
- ✅ Process payments securely
- ✅ Track registration status

### For Administrators  
- ✅ Comprehensive admin dashboard
- ✅ Create and manage exams
- ✅ View all registered students
- ✅ Monitor registrations and payments
- ✅ Generate reports

## 🔮 Future Enhancements

- **Security**: JWT authentication and authorization
- **Testing**: Comprehensive unit and integration tests
- **Deployment**: Docker containerization
- **Performance**: Redis caching and query optimization
- **Monitoring**: Logging and health check endpoints
- **Mobile**: React Native mobile application

## 🤝 Contributing

This is an academic project demonstrating OOAD principles. For suggestions or improvements:

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📝 License

This project is created for educational purposes as part of an Object-Oriented Analysis and Design course.

## 👨‍💻 Author

**MMG159**
- GitHub: [@MMG159](https://github.com/MMG159)

---

## 🎤 Interview Ready

This project is specifically designed to demonstrate proficiency in:

- **Full-Stack Development** with modern technologies
- **Object-Oriented Design** principles and patterns
- **Database Design** and relationship management
- **RESTful API** development and consumption
- **React Development** with hooks and state management
- **Spring Boot** framework and ecosystem
- **Software Engineering** best practices

Perfect for showcasing technical skills in software engineering interviews! 🚀