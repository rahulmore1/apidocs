# 📌 User Module API Documentation

## 🏠 Base URL
- **Production**: `https://api.example.com`
- **Development**: `http://localhost:3000`

## 🆔 Authentication & User Management

### 1️⃣ Get User Profile
**Endpoint**: `GET /users/profile`  
**Description**: Fetches the authenticated user’s details extracted from Azure AD JWT.

#### 🔹 Request Headers
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `Authorization` | `Bearer token` | ✅ Yes | Azure AD JWT Token |

#### 🔹 Response Example
```json
{
  "id": "user-123",
  "email": "john.doe@example.com",
  "role": "Admin"
}
```

#### 🔹 Possible Responses
| Status Code | Description |
|------------|-------------|
| `200 OK` | Successfully retrieved user details. |
| `401 Unauthorized` | Invalid or missing token. |

---

### 2️⃣ Check if User is Admin
**Endpoint**: `GET /users/is-admin`  
**Description**: Returns `true` if the user has **Admin** role.

#### 🔹 Request Headers
| Name | Type | Required | Description |
|------|------|----------|-------------|
| `Authorization` | `Bearer token` | ✅ Yes | Azure AD JWT Token |

#### 🔹 Response Example
```json
{
  "isAdmin": true
}
```

#### 🔹 Possible Responses
| Status Code | Description |
|------------|-------------|
| `200 OK` | Successfully determined admin status. |
| `401 Unauthorized` | Invalid or missing token. |

---

### 3️⃣ Validate JWT Token
**Endpoint**: `POST /users/validate-token`  
**Description**: Verifies if the provided Azure AD JWT token is valid.

#### 🔹 Request Body
```json
{
  "token": "eyJhbGciOiJIUzI1..."
}
```

#### 🔹 Response Example
```json
{
  "valid": true,
  "user": {
    "id": "user-123",
    "email": "john.doe@example.com",
    "role": "User"
  }
}
```

#### 🔹 Possible Responses
| Status Code | Description |
|------------|-------------|
| `200 OK` | Token is valid. Returns user details. |
| `401 Unauthorized` | Invalid or expired token. |

---

### 4️⃣ Logout
**Endpoint**: `POST /users/logout`  
**Description**: Logs out the user by clearing frontend session storage.

#### 🔹 Response Example
```json
{
  "message": "User logged out successfully"
}
```

#### 🔹 Possible Responses
| Status Code | Description |
|------------|-------------|
| `200 OK` | User successfully logged out. |

---

## 🔐 Authentication
This API requires authentication via **Azure AD JWT Bearer Token**.

### 🔹 Security Scheme
```yaml
components:
  securitySchemes:
    bearerAuth:
      type: http
      scheme: bearer
      bearerFormat: JWT
```
All endpoints require the `Authorization` header:
```http
Authorization: Bearer {JWT_TOKEN}
```

---
