# 📡 API Documentation

## Base URL

```
Development:  http://localhost:3000/api/v1
Production:   https://api.vpnapp.com/api/v1
```

## Authentication

All endpoints (except auth endpoints) require JWT token:

```
Authorization: Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...
```

## Response Format

### Success Response
```json
{
  "success": true,
  "data": {},
  "message": "Success message"
}
```

### Error Response
```json
{
  "success": false,
  "error": {
    "code": "INVALID_INPUT",
    "message": "Error description"
  }
}
```

## Error Codes

| Code | Status | Description |
|------|--------|-------------|
| INVALID_INPUT | 400 | Invalid request parameters |
| UNAUTHORIZED | 401 | Missing or invalid token |
| FORBIDDEN | 403 | Insufficient permissions |
| NOT_FOUND | 404 | Resource not found |
| RATE_LIMITED | 429 | Too many requests |
| INTERNAL_ERROR | 500 | Internal server error |

## Authentication Endpoints

### Register User

```http
POST /auth/register
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePassword123!",
  "name": "John Doe"
}
```

### Login User

```http
POST /auth/login
Content-Type: application/json

{
  "email": "user@example.com",
  "password": "SecurePassword123!"
}
```

**Response (200):**
```json
{
  "success": true,
  "data": {
    "id": "user_123",
    "email": "user@example.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9...",
    "expiresIn": 3600
  }
}
```

## User Endpoints

### Get User Profile

```http
GET /users/profile
Authorization: Bearer token_here
```

### Update User Profile

```http
PUT /users/profile
Authorization: Bearer token_here
Content-Type: application/json

{
  "name": "John Updated",
  "country": "CA"
}
```

## VPN Server Endpoints

### List All Servers

```http
GET /servers
Authorization: Bearer token_here
```

## Connection Endpoints

### Log Connection

```http
POST /connections
Authorization: Bearer token_here
Content-Type: application/json

{
  "serverId": "server_us_east_1",
  "protocol": "OpenVPN"
}
```

---

For more information, see:
- [Backend Setup Guide](BACKEND_SETUP.md)
- [Architecture Overview](ARCHITECTURE.md)
