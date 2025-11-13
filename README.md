# SI40 Project: Social Network Database and OLAP Analysis

> [cite_start]This repository contains the complete PostgreSQL database implementation and OLAP analysis for a social network platform, developed as part of the **SI40 (Database Management)** unit at the **UTBM** engineering school[cite: 30, 56, 1609].

---

## 🎯 Overview
[cite_start]This project addresses the design, implementation, and analysis of a relational database system for a social media application[cite: 58]. [cite_start]The core challenge was designing a robust and secure database structure capable of handling core social network functionalities (posts, likes, comments, following) [cite: 104, 166] [cite_start]and enabling strategic decision-making through **Online Analytical Processing (OLAP)**[cite: 61, 78, 1374].

The project involved:
* [cite_start]**Relational Modeling** (MCD/MLD)[cite: 75, 109, 227].
* [cite_start]**PostgreSQL Implementation** including advanced features (Procedures, Triggers, Cursors)[cite: 76, 405, 489, 999].
* [cite_start]**User Management** and Role-Based Access Control (RBAC)[cite: 658, 687].
* [cite_start]**OLAP Analysis** using Power BI and a Star Schema[cite: 91, 1373, 1399].

---

## 📂 Repository Structure
The repository is structured around the main deliverables:

. ├── si40versionfinale.sql # Full PostgreSQL schema, including all tables, functions, │ # procedures, triggers, constraints, and data. ├── Piana_Jury_Chairi_SI40.pdf # Final Project Report (rapport de projet). ├── Piana_Jury_Chairi_SI40/ # Power BI analysis files (PBIX, etc.). └── README.md # This file


## ⚙️ Key Technical Features (PostgreSQL)

The database, implemented in PostgreSQL, includes several advanced features for data integrity, security, and automation[cite: 88, 76]:

### 1. User and Data Management
* **`UTILISATEUR` Table**: Stores user profiles [cite: 1320], including roles (`administrateur`, `user_normal`, `spectateur`)[cite: 688].
* **User Management Procedure (`add_user`)**: Safely inserts a new user[cite: 791], including:
    * Validation of the `ROLE` field against permitted values (`administrateur`, `user_normal`, `spectateur`)[cite: 808].
    * Automatic generation of `ID_UTILISATEUR` using a sequence (`utilisateur_id_seq`)[cite: 938, 940].
* **Email Validation Trigger**: Ensures a valid email format before insertion or update on the `UTILISATEUR` table[cite: 766, 779].
* **Cursor Procedure (`process_utilisateurs`)**: Demonstrates row-by-row data processing and retrieval within PL/pgSQL[cite: 1002, 1041].

### 2. Notification System
A trigger-based notification system is implemented using the `NOTIFICATION` table, automatically responding to user actions[cite: 1054, 174]:
| Action | Trigger | Function | Description |
| :--- | :--- | :--- | :--- |
| **Like** | `trigger_post_liked` | `notify_post_liked()` | Notifies the post author when their post is liked[cite: 1069, 1090]. |
| **Comment** | `trigger_comment_posted` | `notify_comment_posted()` | Notifies the post author when a new comment is posted[cite: 1096, 1092]. |
| **Follow** | `trigger_user_followed` | `notify_user_followed()` | Notifies a user when they gain a new follower[cite: 1131, 1127]. |

### 3. Action History & Audit Log
* **`HISTORIQUE_ACTIONS` Table**: Records all `INSERT`, `UPDATE`, and `DELETE` operations on core tables (`UTILISATEUR`, `POSTE`, `COMMENTAIRE`)[cite: 1237, 1275, 1298].
* **`historique_trigger()` Function**: Uses the `TG_OP` special variable to determine the type of operation and records the old/new data payload in `JSONB` format[cite: 1174, 1199, 1203, 1210, 1222, 1220].

---

## 📊 OLAP Analysis (Power BI)
The project includes an Online Analytical Processing (OLAP) layer built using Power BI to support strategic decision-making[cite: 1374, 1598]:
* **Schema**: A **Star Schema** with `POSTE` as the central Fact Table[cite: 1375, 1388, 1399].
* **Dimensions**: Key dimensions include `Utilisateur`, `Commentaire`, `Notification`, `Aime` (Like), and `Suit` (Follow)[cite: 1379, 1381, 1382, 1383, 1385].
* **Insights**: Visualizations track key metrics like:
    * Post Popularity (Likes vs. Comments)[cite: 1407].
    * Engagement trends over time (Likes by Date)[cite: 1451].
    * User activity (Posts vs. Comments)[cite: 1434].
    * Notification Volume by Day[cite: 1468].

---
## 👤 Author
**Victor Piana**

Engineering Student – UTBM, SI40 [cite: 32, 56]

## 👤 Author
**Victor Piana**
