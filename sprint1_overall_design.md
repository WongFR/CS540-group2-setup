# Game Team Builder - System Design Documentation

This document outlines the overall design, including navigation flow, functional modules, frontend task assignments, and the database schema.

---

## 🧭 Page Navigation Logic

<img src="assets/images/pagenaiv.jpg" alt="Team Info" width="1200"> 

*Note: This flow shows user transitions between login, signup, home, profile, game info, team info, and build team pages.*

---

## 🧩 Functional Module Breakdown

### 🔹 Main Navigation

**Purpose**: Provides core entry points for users to explore games, manage teams, and access their profile.

**Features**:
- Access the Home Page after login
- Search and browse game recommendations
- Navigate to profile or logout
- View and search existing teams

**Pages**:
- `/home`
- `/profile`
- `/logout`
- `/team-search`
- `/game-search`

**Database Relations**:
- Reads from `User`, `Game`, `Team`
- Writes to `AuthLog` on logout (optional)

---

### 🔹 Game Info

**Purpose**: Displays detailed information about a specific game and allows users to initiate team creation.

**Features**:
- Show game image, description, and reviews
- Show available teams for this game (optional extension)
- Link to "Build Team" for team creation

**Pages**:
- `/game/:gameId`

**Database Relations**:
- Reads from `Game`
- May query `Team` to show existing teams related to the game

---

### 🔹 Build Team

**Purpose**: Allows a user to create a new team for a specific game and define its parameters.

**Features**:
- Select game
- Define team name, size, description, and scheduled time
- Add initial teammates (if known)

**Pages**:
- `/team/build`

**Database Relations**:
- Writes to `Team`
- Writes to `TeamMember` (adds creator as first member)
- Reads from `User` (for teammate search/autocomplete)

---

### 🔹 Team Info

**Purpose**: Displays team details and member list; allows users to join the team.

**Features**:
- Show team name, size, game info, and time
- Show current team members
- Option to request or join the team

**Pages**:
- `/team/:teamId`

**Database Relations**:
- Reads from `Team`
- Reads from `TeamMember`, `User`
- Writes to `TeamMember` when joining

---

### 🔹 User Profile & Settings

**Purpose**: Lets users manage their personal profile, view their teams, and update password or info.

**Features**:
- View and update personal profile
- See team participation history
- Reset password or update avatar/bio

**Pages**:
- `/profile`
- `/profile/settings`
- `/profile/teams`

**Database Relations**:
- Reads from `User`, `UserProfile`, `TeamMember`, `Team`
- Writes to `UserProfile` and `User`

---

> Each module is designed with modular, RESTful backend endpoints in mind, and should follow best practices for separation of concerns (e.g., auth, game, team, profile APIs).

---

## 👨‍💻 Frontend Task Assignments

| Task # | Module                     | Pages                         | Assigned To |
|--------|----------------------------|-------------------------------|-------------|
| 1      | Home Page                  | Homepage                      | Xiaofan     |
| 2      | Authentication & Profile   | Login, Signup, My Profile     | Elisa       |
| 3      | Game Info                  | Game Info, Game Review        | Yuxi        |
| 4      | Team Info & Build Team     | Build Team, Team Info         | Yunxiao     |

---

## 🗄️ Database Schema Design

### 📌 User Table

Stores core authentication data.

| Field         | Type        | Description              |
|---------------|-------------|--------------------------|
| id            | INT (PK)    | Unique user ID           |
| username      | VARCHAR     | Unique username          |
| password_hash | VARCHAR     | Hashed password          |
| email         | VARCHAR     | Unique email             |
| created_at    | DATETIME    | Account creation time    |
| updated_at    | DATETIME    | Last profile update time |

---

### 📌 UserProfile Table

Stores additional user information.

| Field         | Type        | Description               |
|---------------|-------------|---------------------------|
| id            | INT (PK)    | Profile ID                |
| user_id       | INT (FK)    | Linked to User table      |
| full_name     | VARCHAR     | Full name                 |
| bio           | TEXT        | Personal bio              |
| avatar_url    | TEXT        | Avatar image URL          |
| team_list     | TEXT        | List of team IDs (JSON)   |

---

### 📌 Game Table

Stores game-related information.

| Field         | Type        | Description            |
|---------------|-------------|------------------------|
| id            | INT (PK)    | Game ID                |
| title         | VARCHAR     | Game name              |
| picture_url   | TEXT        | Image of the game      |
| details       | TEXT        | Game description       |
| review        | TEXT        | User or public reviews |
| created_at    | DATETIME    | Game listing time      |

---

### 📌 Team Table

Teams created by users for games.

| Field         | Type        | Description                |
|---------------|-------------|----------------------------|
| id            | INT (PK)    | Team ID                    |
| game_id       | INT (FK)    | Linked game ID             |
| creator_id    | INT (FK)    | User who created the team  |
| team_name     | VARCHAR     | Name of the team           |
| team_size     | INT         | Number of members needed   |
| description   | TEXT        | Team description           |
| time          | DATETIME    | Scheduled play time        |
| created_at    | DATETIME    | Team creation timestamp    |

---

### 📌 TeamMember Table

Links users to teams they've joined.

| Field         | Type        | Description             |
|---------------|-------------|-------------------------|
| id            | INT (PK)    | Team member ID          |
| team_id       | INT (FK)    | Associated team ID      |
| user_id       | INT (FK)    | Joined user ID          |
| joined_at     | DATETIME    | Join timestamp          |

---

### 📌 AuthLog Table (Optional)

Tracks authentication events for security.

| Field         | Type        | Description             |
|---------------|-------------|-------------------------|
| id            | INT (PK)    | Log entry ID            |
| user_id       | INT (FK)    | User who triggered event|
| action        | VARCHAR     | login / logout / signup |
| timestamp     | DATETIME    | When it happened        |
| ip_address    | VARCHAR     | Source IP address       |

