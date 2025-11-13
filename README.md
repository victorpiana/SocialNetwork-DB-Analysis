# SI40 Project: Social Network Database and OLAP Analysis (2023)

> This repository contains the complete PostgreSQL database implementation and OLAP analysis for a social network platform, developed as part of the **SI40 (Database Management)** unit at the **UTBM** engineering school.

[![Database](https://img.shields.io/badge/Database-PostgreSQL-blue.svg)](https://www.postgresql.org/)
[![Analytics](https://img.shields.io/badge/Analytics-Power_BI-yellow.svg)](https://powerbi.microsoft.com/)
[![Language](https://img.shields.io/badge/Language-PL/pgSQL-orange.svg)](https://www.postgresql.org/docs/current/plpgsql.html)
[![Schema](https://img.shields.io/badge/Schema-Star_Schema-green.svg)](https://en.wikipedia.org/wiki/Star_schema)

---

## 🎯 Overview

This project addresses the design, implementation, and analysis of a relational database system for a social media application. The core challenge was designing a robust and secure database structure capable of handling core social network functionalities (posts, likes, comments, following) and enabling strategic decision-making through **Online Analytical Processing (OLAP)**.

The project involved:

* **Relational Modeling** (MCD/MLD).
* **PostgreSQL Implementation** including advanced features (Procedures, Triggers, Cursors).
* **User Management** and Role-Based Access Control (RBAC).
* **OLAP Analysis** using Power BI and a Star Schema.

---

## ⚙️ Key Technical Features (PostgreSQL)

The database, implemented in PostgreSQL, includes several advanced features for data integrity, security, and automation:

### 1. User and Data Management

* **`UTILISATEUR` Table**: Stores user profiles, including roles (`administrateur`, `user_normal`, `spectateur`).
* **User Management Procedure (`add_user`)**: Safely inserts a new user, including:
    * Validation of the `ROLE` field against permitted values (`administrateur`, `user_normal`, `spectateur`).
    * Automatic generation of `ID_UTILISATEUR` using a sequence (`utilisateur_id_seq`).
* **Email Validation Trigger**: Ensures a valid email format before insertion or update on the `UTILISATEUR` table.
* **Cursor Procedure (`process_utilisateurs`)**: Demonstrates row-by-row data processing and retrieval within PL/pgSQL.

### 2. Notification System

A trigger-based notification system is implemented using the `NOTIFICATION` table, automatically responding to user actions:

| Action | Trigger | Function | Description |
| :--- | :--- | :--- | :--- |
| **Like** | `trigger_post_liked` | `notify_post_liked()` | Notifies the post author when their post is liked. |
| **Comment** | `trigger_comment_posted` | `notify_comment_posted()` | Notifies the post author when a new comment is posted. |
| **Follow** | `trigger_user_followed` | `notify_user_followed()` | Notifies a user when they gain a new follower. |

### 3. Action History & Audit Log

* **`HISTORIQUE_ACTIONS` Table**: Records all `INSERT`, `UPDATE`, and `DELETE` operations on core tables (`UTILISATEUR`, `POSTE`, `COMMENTAIRE`).
* **`historique_trigger()` Function**: Uses the `TG_OP` special variable to determine the type of operation and records the old/new data payload in `JSONB` format.

---

## 📊 OLAP Analysis (Power BI)

The project includes an Online Analytical Processing (OLAP) layer built using Power BI to support strategic decision-making:

* **Schema**: A **Star Schema** with `POSTE` as the central Fact Table.
* **Dimensions**: Key dimensions include `Utilisateur`, `Commentaire`, `Notification`, `Aime` (Like), and `Suit` (Follow).
* **Insights**: Visualizations track key metrics like:
    * Post Popularity (Likes vs. Comments).
    * Engagement trends over time (Likes by Date).
    * User activity (Posts vs. Comments).
    * Notification Volume by Day.

---

## 🚀 Installation and Setup

### Prerequisites

* PostgreSQL 12+ installed
* Power BI Desktop (for OLAP analysis)
* Git

### Database Setup

1. **Clone the repository**:
```bash
git clone https://github.com/victorpiana/SI40_Project.git
cd SI40_Project
```

2. **Create the database**:
```bash
psql -U postgres -c "CREATE DATABASE social_network;"
```

3. **Execute the SQL scripts**:
```bash
psql -U postgres -d social_network -f schema.sql
psql -U postgres -d social_network -f procedures.sql
psql -U postgres -d social_network -f triggers.sql
psql -U postgres -d social_network -f sample_data.sql
```

### Power BI Setup

1. Open the `.pbix` file included in the `/analytics` folder.
2. Configure the PostgreSQL connection with your database credentials.
3. Refresh the data model to load the latest data.

---

## 📁 Project Structure

```
SI40_Project/
├── sql/
│   ├── schema.sql           # Database schema definition
│   ├── procedures.sql       # Stored procedures
│   ├── triggers.sql         # Trigger functions
│   └── sample_data.sql      # Sample data for testing
├── analytics/
│   └── social_network.pbix  # Power BI dashboard
├── docs/
│   ├── MCD.pdf              # Conceptual Data Model
│   └── MLD.pdf              # Logical Data Model
└── README.md
```

---

## 🔒 Security Features

* **Role-Based Access Control (RBAC)**: Three user roles with distinct permissions.
* **Email Validation**: Ensures data quality at the database level.
* **Audit Trail**: Complete history of all data modifications.
* **Input Validation**: Procedures validate data before insertion.

---

## 📈 Key Metrics Tracked

* User engagement (posts, comments, likes)
* Follower growth over time
* Most active users and popular content
* Notification patterns and frequency
* Content interaction rates

---

## 👤 Author

**Victor Piana**  
Engineering Student – UTBM, SI40

---

## 📄 License

This project is part of an academic curriculum and is provided for educational purposes.

---
