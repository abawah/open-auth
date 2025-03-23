[![Stack Logo](/.github/assets/logo.png)](https://stack-auth.com)

<h3 align="center">
  <a href="https://docs.stack-auth.com">📘 Docs</a>
  | <a href="https://stack-auth.com/">☁️ Hosted Version</a>
  | <a href="https://demo.stack-auth.com/">✨ Demo</a>
  | <a href="https://discord.stack-auth.com">🎮 Discord</a>
</h4>

# Stack Auth: Open-source Clerk/Auth0 alternative

Stack Auth is a managed user authentication solution. It is developer-friendly and fully open-source (licensed under MIT and AGPL).

Stack Auth gets you started in just five minutes, after which you'll be ready to use all of its features as you grow your project. Our managed service is completely optional and you can export your user data and self-host, for free, at any time.

We support Next.js, React, and JavaScript frontends, along with any backend that can use our [REST API](https://docs.stack-auth.com/rest-api/overview). Check out our [setup guide](https://docs.stack-auth.com/getting-started/setup) to get started.

<div align="center">
<img alt="Stack Auth Setup" src=".github/assets/create-project.gif" width="400" />
</div>

Below is a detailed documentation for the **Open-Auth** application, inspired by the official documentation of **Stack Auth** (https://docs.stack-auth.com/next/overview). This documentation is structured similarly but tailored for the new name **Open-Auth** and includes all necessary details for understanding, setting up, and using the application.

---

# Open-Auth Documentation

Open-Auth is an open-source, modular, and scalable authentication system designed to simplify user authentication and authorization in modern web applications. Built with Node.js, Express.js, and MongoDB, Open-Auth provides a robust foundation for implementing secure authentication workflows, including user registration, login, role-based access control, and JWT-based authentication.

---

## Overview

Open-Auth is designed to be:

- **Secure**: Uses bcrypt for password hashing and JWT for stateless authentication.
- **Modular**: Easy to integrate into existing projects or use as a standalone service.
- **Scalable**: Built with scalability in mind, making it suitable for small to large applications.
- **Customizable**: Allows developers to extend functionality and tailor it to their needs.

---

## Features

- **User Authentication**:
  - User registration, login, and logout.
  - Secure password storage using bcrypt.
- **JWT-Based Authentication**:
  - Stateless authentication using JSON Web Tokens (JWT).
  - Configurable token expiration.
- **Role-Based Access Control (RBAC)**:
  - Define user roles and permissions.
  - Restrict access to specific routes based on roles.
- **API Endpoints**:
  - RESTful API for authentication and user management.
- **Database Integration**:
  - MongoDB for storing user data.
  - Mongoose for object data modeling.
- **Environment Configuration**:
  - Uses `.env` files for sensitive data and configuration.
- **Validation**:
  - Input validation for user registration and login.
- **Error Handling**:
  - Centralized error handling for consistent API responses.

---

## Getting Started

### Prerequisites

Before using Open-Auth, ensure you have the following installed:

- [Node.js](https://nodejs.org/) (v14 or higher)
- [MongoDB](https://www.mongodb.com/) (local or cloud instance)
- [Git](https://git-scm.com/) (optional, for cloning the repository)

### Installation

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/your-repo/open-auth.git
   cd open-auth
   ```

2. **Install Dependencies**:
   ```bash
   npm install
   ```

3. **Set Up Environment Variables**:
   - Create a `.env` file in the root directory.
   - Add the following variables:
     ```env
     PORT=3000
     MONGO_URI=mongodb://localhost:27017/open-auth
     JWT_SECRET=your_jwt_secret_key
     JWT_EXPIRES_IN=1d
     ```

4. **Start the Server**:
   ```bash
   npm start
   ```

   The server will start running on `http://localhost:3000`.

---

## API Reference

### Authentication

#### Register a New User
- **Endpoint**: `POST /api/auth/register`
- **Request Body**:
  ```json
  {
    "name": "John Doe",
    "email": "john@example.com",
    "password": "password123"
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "token": "your_jwt_token"
  }
  ```

#### Log In
- **Endpoint**: `POST /api/auth/login`
- **Request Body**:
  ```json
  {
    "email": "john@example.com",
    "password": "password123"
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "token": "your_jwt_token"
  }
  ```

#### Log Out
- **Endpoint**: `POST /api/auth/logout`
- **Headers**:
  ```http
  Authorization: Bearer <your_jwt_token>
  ```
- **Response**:
  ```json
  {
    "success": true,
    "message": "Logged out successfully"
  }
  ```

### User Management

#### Get Current User Profile
- **Endpoint**: `GET /api/users/me`
- **Headers**:
  ```http
  Authorization: Bearer <your_jwt_token>
  ```
- **Response**:
  ```json
  {
    "success": true,
    "data": {
      "name": "John Doe",
      "email": "john@example.com"
    }
  }
  ```

#### Update Current User Profile
- **Endpoint**: `PUT /api/users/me`
- **Headers**:
  ```http
  Authorization: Bearer <your_jwt_token>
  ```
- **Request Body**:
  ```json
  {
    "name": "Jane Doe"
  }
  ```
- **Response**:
  ```json
  {
    "success": true,
    "data": {
      "name": "Jane Doe",
      "email": "john@example.com"
    }
  }
  ```

#### Delete Current User Account
- **Endpoint**: `DELETE /api/users/me`
- **Headers**:
  ```http
  Authorization: Bearer <your_jwt_token>
  ```
- **Response**:
  ```json
  {
    "success": true,
    "message": "User deleted successfully"
  }
  ```

---

## Error Handling

Open-Auth uses a centralized error handling mechanism. All errors are returned in the following format:

```json
{
  "success": false,
  "message": "Error message",
  "error": {
    "code": 400,
    "details": "Additional error details"
  }
}
```

### Common Error Codes

- **400**: Bad Request (e.g., invalid input).
- **401**: Unauthorized (e.g., missing or invalid token).
- **404**: Not Found (e.g., resource not found).
- **500**: Internal Server Error (e.g., server-side issue).

---

## Configuration

Open-Auth uses environment variables for configuration. Below are the key variables:

| Variable       | Description                          | Default Value               |
|----------------|--------------------------------------|-----------------------------|
| `PORT`         | Port on which the server runs.       | `3000`                      |
| `MONGO_URI`    | MongoDB connection string.           | `mongodb://localhost:27017/open-auth` |
| `JWT_SECRET`   | Secret key for signing JWTs.         | (Required)                  |
| `JWT_EXPIRES_IN` | JWT expiration time.               | `1d` (1 day)                |

---

## Customization

### Extending Functionality

Open-Auth is designed to be modular. You can extend its functionality by:

1. Adding new routes in the `routes` directory.
2. Creating new controllers in the `controllers` directory.
3. Defining new models in the `models` directory.

### Adding Roles and Permissions

To implement role-based access control (RBAC):

1. Update the `User` model to include a `role` field.
2. Create middleware to check user roles before granting access to specific routes.

---

## Contributing

We welcome contributions! Here’s how you can help:

1. Fork the repository.
2. Create a new branch for your feature or bugfix.
3. Commit your changes and push to the branch.
4. Submit a pull request.

Please ensure your code follows the project’s coding standards and includes appropriate tests.

---

## License

Open-Auth is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

---

## Support

For questions, issues, or feature requests, please open an issue on the [GitHub repository](https://github.com/your-repo/open-auth).

---

## Acknowledgments

- Inspired by modern authentication best practices.
- Built with the support of the open-source community.

---

This documentation provides a comprehensive guide to using and customizing Open-Auth. For more details, refer to the official documentation or explore the source code.
