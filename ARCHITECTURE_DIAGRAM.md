# System Architecture Diagram

```
┌─────────────────────────────────────────────────────────────────────────┐
│                           EXAM MANAGEMENT SYSTEM                        │
│                              ARCHITECTURE                               │
└─────────────────────────────────────────────────────────────────────────┘

┌─────────────────────────────────────────────────────────────────────────┐
│                          PRESENTATION LAYER                             │
│                               (React)                                   │
├─────────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │   Student   │  │    Admin    │  │    Exam     │  │   Payment   │     │
│  │ Components  │  │ Components  │  │ Components  │  │ Components  │     │
│  │             │  │             │  │             │  │             │     │
│  │ • Login     │  │ • Dashboard │  │ • View List │  │ • Process   │     │
│  │ • Register  │  │ • Exam Mgmt │  │ • Register  │  │ • History   │     │
│  │ • Dashboard │  │ • Students  │  │ • Schedule  │  │ • Status    │     │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                               HTTP REST API
                              (Axios Requests)
                                    │
┌─────────────────────────────────────────────────────────────────────────┐
│                            API GATEWAY LAYER                            │
│                            (Spring Boot)                                │
├─────────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │   Student   │  │    Admin    │  │    Exam     │  │   Payment   │     │
│  │ Controller  │  │ Controller  │  │ Controller  │  │ Controller  │     │
│  │             │  │             │  │             │  │             │     │
│  │ @RestCtrl   │  │ @RestCtrl   │  │ @RestCtrl   │  │ @RestCtrl   │     │
│  │ @CrossOrg   │  │ @CrossOrg   │  │ @CrossOrg   │  │ @CrossOrg   │     │
│  │ @RequestM   │  │ @RequestM   │  │ @RequestM   │  │ @RequestM   │     │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                               Dependency Injection
                                (@Autowired)
                                    │
┌─────────────────────────────────────────────────────────────────────────┐
│                          BUSINESS LOGIC LAYER                           │
│                              (Services)                                 │
├─────────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │   Student   │  │    Admin    │  │    Exam     │  │   Payment   │     │
│  │   Service   │  │   Service   │  │   Service   │  │   Service   │     │
│  │             │  │             │  │             │  │             │     │
│  │ @Service    │  │ @Service    │  │ @Service    │  │ @Service    │     │
│  │ • Business  │  │ • Business  │  │ • Business  │  │ • Business  │     │
│  │   Logic     │  │   Logic     │  │   Logic     │  │   Logic     │     │
│  │ • Validation│  │ • Validation│  │ • Validation│  │ • Validation│     │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                               JPA Repository
                                 Interface
                                    │
┌─────────────────────────────────────────────────────────────────────────┐
│                          DATA ACCESS LAYER                              │
│                             (Repositories)                              │
├─────────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │   Student   │  │    Admin    │  │    Exam     │  │   Payment   │     │
│  │ Repository  │  │ Repository  │  │ Repository  │  │ Repository  │     │
│  │             │  │             │  │             │  │             │     │
│  │@Repository  │  │@Repository  │  │@Repository  │  │@Repository  │     │
│  │extends JPA  │  │extends JPA  │  │extends JPA  │  │extends JPA  │     │
│  │Repository   │  │Repository   │  │Repository   │  │Repository   │     │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘     │
└─────────────────────────────────────────────────────────────────────────┘
                                    │
                               Hibernate ORM
                                JPA Mapping
                                    │
┌─────────────────────────────────────────────────────────────────────────┐
│                            DATABASE LAYER                               │
│                               (MySQL)                                   │
├─────────────────────────────────────────────────────────────────────────┤
│  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐  ┌─────────────┐     │
│  │   student   │  │    admin    │  │    exam     │  │   payment   │     │
│  │   table     │  │   table     │  │   table     │  │   table     │     │
│  │             │  │             │  │             │  │             │     │
│  │ student_id  │  │ admin_id    │  │ exam_id     │  │ payment_id  │     │
│  │ name        │  │ name        │  │ course_code │  │ amount      │     │
│  │ email       │  │ email       │  │ course_name │  │ payment_st  │     │
│  │ branch      │  │ password    │  │ exam_date   │  │ payment_dt  │     │
│  │ semester    │  │             │  │ start_time  │  │             │     │
│  │ password    │  │             │  │ end_time    │  │             │     │
│  │ is_blocked  │  │             │  │ total_marks │  │             │     │
│  └─────────────┘  └─────────────┘  └─────────────┘  └─────────────┘     │
│                                                                         │
│                        ┌─────────────────────┐                         │
│                        │    registration     │                         │
│                        │       table         │                         │
│                        │                     │                         │
│                        │ registration_id     │                         │
│                        │ student_id (FK)     │                         │
│                        │ exam_id (FK)        │                         │
│                        │ status              │                         │
│                        │ attempts            │                         │
│                        │ registration_date   │                         │
│                        └─────────────────────┘                         │
└─────────────────────────────────────────────────────────────────────────┘

DATA FLOW:
┌─────────┐    HTTP     ┌────────────┐    @Autowired    ┌─────────┐
│ React   │ ────────── │ Controller │ ───────────────  │ Service │
│ Frontend│    Request  │  (@Rest)   │                  │(@Service│
└─────────┘             └────────────┘                  └─────────┘
                                                             │
                                                        JPA Interface
                                                             │
                                               ┌─────────────▼──────────────┐
                                               │    Repository Interface    │
                                               │    (extends JpaRepository) │
                                               └─────────────┬──────────────┘
                                                             │
                                                        Hibernate ORM
                                                             │
                                                        ┌────▼─────┐
                                                        │  MySQL   │
                                                        │ Database │
                                                        └──────────┘

ENTITY RELATIONSHIPS:
Student ────── (1:N) ────── Registration ────── (N:1) ────── Exam
                                   │
                                (1:1)
                                   │
                               Payment

KEY PATTERNS USED:
• MVC (Model-View-Controller)
• Repository Pattern
• Data Transfer Object (DTO)
• Service Layer Pattern
• Dependency Injection
• RESTful API Design