# Mess/Hostel Management System

A full-stack web-based application that helps users find messes or hostels, connect with roommates, and manage accommodations and expenses. The system includes both user and admin dashboards for organized data control and functionality.

---

## Table of Contents

- [Technologies Used](#technologies-used)
- [Features](#features)
- [Database Schema](#database-schema)

---

## Technologies Used

- **Frontend**: HTML, CSS, JavaScript  
- **Backend**: Go or Node.js  
- **Database**: MySQL  
- **Additional Libraries**: Chart.js (for data visualization)

---

## Features

### General
- Search for hostels based on location
- Find potential roommates with filtering options
- Secure user registration and authentication

### User Dashboard
- View and update personal profile
- Join or leave a hostel
- View hostel and room details
- Track expenses with charts

### Admin Dashboard
- Add/edit/delete hostels and rooms
- Manage user data and access
- View statistics related to rooms and expenses
- Moderate roommate requests

---

## Database Schema

```sql
CREATE TABLE Users (
    user_id INT AUTO_INCREMENT PRIMARY KEY,
    username VARCHAR(50) UNIQUE NOT NULL,
    password VARCHAR(100) NOT NULL,
    email VARCHAR(100),
    full_name VARCHAR(100),
    is_admin BOOLEAN DEFAULT FALSE
);

CREATE TABLE Hostels (
    hostel_id INT AUTO_INCREMENT PRIMARY KEY,
    name VARCHAR(100) NOT NULL,
    location VARCHAR(150),
    total_rooms INT,
    available_rooms INT,
    owner_id INT,
    FOREIGN KEY (owner_id) REFERENCES Users(user_id)
);

CREATE TABLE Rooms (
    room_id INT AUTO_INCREMENT PRIMARY KEY,
    hostel_id INT,
    room_number VARCHAR(10),
    capacity INT,
    current_occupants INT,
    rent INT,
    FOREIGN KEY (hostel_id) REFERENCES Hostels(hostel_id)
);

CREATE TABLE RoommateRequests (
    request_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    preferred_location VARCHAR(100),
    budget_range VARCHAR(50),
    notes TEXT,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);

CREATE TABLE Expenses (
    expense_id INT AUTO_INCREMENT PRIMARY KEY,
    user_id INT,
    amount DECIMAL(10,2),
    description TEXT,
    date DATE,
    FOREIGN KEY (user_id) REFERENCES Users(user_id)
);
