# ServiceHub-booking-platform
Java full stack project 
# ServiceHub Handyman Booking Platform

ServiceHub is a full-stack home service booking application for browsing services, booking slots, managing carts and payments, approving service providers, and administering services, users, slots, and bookings.

## Tech Stack

**Frontend**

- React 18
- Vite
- Tailwind CSS
- React Router DOM
- Axios
- Framer Motion
- Lucide React

**Backend**

- Java 17
- Spring Boot 3
- Spring Web
- Spring Data JPA
- Spring Security
- JWT authentication
- Maven
- Razorpay Java SDK

**Database**

- MySQL
- SQL migration and seed scripts in the `database/` folder

## Project Structure

```text
HomeService/
+-- frontend/
|   +-- public/
|   +-- src/
|   |   +-- components/
|   |   +-- hooks/
|   |   +-- pages/
|   |   +-- services/
|   |   +-- App.jsx
|   |   +-- main.jsx
|   |   +-- index.css
|   +-- .env
|   +-- .env.example
|   +-- index.html
|   +-- package.json
|   +-- postcss.config.js
|   +-- tailwind.config.js
|   +-- vite.config.js
|
+-- backend/
|   +-- src/
|   |   +-- main/
|   |       +-- java/com/homeservice/handyman/
|   |       |   +-- config/
|   |       |   +-- controller/
|   |       |   +-- dto/
|   |       |   +-- entity/
|   |       |   +-- exception/
|   |       |   +-- repository/
|   |       |   +-- security/
|   |       |   +-- service/
|   |       |   +-- HandymanApplication.java
|   |       +-- resources/
|   |           +-- application.properties
|   |           +-- schema.sql
|   |           +-- data.sql
|   +-- uploads/
|   +-- pom.xml
|
+-- database/
|   +-- schema.sql
|   +-- sample-data.sql
|   +-- booking-contact-migration.sql
|   +-- offline-payment-migration.sql
|   +-- provider-registration-migration.sql
|
+-- .gitignore
+-- README.md
```

## Frontend Setup

Open a terminal in the project root and run:

```bash
cd frontend
npm install
npm run dev
```

Frontend URL:

```text
http://localhost:5173
```

Frontend environment variable:

```text
VITE_API_BASE_URL=http://localhost:8081/api
```

If needed, update `frontend/.env` to use the backend port `8081`.

## Backend Setup

Make sure MySQL is running, then update the database settings in:

```text
backend/src/main/resources/application.properties
```

Default backend configuration:

```properties
server.port=8081
spring.datasource.url=jdbc:mysql://localhost:3306/handyman?useSSL=false&allowPublicKeyRetrieval=true&serverTimezone=UTC
spring.datasource.username=root
spring.datasource.password=
```

Run the Spring Boot API:

```bash
cd backend
mvn spring-boot:run
```

Backend URL:

```text
http://localhost:8081
```

API base URL:

```text
http://localhost:8081/api
```

## Database Setup

Create and seed the MySQL database from the project root:

```bash
mysql -u root -p < database/schema.sql
mysql -u root -p handyman < database/sample-data.sql
```

Additional migration files are available in `database/`:

```text
booking-contact-migration.sql
offline-payment-migration.sql
provider-registration-migration.sql
```

Run them only when the matching feature columns/tables are missing from your local database.

## Admin Login

Use this admin account for the admin dashboard:

```text
Email: admin@ServiceHub.com
Password: admin123
```

Admin dashboard:

```text
http://localhost:5173/admin
```

If the admin user is not already present in your database, create/register a user with role `ADMIN` using the backend auth flow or insert an admin user directly in MySQL.

## Useful Routes

```text
Frontend home:       http://localhost:5173
Admin dashboard:     http://localhost:5173/admin
Provider dashboard:  http://localhost:5173/provider
User dashboard:      http://localhost:5173/dashboard
Backend API:         http://localhost:8081/api
```

## Core API Endpoints

```text
POST /api/auth/register
POST /api/auth/login
GET  /api/services
GET  /api/services?location=Mumbai
GET  /api/slots/{serviceId}
POST /api/bookings
GET  /api/bookings/user/{id}
GET  /api/admin/services
GET  /api/admin/bookings
GET  /api/admin/users
GET  /api/admin/providers/pending
```

Authenticated requests must include:

```text
Authorization: Bearer <jwt>
```

## Sample Booking Payload

```json
{
  "userId": 1,
  "serviceId": 1,
  "slotId": 1
}
```

## Notes

- Frontend runs on `http://localhost:5173`.
- Backend runs on `http://localhost:8081`.
- The backend allows CORS from `http://localhost:5173` and `http://localhost:5174`.
- Uploaded provider photos and service images are stored in `backend/uploads/`.
