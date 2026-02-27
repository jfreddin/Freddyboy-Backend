# Freddyboy Backend — Auth System

A production-ready authentication backend service built with Node.js, Express, and MongoDB. This service handles user registration, secure login, email verification, and password recovery.

---

## 🚀 Features

- **User Authentication:** Signup and login with secure password hashing via `bcryptjs`
- **JWT Management:** Session handling via JSON Web Tokens stored in HTTP-only cookies
- **Email Service:** Automated transactional emails via `nodemailer` and Gmail for:
  - Email verification codes
  - Password reset links
  - Password reset success confirmations
- **Security Middleware:** Protected routes using token verification
- **Database Integration:** Object data modeling with `mongoose` and MongoDB connection handling

---

## 🛠️ Tech Stack

| Layer | Technology |
|---|---|
| Runtime | Node.js |
| Framework | Express.js |
| Database | MongoDB via Mongoose |
| Authentication | JWT & bcryptjs |
| Email | Nodemailer + Gmail SMTP |

---

## 📂 Project Structure

```
backend/
├── configs/          # Database configuration
├── controllers/      # Request handling logic
├── mail-service/     # Email templates and transporter config
├── middleware/       # Auth guarding (verifyToken)
├── models/           # Mongoose User schema
├── routes/           # API route definitions
├── utils/            # Token generation and cookie utilities
└── server.js         # Application entry point
```

---

## ⚙️ Prerequisites

- Node.js (v18+ recommended)
- MongoDB instance (local or Atlas)
- Gmail account with an App Password for the mail service

---

## 🚀 Getting Started

**1. Clone the repository**

```bash
git clone https://github.com/jfreddin/Freddyboy-Backend.git
```

**2. Install dependencies**

```bash
cd backend
npm install
```

**3. Set up environment variables**

Create a `.env` file in the `backend/` directory:

```env
PORT=5001
MONGO_URI=your_mongodb_connection_string
JWT_SECRET=your_super_secret_key
NODE_ENV=development
GMAIL=your_email@gmail.com
PASS=your_gmail_app_password
CLIENT_URL=http://localhost:5173
```

**4. Run the application**

```bash
npm run dev    # development (nodemon)
npm start      # production
```

---

## 🛣️ API Endpoints

| Method | Endpoint | Description |
|---|---|---|
| `POST` | `/api/auth/signup` | Register a new user & send verification email |
| `POST` | `/api/auth/login` | Authenticate user & set session cookie |
| `POST` | `/api/auth/logout` | Clear auth cookie |
| `POST` | `/api/auth/verify-email` | Verify account with 6-digit code |
| `POST` | `/api/auth/forgot-password` | Request a password reset link |
| `POST` | `/api/auth/reset-password/:token` | Reset password using email token |
| `GET` | `/api/auth/check-auth` | Validate current user session |

---

## 🛡️ Security Implementation

- **HTTP-only Cookies:** JWTs are sent via cookies with `httpOnly: true` and `sameSite: strict` to prevent XSS and CSRF attacks
- **Password Hashing:** Uses `bcryptjs` with 10 salt rounds
- **Token Expiry:** Verification tokens and password reset links are time-limited