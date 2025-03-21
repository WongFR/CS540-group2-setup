# Login/Register and Profile pages Design and Interface

This document describes the main authentication interfaces for the login, register and personal profile pages of the app, including the Login and Registration APIs. As well as images of a basic design/layout.
![login design](https://github.com/user-attachments/assets/797cc6f3-3174-44c2-b781-a7ae3c70fb10)

![profile design](https://github.com/user-attachments/assets/1aba4cc4-cc30-479f-8058-cc78dc07d9c6)


---

## 1. Login API

**Endpoint:** `/api/login`  
**HTTP Method:** `POST`

### Request 

The login request requires the user's credentials:

```json
{
  "username": "user123",
  "password": "yourSecurePassword"
}

```

### Response

```json
{
  "code": 200,
  "message": "Login successful",
  "data": {
    "userId": "abc123",
    "username": "user123",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

## 2. Registration API

**Endpoint:** `/api/register`
**HTTP Method:** `POST`  

### Request
```json
{
  "firstname: "userfirst",
  "lastname: "userlast",
  "username": "newuser",
  "email": "newuser@example.com",
  "password": "yourSecurePassword",
}
```

### Response 
```json
{
  "code": 201,
  "message": "Registration successful",
  "data": {
    "userId": "def456",
    "username": "newuser",
    "email": "newuser@example.com",
    "token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9..."
  }
}
```

## 1. Update Profile API

**Endpoint:** `/api/profile`  
**HTTP Method:** `PUT` or `PATCH`

### Request

This endpoint accepts updates to the user's profile. For updating the first and last name:

```json
{
  "firstName": "John",
  "lastName": "Doe"
}
```

### Response 
```json
{
  "code": 200,
  "message": "Profile updated successfully",
  "data": {
    "userId": "abc123",
    "firstName": "John",
    "lastName": "Doe",
    "email": "johndoe@example.com"
  }
}
```

## 2. Reset Password API

**Endpoint:** `/api/profile/reset-password`
**HTTP Method:** `POST`

This endpoint is used to update the user's password I pictured it triggered from a popup window within the profile page.

### Request 
The request should include the current password along with the new password and a confirmation:
```json
{
  "currentPassword": "currentSecurePassword",
  "newPassword": "newSecurePassword",
  "confirmPassword": "newSecurePassword"
}
```

### Response
```json
{
  "code": 200,
  "message": "Password reset successfully"
}
```



