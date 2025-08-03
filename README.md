# Clinic-Management-SQL-Project
Welcome to the Clinic Management System project!
This repository contains a complete SQL script to create, populate, and query a database for a small clinic. It's designed to manage patient information, doctor schedules, appointments, and billing efficiently.

🧩 Database Design
The core of this project is the clinic_db database, which organizes information across four connected tables:

doctors: Stores a record for each doctor, including their name and speciality.

patients: Contains essential patient details like name, date of birth, and phone number.

appointments: A crucial table that links patients to doctors for specific dates and reasons.

billings: Tracks the financial side of appointments—total amount, amount paid, and bill date.

🔗 These tables are linked using primary and foreign keys to ensure data integrity.

🚀 Getting Started
You can get this database running on your local MySQL server with just a few simple steps:

Create the Database

sql
Copy
Edit
CREATE DATABASE clinic_db;
Use the Database

sql
Copy
Edit
USE clinic_db;
Run the Script
Execute the entire health_MYSQL_PRoject.sql file.
This will create all tables and populate them with sample data.

📊 Analytical Queries & Insights
The real value of this project lies in the business insights you can gain through SQL queries.

🔍 1. Find a Patient's Complete Appointment History
sql
Copy
Edit
-- Finds all appointments for Amit Patel
SELECT
    p.first_name, p.last_name,
    d.first_name AS doctor_first_name, d.speciality,
    a.appointment_date, a.reason
FROM appointments a
JOIN patients p ON a.patient_id = p.patient_id
JOIN doctors d ON a.doctor_id = d.doctor_id
WHERE p.first_name = 'Amit' AND p.last_name = 'Patel';
💰 2. Calculate Revenue and Doctor Performance
sql
Copy
Edit
-- Shows total revenue per doctor
SELECT
    d.first_name, d.last_name, d.speciality,
    SUM(b.total_amount) AS total_revenue
FROM billings b
JOIN appointments a ON b.appointment_id = a.appointment_id
JOIN doctors d ON a.doctor_id = d.doctor_id
GROUP BY d.doctor_id
ORDER BY total_revenue DESC;
🧾 3. Manage Outstanding Balances
sql
Copy
Edit
-- Identifies patients with an outstanding balance
SELECT
    p.first_name, p.last_name, p.phone_number,
    b.total_amount, b.amount_paid,
    (b.total_amount - b.amount_paid) AS outstanding_balance
FROM billings b
JOIN appointments a ON b.appointment_id = a.appointment_id
JOIN patients p ON a.patient_id = p.patient_id
WHERE b.total_amount > b.amount_paid;
🩺 4. Identify the Busiest Doctors and Services
sql
Copy
Edit
-- Finds the doctor with the most appointments
SELECT
    d.first_name, d.last_name, d.speciality,
    COUNT(a.appointment_id) AS no_of_appointments
FROM appointments a
JOIN doctors d ON d.doctor_id = a.doctor_id
GROUP BY d.doctor_id
ORDER BY no_of_appointments DESC
LIMIT 1;
sql
Copy
Edit
-- Finds the most common reasons for visits
SELECT
    reason,
    COUNT(appointment_id) AS number_of_visits
FROM appointments
GROUP BY reason
ORDER BY number_of_visits DESC;
