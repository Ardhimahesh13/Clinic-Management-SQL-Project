# 🏥 Clinic Management System – SQL Project

Welcome to the **Clinic Management System** project!  
This repository contains a complete SQL script to **create**, **populate**, and **query** a database for a small clinic.  
It's designed to manage **patient information**, **doctor schedules**, **appointments**, and **billing** efficiently.

---

## 📐 Database Design

The core of this project is the `clinic_db` database, which organizes information across four connected tables:

- **doctors**: Stores a record for each doctor, including their name and speciality.
- **patients**: Contains essential patient details like name, date of birth, and phone number.
- **appointments**: A crucial table that links patients to doctors for specific dates and reasons. It acts as the central hub for clinic activity.
- **billings**: Tracks the financial side of appointments, logging the total amount, amount paid, and bill date.

These tables are linked using **primary** and **foreign keys** to ensure data integrity.

---

## ⚙️ Getting Started

You can get this database running on your local MySQL server in a few simple steps:

### 1. Create the Database

```sql
CREATE DATABASE clinic_db;

