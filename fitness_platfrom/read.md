# Database Schema Documentation

This document outlines the database schema for a Fitness Influencer Coaching Platform.  
The system supports online coaching where trainers manage clients, sell plans, schedule sessions, and track client progress.

---

## Tables Overview

### 1. clients
Stores primary information about the platform's clients.

- id (UUID, PK): Unique identifier for the client.
- name (string, NOT NULL): Full name.
- phone (string, UNIQUE): Phone number.
- email (string, UNIQUE): Email address.
- created_at (timestamp): Account creation time.

---

### 2. trainers
Stores information about trainers/coaches.

- id (UUID, PK): Unique identifier for the trainer.
- name (string, NOT NULL): Trainer name.
- bio (text): Description or expertise.
- experience (int): Years of experience.
- active (boolean): Availability status.
- created_at (timestamp): Account creation time.

---

### 3. plans
Defines fitness programs offered on the platform.

- id (UUID, PK): Unique identifier for the plan.
- name (string): Plan name (e.g., Weight Loss).
- description (text): Plan details.
- is_group_plan (boolean): Group or individual plan.
- created_at (timestamp): Creation time.

---

### 4. plan_variants
Represents variations of a plan.

- id (UUID, PK): Unique identifier.
- plan_id (UUID, FK): References plans.
- sessions_per_week (int): Weekly sessions count.
- is_offline (boolean): Online/offline mode.
- duration_weeks (int): Duration of plan.
- created_at (timestamp): Creation time.

---

### 5. subscriptions
Tracks which client subscribed to which plan.

- id (UUID, PK): Unique subscription ID.
- client_id (UUID, FK): References clients.
- trainer_id (UUID, FK): References trainers.
- variant_id (UUID, FK): References plan_variants.
- start_date (date): Subscription start date.
- end_date (date): Subscription end date.
- price (decimal): Paid amount.
- status (enum): active, completed, cancelled.
- created_at (timestamp): Creation time.

---

### 6. payments
Stores payment transactions.

- id (UUID, PK): Unique payment ID.
- subscription_id (UUID, FK): References subscriptions.
- amount (decimal): Paid amount.
- status (enum): success, failed, pending.
- method (enum): upi, card, cash.
- paid_at (timestamp): Payment time.

---

### 7. consultations
Stores one-time consultation bookings.

- id (UUID, PK): Unique consultation ID.
- client_id (UUID, FK): References clients.
- trainer_id (UUID, FK): References trainers.
- scheduled_at (timestamp): Scheduled time.
- status (enum): pending, completed, cancelled.
- notes (text): Optional notes.

---

### 8. sessions
Represents scheduled coaching sessions under a subscription.

- id (UUID, PK): Unique session ID.
- subscription_id (UUID, FK): References subscriptions.
- client_id (UUID, FK): References clients.
- meet_link (string): Online meeting link.
- scheduled_at (timestamp): Planned session time.
- started_at (timestamp): Actual start time.
- ended_at (timestamp): End time.
- status (enum): scheduled, completed, cancelled.

---

### 9. checkins
Tracks client progress over time.

- id (UUID, PK): Unique check-in ID.
- client_id (UUID, FK): References clients.
- subscription_id (UUID, FK): References subscriptions.
- weight (decimal): Recorded weight.
- body_fat (decimal): Body fat percentage.
- notes (text): Client notes.
- submitted_at (timestamp): Submission time.

---

### 10. trainer_notes
Stores trainer feedback on client progress.

- id (UUID, PK): Unique note ID.
- checkin_id (UUID, FK): References checkins.
- trainer_id (UUID, FK): References trainers.
- feedback (text): Trainer feedback.
- created_at (timestamp): Creation time.

---

### 11. diet_plans
Stores diet plans assigned to clients.

- id (UUID, PK): Unique diet plan ID.
- subscription_id (UUID, FK): References subscriptions.
- details (text): Diet plan content.
- calories (int): Daily calories.
- protein (int): Protein intake.
- carbs (int): Carbohydrates intake.
- fat (int): Fat intake.
- created_at (timestamp): Creation time.

---

### 12. workout_plans
Stores workout routines assigned to clients.

- id (UUID, PK): Unique workout plan ID.
- subscription_id (UUID, FK): References subscriptions.
- details (text): Workout plan content.
- created_at (timestamp): Creation time.

---

## Entity Relationships

- A trainer can manage multiple clients through subscriptions.
- A client can purchase multiple plans over time.
- A plan can have multiple variants and many clients can subscribe to them.
- Subscriptions connect clients, trainers, and plan variants.
- Payments are linked to subscriptions.
- Consultations are independent one-time interactions between client and trainer.
- Sessions are recurring events under a subscription.
- Check-ins track client progress over time and are not mixed with user data.
- Trainer notes provide feedback on check-ins.
- Diet and workout plans are assigned per subscription.

---