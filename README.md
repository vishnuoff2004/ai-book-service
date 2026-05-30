# BookEase – Full-Stack Booking Services Web Application

## 🗂️ Project Structure

```
booking-app/
├── backend/          → Node.js + Express + MySQL API
└── frontend/         → React + Vite + Tailwind CSS
```

## ⚙️ Prerequisites

- **Node.js** v18+
- **MySQL** running locally
- **npm**

---

## 🚀 Backend Setup

### 1. Configure MySQL Database

Create the database in MySQL:
```sql
CREATE DATABASE booking_db;
```

### 2. Configure Environment Variables

Edit `backend/.env`:
```env
PORT=5000
DB_HOST=localhost
DB_PORT=3306
DB_USER=root
DB_PASSWORD=yourpassword      ← change this
DB_NAME=booking_db
JWT_SECRET=your_super_secret_jwt_key_change_this_in_production
JWT_EXPIRES_IN=7d
NODE_ENV=development
```

### 3. Install Dependencies

```bash
cd backend
npm install
```

### 4. Run Migrations

```bash
npx sequelize-cli db:migrate
```

### 5. Seed Initial Data

```bash
npx sequelize-cli db:seed:all
```

This seeds:
- Admin user: `admin@booking.com` / `admin123`
- 6 sample services (Cleaning, Plumbing, Electrical, AC, Pest Control, Painting)
- 7 sample providers

### 6. Start Backend

```bash
npm run dev
```

Backend runs at: **http://localhost:5000**

---

## 🎨 Frontend Setup

### 1. Configure Environment (optional)

`frontend/.env` already points to `http://localhost:5000/api`

### 2. Install Dependencies

```bash
cd frontend
npm install
```

### 3. Start Frontend

```bash
npm run dev
```

Frontend runs at: **http://localhost:5173**

---

## 🔑 Demo Login Credentials

| Role  | Email                | Password  |
|-------|----------------------|-----------|
| Admin | admin@booking.com    | admin123  |
| User  | Register a new account | —       |

---

## 📡 API Endpoints

### Auth
| Method | Endpoint            | Description         | Auth     |
|--------|---------------------|---------------------|----------|
| POST   | /api/auth/register  | Register user       | Public   |
| POST   | /api/auth/login     | Login               | Public   |
| GET    | /api/auth/me        | Get current user    | 🔒 JWT  |

### Services
| Method | Endpoint            | Description         | Auth          |
|--------|---------------------|---------------------|---------------|
| GET    | /api/services       | List with search    | Public        |
| GET    | /api/services/:id   | Get service         | Public        |
| POST   | /api/services       | Create service      | 🔒 Admin     |
| PUT    | /api/services/:id   | Update service      | 🔒 Admin     |
| DELETE | /api/services/:id   | Delete service      | 🔒 Admin     |

### Providers
| Method | Endpoint             | Description         | Auth          |
|--------|----------------------|---------------------|---------------|
| GET    | /api/providers       | List with filters   | 🔒 JWT       |
| GET    | /api/providers/:id   | Get provider        | 🔒 JWT       |
| POST   | /api/providers       | Create provider     | 🔒 Admin     |
| PUT    | /api/providers/:id   | Update provider     | 🔒 Admin     |
| DELETE | /api/providers/:id   | Delete provider     | 🔒 Admin     |

### Bookings (User)
| Method | Endpoint              | Description          | Auth          |
|--------|-----------------------|----------------------|---------------|
| POST   | /api/bookings         | Create booking       | 🔒 User      |
| GET    | /api/bookings/my      | My bookings          | 🔒 JWT       |
| GET    | /api/bookings/stats   | My dashboard stats   | 🔒 User      |
| GET    | /api/bookings/:id     | Get booking          | 🔒 JWT       |

### Admin
| Method | Endpoint                          | Description           | Auth          |
|--------|-----------------------------------|-----------------------|---------------|
| GET    | /api/admin/dashboard              | Admin stats           | 🔒 Admin     |
| GET    | /api/admin/bookings               | All bookings          | 🔒 Admin     |
| PUT    | /api/admin/bookings/:id/status    | Update status         | 🔒 Admin     |
| GET    | /api/admin/users                  | All users             | 🔒 Admin     |

---

## 🗄️ Database Schema

```
users              → id, name, email, password, role
services           → id, name, description, price, duration
service_providers  → id, name, skill_type, phoneno, availabilitystatus
booking_status     → id, status (pending/confirmed/completed/cancelled)
bookings           → id, userId, serviceId, providerId, bookingStatusId, address, bookingDate
```

## 🎨 Theme Colors
- `#FFF7D1` – Background
- `#FFECC8` – Cards
- `#FFD09B` – Accent/Primary
- `#FFB0B0` – Highlight
