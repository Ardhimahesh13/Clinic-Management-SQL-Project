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

Markdown

2.  **Use the Database**
    ```sql
    USE clinic_db;
    ```
3.  **Run the Script**

    Execute the `health_MYSQL_PRoject.sql` file. This will create all tables and insert the sample data.

## 📊 Analytical Queries & Insights
This section includes SQL queries that answer key business questions from the database.

### 🔎 Find a Patient's Complete Appointment History
```sql
-- Finds all appointments for Amit Patel
SELECT
    p.first_name, p.last_name,
    d.first_name AS doctor_first_name, d.speciality,
    a.appointment_date, a.reason
FROM appointments a
JOIN patients p ON a.patient_id = p.patient_id
JOIN doctors d ON a.doctor_id = d.doctor_id
WHERE p.first_name = 'Amit' AND p.last_name = 'Patel';

### 💸 Calculate Revenue and Performance
```sql
--- Shows total revenue per doctor
SELECT
    d.first_name, d.last_name, d.speciality,
    SUM(b.total_amount) AS total_revenue
FROM billings b
JOIN appointments a ON b.appointment_id = a.appointment_id
JOIN doctors d ON a.doctor_id = d.doctor_id
GROUP BY d.doctor_id
ORDER BY total_revenue DESC;
