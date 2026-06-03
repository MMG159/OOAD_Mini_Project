# Exam Management System (OOAD Mini Project)

A full-stack web application for managing student exam registration and administration.

## Tech Stack

### Backend
- Java 24
- Spring Boot 3.4.4
- Spring Web
- Spring Data JPA
- MySQL
- Maven Wrapper (`mvnw`)

### Frontend
- React 19
- Vite
- React Router
- Axios
- ESLint

## Features

- Student registration and login
- Student dashboard/home view
- Student exam registration
- Repeater payment flow during registration
- Admin login
- Admin exam management (add/list/delete)
- Admin views:
  - all students
  - all exams
  - exam-wise registered students

## Repository Structure

```text
OOAD_Mini_Project/
├── pom.xml
├── mvnw / mvnw.cmd
├── src/
│   ├── main/
│   │   ├── java/com/ooad/demo/
│   │   │   ├── config/
│   │   │   ├── controller/
│   │   │   ├── dto/
│   │   │   ├── mapper/
│   │   │   ├── model/
│   │   │   ├── repository/
│   │   │   ├── service/
│   │   │   └── DemoApplication.java
│   │   └── resources/
│   │       └── application.properties
│   └── test/java/com/ooad/demo/
│       └── DemoApplicationTests.java
└── frontend/
    ├── package.json
    ├── index.html
    └── src/
        ├── components/
        ├── context/
        ├── pages/
        ├── services/
        ├── App.jsx
        └── main.jsx
```

## Prerequisites

- Java 24
- MySQL server
- Node.js + npm

## Configuration

Backend config file: `src/main/resources/application.properties`

Current default DB settings:
- URL: `jdbc:mysql://localhost:3306/userdb`
- Username: `root`
- Password: configured directly in file

CORS is configured for frontend origin:
- `http://localhost:5173`

## Run Locally

### 1) Start MySQL and create database

```sql
CREATE DATABASE userdb;
```

### 2) Run backend

```bash
cd /tmp/workspace/MMG159/OOAD_Mini_Project
./mvnw spring-boot:run
```

### 3) Run frontend

```bash
cd /tmp/workspace/MMG159/OOAD_Mini_Project/frontend
npm install
npm run dev
```

## Build and Test

### Backend
```bash
cd /tmp/workspace/MMG159/OOAD_Mini_Project
./mvnw test
./mvnw package
```

### Frontend
```bash
cd /tmp/workspace/MMG159/OOAD_Mini_Project/frontend
npm run lint
npm run build
```

## Main API Areas

- `/students` — student registration/login/info
- `/admin` — admin login and admin views
- `/exams` — exam CRUD/listing
- `/registrations` — exam registration
- `/payments` — payment processing

## Notes / Known Gaps

- No admin sign-up endpoint exists; admin records must exist in DB.
- Minimal automated tests currently (backend context-load test only).
- Frontend and backend base URLs are hardcoded to localhost.
- Post-payment navigation route currently points to `/student/registration` while router defines `/student/register`.
