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

## 📁 Repository Contents

* **`si40versionfinale (1).sql`**: Complete database implementation including schema, procedures, triggers, and sample data
* **`Piana_Jury_Chairi_SI40_rapport.pdf`**: Comprehensive project report (in French) with:
  - MCD/MLD diagrams
  - Detailed SQL query explanations
  - OLAP analysis and Power BI dashboard
  - Complete technical documentation

---

## 📄 Documentation

For detailed information about the project, please refer to the **[project report](Piana_Jury_Chairi_SI40_rapport.pdf)** which includes:

- Complete database modeling (MCD/MLD)
- Step-by-step implementation guide
- SQL query examples with screenshots
- OLAP analysis methodology
- Power BI dashboard design
- Entity Relationship Diagram (ERD)

---

## ⚙️ Key Technical Features (PostgreSQL)

The database, implemented in PostgreSQL, includes several advanced features for data integrity, security, and automation:

### 1. User and Data Management

* **`UTILISATEUR` Table**: Stores user profiles, including roles (`administrateur`, `user_normal`, `spectateur`).
* **User Management Procedure (`add_user`)**: Safely inserts a new user, including:
    * Validation of the `ROLE` field against permitted values (`administrateur`, `user_normal`, `spectateur`).
    * Automatic generation of `ID_UTILISATEUR` using a sequence (`utilisateur_id_seq`).
    * Email format validation before insertion.
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
* **Key Metrics Tracked**:
    * Post Popularity (Likes vs. Comments)
    * Engagement trends over time (Likes by Date)
    * User activity (Posts vs. Comments)
    * Notification Volume by Day
    * Average user age and demographics

---

## 🚀 Installation and Setup

### Prerequisites

* PostgreSQL 12+ installed
* psql command-line tool or pgAdmin 4
* Git

### Database Setup

1. **Clone the repository**:
```bash
git clone https://github.com/victorpiana/SocialNetwork-DB-Analysis.git
cd SocialNetwork-DB-Analysis
```

2. **Create the database**:
```bash
psql -U postgres -c "CREATE DATABASE social_network;"
```

3. **Execute the SQL file**:
```bash
psql -U postgres -d social_network -f "si40versionfinale (1).sql"
```

That's it! The database is now ready with all tables, procedures, triggers, and sample data.

---

## 🔒 Security Features

* **Role-Based Access Control (RBAC)**: Three user roles with distinct permissions:
  - `administrateur`: Full access to all tables and operations
  - `user_normal`: Standard user operations (create posts, like, comment, follow)
  - `spectateur`: Read-only access
* **Email Validation**: Ensures data quality at the database level through triggers
* **Audit Trail**: Complete history of all data modifications in `HISTORIQUE_ACTIONS`
* **Input Validation**: Procedures validate data before insertion to maintain integrity

---

## 🛠️ Available Functions and Procedures

The database includes several callable functions and procedures:

```sql
-- Add a new user with validation
CALL add_user('John Doe', 'john@example.com', 'user_normal', 'securePassword123');

-- Process and display all users (using cursor)
SELECT * FROM process_utilisateurs();

-- View recent notifications
SELECT * FROM NOTIFICATION ORDER BY DATE_NOTIFICATION DESC;

-- Check audit log
SELECT * FROM HISTORIQUE_ACTIONS ORDER BY DATE_ACTION DESC;

-- Get user statistics
SELECT COUNT(*) as total_users FROM UTILISATEUR;
SELECT AVG(EXTRACT(YEAR FROM AGE(DATE_NAISSANCE))) as avg_age FROM UTILISATEUR;
```

---

## 👥 Team

**Victor Piana** - Database modeling, SQL implementation  
**Cyprien Jury** - SQL queries, procedures, triggers  
**Hamza Chairi** - OLAP analysis, Power BI dashboard

Engineering Students – UTBM, SI40 (June 2024)

**Supervised by**: Mme Christine Lahoud

---

## 📚 Technologies Used

| Category | Technology | Usage |
|----------|-----------|--------|
| Database | PostgreSQL | Core database management system |
| Modeling | WinDesign | MCD/MLD diagram creation |
| Administration | pgAdmin 4 | Database administration and testing |
| Analytics | Power BI | OLAP analysis and visualization |
| Language | PL/pgSQL | Stored procedures and triggers |

---

## 📄 License

This project is part of an academic curriculum at UTBM and is provided for educational purposes.

---
