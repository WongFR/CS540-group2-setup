# Game Info pages Design and Interface

This document describes the main authentication interfaces for the game info of the app, including the Game Info and potential APIs. As well as images of a basic design/layout.

![Game Info](https://github.com/user-attachments/assets/50e6fdd3-d4de-4f66-940e-59873fe09dee)


---
## 1. Get Game Info API

**Endpoint:** `/api/games/:gameId`  
**HTTP Method:** `GET`

### Request

No request body. `gameId` is passed as a URL parameter.

Example:  
`/api/games/game123`

### Response
```json
{
  "code": 200,
  "message": "Game info fetched successfully",
  "data": {
    "gameId": "game123",
    "title": "Epic Quest",
    "genre": "RPG",
    "platform": "PC",
    "releaseDate": "2024-01-01",
    "coverImageUrl": "/images/epic-quest.jpg",
    "details": "An immersive RPG set in a fantasy world.",
    "review": "Top-notch gameplay and storytelling. A must-play for RPG fans!"
  }
}
```

## 2. Get Game Comments API

**Endpoint:** `/api/games/:gameId/comments`  
**HTTP Method:** `GET`

### Request

No request body. `gameId` is passed as a URL parameter.  
Example: `/api/games/game123/comments`

### Response
```json
{
  "code": 200,
  "message": "Comments fetched successfully",
  "data": [
    {
      "commentId": "cmt001",
      "userId": "user001",
      "username": "gamerX",
      "content": "This game is awesome!",
      "timestamp": "2025-03-21T10:15:00Z"
    },
    {
      "commentId": "cmt002",
      "userId": "user002",
      "username": "playerTwo",
      "content": "Great graphics, but the controls need improvement.",
      "timestamp": "2025-03-21T11:00:00Z"
    }
  ]
}

```
## 3. Add Game Comment API

**Endpoint:** `/api/games/:gameId/comments`  
**HTTP Method:** `POST`

### Request
```json
{
  "userId": "user001",
  "username": "gamerX",
  "content": "This game is awesome!"
}
```

### Response
```json
{
  "code": 201,
  "message": "Comment added successfully",
  "data": {
    "commentId": "cmt003",
    "gameId": "game123",
    "userId": "user001",
    "content": "This game is awesome!",
    "timestamp": "2025-03-21T12:00:00Z"
  }
}
```
