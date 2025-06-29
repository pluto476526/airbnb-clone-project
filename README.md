## Summary of Overview and Tech Stack

### Overview

The Airbnb Clone backend replicates key features of the Airbnb platform, focusing on user management, property listings, booking flows, payment processing, and reviews. It aims to provide a secure, scalable, and well-documented API using REST and GraphQL, with performance enhancements such as caching and indexing. The system supports both hosts and guests, ensuring smooth interactions and efficient data handling.

### Technology Stack

* **Django** – Core web framework for backend development.
* **Django REST Framework** – For building RESTful APIs.
* **GraphQL** – Enables flexible and precise data queries.
* **PostgreSQL** – Reliable relational database system.
* **Celery** – Handles background tasks asynchronously.
* **Redis** – Used for caching and task queue management.
* **Docker** – Ensures consistent development and deployment.
* **CI/CD Pipelines** – Automates testing and deployment workflows.


## Team Roles

A well-structured development team is essential for delivering a scalable and maintainable Airbnb Clone backend. Below are the key roles, drawn from both the project overview and industry standards like those outlined by ITRexGroup:

### Backend Developer

Responsible for implementing the core logic of the application, including building API endpoints, managing business rules, and integrating third-party services. They also handle authentication, data validation, and performance tuning.

### Database Administrator (DBA)

Designs, implements, and maintains the database architecture. Their tasks include schema creation, indexing strategies, data integrity enforcement, backup planning, and performance optimization to ensure high availability and data security.

### DevOps Engineer

Oversees infrastructure, deployment pipelines, and system monitoring. They automate testing and deployment (CI/CD), manage Docker environments, and ensure the system runs reliably at scale with tools like Kubernetes, logging, and monitoring services.

### QA Engineer

Ensures the application meets functional and non-functional requirements through systematic testing. They write and execute test cases, manage automated testing suites, and verify that APIs, database logic, and integrations behave as expected.


## Database Design

A well-structured relational database is crucial for managing the core entities of the Airbnb Clone. Below are the primary entities, their key fields, and the relationships between them.

### Users

**Key Fields**:

* `user_id` (Primary Key, UUID)
* `first_name` (String)
* `email` (Unique, String)
* `password_hash` (String)
* `role` (Enum: guest, host, admin)

**Description**:
Users can act as guests, hosts, or administrators. A host can list multiple properties, and a guest can make multiple bookings and write reviews.

---

### Properties

**Key Fields**:

* `property_id` (Primary Key, UUID)
* `host_id` (Foreign Key → Users)
* `title` (String)
* `location` (String)
* `price_per_night` (Decimal)

**Description**:
Each property is owned by a host (user) and can be booked by multiple guests. Properties can also receive multiple reviews.

---

### Bookings

**Key Fields**:

* `booking_id` (Primary Key, UUID)
* `guest_id` (Foreign Key → Users)
* `property_id` (Foreign Key → Properties)
* `check_in` (Date)
* `check_out` (Date)

**Description**:
Each booking is made by a guest for a specific property. One property can have many bookings over time.

---

### Payments

**Key Fields**:

* `payment_id` (Primary Key, UUID)
* `booking_id` (Foreign Key → Bookings)
* `amount` (Decimal)
* `status` (Enum: pending, completed, failed)
* `payment_date` (DateTime)

**Description**:
Each payment is linked to a specific booking and captures the transaction details for that booking.

---

### Reviews

**Key Fields**:

* `review_id` (Primary Key, UUID)
* `guest_id` (Foreign Key → Users)
* `property_id` (Foreign Key → Properties)
* `rating` (Integer 1–5)
* `comment` (Text)

**Description**:
Reviews are written by guests after completing a booking. A guest can write one review per property per booking.

---

### Entity Relationships Summary

* A **User** (host) can have **many Properties**.
* A **User** (guest) can make **many Bookings**.
* A **Property** can receive **many Bookings** and **many Reviews**.
* A **Booking** has **one Payment**.
* A **Review** links a **guest** to a **property** with feedback and rating.

