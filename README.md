# Mess/Hostel Management System

A full-stack web-based application that helps users find messes, connect with roommates, and manage accommodations and expenses. The system includes both user and admin dashboards for organized data control and functionality.

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

### 🔍 General
- Search for hostels based on location  
- Find potential roommates with filtering options  
- Secure user registration and authentication  

### 👤 User Dashboard
- View and update personal profile  
- Join or leave a hostel  
- View hostel and room details  
- Track expenses with charts  

### 🛠️ Admin Dashboard
- Add/edit/delete hostels and rooms  
- Manage user data and access  
- View statistics related to rooms and expenses  
- Moderate roommate requests  

---

### ✅ Core Mess Management Features
These are essential features for managing mess life even without authentication/admin roles:

1. **Member Information Manager**  
   Add/remove/edit roommate names and contact info. View active members in a mess.

2. **Expense Tracker**  
   Record and categorize shared expenses (groceries, rent, utilities) and split costs equally.

3. **Monthly Summary Dashboard**  
   Display total monthly expenses, per-person costs, and all transactions.

4. **Individual Contribution Tracker**  
   Track who paid what, and calculate how much each member owes or is owed.

5. **Bill Management**  
   Manage recurring bills (rent, internet, etc.), their due dates, and payment status.

6. **Editable Shared Table View**  
   A spreadsheet-style interface that allows everyone to view and edit data easily.

---

### ✨ Additional Features
These features improve convenience, tracking, and accountability in mess life:

1. **Meal Count System**  
   Track daily meals for each person and calculate individual meal-based costs.

2. **Leave Tracker**  
   Members can log when they're away; expense/meal shares are adjusted accordingly.

3. **Shared Item Tracker**  
   Keep track of common-use items (e.g., gas, oil, cleaning supplies) and alert when low.

4. **Chore Management**  
   Create and rotate responsibility schedules for tasks like cleaning, shopping, etc.

5. **Notice Board**  
   Post public notes or reminders visible to all mess members (e.g., “cleaning on Friday”).

6. **Export & Backup**  
   Export data to Excel or PDF, and optionally back up data as JSON or via localStorage.

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
