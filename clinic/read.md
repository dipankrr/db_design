# Clinic Appointment and Diagnostics Platform – ERD

## Overview

This project models a clinic system that manages:

* Patients and doctors
* Appointments and consultations
* Diagnostic tests and reports
* Payments and medical history

The design focuses on a **clear real-world workflow** while remaining simple and scalable.

---

## System Flow

**Patient → Appointment → Consultation → Tests → Reports → Payment**

Additional scenarios handled:

* Walk-in consultations (no appointment)
* Direct test orders (without consultation)
* Appointments that do not result in consultations

---

## Key Design Decisions

### 1. Patients and Doctors

* Separate `patients` and `doctors` tables are used
* Keeps the model simple and easy to understand
* Doctors can have multiple specialties

---

### 2. Doctor Specialties

* Stored in `specialties`
* Many-to-many relationship via `doctor_specialties`

---

### 3. Appointment vs Consultation

* **Appointments** represent scheduled bookings
* **Consultations** represent actual visits

Key points:

* One appointment → zero or one consultation
* Consultations can exist without appointments (walk-ins)

---

### 4. Diagnostics System

* Tests are structured using:

  * `test_orders`
  * `test_order_items`
  * `test_types`

* Supports:

  * Multiple tests in a single order
  * Tests linked to consultations
  * Direct test orders without consultation

---

### 5. Reports

* Each test item generates a report
* Reports are linked to `test_order_items`

---

### 6. Payments

* Payments are linked to `consultations`
* Represents charges for actual services provided

---

### 7. Medical History

Medical history is handled through:

* `consultations` → visit history
* `patient_conditions` → chronic conditions
* `patient_allergies` → allergies

---

## Key Relationships

* One patient → many appointments
* One doctor → many appointments
* One appointment → zero or one consultation
* One consultation → many test orders
* One test order → many test items
* One test item → one report
* One patient → many medical conditions and allergies

---

## Notes

* The design clearly separates **appointments (intent)** from **consultations (actual visits)**
* Supports real-world edge cases like walk-ins and direct tests
* Avoids overengineering while maintaining scalability

---

## Submission

The ER diagram is created using **Eraser syntax** and designed for clarity and readability.

---
