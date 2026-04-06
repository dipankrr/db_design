## Database Design Overview

### Purpose

* Designed for an Instagram-based thrift + handmade store
* Supports both single-piece (thrift) and multi-piece (handmade) products

---

### Core Entities

* **customer** – user account data
* **address** – delivery addresses (linked to customer)
* **category** – product grouping
* **product** – base product info (type: thrift/handmade)
* **product_variant** – size, color, condition
* **inventory** – stock per variant
* **cart, cart_item** – pre-order flow
* **order** – main order record
* **order_item** – products inside an order
* **payment** – payment tracking
* **shipment** – delivery tracking
* **order_status_history** – status logs

---

### Key Relationships

* 1 customer → many orders
* 1 customer → many addresses
* 1 product → many variants
* 1 variant → 1 inventory
* 1 order → many order_items
* many products ↔ many orders (via order_item)
* 1 order → 1 payment
* 1 order → 1 shipment

---

### Important Design Decisions

* Use **product_variant** for size/color/condition
* Track stock at **variant level** (not product)
* Thrift items → stock = 1
* Handmade items → stock > 1
* Store **price + product details in order_item** (snapshot)
* Separate **payment** and **shipment** for flexibility
* Use **order_status_history** for tracking changes

---

### Outcome

* Normalized and clean structure
* Supports real-world order flow
* Scalable for future features
* Maintains historical accuracy
