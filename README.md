# LogAI - Backend

A robust backend API server for the LogAI application, providing comprehensive authentication services with support for multiple authentication methods.

## 🚀 Features

- **Email/Password Authentication** - Traditional login and signup with secure session management
- **OAuth Integration** - Seamless login with Google and GitHub
- **Session Management** - Secure server-side sessions with express-session
- **RESTful API** - Clean and well-structured API endpoints for frontend integration
- **CORS Support** - Configured for cross-origin requests with credentials
- **Profile Picture Handling** - Automatic extraction and optimization of user profile pictures from OAuth providers

## 🛠️ Tech Stack

- **Node.js** - JavaScript runtime environment
- **Express** - Web application framework
- **Passport.js** - Authentication middleware
  - `passport-google-oauth20` - Google OAuth 2.0 strategy
  - `passport-github2` - GitHub OAuth 2.0 strategy
- **Express Session** - Session management
- **CORS** - Cross-Origin Resource Sharing
- **dotenv** - Environment variable management

## 📦 Installation

### 1. Clone the Repository

```bash
git clone <repository-url>
cd LogAI---Backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Configure Environment Variables

Create a `.env` file in the root directory:

```env
# Server Configuration
PORT=4001
SESSION_SECRET=your_session_secret_here

# Google OAuth (Optional - leave empty to disable)
GOOGLE_CLIENT_ID=your_google_client_id
GOOGLE_CLIENT_SECRET=your_google_client_secret
GOOGLE_REDIRECT_URI=http://localhost:4001/api/auth/google/callback

# GitHub OAuth (Optional - leave empty to disable)
GITHUB_CLIENT_ID=your_github_client_id
GITHUB_CLIENT_SECRET=your_github_client_secret
GITHUB_REDIRECT_URI=http://localhost:4001/api/auth/github/callback
```

### 4. Start the Server

**Development mode (with auto-reload):**
```bash
npm run dev
```

**Production mode:**
```bash
npm start
```

The API server will be running at `http://localhost:4001`.

## 📡 API Endpoints

### Authentication Endpoints

#### Email/Password Authentication

- **POST** `/api/login` - User login
  - Body: `{ "email": "user@example.com", "password": "password123" }`
  - Returns: `{ "success": true, "user": { "id", "name", "email" } }`

- **POST** `/api/signup` - User registration
  - Body: `{ "email": "user@example.com", "password": "password123", "name": "User Name" }`
  - Returns: `{ "success": true, "user": { "id", "name", "email" } }`

- **POST** `/api/logout` - User logout
  - Returns: `{ "success": true }`

- **GET** `/api/me` - Get current authenticated user
  - Returns: `{ "id", "name", "email", "picture", "provider" }` or `401 Unauthorized`

#### OAuth Authentication

- **GET** `/api/auth/google` - Initiate Google OAuth login
  - Redirects to Google authentication page

- **GET** `/api/auth/google/callback` - Google OAuth callback
  - Handles OAuth callback and redirects to frontend

- **GET** `/api/auth/github` - Initiate GitHub OAuth login
  - Redirects to GitHub authentication page

- **GET** `/api/auth/github/callback` - GitHub OAuth callback
  - Handles OAuth callback and redirects to frontend

## 🔧 Configuration

### OAuth Setup

#### Google OAuth Setup

1. Go to [Google Cloud Console](https://console.cloud.google.com/)
2. Create a new project or select an existing one
3. Enable Google+ API
4. Create OAuth 2.0 credentials
5. Add authorized redirect URI: `http://localhost:4001/api/auth/google/callback`
6. Copy Client ID and Client Secret to `.env` file

#### GitHub OAuth Setup

1. Go to GitHub Settings > Developer settings > OAuth Apps
2. Create a new OAuth App
3. Set Authorization callback URL: `http://localhost:4001/api/auth/github/callback`
4. Copy Client ID and Client Secret to `.env` file

### CORS Configuration

The server is configured to accept requests from:
- `http://localhost:5173`
- `http://127.0.0.1:5173`

To modify CORS settings, edit the `cors` configuration in `index.js`.

## 🔐 Security Features

- **Session Security**: HTTP-only cookies with secure session management
- **CORS Protection**: Configured for specific origins
- **Environment Variables**: Sensitive data stored in `.env` file
- **Session Timeout**: 24-hour session expiration

## 🎯 Integration with Frontend

This backend service is designed to work with the LogAI frontend application. The frontend should:

1. Make API requests to `http://localhost:4001`
2. Include credentials in requests (for session cookies)
3. Handle OAuth redirects appropriately
4. Store session cookies automatically

### Example Frontend Integration

```javascript
// Login request
fetch('http://localhost:4001/api/login', {
  method: 'POST',
  headers: { 'Content-Type': 'application/json' },
  credentials: 'include',
  body: JSON.stringify({ email, password })
})

// Get current user
fetch('http://localhost:4001/api/me', {
  credentials: 'include'
})
```

## 📝 Notes

- User data is currently stored in memory (Map). For production, replace with a proper database.
- OAuth providers are optional - the server will work without them, but OAuth endpoints will return errors.
- Session cookies are configured for development (secure: false). Update for production.

## 🤝 Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## 📄 License

This project is private and proprietary.