# LogAI - Backend

This is the backend API server for the LogAI application, providing authentication and data services.

## Features

- **Email/Password Authentication** - Traditional login and signup
- **OAuth Integration** - Login with Google and GitHub
- **Session Management** - Secure server-side sessions with express-session
- **RESTful API** - Clean API endpoints for frontend integration

## Tech Stack

- Node.js
- Express
- Passport.js (Google & GitHub OAuth)
- Express Session

## Setup

### 1. Install Dependencies

```bash
npm install
```

### 2. Configure Environment Variables

Create a `.env` file based on the `.env.example` file:

```env
# Server Configuration
PORT=4001
SESSION_SECRET=your_session_secret_here

# Google OAuth (Optional)
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_REDIRECT_URI=http://localhost:4001/api/auth/google/callback

# GitHub OAuth (Optional)
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
GITHUB_REDIRECT_URI=http://localhost:4001/api/auth/github/callback
```

### 3. Start Development Server

```bash
npm run dev
```

The API server will be running at http://localhost:4001.

## API Endpoints

- `POST /api/login` - User login
- `POST /api/signup` - User registration
- `POST /api/logout` - User logout
- `GET /api/me` - Get current user
- `GET /api/auth/google` - Google OAuth login
- `GET /api/auth/github` - GitHub OAuth login

## Integration with Frontend

This backend service is designed to work with the LogAI-Frontend application. The frontend should be configured to connect to this backend at http://localhost:4001.