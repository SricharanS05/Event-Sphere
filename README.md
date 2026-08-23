# Event Management System

A full-stack web application for organizing and managing events — registrations, teams, attendance (including QR-based check-in), certificate generation, and organizer dashboards. Intended for event organizers and participants to streamline event workflows and communications.

## Features
- User authentication and profile management
- Event creation, editing, listing and detailed views
- Participant registration and team management
- Attendance tracking (including QR code based check-in)
- Certificate generation and download
- Email notifications (invitations/confirmations/certificates)
- File uploads (images/assets) — Cloudinary integration present
- Admin/organizer dashboard with metrics and reports

## Tech stack
- Language: Java (Spring ecosystem) for backend
- Framework / build: Spring Boot (Maven) — wrapper scripts included (`mvnw`, `mvnw.cmd`, `pom.xml`)
- Frontend: present in `event-management-frontend` (see that directory for exact stack and commands)
- Notable backend components (based on source layout):
  - Spring Web (REST controllers)
  - Spring Data JPA (repositories / entities)
  - Spring Security (authentication)
  - Email sending service (JavaMail / SMTP)
  - Cloudinary integration for uploads
  - QR code generation service

## Repo layout
Top-level:
```
event-management-backend/        Backend: Spring Boot application (Maven)
  pom.xml
  mvnw, mvnw.cmd
  src/
    main/java/com/event/event_management/
      controller/     HTTP controllers (AuthController, EventController, RegistrationController, AttendanceController, CertificateController, QrController, TeamController, ProfileController, DashboardController, ...)
      service/        Business logic (EventService, RegistrationService, AttendanceService, QrCodeService, CloudinaryService, EmailService, ...)
      repository/     Spring Data repositories
      entity/         JPA entities (Event, Registration, Attendance, User, Team, Role, ...)
      dto/            Data Transfer Objects
      config/         App configuration
      security/       Security configuration and JWT handling
    resources/        (application properties, static resources — check this folder)
  uploads/            local uploads folder (used at runtime)
  logs/                runtime logs (tracked here)

event-management-frontend/     Frontend client (see its README for exact stack & commands)
logs/                         Root-level logs directory
.idea/ .vscode/               Editor configs (ignore)
```

How it fits together:
- The frontend interacts with the backend REST API endpoints implemented by controllers under `controller/`. Controllers call `service/` classes for business logic. `repository/` classes persist `entity/` objects to the database via Spring Data JPA. Supporting services handle email, file uploads (Cloudinary), QR code generation and certificate creation. Security and authentication are configured under `security/`.

## How to run it
The shortest path from a fresh clone to a running process or passing tests.

Backend (shortest path)
1. Configure environment variables / application properties (see below).
2. From repository root:
   - Linux/macOS:
     ```
     cd event-management-backend
     ./mvnw clean package
     ./mvnw spring-boot:run
     ```
   - Windows (PowerShell/CMD):
     ```
     cd event-management-backend
     mvnw.cmd clean package
     mvnw.cmd spring-boot:run
     ```
3. The backend will start on the configured port (default commonly 8080 unless overridden). Check logs in `event-management-backend/logs/` or top-level `logs/`.

Frontend (typical steps — confirm in event-management-frontend/README):
```
cd event-management-frontend
npm install
npm start               # or `npm run dev` / `yarn start` depending on setup
```
Adjust commands if the frontend uses a different toolchain (Angular/React/Vue).

## Required configuration / environment variables
The backend expects standard Spring Boot configuration. Commonly required values include:
- Database:
  - SPRING_DATASOURCE_URL (jdbc URL)
  - SPRING_DATASOURCE_USERNAME
  - SPRING_DATASOURCE_PASSWORD
- Security:
  - JWT_SECRET (if JWT is used)
  - JWT_EXPIRATION_MS (optional)
- Cloudinary (for image uploads):
  - CLOUDINARY_URL or CLOUDINARY_CLOUD_NAME, CLOUDINARY_API_KEY, CLOUDINARY_API_SECRET
- Email (SMTP) for EmailService:
  - SPRING_MAIL_HOST (or EMAIL_HOST)
  - SPRING_MAIL_PORT
  - SPRING_MAIL_USERNAME
  - SPRING_MAIL_PASSWORD
  - SPRING_MAIL_PROPERTIES_MAIL_SMTP_AUTH / TLS settings
- Other:
  - FILE_UPLOAD_DIR (if local uploads used)
  - SERVER_PORT (optional to override default)

Check `src/main/resources/application.properties` or `application.yml` inside `event-management-backend` for exact property keys.

## Notable endpoints (example resource routes)
(Controller names available in code; confirm exact paths and request bodies in controllers)
- POST /api/auth/login, POST /api/auth/register
- GET /api/events, POST /api/events, GET /api/events/{id}, PUT /api/events/{id}, DELETE /api/events/{id}
- POST /api/registrations, GET /api/registrations (by user/event)
- POST /api/attendance/qr-checkin, POST /api/attendance/manual
- GET /api/teams, POST /api/teams
- GET /api/profile, PUT /api/profile
- GET /api/certificates/{registrationId} (generate/download)

## Database model (core entities)
- Event
- Registration
- Attendance
- User
- Team
- Role
(Inspect `event-management-backend/src/main/java/com/event/event_management/entity/` for fields and relationships.)

## Testing
- The backend has `src/test/` — run tests with:
  ```
  cd event-management-backend
  ./mvnw test
  ```
- Frontend testing commands depend on the frontend stack.

## Development notes
- There are services for Cloudinary and Email; to test locally you can stub/mock these or provide real credentials.
- QR code generation and certificate creation are implemented server-side — verify dependencies if you add or modify code.
- Logs are written to `event-management-backend/logs` and a top-level `logs/` directory.

## Contributing
- Fork, create a feature branch, run tests, and open a PR with a clear description.
- Add/update API documentation if you modify endpoints or request/response shapes.

## License
No license file detected in the repository. Add a LICENSE (for example, MIT) to make usage terms explicit.

## Contact
Repository owner: SricharanS05 (https://github.com/SricharanS05)
