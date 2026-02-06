# LifeFlow - Personal Life Management Application

A comprehensive web application for managing tasks, notes, sleep tracking, nutrition monitoring, and activity logging built with Go and MongoDB.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Technology Stack](#technology-stack)
- [Project Structure](#project-structure)
- [Installation](#installation)
- [Configuration](#configuration)
- [Running the Application](#running-the-application)
- [Pages](#pages)
- [API Endpoints](#api-endpoints)
- [Data Models](#data-models)
- [Database Collections](#database-collections)

## Overview

LifeFlow is a personal productivity and health tracking application that helps users manage their daily tasks, take notes, monitor sleep patterns, track nutrition intake, and log physical activities. The application features a clean, modern UI with data visualization using Chart.js.

## Features

- **Task Management**: Create, update, delete, and organize tasks with folders
- **Note Taking**: Simple note-taking system with title and description
- **Sleep Tracking**: Log sleep and wake times with duration visualization
- **Nutrition Monitoring**: Track daily calories, water intake, and healthy eating habits
- **Activity Logging**: Record daily activities with timestamps
- **User Profile**: View personal statistics and information
- **Data Visualization**: Interactive charts powered by Chart.js
- **Responsive Design**: Mobile-friendly interface with gradient themes
- **Time Series Data**: All tracking data stored with timestamps for historical analysis

## Technology Stack

### Backend
- **Language**: Go 1.x
- **Database**: MongoDB
- **Driver**: mongo-driver (official MongoDB Go driver)
- **Environment**: godotenv for configuration management

### Frontend
- **HTML5**: Semantic markup
- **CSS3**: Custom styling with gradients and animations
- **JavaScript**: Vanilla JS for interactivity
- **Chart.js**: Data visualization library (CDN)

### Architecture
- **Pattern**: Repository-Service-Handler (layered architecture)
- **Routing**: Native Go http package
- **Templating**: Go html/template package

## Project Structure

```
Assignment3/
├── cmd/
│   └── server/
│       └── main.go                 # Application entry point
├── internal/
│   ├── app/
│   │   ├── router.go              # Route definitions
│   │   └── server.go              # HTTP server setup
│   ├── config/
│   │   └── config.go              # Configuration management
│   ├── handlers/
│   │   ├── task_handler.go        # Task HTTP handlers
│   │   ├── note_handler.go        # Note HTTP handlers
│   │   ├── sleep_handler.go       # Sleep HTTP handlers
│   │   ├── nutrition_handler.go   # Nutrition HTTP handlers
│   │   ├── activity_handler.go    # Activity HTTP handlers
│   │   └── user_handler.go        # User HTTP handlers
│   ├── middleware/
│   │   ├── auth_middleware.go     # Authentication middleware
│   │   └── logging_middleware.go  # Logging middleware
│   ├── models/
│   │   ├── task.go                # Task data model
│   │   ├── note.go                # Note data model
│   │   ├── sleep.go               # Sleep data model
│   │   ├── nutrition.go           # Nutrition data model
│   │   ├── activity.go            # Activity data model
│   │   └── user.go                # User data model
│   ├── repository/
│   │   ├── mongo_client.go                    # MongoDB connection
│   │   ├── task_repository_interface.go       # Task repository interface
│   │   ├── task_mongo_repository.go           # Task MongoDB implementation
│   │   ├── note_repository_interface.go       # Note repository interface
│   │   ├── note_mongo_repository.go           # Note MongoDB implementation
│   │   ├── sleep_repository_interface.go      # Sleep repository interface
│   │   ├── sleep_mongo_repository.go          # Sleep MongoDB implementation
│   │   ├── nutrition_repository_interface.go  # Nutrition repository interface
│   │   ├── nutrition_mongo_repository.go      # Nutrition MongoDB implementation
│   │   ├── activity_repository_interface.go   # Activity repository interface
│   │   └── activity_mongo_repository.go       # Activity MongoDB implementation
│   └── service/
│       ├── task_service.go        # Task business logic
│       ├── note_service.go        # Note business logic
│       ├── sleep_service.go       # Sleep business logic
│       ├── nutrition_service.go   # Nutrition business logic
│       └── activity_service.go    # Activity business logic
├── templates/
│   ├── tasks.html                 # Tasks page template
│   ├── notes.html                 # Notes page template
│   ├── sleep.html                 # Sleep tracking page template
│   ├── nutrition.html             # Nutrition tracking page template
│   ├── activity.html              # Activity logging page template
│   ├── profile.html               # User profile page template
│   └── style.css                  # Shared styles
├── go.mod                         # Go module definition
├── go.sum                         # Go dependencies checksums
└── README.md                      # This file
```

## Installation

### Prerequisites

- Go 1.19 or higher
- MongoDB 4.4 or higher
- Git

### Steps

1. Clone the repository:
```bash
git clone <repository-url>
cd Assignment3
```

2. Install Go dependencies:
```bash
go mod download
```

3. Ensure MongoDB is installed and running:
```bash
mongod --version
```

## Configuration

1. Create a `.env` file in the project root:
```bash
cp .env.example .env
```

2. Configure the MongoDB connection string in `.env`:
```env
MONGO_URI=mongodb://localhost:27017
```

### Environment Variables

| Variable | Description | Default | Required |
|----------|-------------|---------|----------|
| MONGO_URI | MongoDB connection string | - | Yes |

## Running the Application

### Development Mode

```bash
go run cmd/server/main.go
```

### Production Build

```bash
go build -o lifeflow cmd/server/main.go
./lifeflow
```

The server will start on `http://localhost:8080`

## Pages

The application consists of 6 main pages:

### 1. Tasks Page (`/`)
- **URL**: `http://localhost:8080/`
- **Description**: Main dashboard for task management
- **Features**:
  - Create new tasks with title, body, and folder
  - Mark tasks as done/undone with toggle
  - Update task details inline
  - Delete tasks
  - Filter tasks by folder
  - Statistics showing total, completed, and pending tasks
- **Theme**: Blue gradient (4facfe → 00f2fe)

### 2. Notes Page (`/notes`)
- **URL**: `http://localhost:8080/notes`
- **Description**: Simple note-taking interface
- **Features**:
  - Create notes with title and description
  - Update existing notes
  - Delete notes
  - View total notes count
  - Inline editing with form toggle
- **Theme**: Green gradient (28a745 → 20c997)

### 3. Sleep Tracking Page (`/sleep`)
- **URL**: `http://localhost:8080/sleep`
- **Description**: Monitor sleep patterns and duration
- **Features**:
  - Log sleep time (when went to bed)
  - Log wake time (when woke up)
  - Automatic duration calculation
  - Line chart showing sleep duration over time
  - List of recent sleep records with formatted dates
- **Theme**: Purple gradient (667eea → 764ba2)
- **Visualization**: Chart.js line chart

### 4. Nutrition Tracking Page (`/nutrition`)
- **URL**: `http://localhost:8080/nutrition`
- **Description**: Track daily nutrition and hydration
- **Features**:
  - Log daily calorie intake
  - Track water consumption in litres
  - Record healthy eating (yes/no)
  - Bar chart for calorie tracking
  - Line chart for water intake
  - Doughnut chart for healthy vs unhealthy days ratio
  - List of recent nutrition records
- **Theme**: Pink gradient (f093fb → f5576c)
- **Visualization**: Chart.js bar, line, and doughnut charts

### 5. Activity Logging Page (`/activity`)
- **URL**: `http://localhost:8080/activity`
- **Description**: Log daily physical activities
- **Features**:
  - Record activity descriptions
  - Automatic timestamp for each activity
  - View all previous activities chronologically
  - Total activity count statistics
  - Simple text-based activity log
- **Theme**: Orange gradient (fa709a → fee140)

### 6. Profile Page (`/profile`)
- **URL**: `http://localhost:8080/profile`
- **Description**: User profile and statistics
- **Features**:
  - Display user information (name, email)
  - Show task statistics
  - Show note statistics
  - User activity summary
- **Theme**: Purple gradient (667eea → 764ba2)

## API Endpoints

Total Endpoints: **21**

### Task Endpoints (8 endpoints)

#### 1. Get All Tasks (JSON)
- **Method**: `GET`
- **Path**: `/tasks`
- **Description**: Retrieve all tasks in JSON format
- **Response**: Array of task objects
- **Status Codes**: 200 (Success), 500 (Server Error)

#### 2. Create Task (JSON)
- **Method**: `POST`
- **Path**: `/tasks`
- **Description**: Create a new task via JSON API
- **Request Body**:
```json
{
  "title": "Task title",
  "body": "Task description",
  "folder": "Work",
  "user_id": "user1"
}
```
- **Response**: Created task object
- **Status Codes**: 200 (Success), 400 (Bad Request), 500 (Server Error)

#### 3. Get Task by ID
- **Method**: `GET`
- **Path**: `/tasks/item?id=<task_id>`
- **Description**: Retrieve a specific task by ID
- **Query Parameters**: `id` (ObjectID)
- **Response**: Task object
- **Status Codes**: 200 (Success), 400 (Bad ID), 404 (Not Found), 500 (Server Error)

#### 4. Update Task (JSON)
- **Method**: `PUT`
- **Path**: `/tasks/item?id=<task_id>`
- **Description**: Update an existing task via JSON API
- **Query Parameters**: `id` (ObjectID)
- **Request Body**: Task object with updated fields
- **Response**: Updated task object
- **Status Codes**: 200 (Success), 400 (Bad Request), 500 (Server Error)

#### 5. Delete Task (JSON)
- **Method**: `DELETE`
- **Path**: `/tasks/item?id=<task_id>`
- **Description**: Delete a task via JSON API
- **Query Parameters**: `id` (ObjectID)
- **Status Codes**: 200 (Success), 400 (Bad ID), 500 (Server Error)

#### 6. Create Task (HTML Form)
- **Method**: `POST`
- **Path**: `/tasks/html`
- **Description**: Create a new task from HTML form submission
- **Form Data**: `title`, `body`, `folder`
- **Response**: Redirect to `/`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

#### 7. Toggle Task Status
- **Method**: `GET`
- **Path**: `/tasks/toggle?id=<task_id>`
- **Description**: Toggle task completion status (done/undone)
- **Query Parameters**: `id` (ObjectID)
- **Response**: Redirect to `/`
- **Status Codes**: 303 (Redirect), 400 (Bad ID), 500 (Server Error)

#### 8. Update Task (HTML Form)
- **Method**: `POST`
- **Path**: `/tasks/update`
- **Description**: Update task from HTML form submission
- **Form Data**: `id`, `title`, `body`, `folder`
- **Response**: Redirect to `/`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

### Note Endpoints (4 endpoints)

#### 9. View Notes Page
- **Method**: `GET`
- **Path**: `/notes`
- **Description**: Display notes page with all notes
- **Response**: HTML page
- **Status Codes**: 200 (Success), 500 (Server Error)

#### 10. Create Note (HTML Form)
- **Method**: `POST`
- **Path**: `/notes/html`
- **Description**: Create a new note from HTML form
- **Form Data**: `title`, `description`
- **Response**: Redirect to `/notes`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

#### 11. Update Note (HTML Form)
- **Method**: `POST`
- **Path**: `/notes/update`
- **Description**: Update an existing note from HTML form
- **Form Data**: `id`, `title`, `description`
- **Response**: Redirect to `/notes`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

#### 12. Delete Note
- **Method**: `GET`
- **Path**: `/notes/delete?id=<note_id>`
- **Description**: Delete a note
- **Query Parameters**: `id` (ObjectID)
- **Response**: Redirect to `/notes`
- **Status Codes**: 303 (Redirect), 400 (Bad ID), 500 (Server Error)

### Sleep Endpoints (3 endpoints)

#### 13. View Sleep Page
- **Method**: `GET`
- **Path**: `/sleep`
- **Description**: Display sleep tracking page with chart and records
- **Response**: HTML page with Chart.js visualization
- **Status Codes**: 200 (Success), 500 (Server Error)

#### 14. Create Sleep Record (HTML Form)
- **Method**: `POST`
- **Path**: `/sleep/html`
- **Description**: Log sleep and wake times from HTML form
- **Form Data**: `slept` (datetime-local), `woke_up` (datetime-local)
- **Response**: Redirect to `/sleep`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

#### 15. Get All Sleep Records (JSON)
- **Method**: `GET`
- **Path**: `/sleep/json`
- **Description**: Retrieve all sleep records in JSON format
- **Response**: Array of sleep objects sorted by timestamp (descending)
- **Status Codes**: 200 (Success), 500 (Server Error)

### Nutrition Endpoints (3 endpoints)

#### 16. View Nutrition Page
- **Method**: `GET`
- **Path**: `/nutrition`
- **Description**: Display nutrition tracking page with charts
- **Response**: HTML page with Chart.js visualizations (bar, line, doughnut)
- **Status Codes**: 200 (Success), 500 (Server Error)

#### 17. Create Nutrition Record (HTML Form)
- **Method**: `POST`
- **Path**: `/nutrition/html`
- **Description**: Log nutrition data from HTML form
- **Form Data**: `calories` (int), `water` (float), `healthy` (yes/no)
- **Response**: Redirect to `/nutrition`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

#### 18. Get All Nutrition Records (JSON)
- **Method**: `GET`
- **Path**: `/nutrition/json`
- **Description**: Retrieve all nutrition records in JSON format
- **Response**: Array of nutrition objects sorted by timestamp (descending)
- **Status Codes**: 200 (Success), 500 (Server Error)

### Activity Endpoints (3 endpoints)

#### 19. View Activity Page
- **Method**: `GET`
- **Path**: `/activity`
- **Description**: Display activity logging page with all activities
- **Response**: HTML page
- **Status Codes**: 200 (Success), 500 (Server Error)

#### 20. Create Activity (HTML Form)
- **Method**: `POST`
- **Path**: `/activity/html`
- **Description**: Log a new activity from HTML form
- **Form Data**: `description` (text)
- **Response**: Redirect to `/activity`
- **Status Codes**: 303 (Redirect), 400 (Bad Request), 405 (Method Not Allowed), 500 (Server Error)

#### 21. Get All Activities (JSON)
- **Method**: `GET`
- **Path**: `/activity/json`
- **Description**: Retrieve all activities in JSON format
- **Response**: Array of activity objects sorted by timestamp (descending)
- **Status Codes**: 200 (Success), 500 (Server Error)

### Profile Endpoint (1 endpoint)

#### 22. View Profile Page
- **Method**: `GET`
- **Path**: `/profile`
- **Description**: Display user profile with statistics
- **Response**: HTML page
- **Status Codes**: 200 (Success), 500 (Server Error)

## Data Models

### Task Model
```go
type Task struct {
    ID     primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Title  string             `json:"title" bson:"title"`
    Body   string             `json:"body" bson:"body"`
    Done   bool               `json:"done" bson:"done"`
    Folder string             `json:"folder" bson:"folder"`
    UserID string             `json:"user_id" bson:"user_id"`
}
```

**Fields**:
- `ID`: Unique MongoDB ObjectID
- `Title`: Task title (required)
- `Body`: Task description/details
- `Done`: Completion status (true/false)
- `Folder`: Category/folder name for organization
- `UserID`: Associated user identifier

### Note Model
```go
type Note struct {
    ID          primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Title       string             `json:"title" bson:"title"`
    Description string             `json:"description" bson:"description"`
    UserID      string             `json:"user_id" bson:"user_id"`
}
```

**Fields**:
- `ID`: Unique MongoDB ObjectID
- `Title`: Note title (required)
- `Description`: Note content/body
- `UserID`: Associated user identifier

### Sleep Model
```go
type Sleep struct {
    ID        primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    WokeUp    time.Time          `json:"woke_up" bson:"woke_up"`
    Slept     time.Time          `json:"slept" bson:"slept"`
    UserID    string             `json:"user_id" bson:"user_id"`
    Timestamp time.Time          `json:"timestamp" bson:"timestamp"`
}
```

**Fields**:
- `ID`: Unique MongoDB ObjectID
- `WokeUp`: Wake up time (datetime)
- `Slept`: Sleep time (datetime)
- `UserID`: Associated user identifier
- `Timestamp`: Record creation time (for time series)

### Nutrition Model
```go
type Nutrition struct {
    ID        primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Calories  int                `json:"calories" bson:"calories"`
    Water     float64            `json:"water" bson:"water"`
    Healthy   bool               `json:"healthy" bson:"healthy"`
    UserID    string             `json:"user_id" bson:"user_id"`
    Timestamp time.Time          `json:"timestamp" bson:"timestamp"`
}
```

**Fields**:
- `ID`: Unique MongoDB ObjectID
- `Calories`: Daily calorie intake (integer)
- `Water`: Water consumption in litres (float)
- `Healthy`: Healthy eating indicator (true/false)
- `UserID`: Associated user identifier
- `Timestamp`: Record creation time (for time series)

### Activity Model
```go
type Activity struct {
    ID          primitive.ObjectID `json:"id" bson:"_id,omitempty"`
    Description string             `json:"description" bson:"description"`
    UserID      string             `json:"user_id" bson:"user_id"`
    Timestamp   time.Time          `json:"timestamp" bson:"timestamp"`
}
```

**Fields**:
- `ID`: Unique MongoDB ObjectID
- `Description`: Activity description (required)
- `UserID`: Associated user identifier
- `Timestamp`: Record creation time (for time series)

### User Model
```go
type User struct {
    ID       string `json:"id" bson:"_id,omitempty"`
    Name     string `json:"name" bson:"name"`
    Email    string `json:"email" bson:"email"`
    TasksNum int    `json:"tasks_num" bson:"tasks_num"`
    NotesNum int    `json:"notes_num" bson:"notes_num"`
}
```

**Fields**:
- `ID`: Unique user identifier
- `Name`: User's full name
- `Email`: User's email address
- `TasksNum`: Total number of tasks
- `NotesNum`: Total number of notes

## Database Collections

The application uses the following MongoDB collections in the `lifeflow` database:

| Collection | Description | Indexes |
|------------|-------------|---------|
| `tasks` | Stores all task records | `_id`, `user_id` |
| `notes` | Stores all note records | `_id`, `user_id` |
| `sleep` | Stores sleep tracking records | `_id`, `user_id`, `timestamp` |
| `nutrition` | Stores nutrition tracking records | `_id`, `user_id`, `timestamp` |
| `activity` | Stores activity log records | `_id`, `user_id`, `timestamp` |

### Time Series Data

Collections `sleep`, `nutrition`, and `activity` are designed as time series data with the following characteristics:
- Each record includes a `timestamp` field
- Records are sorted by timestamp in descending order (newest first)
- Suitable for historical analysis and trend visualization
- Can be aggregated for daily, weekly, or monthly reports

## License

This project is created for educational purposes.
