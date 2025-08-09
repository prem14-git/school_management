# 🏫 School Management API

A comprehensive Node.js REST API for managing school data with geographical proximity-based sorting functionality.

## 📋 Project Overview

This project implements a Node.js API system for school management that allows users to:
- Add new schools to the database
- Retrieve schools sorted by proximity to a user's location
- Calculate geographical distances using the Haversine formula

## 🚀 Features

- **Clean API Design**: Simple and intuitive API endpoints
- **Geographical Sorting**: Schools sorted by distance from user location
- **Data Validation**: Comprehensive input validation for all endpoints
- **Database Integration**: MySQL database with connection pooling
- **Error Handling**: Robust error handling and meaningful responses
- **Environment Configuration**: Secure configuration management
- **Cloud Deployment Ready**: Optimized for cloud hosting

## 🛠️ Tech Stack

- **Runtime**: Node.js
- **Framework**: Express.js
- **Database**: MySQL
- **Database Driver**: mysql2
- **Environment Management**: dotenv
- **CORS**: Cross-Origin Resource Sharing enabled

## 📁 Project Structure

```
School/
├── backend/
│   ├── config/
│   │   └── db.js              # Database configuration
│   ├── controllers/
│   │   └── schoolController.js # Business logic
│   ├── routes/
│   │   └── schoolRoutes.js     # API routes
│   ├── app.js                  # Main application file
│   ├── package.json            # Dependencies
│   └── .gitignore             # Git ignore rules
└── README.md                   # Project documentation
```

## 🗄️ Database Schema

### Schools Table

```sql
CREATE TABLE schools (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    address VARCHAR(500) NOT NULL,
    latitude FLOAT NOT NULL,
    longitude FLOAT NOT NULL
);
```

## 🔧 Installation & Setup

### Prerequisites

- Node.js (v14 or higher)
- MySQL database (local or cloud)
- npm or yarn package manager

### 1. Clone the Repository

```bash
git clone <repository-url>
cd School/backend
```

### 2. Install Dependencies

```bash
npm install
```

### 3. Environment Configuration

Create a `.env` file in the backend directory:

```env
# Database Configuration
DB_HOST=your_database_host
DB_USER=your_database_username
DB_PASSWORD=your_database_password
DB_NAME=your_database_name

# Server Configuration
PORT=5000
```

### 4. Database Setup

Create the schools table in your MySQL database:

```sql
CREATE DATABASE school_management;
USE school_management;

CREATE TABLE schools (
    id INT PRIMARY KEY AUTO_INCREMENT,
    name VARCHAR(255) NOT NULL,
    address VARCHAR(500) NOT NULL,
    latitude FLOAT NOT NULL,
    longitude FLOAT NOT NULL
);
```

### 5. Start the Server

```bash
# Development mode
npm run dev

# Production mode
npm start
```

The server will start on `http://localhost:5000`

## 📚 API Documentation

### Base URL
```
http://localhost:5000/api
```

### Endpoints

#### 1. Add School

**POST** `/addSchool`

Adds a new school to the database.

**Request Body:**
```json
{
    "name": "ABC High School",
    "address": "123 Education Street, City, State",
    "latitude": 40.7128,
    "longitude": -74.0060
}
```

**Response:**
```json
{
    "message": "School added successfully"
}
```

**Validation Rules:**
- `name`: Required, non-empty string
- `address`: Required, non-empty string
- `latitude`: Required, valid number (-90 to 90)
- `longitude`: Required, valid number (-180 to 180)

#### 2. List Schools

**GET** `/listSchools`

Retrieves all schools sorted by proximity to user's location.

**Query Parameters:**
- `latitude`: User's latitude (required)
- `longitude`: User's longitude (required)

**Example Request:**
```
GET /api/listSchools?latitude=40.7128&longitude=-74.0060
```

**Response:**
```json
[
    {
        "id": 1,
        "name": "ABC High School",
        "address": "123 Education Street, City, State",
        "latitude": 40.7128,
        "longitude": -74.0060,
        "distance": 0.5
    },
    {
        "id": 2,
        "name": "XYZ Elementary",
        "address": "456 Learning Avenue, City, State",
        "latitude": 40.7589,
        "longitude": -73.9851,
        "distance": 2.3
    }
]
```

## 🔍 Error Handling

The API provides comprehensive error handling:

- **400 Bad Request**: Invalid input data or missing parameters
- **500 Internal Server Error**: Database or server errors

Example error response:
```json
{
    "message": "Invalid input data"
}
```

## 🧪 Testing with Postman

### Collection Setup

1. **Create New Collection**: "School Management API"
2. **Set Base URL**: `{{baseUrl}}/api` where `baseUrl = http://localhost:5000`

### Test Cases

#### Add School
```
POST {{baseUrl}}/api/addSchool
Content-Type: application/json

{
    "name": "Test School",
    "address": "123 Test Street",
    "latitude": 40.7128,
    "longitude": -74.0060
}
```

#### List Schools
```
GET {{baseUrl}}/api/listSchools?latitude=40.7128&longitude=-74.0060
```

## 🚀 Deployment

### Environment Variables for Production

```env
DB_HOST=your_cloud_database_host
DB_USER=your_database_username
DB_PASSWORD=your_secure_password
DB_NAME=school_management
PORT=5000
```

### Deployment Platforms

This API is ready for deployment on:
- **Heroku**
- **Railway**
- **Render**
- **AWS EC2**
- **Google Cloud Platform**
- **Azure**

## 📝 Sample Data

```sql
INSERT INTO schools (name, address, latitude, longitude) VALUES
('Central High School', '100 Main Street, Downtown', 40.7589, -73.9851),
('Westside Elementary', '250 West Avenue, Westside', 40.7505, -73.9934),
('Eastbrook Academy', '75 East Road, Eastside', 40.7614, -73.9776),
('Northgate School', '500 North Street, Uptown', 40.7831, -73.9712);
```

## 📄 License

This project is licensed under the ISC License.

## 👨‍💻 Author

Created as part of a Node.js assignment for school management system development.

---