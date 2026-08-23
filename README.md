# 🎟️ Event Management System

A full-stack web-based **Event Management System** designed to simplify event creation, registration, team management, attendance tracking, QR-based attendance verification, and certificate generation.

The application provides separate role-based functionality for **Admin, Organizer, and Student**, with a secure REST API backend and a responsive React frontend.

---

## 🚀 Live Application

🌐 **Frontend:** Add your deployed frontend URL here

🔗 **Backend API:** Add your backend URL here

📦 **GitHub Repository:**  
https://github.com/shanjaiy2006/Event-Management-System

---

## 📌 Project Overview

The Event Management System provides an end-to-end platform for managing the complete lifecycle of an event.

The system supports:

- 👤 User registration and login
- 🔐 JWT-based authentication
- 🛡️ Role-based access control
- 📅 Event creation and management
- 🔎 Event browsing and filtering
- 📝 Event registration
- 👥 Team creation and management
- 🔗 Team joining using team codes
- 📱 QR-code-based attendance
- ✅ Attendance verification
- 📄 Automated certificate generation
- 📧 Email notifications
- 📊 Admin management and analytics
- ⚡ Application-level caching
- 🗄️ Relational database management

---

# 🏗️ System Architecture

```text
                         ┌──────────────────────┐
                         │       Users          │
                         │ Admin / Organizer    │
                         │      / Student       │
                         └──────────┬───────────┘
                                    │
                                    ▼
                         ┌──────────────────────┐
                         │    React Frontend    │
                         │                      │
                         │ React.js             │
                         │ React Router         │
                         │ Axios                │
                         │ Responsive UI        │
                         └──────────┬───────────┘
                                    │
                              REST API / HTTP
                                    │
                                    ▼
                    ┌────────────────────────────────┐
                    │       Spring Boot Backend      │
                    │                                │
                    │ ┌────────────────────────────┐ │
                    │ │ Controller Layer            │ │
                    │ │ REST APIs                   │ │
                    │ └──────────────┬─────────────┘ │
                    │                ▼               │
                    │ ┌────────────────────────────┐ │
                    │ │ Service Layer               │ │
                    │ │ Business Logic              │ │
                    │ └──────────────┬─────────────┘ │
                    │                ▼               │
                    │ ┌────────────────────────────┐ │
                    │ │ Repository Layer            │ │
                    │ │ Spring Data JPA             │ │
                    │ └──────────────┬─────────────┘ │
                    │                ▼               │
                    │ ┌────────────────────────────┐ │
