# Quick Reference - Technical Concepts for Interview

## 🏗️ Design Patterns Used

### **1. Model-View-Controller (MVC)**
- **Model**: Entity classes (Student, Exam, Registration, Payment)
- **View**: React components and pages
- **Controller**: REST controllers handling HTTP requests

### **2. Data Transfer Object (DTO)**
```java
// Separates API contract from internal entity structure
public class ExamDTO {
    private int examId;
    private String courseName;
    // ... only fields needed by frontend
}
```

### **3. Repository Pattern**
```java
@Repository
public interface ExamRepository extends JpaRepository<Exam, Integer> {
    List<Exam> findByBranchAndSemester(String branch, int semester);
}
```

### **4. Service Layer Pattern**
```java
@Service
public class ExamService {
    @Autowired
    private ExamRepository examRepository;
    
    public List<Exam> getAllExams() {
        return examRepository.findAll();
    }
}
```

### **5. Mapper Pattern**
```java
public class ExamMapper {
    public static ExamDTO toDTO(Exam exam) {
        // Convert entity to DTO
    }
    
    public static Exam toEntity(ExamDTO dto) {
        // Convert DTO to entity
    }
}
```

---

## 📊 Database Relationships

### **Entity Relationship Summary**
```
Student (1) ──── (N) Registration (N) ──── (1) Exam
                       │
                      (1)
                       │
                   Payment (1)
```

### **Key Annotations**
- `@OneToMany`: Student → Registrations, Exam → Registrations
- `@ManyToOne`: Registration → Student, Registration → Exam  
- `@OneToOne`: Registration → Payment
- `@JoinColumn`: Defines foreign key columns

---

## 🔄 Request Flow

```
React Component → Axios → REST Controller → Service → Repository → Database
                                ↓
                            DTO Mapping
                                ↓
                        JSON Response ← ← ← ← ← ← ← ← ← ← ← ← ← ←
```

---

## 🛠️ Key Annotations Explained

### **Spring Boot Annotations**
- `@SpringBootApplication`: Main application class
- `@RestController`: REST endpoint controller
- `@Service`: Business logic service
- `@Repository`: Data access layer
- `@Autowired`: Dependency injection
- `@CrossOrigin`: CORS configuration

### **JPA Annotations**
- `@Entity`: Database table mapping
- `@Id`: Primary key
- `@GeneratedValue`: Auto-increment ID
- `@OneToMany`, `@ManyToOne`, `@OneToOne`: Relationships
- `@JoinColumn`: Foreign key definition

### **HTTP Mapping**
- `@GetMapping`: HTTP GET requests
- `@PostMapping`: HTTP POST requests
- `@DeleteMapping`: HTTP DELETE requests
- `@PathVariable`: URL parameter extraction
- `@RequestBody`: JSON request body mapping

---

## 🗃️ Database Schema

### **Student Table**
```sql
CREATE TABLE student (
    student_id VARCHAR(255) PRIMARY KEY,
    name VARCHAR(255),
    email VARCHAR(255),
    branch VARCHAR(255),
    semester INT,
    password VARCHAR(255),
    is_blocked BOOLEAN DEFAULT FALSE
);
```

### **Exam Table**
```sql
CREATE TABLE exam (
    exam_id INT AUTO_INCREMENT PRIMARY KEY,
    course_code VARCHAR(255),
    course_name VARCHAR(255),
    exam_date DATE,
    start_time TIME,
    end_time TIME,
    total_marks INT,
    semester INT,
    branch VARCHAR(255),
    prerequisites VARCHAR(255)
);
```

### **Registration Table**
```sql
CREATE TABLE registration (
    registration_id INT AUTO_INCREMENT PRIMARY KEY,
    student_id VARCHAR(255),
    exam_id INT,
    status VARCHAR(255),
    attempts INT,
    registration_date TIMESTAMP,
    FOREIGN KEY (student_id) REFERENCES student(student_id),
    FOREIGN KEY (exam_id) REFERENCES exam(exam_id)
);
```

---

## 🔧 Configuration Files

### **application.properties**
```properties
spring.application.name=demo
spring.datasource.url=jdbc:mysql://localhost:3306/userdb
spring.datasource.username=root
spring.datasource.password=yourpassword
spring.jpa.hibernate.ddl-auto=update
spring.jpa.show-sql=true
```

### **pom.xml Dependencies**
```xml
<dependencies>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-data-jpa</artifactId>
    </dependency>
    <dependency>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-web</artifactId>
    </dependency>
    <dependency>
        <groupId>com.mysql</groupId>
        <artifactId>mysql-connector-j</artifactId>
    </dependency>
</dependencies>
```

---

## 🎯 OOAD Principles Implementation

### **Encapsulation**
```java
public class Student {
    private String studentId;  // Private fields
    
    public String getStudentId() {  // Public accessors
        return studentId;
    }
    
    public void setStudentId(String studentId) {
        this.studentId = studentId;
    }
}
```

### **Inheritance**
```java
// Repository inheritance
public interface ExamRepository extends JpaRepository<Exam, Integer> {
    // Inherits CRUD operations from JpaRepository
}
```

### **Abstraction**
```java
// Service interface abstracts implementation
public interface ExamService {
    List<Exam> getAllExams();
    Optional<Exam> getExamById(int id);
}
```

### **Polymorphism**
```java
// Different implementations of same interface
JpaRepository<Exam, Integer> repo = examRepository;
repo.findAll();  // Calls appropriate implementation
```

---

## 🚀 API Endpoints Quick Reference

| Method | Endpoint | Purpose |
|--------|----------|---------|
| GET | `/exams` | Get all exams |
| GET | `/exams/{id}` | Get exam by ID |
| POST | `/exams/add` | Create new exam |
| DELETE | `/exams/{id}` | Delete exam |
| GET | `/students` | Get all students |
| POST | `/students/register` | Register student |
| POST | `/students/login` | Student login |
| POST | `/registrations/register` | Register for exam |
| GET | `/registrations/student/{email}` | Get student registrations |
| POST | `/payments/process` | Process payment |

---

## 🔍 Testing Commands

### **Backend Testing**
```bash
# Build project
mvn clean compile

# Run tests
mvn test

# Start application
mvn spring-boot:run
```

### **Frontend Testing**
```bash
# Install dependencies
npm install

# Start development server
npm run dev

# Build for production
npm run build
```

### **API Testing**
```bash
# Test GET endpoint
curl http://localhost:8080/exams

# Test POST endpoint
curl -X POST http://localhost:8080/exams/add \
     -H "Content-Type: application/json" \
     -d '{"courseName":"Test","examDate":"2024-12-01"}'
```

---

## 💡 Interview Tips

### **When discussing architecture:**
- Emphasize separation of concerns
- Mention scalability considerations
- Highlight error handling approaches

### **When showing code:**
- Explain naming conventions
- Point out design pattern usage
- Demonstrate understanding of frameworks

### **When discussing database:**
- Explain relationship choices
- Mention data integrity measures
- Discuss performance considerations

### **Common follow-up questions:**
- "How would you add authentication?"
- "How would you handle concurrent users?"
- "What about data validation?"
- "How would you deploy this?"