# OOAD Mini Project - Exam Management System

## Project Overview for Interview Preparation

### What is this project?
This is a **comprehensive Exam Management System** built using Object-Oriented Analysis and Design (OOAD) principles. It's a full-stack web application that manages student exam registrations, payments, and administrative operations for an educational institution.

## 🏗️ Architecture & Technologies

### Backend (Spring Boot)
- **Framework**: Spring Boot 3.4.4 with Java
- **Database**: MySQL with JPA/Hibernate ORM
- **Architecture**: RESTful API following MVC pattern
- **Build Tool**: Maven
- **Key Dependencies**: Spring Data JPA, Spring Web, Lombok, MySQL Connector

### Frontend (React)
- **Framework**: React 19 with Vite as build tool
- **Styling**: Tailwind CSS
- **HTTP Client**: Axios for API communication
- **Routing**: React Router DOM
- **State Management**: React hooks (useState, useEffect)

## 🎯 Core Functionalities

### 1. Student Management
- **Registration**: Students can create accounts with branch and semester details
- **Authentication**: Login system with email/password
- **Profile Management**: View and manage student information

### 2. Exam Management
- **Exam Creation**: Admins can create exams with course details, dates, and timing
- **Exam Filtering**: Filter exams by branch and semester
- **Exam Information**: Includes course code, name, date, time, total marks, prerequisites

### 3. Registration System
- **Exam Registration**: Students can register for available exams
- **Registration Tracking**: Track registration status and attempts
- **Eligibility Checking**: Verify student eligibility for specific exams

### 4. Payment Processing
- **Payment Integration**: Handle exam registration fees
- **Payment Tracking**: Monitor payment status and dates
- **Financial Records**: Maintain payment history

### 5. Administrative Features
- **Admin Dashboard**: Comprehensive view of system statistics
- **Student Management**: View all registered students
- **Exam Oversight**: Monitor all exams and registrations
- **Reports**: Generate reports on exam registrations

## 🗃️ Database Design (Entity Relationships)

### Core Entities:
1. **Student**: StudentID (PK), name, email, branch, semester, password, blocked status
2. **Exam**: ExamID (PK), courseCode, courseName, examDate, startTime, endTime, totalMarks, semester, branch, prerequisites
3. **Registration**: RegistrationID (PK), studentID (FK), examID (FK), status, attempts, registrationDate
4. **Payment**: PaymentID (PK), registrationID (FK), amount, paymentStatus, paymentDate
5. **Admin**: AdminID (PK), email, password

### Relationships:
- **Student** ↔ **Registration** (One-to-Many)
- **Exam** ↔ **Registration** (One-to-Many)
- **Registration** ↔ **Payment** (One-to-One)

## 🎨 OOAD Principles Implemented

### 1. **Encapsulation**
- Private fields in entity classes with public getter/setter methods
- DTOs (Data Transfer Objects) separate internal models from API responses

### 2. **Inheritance**
- Spring Boot's component hierarchy (Controller → Service → Repository)
- JPA entity inheritance from base classes

### 3. **Polymorphism**
- Interface-based design (Repository interfaces)
- Service layer abstractions

### 4. **Abstraction**
- Service layer abstracts business logic from controllers
- Repository pattern abstracts data access
- DTO pattern abstracts internal model structure

### 5. **Composition**
- Entity relationships (Student has Registrations, Registration has Payment)
- Dependency injection in Spring components

## 🔧 Key Design Patterns

### 1. **MVC (Model-View-Controller)**
- **Model**: JPA entities (Student, Exam, Registration, Payment)
- **View**: React frontend components
- **Controller**: Spring REST controllers

### 2. **Repository Pattern**
- Data access abstraction through Spring Data JPA repositories
- Custom query methods for specific business needs

### 3. **DTO Pattern**
- Separate data transfer objects for API communication
- Mapper classes to convert between entities and DTOs

### 4. **Dependency Injection**
- Spring's @Autowired annotation for loose coupling
- Service layer injection into controllers

## 🚀 API Endpoints

### Student APIs:
- `GET /students` - Get all students
- `POST /students/register` - Register new student
- `POST /students/login` - Student authentication
- `GET /students/{email}` - Get student by email

### Exam APIs:
- `GET /exams` - Get all exams
- `POST /exams/add` - Add new exam
- `GET /exams/{examId}` - Get exam by ID
- `DELETE /exams/{examId}` - Delete exam

### Registration APIs:
- `POST /registrations/register` - Register for exam
- `GET /registrations` - Get all registrations
- `GET /registrations/student/{email}` - Get student's registrations

### Admin APIs:
- `POST /admin/login` - Admin authentication
- `GET /admin/students` - Get all students
- `GET /admin/exams` - Get all exams
- `GET /admin/exams/{examId}/students` - Get students registered for specific exam

## 💡 Interview Talking Points

### Technical Implementation:
1. **"I designed a scalable exam management system using Spring Boot and React"**
2. **"Implemented RESTful APIs following REST conventions"**
3. **"Used JPA/Hibernate for ORM with MySQL database"**
4. **"Applied SOLID principles and design patterns like Repository and MVC"**

### Problem Solving:
1. **"Handled complex entity relationships with proper foreign key constraints"**
2. **"Implemented authentication system for both students and admins"**
3. **"Created efficient filtering mechanisms for exams by branch and semester"**
4. **"Designed payment tracking system with status management"**

### OOAD Focus:
1. **"Demonstrated encapsulation through proper class design"**
2. **"Used composition for entity relationships"**
3. **"Applied abstraction through service layer architecture"**
4. **"Implemented polymorphism through interface-based design"**

## 🎯 Business Value:
- **Automated exam registration** reducing manual paperwork
- **Centralized student management** for educational institutions
- **Real-time payment tracking** for financial transparency
- **Administrative dashboard** for efficient management
- **Scalable architecture** supporting multiple branches and semesters

This project demonstrates your understanding of full-stack development, database design, OOAD principles, and modern web technologies - making it an excellent showcase for technical interviews!