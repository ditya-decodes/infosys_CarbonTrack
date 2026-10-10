# 🌱 CarbonTrack — Environmental Impact Tracking & Sustainability Analytics

**Measure your footprint. Build greener habits. Make every action count.**

CarbonTrack is a full-stack sustainability web application designed to help individuals understand, monitor, and reduce their everyday carbon footprint. By converting daily activities into measurable CO₂-equivalent (CO₂e) emissions, the platform encourages informed decisions through analytics, personalized sustainability insights, goal tracking, and community engagement.

Developed as part of **Infosys Springboard Virtual Internship 7.0**.

---

## Table of Contents

* [Overview](#-overview)
* [Key Features](#-key-features)
* [Technology Stack](#-technology-stack)
* [System Architecture](#-system-architecture)
* [Project Structure](#-project-structure)
* [Getting Started](#-getting-started)
* [Environment Configuration](#-environment-configuration)
* [Database Setup](#-database-setup)
* [Application Modules](#-application-modules)
* [Future Enhancements](#-future-enhancements)
* [Team and Acknowledgements](#-team-and-acknowledgements)

## Overview

Everyday activities such as transportation, electricity consumption, food choices, and shopping contribute to our environmental footprint. CarbonTrack provides a centralized platform to record these activities, estimate their emissions, and track progress toward more sustainable habits.

The application combines a **Spring Boot REST API backend**, a **React.js frontend**, and a **MySQL database** to provide an interactive carbon-tracking experience.

## Key Features

* **Activity Tracking:** Record everyday activities across transportation, energy, food, and waste or shopping categories, depending on the configured activity types.
* **Carbon Footprint Analytics:** Monitor emissions through dashboard summaries, category-wise breakdowns, and historical trends.
* **Personalized Insights:** Receive actionable sustainability recommendations based on emission patterns.
* **Sustainability Goals:** Set reduction targets and monitor progress over time.
* **Achievements and Badges:** Encourage sustainable habits through milestones and achievements.
* **Community and Leaderboard:** Support community engagement and sustainability-oriented competition.
* **Team and Organizational Reporting:** Provide an organizational perspective on environmental impact.
* **Authentication:** Support secure user authentication using JWT, with Google OAuth2 configuration.
* **Sprout AI Eco-Assistant:** Offer sustainability guidance and environmental insights.
* **Responsive Interface:** Access sustainability information through an interactive web interface.

*Feature availability depends on the modules implemented and configured in the current version.*

## 🛠️Technology Stack

| Layer               | Technologies                            |
| ------------------- | --------------------------------------- |
| Frontend            | React.js, JavaScript, HTML5, CSS3, Vite |
| Backend             | Java, Spring Boot, Spring Security      |
| API Communication   | REST APIs                               |
| Database            | MySQL                                   |
| ORM                 | Spring Data JPA, Hibernate              |
| Database Migrations | Flyway                                  |
| Authentication      | JWT, Google OAuth2 configuration        |
| Build Tools         | Maven, npm                              |
| Testing             | JUnit, Spring Boot testing tools        |
| Version Control     | Git, GitHub                             |

## 🏗️System Architecture

CarbonTrack follows a frontend–backend architecture.

1. **User Interface:** Users interact with the React.js dashboard to record activities, view analytics, and manage sustainability goals.
2. **REST API Layer:** The frontend communicates with backend endpoints over HTTP.
3. **Business Logic:** Spring Boot services process activity records, manage application operations, and support carbon-tracking functionality.
4. **Data Layer:** Spring Data JPA and Hibernate handle database interactions.
5. **Database:** MySQL stores application data, with Flyway managing versioned schema migrations.
6. **Security:** JWT-based authentication and optional Google OAuth2 integration support protected access.

```text
                 ┌─────────────────────┐
                 │       User          │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ React.js Frontend   │
                 │ Dashboard & UI      │
                 └──────────┬──────────┘
                            │ HTTP / REST
                 ┌──────────▼──────────┐
                 │ Spring Boot Backend │
                 │ Controllers         │
                 │ Services & Security │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │ Spring Data JPA     │
                 │ Hibernate / Flyway  │
                 └──────────┬──────────┘
                            │
                 ┌──────────▼──────────┐
                 │     MySQL DB        │
                 └─────────────────────┘
```

## 📁Project Structure

```text
infosys-CarbonTrack/
│
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/com/carbontrack/app/
│   │   │   │   ├── config/
│   │   │   │   ├── controller/
│   │   │   │   ├── dto/
│   │   │   │   ├── entity/
│   │   │   │   ├── exception/
│   │   │   │   ├── mapper/
│   │   │   │   ├── oauth/
│   │   │   │   ├── repository/
│   │   │   │   ├── security/
│   │   │   │   ├── service/
│   │   │   │   └── CarbonTrackApplication.java
│   │   │   └── resources/
│   │   │       ├── application.properties
│   │   │       └── db/migration/
│   │   └── test/
│   ├── pom.xml
│   ├── mvnw
│   └── mvnw.cmd
│
├── frontend/
│   └── canopy-dashboard/
│       ├── public/
│       ├── src/
│       ├── package.json
│       ├── package-lock.json
│       └── vite.config.js
│
└── .gitignore
```

## Getting Started🚀

### Prerequisites

Install the following before running the application:

* Java Development Kit (JDK) compatible with the backend configuration
* Node.js and npm
* MySQL Server
* Git

### 1. Clone the repository

```bash
git clone https://github.com/ditya-decodes/infosys_CarbonTrack.git
cd infosys_CarbonTrack
```

### 2. Configure the backend

Open a terminal in the project root and configure the required environment variables before starting Spring Boot.

Required variables:

```text
DB_USERNAME
DB_PASSWORD
JWT_SECRET
```

For Google OAuth2 login, also configure:

```text
GOOGLE_CLIENT_ID
GOOGLE_CLIENT_SECRET
```

See [Environment Configuration](#-environment-configuration) for details.

### 3. Configure the database

Create a MySQL database named `carbontrack_db`, or use the database URL configured in `application.properties`.

```sql
CREATE DATABASE carbontrack_db;
```

Flyway is enabled in the application configuration. Verify that the migration scripts match your database schema before running the backend.

### 4. Start the backend

From the repository root, run:

**Windows PowerShell:**

```powershell
cd backend
.\mvnw.cmd spring-boot:run
```

**macOS / Linux:**

```bash
cd backend
chmod +x mvnw
./mvnw spring-boot:run
```

Alternatively, open the backend folder in IntelliJ IDEA and run `CarbonTrackApplication.java`.

Ensure the database is running and the required environment variables are available to the application process.

### 5. Start the frontend

Open a second terminal:

```bash
cd frontend/canopy-dashboard
npm install
npm run dev
```

Open the local URL printed by Vite in your terminal, commonly `http://localhost:5173`.

Ensure the frontend API configuration points to the running backend. Update the API base URL in the frontend configuration if necessary.

## 🔐 Environment Configuration

The backend reads sensitive configuration from environment variables rather than storing credentials in source code.

| Variable               | Purpose                        |
| ---------------------- | ------------------------------ |
| `DB_USERNAME`          | MySQL username                 |
| `DB_PASSWORD`          | MySQL password                 |
| `JWT_SECRET`           | Secret used for JWT operations |
| `GOOGLE_CLIENT_ID`     | Google OAuth2 client ID        |
| `GOOGLE_CLIENT_SECRET` | Google OAuth2 client secret    |

Set these variables in your operating system or IntelliJ IDEA Run Configuration.

For local development, you can create an untracked environment file if your application setup supports loading it. **Never commit real passwords, OAuth credentials, JWT secrets, or other private configuration to GitHub.**

## 🧩 Application Modules

| Module                | Purpose                                                |
| --------------------- | ------------------------------------------------------ |
| Authentication        | User login, registration, and access security          |
| Dashboard             | Overview of footprint data and sustainability progress |
| Activity Logging      | Record activities and associated emission data         |
| Trends                | Analyze emissions over time                            |
| Goals & Benchmarks    | Manage reduction targets and compare progress          |
| Insights              | Present sustainability recommendations                 |
| Badges & Achievements | Track milestones and accomplishments                   |
| Community             | Encourage participation in sustainable practices       |
| Sprout AI             | Provide sustainability guidance                        |
| Team Reports          | Support organizational environmental reporting         |

## 🔮 Future Enhancements

Potential areas for continued development include:

* More comprehensive emission-factor datasets and source attribution.
* Expanded analytics and interactive visualizations.
* Improved recommendation personalization.
* Enhanced multilingual accessibility.
* Deeper organizational reporting and export capabilities.
* Automated deployment, performance testing, and API documentation.

## 👥 Team and Acknowledgements

**Project:** CarbonTrack — Web Platform for Environmental Impact Tracking and Sustainability Analytics
**Program:** Infosys Springboard Virtual Internship 7.0
**Batch:** Batch 1

We sincerely thank Infosys Springboard, our mentors and coordinators, Mr. Sainath and Mr. Jothiragavan T., and our teammates for their guidance, collaboration, and support throughout the project.
This project provided practical experience in full-stack development, REST API integration, database management, testing, documentation, and collaborative software engineering.
---
**Built to make everyday sustainability measurable.🌱**
