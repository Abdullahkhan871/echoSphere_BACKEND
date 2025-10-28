# 🌐 EchoSphere Backend

A robust real-time chat application backend built with Node.js, Express, Socket.IO, and MongoDB. EchoSphere provides comprehensive authentication, user management, and real-time messaging capabilities.

## 🚀 Features

- **User Authentication & Authorization**
  - JWT-based authentication with access and refresh tokens
  - Secure password hashing with bcrypt
  - Email verification system
  - Password reset functionality via email

- **User Profile Management**
  - Profile picture upload with Cloudinary integration
  - Custom "About Me" status
  - Phone number management
  - Online/offline status tracking

- **Real-time Communication**
  - Socket.IO integration for real-time messaging
  - User presence tracking
  - Group chat support (schema ready)

- **Security Features**
  - HTTP-only cookies for token storage
  - Password strength validation
  - Email format validation
  - Profanity filter integration

## 🛠️ Tech Stack

- **Runtime:** Node.js
- **Framework:** Express.js v5.1.0
- **Database:** MongoDB with Mongoose ODM
- **Real-time:** Socket.IO v4.8.1
- **Authentication:** JWT (jsonwebtoken)
- **File Upload:** Multer v2.0.2
- **Cloud Storage:** Cloudinary
- **Email Service:** Nodemailer v7.0.5
- **Security:** bcrypt v6.0.0, cookie-parser, cors
- **Content Moderation:** bad-words v4.0.0

## 📁 Folder Structure

```
echosphere/
├── config/
│   ├── cloudinary.js      # Cloudinary configuration
│   └── db.js              # MongoDB connection
├── controllers/
│   └── auth.controller.js # Authentication logic
├── middleware/
│   ├── auth.middleware.js # JWT verification
│   └── multer.middleware.js # File upload handling
├── models/
│   ├── user.model.js      # User schema
│   └── group.model.js     # Group schema
├── routes/
│   └── auth.routes.js     # Authentication routes
├── utils/
│   ├── customeResponse.js # Response helper
│   ├── jwtUtils.js        # JWT utilities
│   └── patternValidator.js # Input validation
├── views/
│   └── inbox.ejs          # Email template
├── .env                   # Environment variables
├── index.js               # Application entry point
├── package.json
└── package-lock.json
```

## ⚙️ Installation and Setup

### Prerequisites
- Node.js (v18 or higher)
- MongoDB (local or Atlas)
- Cloudinary account
- Gmail account for email service

### Steps

1. **Clone the repository**
   ```bash
   git clone https://github.com/yourusername/echosphere.git
   cd echosphere
   ```

2. **Install dependencies**
   ```bash
   npm install
   ```

3. **Set up environment variables**
   
   Create a `.env` file in the root directory:
   ```env
   PORT=5000
   MONGO_URI=mongodb://localhost:27017/echosphere
   JWT_SECRET=your_jwt_secret_key_here
   JWT_REFRESH_SECRET=your_refresh_secret_key_here
   
   CLOUDINARY_CLOUD_NAME=your_cloudinary_cloud_name
   CLOUDINARY_API_KEY=your_cloudinary_api_key
   CLOUDINARY_API_SECRET=your_cloudinary_api_secret
   
   EMAIL_USER=your_gmail@gmail.com
   EMAIL_PASS=your_gmail_app_password
   
   BACKEND_URL=localhost:5000
   ```

4. **Run the application**
   
   Development mode (with nodemon):
   ```bash
   npm start
   ```
   
   The server will start on `http://localhost:5000`

## 🔐 Environment Variables

| Variable | Description | Required |
|----------|-------------|----------|
| `PORT` | Server port number | Yes |
| `MONGO_URI` | MongoDB connection string | Yes |
| `JWT_SECRET` | Secret key for access tokens | Yes |
| `JWT_REFRESH_SECRET` | Secret key for refresh tokens | Yes |
| `CLOUDINARY_CLOUD_NAME` | Cloudinary cloud name | Yes |
| `CLOUDINARY_API_KEY` | Cloudinary API key | Yes |
| `CLOUDINARY_API_SECRET` | Cloudinary API secret | Yes |
| `EMAIL_USER` | Gmail address for sending emails | Yes |
| `EMAIL_PASS` | Gmail app password | Yes |
| `BACKEND_URL` | Backend server URL | Yes |

### Gmail App Password Setup
1. Enable 2-Factor Authentication on your Gmail account
2. Go to Google Account Settings → Security → App Passwords
3. Generate a new app password for "Mail"
4. Use this password in the `EMAIL_PASS` variable

## 📚 API Documentation

### Authentication Endpoints

#### 1. Sign Up
```http
POST /auth/signup
Content-Type: application/json

{
  "name": "John Doe",
  "email": "john@example.com",
  "password": "StrongP@ss1"
}
```

**Response:**
```json
{
  "message": "User registered successfully",
  "data": {
    "userId": "60d5ec49f1b2c72b8c8e4f1a",
    "name": "John Doe",
    "email": "john@example.com"
  }
}
```

#### 2. Login
```http
POST /auth/login
Content-Type: application/json

{
  "email": "john@example.com",
  "password": "StrongP@ss1"
}
```

#### 3. Logout
```http
POST /auth/logout
Cookie: accessToken=xxx; refreshToken=xxx
```

#### 4. Add Profile Picture
```http
POST /auth/add-profile-pic
Content-Type: multipart/form-data
Cookie: accessToken=xxx

image: [file]
```

#### 5. Add About Me
```http
POST /auth/add-about-me
Content-Type: application/json
Cookie: accessToken=xxx

{
  "aboutMe": "Hey there! I am using EchoSphere"
}
```

#### 6. Add Mobile Number
```http
POST /auth/add-mobile-number
Content-Type: application/json
Cookie: accessToken=xxx

{
  "phone": "+1234567890"
}
```

#### 7. Request Password Reset
```http
POST /auth/request-password-reset
Content-Type: application/json

{
  "email": "john@example.com"
}
```

#### 8. Reset Password
```http
POST /auth/reset-password
Content-Type: application/json

{
  "password": "NewStrongP@ss1"
}
```

#### 9. Request Email Verification
```http
POST /auth/verify-email
Cookie: accessToken=xxx
```

### Password Requirements
- Minimum 8 characters
- At least one uppercase letter
- At least one lowercase letter
- At least one number
- At least one special character (@$!%*?#&)

## 🧪 Testing

Currently, the project doesn't have automated tests. To manually test:

1. Use Postman or Thunder Client
2. Import the endpoints listed above
3. Test authentication flow:
   - Sign up → Login → Access protected routes
4. Test file uploads with profile picture endpoint
5. Test email functionality with password reset

## 🚢 Deployment

### Recommended Platforms
- **Render**: Easy Node.js deployment with free tier
- **Railway**: Simple deployment with automatic HTTPS
- **AWS EC2**: Full control with EC2 instances
- **Heroku**: Classic PaaS solution
- **DigitalOcean**: App Platform for containerized apps

### Deployment Checklist
- [ ] Set all environment variables
- [ ] Change `secure: false` to `secure: true` in cookie settings for HTTPS
- [ ] Update CORS origin from `*` to specific frontend URL
- [ ] Set up MongoDB Atlas for production database
- [ ] Configure Cloudinary for production
- [ ] Set up proper logging and error tracking

### Docker Deployment (Optional)

Create a `Dockerfile`:
```dockerfile
FROM node:18-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production
COPY . .
EXPOSE 5000
CMD ["node", "index.js"]
```

Build and run:
```bash
docker build -t echosphere-backend .
docker run -p 5000:5000 --env-file .env echosphere-backend
```

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

### Contribution Guidelines
- Follow existing code style and conventions
- Add comments for complex logic
- Update documentation for new features
- Test your changes thoroughly

## 📝 License

This project is licensed under the ISC License - see the [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Your Name**

- GitHub: [@yourusername](https://github.com/yourusername)
- LinkedIn: [Your Name](https://linkedin.com/in/yourprofile)
- Email: your.email@example.com

## 🙏 Acknowledgments

- [Express.js](https://expressjs.com/) - Fast, unopinionated web framework
- [Socket.IO](https://socket.io/) - Real-time bidirectional event-based communication
- [MongoDB](https://www.mongodb.com/) - Document-oriented database
- [Cloudinary](https://cloudinary.com/) - Cloud-based image and video management

---

⭐ Star this repo if you find it helpful!
