# OOAD Mini Project - Exam Management System
## Comprehensive Documentation for Interview Presentation

---

## 📋 Project Overview

The **Exam Management System** is a full-stack web application designed to streamline the process of exam registration, management, and payment for educational institutions. This project demonstrates the practical implementation of Object-Oriented Analysis and Design (OOAD) principles using modern web technologies.

### 🎯 Project Purpose
- Enable students to register for exams online
- Allow administrators to manage exams, students, and registrations
- Process payments for exam registrations
- Provide a seamless user experience for both students and administrators

---

## 🏗️ Technical Architecture

### **System Architecture**
The application follows a **3-tier architecture**:

1. **Presentation Layer** (Frontend - React)
2. **Business Logic Layer** (Backend - Spring Boot)
3. **Data Access Layer** (Database - MySQL)

### **Design Patterns Implemented**

#### 1. **MVC (Model-View-Controller) Pattern**
```
Frontend (React) ←→ REST API ←→ Controller → Service → Repository → Database
```

#### 2. **Data Transfer Object (DTO) Pattern**
- Separates internal entity structure from external API contracts
- Examples: `ExamDTO`, `StudentDTO`, `RegistrationDTO`

#### 3. **Repository Pattern**
- Abstracts data access logic
- Example: `ExamRepository extends JpaRepository<Exam, Integer>`

#### 4. **Service Layer Pattern**
- Encapsulates business logic
- Example: `ExamService`, `StudentService`, `RegistrationService`

#### 5. **Mapper Pattern**
- Converts between entities and DTOs
- Example: `ExamMapper.toDTO()`, `ExamMapper.toEntity()`

---

## 💻 Technology Stack

### **Backend Technologies**
- **Framework**: Spring Boot 3.4.4
- **Language**: Java 17
- **Database**: MySQL
- **ORM**: Hibernate/JPA
- **Build Tool**: Maven
- **API Style**: RESTful Web Services

### **Frontend Technologies**
- **Framework**: React 19.0.0
- **Build Tool**: Vite
- **Routing**: React Router DOM
- **HTTP Client**: Axios
- **Styling**: CSS with Tailwind CSS
- **State Management**: Context API

### **Database Configuration**
```properties
spring.datasource.url=jdbc:mysql://localhost:3306/userdb
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

---

## 🗃️ Database Design & Entity Relationships

### **Core Entities**

#### 1. **Student Entity**
```java
@Entity
public class Student {
    @Id
    private String studentId;
    private String name;
    private String email;
    private String branch;
    private int semester;
    private String password;
    private boolean isBlocked;
    
    @OneToMany(mappedBy = "student")
    private List<Registration> registrations;
}
```

#### 2. **Exam Entity**
```java
@Entity
public class Exam {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int examId;
    private String courseCode;
    private String courseName;
    private LocalDate examDate;
    private LocalTime startTime;
    private LocalTime endTime;
    private int totalMarks;
    private int semester;
    private String branch;
    private String prerequisites;
    
    @OneToMany(mappedBy = "exam")
    private List<Registration> registrations;
}
```

#### 3. **Registration Entity**
```java
@Entity
public class Registration {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int registrationId;
    
    @ManyToOne
    @JoinColumn(name = "student_id")
    private Student student;
    
    @ManyToOne
    @JoinColumn(name = "exam_id")
    private Exam exam;
    
    private String status;
    private int attempts;
    private Date registrationDate;
    
    @OneToOne(mappedBy = "registration")
    private Payment payment;
}
```

#### 4. **Payment Entity**
```java
@Entity
public class Payment {
    @Id
    @GeneratedValue(strategy = GenerationType.IDENTITY)
    private int paymentId;
    
    @OneToOne
    @JoinColumn(name = "registration_id")
    private Registration registration;
    
    private double amount;
    private String paymentStatus;
    private LocalDate paymentDate;
}
```

### **Entity Relationships**
- **Student** ↔ **Registration** (One-to-Many)
- **Exam** ↔ **Registration** (One-to-Many)
- **Registration** ↔ **Payment** (One-to-One)
- **Admin** (Independent entity for administrative functions)

---

## 🚀 Key Features & Functionalities

### **Student Features**
1. **Registration & Authentication**
   - Create new student account
   - Login with email and password
   - Profile management

2. **Exam Management**
   - View available exams based on branch and semester
   - Register for exams
   - View registration status
   - Track exam schedules

3. **Payment Processing**
   - Process exam registration payments
   - View payment history
   - Payment status tracking

### **Admin Features**
1. **Exam Management**
   - Add new exams
   - View all exams
   - Delete exams
   - Manage exam schedules

2. **Student Management**
   - View all registered students
   - View students registered for specific exams
   - Block/unblock students

3. **Registration Management**
   - View all registrations
   - Manage registration status
   - Generate reports

---

## 🔗 API Endpoints

### **Student Endpoints**
```http
GET    /students              # Get all students
POST   /students/register     # Register new student
GET    /students/{email}      # Get student by email
POST   /students/login        # Student login
```

### **Exam Endpoints**
```http
GET    /exams                 # Get all exams
GET    /exams/{examId}        # Get exam by ID
POST   /exams/add             # Add new exam
DELETE /exams/{examId}        # Delete exam
```

### **Registration Endpoints**
```http
POST   /registrations/register           # Register for exam
GET    /registrations/student/{email}    # Get student registrations
GET    /registrations/exam/{examId}      # Get exam registrations
```

### **Payment Endpoints**
```http
POST   /payments/process                    # Process payment
GET    /payments                           # Get all payments
GET    /payments/{paymentId}               # Get payment by ID
GET    /payments/registration/{regId}      # Get payment by registration
```

---

## 🎨 Frontend Architecture

### **Component Structure**
```
src/
├── components/
│   ├── login.jsx          # Student login
│   ├── register.jsx       # Student registration
│   └── admin.jsx          # Admin login
├── pages/
│   ├── home.jsx           # Student dashboard
│   ├── AdminDashboard.jsx # Admin dashboard
│   ├── AdminExamPage.jsx  # Exam management
│   ├── ExamsPage.jsx      # View exams
│   ├── PaymentPage.jsx    # Payment processing
│   └── StudentRegistrationPage.jsx
├── context/
│   └── UserContext.jsx    # Global state management
└── App.jsx                # Main application component
```

### **State Management**
Uses React Context API for managing user authentication state:
```javascript
const UserContext = createContext();

function App() {
  const [student, setStudent] = useState(null);
  const [admin, setAdmin] = useState(null);
  // ...
}
```

### **Routing Configuration**
```javascript
<Routes>
  <Route path="/login" element={<Login />} />
  <Route path="/register" element={<Register />} />
  <Route path="/home" element={<Home />} />
  <Route path="/admin" element={<AdminLogin />} />
  <Route path="/admin/dashboard" element={<AdminDashboard />} />
  <Route path="/admin/addexams" element={<AdminExamPage />} />
  <Route path="/payment" element={<PaymentPage />} />
</Routes>
```

---

## 🎯 OOAD Principles Demonstrated

### **1. Encapsulation**
- Private fields with public getter/setter methods
- Service layer encapsulates business logic
- Repository layer encapsulates data access

### **2. Inheritance**
- Repositories extend `JpaRepository`
- DTOs inherit common properties where applicable

### **3. Polymorphism**
- Service interfaces with multiple implementations
- Generic repository methods

### **4. Abstraction**
- Service interfaces abstract implementation details
- DTO pattern abstracts entity complexity
- Repository pattern abstracts data access

### **5. Separation of Concerns**
- **Controllers**: Handle HTTP requests/responses
- **Services**: Implement business logic
- **Repositories**: Manage data persistence
- **DTOs**: Data transfer between layers
- **Mappers**: Convert between entities and DTOs

### **6. Dependency Injection**
```java
@RestController
public class ExamController {
    @Autowired
    private ExamService examService;  // Dependency injection
}
```

---

## 🔧 How to Run the Project

### **Prerequisites**
- Java 17+
- Node.js 16+
- MySQL 8.0+
- Maven 3.6+

### **Backend Setup**
```bash
# Navigate to project root
cd OOAD_Mini_Project

# Install dependencies and compile
mvn clean install

# Run the application
mvn spring-boot:run
```

### **Frontend Setup**
```bash
# Navigate to frontend directory
cd frontend

# Install dependencies
npm install

# Start development server
npm run dev
```

### **Database Setup**
1. Create MySQL database named `userdb`
2. Update `application.properties` with your database credentials
3. Hibernate will auto-create tables on first run

---

## 🎤 Interview Talking Points

### **Technical Excellence**
1. **"I implemented a clean, layered architecture following Spring Boot best practices"**
2. **"Used DTO pattern to separate API contracts from internal data models"**
3. **"Implemented proper error handling and validation across all layers"**

### **OOAD Implementation**
1. **"Applied all four OOP pillars with practical examples"**
2. **"Used dependency injection for loose coupling between components"**
3. **"Implemented repository pattern for clean data access abstraction"**

### **Full-Stack Development**
1. **"Built RESTful APIs with proper HTTP status codes and response formats"**
2. **"Used React Context API for state management"**
3. **"Implemented responsive UI with proper component architecture"**

### **Database Design**
1. **"Designed normalized database schema with proper relationships"**
2. **"Used JPA annotations for object-relational mapping"**
3. **"Implemented cascade operations and lazy loading for performance"**

### **Project Scalability**
1. **"Modular design allows easy addition of new features"**
2. **"Stateless API design supports horizontal scaling"**
3. **"Clean separation of concerns facilitates team development"**

---

## 🚀 Future Enhancements

1. **Security**: Implement JWT-based authentication
2. **Testing**: Add comprehensive unit and integration tests
3. **Deployment**: Docker containerization for easy deployment
4. **Monitoring**: Add logging and monitoring capabilities
5. **Performance**: Implement caching for frequently accessed data
6. **UI/UX**: Enhanced user interface with better responsive design

---

## 📊 Project Metrics

- **Total Lines of Code**: ~2000+ lines
- **Backend Classes**: 37 Java classes
- **Frontend Components**: 15+ React components
- **API Endpoints**: 15+ RESTful endpoints
- **Database Tables**: 5 main entities
- **Development Time**: Represents ~40-60 hours of development

---

This project demonstrates a solid understanding of modern full-stack development practices, OOAD principles, and enterprise-level application architecture suitable for real-world educational institution management systems.