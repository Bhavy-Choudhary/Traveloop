# ✈️ Traveloop — Personalized Travel Planning Made Easy

> A user-centric, responsive travel planning web application built for the **Odoo Hackathon**.  
> Plan multi-city trips, manage itineraries, track budgets, and share adventures — all in one place.

---

## 📌 Table of Contents

- [Overview](#-overview)
- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Project Structure](#-project-structure)
- [Screens & Pages](#-screens--pages)
- [Getting Started](#-getting-started)
- [Database Schema](#-database-schema)
- [Team](#-team)

---

## 🌍 Overview

**Traveloop** is a personalized, intelligent, and collaborative travel planning platform that transforms how individuals plan and experience travel.

Users can explore global destinations, visualize journeys through structured itineraries, make cost-effective decisions, and share their travel plans within a community — making travel planning as exciting as the trip itself.

---

## ✨ Features

| # | Feature | Description |
|---|---------|-------------|
| 1 | 🔐 Login / Signup | Email & password auth with validation |
| 2 | 🏠 Dashboard | Upcoming trips, recommended destinations, quick actions |
| 3 | ➕ Create Trip | Name, dates, budget, cover photo & visibility settings |
| 4 | 📋 My Trips | List view of all trips with edit / delete actions |
| 5 | 🗺️ Itinerary Builder | Add cities, assign activities, reorder stops |
| 6 | 📅 Itinerary View | Day-wise timeline with calendar / list toggle |
| 7 | 🔍 City Search | Search cities with cost index, country & popularity |
| 8 | 🎯 Activity Search | Browse activities by type, cost, and duration |
| 9 | 💰 Budget Tracker | Cost breakdown by transport, stay, meals & activities |
| 10 | 🧳 Packing Checklist | Add, check off & categorize packing items |
| 11 | 🌐 Public Itinerary | Shareable read-only view with "Copy Trip" option |
| 12 | 👤 Profile / Settings | Edit profile, language preference, saved destinations |
| 13 | 📝 Trip Notes | Per-trip notes and day-specific reminders |
| 14 | 📊 Admin Dashboard *(optional)* | User trends, popular cities, engagement stats |

---

## 🛠️ Tech Stack

### Frontend
![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![CSS3](https://img.shields.io/badge/CSS3-1572B6?style=flat&logo=css3&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)

- Plain HTML, CSS, and Vanilla JavaScript
- Responsive design — works on desktop & mobile
- No external frameworks or build tools required

### Backend *(to be integrated)*
- **Node.js** with Express.js — REST API
- **MongoDB** (Mongoose) — NoSQL database  
  *or*
- **MySQL** — Relational database

### Authentication *(to be integrated)*
- JWT (JSON Web Tokens)
- bcrypt for password hashing

---

## 📁 Project Structure

```
Traveloop/
│
├── index.html              # Login / Signup screen
├── dashboard.html          # Home / Dashboard screen
├── create-trip.html        # Create Trip screen ✅
├── my-trips.html           # Trip list screen
├── itinerary-builder.html  # Itinerary builder screen
├── itinerary-view.html     # Itinerary view screen
├── city-search.html        # City search screen
├── activity-search.html    # Activity search screen
├── budget.html             # Budget & cost breakdown screen
├── checklist.html          # Packing checklist screen
├── public-trip.html        # Shared / public itinerary screen
├── profile.html            # User profile & settings screen
├── notes.html              # Trip notes / journal screen
│
├── css/
│   └── styles.css          # Shared global styles
│
├── js/
│   └── main.js             # Shared JavaScript utilities
│
└── assets/
    └── images/             # Static images and icons
```

---

## 🖥️ Screens & Pages

### 1. Login / Signup
Entry point for the app. Users can create or access their account using email and password.

### 2. Dashboard / Home
Central hub showing upcoming trips, popular cities, quick actions, and budget highlights.

### 3. Create Trip ✅ *(built)*
Form to initiate a new trip — includes trip name, type, travel dates, budget, cover photo, and visibility settings.

### 4. My Trips
Card-based list of all user trips with name, date range, destination count, and actions.

### 5. Itinerary Builder
Interactive interface to add cities, assign activities, and reorder stops day by day.

### 6. Itinerary View
Structured day-wise view of the complete trip plan with calendar/list toggle.

### 7. City Search
Search and add cities with info like country, cost index, and popularity.

### 8. Activity Search
Browse and add activities per stop — filtered by type, cost, and duration.

### 9. Budget & Cost Breakdown
Financial summary showing estimated total, breakdown by category, and over-budget alerts.

### 10. Packing Checklist
Per-trip checklist with categories (clothing, documents, electronics), mark as packed.

### 11. Shared / Public Itinerary
Public read-only trip page with social sharing and "Copy Trip" button.

### 12. Profile / Settings
Edit user info, language preferences, saved destinations, and manage account.

### 13. Trip Notes / Journal
Per-trip and per-stop note taking with timestamps, sorted by date.

### 14. Admin Dashboard *(optional)*
Analytics for admins — trips created, top cities, user engagement, management tools.

---

## 🚀 Getting Started

### Prerequisites
- A modern browser (Chrome, Firefox, Edge)
- No installations needed for the frontend

### Run the Frontend
```bash
# Clone the repository
git clone https://github.com/Bhavy-Choudhary/Traveloop.git

# Navigate into the folder
cd Traveloop

# Open in browser — no server required
open index.html
# or just double-click index.html
```

### Backend Setup *(once backend is added)*
```bash
# Install dependencies
npm install

# Set up environment variables
cp .env.example .env
# Edit .env with your DB connection string and JWT secret

# Start the server
npm start
```

---

## 🗃️ Database Schema

### MongoDB (Mongoose)

```js
// Users
const userSchema = new Schema({
  name:      String,
  email:     { type: String, required: true, unique: true },
  password:  String,   // bcrypt hashed
  photo:     String,
  language:  { type: String, default: 'en' },
  createdAt: { type: Date, default: Date.now }
});

// Trips
const tripSchema = new Schema({
  userId:        { type: ObjectId, ref: 'User', required: true },
  tripName:      { type: String, required: true },
  tripType:      String,
  description:   String,
  startDate:     Date,
  endDate:       Date,
  budget:        Number,
  currency:      { type: String, default: 'INR' },
  visibility:    { type: String, enum: ['private','friends','public'], default: 'private' },
  coverPhotoUrl: String,
  createdAt:     { type: Date, default: Date.now }
});

// Stops (cities within a trip)
const stopSchema = new Schema({
  tripId:     { type: ObjectId, ref: 'Trip' },
  cityName:   String,
  country:    String,
  startDate:  Date,
  endDate:    Date,
  order:      Number
});

// Activities
const activitySchema = new Schema({
  stopId:      { type: ObjectId, ref: 'Stop' },
  name:        String,
  type:        String,
  cost:        Number,
  duration:    Number,  // in minutes
  description: String,
  time:        String
});
```

### MySQL

```sql
CREATE TABLE users (
  id         INT AUTO_INCREMENT PRIMARY KEY,
  name       VARCHAR(100),
  email      VARCHAR(200) NOT NULL UNIQUE,
  password   VARCHAR(255),
  photo      VARCHAR(500),
  language   VARCHAR(10) DEFAULT 'en',
  created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);

CREATE TABLE trips (
  id             INT AUTO_INCREMENT PRIMARY KEY,
  user_id        INT NOT NULL,
  trip_name      VARCHAR(200) NOT NULL,
  trip_type      VARCHAR(100),
  description    TEXT,
  start_date     DATE,
  end_date       DATE,
  budget         DECIMAL(12,2),
  currency       CHAR(3) DEFAULT 'INR',
  visibility     ENUM('private','friends','public') DEFAULT 'private',
  cover_photo    VARCHAR(500),
  created_at     TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
  FOREIGN KEY (user_id) REFERENCES users(id)
);

CREATE TABLE stops (
  id         INT AUTO_INCREMENT PRIMARY KEY,
  trip_id    INT NOT NULL,
  city_name  VARCHAR(100),
  country    VARCHAR(100),
  start_date DATE,
  end_date   DATE,
  sort_order INT DEFAULT 0,
  FOREIGN KEY (trip_id) REFERENCES trips(id)
);

CREATE TABLE activities (
  id          INT AUTO_INCREMENT PRIMARY KEY,
  stop_id     INT NOT NULL,
  name        VARCHAR(200),
  type        VARCHAR(100),
  cost        DECIMAL(10,2),
  duration    INT,
  description TEXT,
  time        VARCHAR(20),
  FOREIGN KEY (stop_id) REFERENCES stops(id)
);
```

---

## 👥 Team

Built with ❤️ for the **Odoo Hackathon**

| Member | Role |
|--------|------|
| Rishuraj Kashyap | 👑 Team Leader |
| Bhavy Choudhary | Developer |

---

## 📄 License

This project was built for the Odoo Hackathon. All rights reserved to the team.

---

> 🔗 Mockup Reference: [Excalidraw](https://link.excalidraw.com/l/65VNwvy7c4X/22o30WE3bE4)
