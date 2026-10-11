# 🚗 Smart Parking Reservation System

A complete, full-stack **Smart Parking Reservation System** built for technical training demonstrations. It allows users to view real-time parking slot availability, reserve parking spots, track booking history, and provides admins with a complete dashboard to manage slots and reservations.

---

## 🌟 Key Features

1. **Visual Parking Grid**: Displays all parking slots visually grouped by floor and type (Regular, EV Charging, Compact, SUV, Disabled).
2. **Real-Time Slot Status**: Live visual indicators for slot status:
   - 🟢 **AVAILABLE**: Green badge, ready for booking.
   - 🟡 **RESERVED**: Yellow badge, booked by a user.
   - 🔴 **OCCUPIED**: Red badge, vehicle currently parked.
3. **User Authentication & Authorization**:
   - Registration and Login for **USER** and **ADMIN** roles.
   - Quick Demo Login buttons for instant presentation.
4. **Slot Reservation**:
   - Select available parking slot, enter vehicle license plate number, select start & end times.
   - Automatic duration and price calculation.
5. **Booking History**: Users can view their active and past reservations and cancel upcoming bookings.
6. **Admin Dashboard**:
   - Live revenue and slot utilization statistics.
   - Add new parking slots (Slot Number, Floor, Type, Price).
   - Change slot statuses directly (AVAILABLE / RESERVED / OCCUPIED).
   - Manage all customer reservations (Mark as CONFIRMED, OCCUPIED, COMPLETED, or CANCELLED).
7. **Form Validation & Alerts**: Client-side and server-side validation with clean success and error notifications.

---

## 🛠️ Technology Stack

- **Backend**:
  - Java 17
  - Spring Boot 3.2.5 (REST API)
  - Spring Data JPA & Hibernate
  - MySQL Database
  - Maven
- **Frontend**:
  - React.js (Vite)
  - React Router DOM v6
  - Axios (HTTP Client)
  - Lucide React (Modern Icons)
  - Vanilla CSS3 (Custom Glassmorphism Design System)

---

## 📂 Project Structure

```
Smart-Parking-Reservation-System/
├── backend/
│   ├── pom.xml
│   └── src/
│       ├── main/
│       │   ├── java/com/parking/system/
│       │   │   ├── SmartParkingApplication.java
│       │   │   ├── config/ (WebConfig CORS, DataInitializer)
│       │   │   ├── controller/ (AuthController, ParkingSlotController, ReservationController, AdminController)
│       │   │   ├── dto/ (RegisterRequest, LoginRequest, AuthResponse, ReservationRequest, etc.)
│       │   │   ├── exception/ (GlobalExceptionHandler, CustomExceptions)
│       │   │   ├── model/ (User, ParkingSlot, Reservation, Enums)
│       │   │   ├── repository/ (UserRepository, ParkingSlotRepository, ReservationRepository)
│       │   │   └── service/ (AuthService, ParkingSlotService, ReservationService)
│       │   └── resources/
│       │       └── application.properties
│       └── test/
└── frontend/
    ├── package.json
    ├── vite.config.js
    ├── index.html
    └── src/
        ├── App.jsx
        ├── main.jsx
        ├── index.css
        ├── api/ (axios, authApi, slotApi, reservationApi, adminApi)
        ├── components/ (Navbar, Footer, ProtectedRoute, SlotCard, StatusBadge)
        ├── context/ (AuthContext.jsx)
        └── pages/ (ParkingGrid, Login, Register, ReserveSlot, MyReservations, AdminDashboard)
```

---

## 🔑 Demo Login Credentials

The application automatically seeds sample users and parking slots on initial startup:

| Role | Email | Password | Access Level |
| :--- | :--- | :--- | :--- |
| **Admin** | `admin@parking.com` | `admin123` | Full Admin Panel, Slot & Booking Management |
| **User** | `user@parking.com` | `user123` | Reserve Slots, View Booking History |

---

## 🚀 Step-by-Step Setup & Execution Instructions

### Prerequisites
- **Java 17 JDK** installed (`java -version`)
- **Maven** installed (`mvn -v`)
- **Node.js** (v18+) and **npm** installed (`node -v`, `npm -v`)
- **MySQL Server** running on `localhost:3306`

---

### Step 1: Database Setup (MySQL)

1. Start your MySQL Server (via MySQL Workbench, XAMPP, or Windows Service).
2. Ensure MySQL is running on port `3306`.
3. Spring Boot will **automatically create** the database (`smart_parking_db`) and tables on launch.
4. *(Optional)* If your MySQL username or password differs from `root`/`root`, open `backend/src/main/resources/application.properties` and update:
   ```properties
   spring.datasource.username=YOUR_MYSQL_USERNAME
   spring.datasource.password=YOUR_MYSQL_PASSWORD
   ```

> 💡 **Note for offline/H2 testing**: If MySQL is unavailable, you can uncomment the H2 configuration lines in `backend/src/main/resources/application.properties` to run with an in-memory H2 database instantly.

---

### Step 2: Start the Backend (Spring Boot)

1. Open terminal and navigate to the `backend` directory:
   ```bash
   cd backend
   ```
2. Build and compile the backend:
   ```bash
   mvn compile
   ```
3. Run the Spring Boot application:
   ```bash
   mvn spring-boot:run
   ```
4. The backend API will start at: `http://localhost:8080`

---

### Step 3: Start the Frontend (React.js)

1. Open a second terminal and navigate to the `frontend` directory:
   ```bash
   cd frontend
   ```
2. Install npm dependencies (if not already installed):
   ```bash
   npm install
   ```
3. Launch the React dev server:
   ```bash
   npm run dev
   ```
4. Open your web browser and visit: `http://localhost:5173`

---

## 📡 REST API Reference Endpoints

### Authentication API (`/api/auth`)
- `POST /api/auth/register` - Register new user
- `POST /api/auth/login` - Authenticate user & return role/profile

### Parking Slots API (`/api/slots`)
- `GET /api/slots` - Get all parking slots (supports `?floor=...` & `?status=...`)
- `GET /api/slots/{id}` - Get slot by ID
- `POST /api/slots` - Admin: Add new parking slot
- `PUT /api/slots/{id}` - Admin: Update parking slot details
- `PUT /api/slots/{id}/status?status=...` - Update slot status
- `DELETE /api/slots/{id}` - Admin: Delete parking slot

### Reservations API (`/api/reservations`)
- `POST /api/reservations` - Create a slot reservation
- `GET /api/reservations` - Admin: Get all reservations
- `GET /api/reservations/user/{userId}` - Get user booking history
- `PUT /api/reservations/{id}/cancel` - Cancel a reservation
- `PUT /api/reservations/{id}/status?status=...` - Admin: Update reservation status

### Admin Analytics API (`/api/admin`)
- `GET /api/admin/stats` - Fetch total slots, available, reserved, occupied counts, and total revenue

---

## 🧪 Testing the Project Workflow

1. Open `http://localhost:5173` in your browser.
2. View the visual **Parking Grid** displaying Ground Floor and 1st Floor slots (`A-101`, `A-102`, `B-201`, etc.).
3. Click **Login** and use the **Quick Demo User** button or type `user@parking.com` / `user123`.
4. Click **Reserve Now** on any **AVAILABLE** slot (e.g. `A-101`).
5. Fill in the Vehicle License Plate Number (e.g. `KA-05-EV-9999`) and select your start/end times. Review the calculated total price and click **Confirm Reservation**.
6. You will be redirected to **My Bookings** showing your newly confirmed reservation.
7. Log out and log in as **Admin** (`admin@parking.com` / `admin123`).
8. Navigate to **Admin Panel** to observe real-time stats, add a new parking slot, or change reservation statuses!

---
*Created for Technical Training Project Presentation.*
