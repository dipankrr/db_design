# Comic-Con Parking System ERD

## Overview

This ERD represents a multi-zone parking system for a large event, supporting vehicle tracking, structured parking, reserved access, session lifecycle, and payments.

---

## Entities & Attributes

### Vehicles

* **vehicle_categories**: id (PK), name (UNIQUE), size_type
* **vehicles**: id (PK), license_plate (UNIQUE), vehicle_category_id (FK), brand, model, color

### Access Control

* **access_categories**: id (PK), name (UNIQUE)

### Parking Structure

* **parking_zones**: id (PK), name, level
* **spot_categories**: id (PK), name (UNIQUE)
* **parking_spots**: id (PK), zone_id (FK), spot_category_id (FK), spot_code, is_active

### Mapping

* **spot_access**: spot_id (FK), access_category_id (FK), UNIQUE (spot_id, access_category_id)

### Sessions & Tickets

* **parking_sessions**: id (PK), vehicle_id (FK), spot_id (FK), access_category_id (FK), entry_time, exit_time, status
* **parking_tickets**: id (PK), session_id (FK), ticket_number (UNIQUE), issued_at

### Payments & Pricing

* **payments**: id (PK), session_id (FK), amount, payment_time, payment_method, payment_status
* **pricing_rules**: id (PK), vehicle_category_id (FK), spot_category_id (FK), access_category_id (FK), hourly_rate, flat_rate

---

## Relationships

* vehicles.vehicle_category_id → vehicle_categories.id

* parking_spots.zone_id → parking_zones.id

* parking_spots.spot_category_id → spot_categories.id

* spot_access.spot_id → parking_spots.id

* spot_access.access_category_id → access_categories.id

* parking_sessions.vehicle_id → vehicles.id

* parking_sessions.spot_id → parking_spots.id

* parking_sessions.access_category_id → access_categories.id

* parking_tickets.session_id → parking_sessions.id

* payments.session_id → parking_sessions.id

* pricing_rules.vehicle_category_id → vehicle_categories.id

* pricing_rules.spot_category_id → spot_categories.id

* pricing_rules.access_category_id → access_categories.id

---

## Notes

* A vehicle can have multiple parking sessions
* Parking spots are reusable across sessions
* Reserved access is handled via mapping (`spot_access`)
* Availability is derived from active sessions (`exit_time IS NULL`)
