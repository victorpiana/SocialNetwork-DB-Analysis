# SI40 Project: Social Network Database and OLAP Analysis (2023)

> This repository contains the complete PostgreSQL database implementation and OLAP analysis for a social network platform, developed as part of the **SI40 (Database Management)** unit at the **UTBM** engineering school.

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

## 👤 Author
**Victor Piana**

Engineering Student – UTBM, SI40
