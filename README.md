# airbnb-clone-project

## Team Roles
*(Note: As the sole contributor, you are responsible for fulfilling all these roles and responsibilities.)*

| Role | Responsibility in the Project |
| :--- | :--- |
| **Business Analyst (BA)** | Define and translate all business needs into technical requirements. |
| **Product Owner (PO)** | Maintain the project vision, define the product strategy, and manage the feature backlog. |
| **Project Manager (PM)** | Plan sprints, manage timelines, and ensure all work stays on budget (time) and scope. |
| **Front-end Developer** | Build the user interface and ensure a consistent, smooth user experience. |
| **Back-end Developer** | Develop the core business logic, handle server-side operations, and manage the database. |
| **Quality Assurance (QA) Engineer** | Design and execute tests (manual and automated) to ensure the application meets all requirements and is free of defects. |

---
## Technology Stack

| Technology | Purpose in the Project |
| :--- | :--- |
| **Django** | A high-level Python web framework used for quickly building the secure, scalable, and maintainable backend, primarily handling the application's business logic and serving the API. |
| **PostgreSQL** | The robust, object-relational database used to store all structured project data, including users, properties, bookings, and reviews, ensuring data integrity and reliability. |
| **GraphQL** | A query language for your API and a server-side runtime for executing those queries. It allows the frontend to request **exactly the data it needs**, optimizing data fetching and performance. |

---
## Database Design

The database will be structured around key entities that represent the core data of the clone application.

| Entity | Important Fields (3-5) | Relationships |
| :--- | :--- | :--- |
| **Users** | `id`, `email`, `password_hash`, `first_name`, `is_host` | A **User** can have multiple **Properties** (if `is_host` is true), multiple **Bookings**, and multiple **Reviews**. |
| **Properties** | `id`, `host_id` (FK to Users), `title`, `description`, `price_per_night`, `location` | A **Property** belongs to one **User** (Host) and can have multiple **Bookings** and multiple **Reviews**. |
| **Bookings** | `id`, `user_id` (FK to Users), `property_id` (FK to Properties), `check_in_date`, `check_out_date`, `total_price` | A **Booking** belongs to one **User** (Guest) and one **Property**. |
| **Reviews** | `id`, `property_id` (FK to Properties), `user_id` (FK to Users), `rating`, `comment`, `created_at` | A **Review** is given by one **User** (Guest) and is associated with one **Property**. |
| **Payments** | `id`, `booking_id` (FK to Bookings), `amount`, `status`, `transaction_id` | A **Payment** belongs to a single **Booking**. |

---
## Feature Breakdown

#### User Management
This feature handles all aspects of user authentication and account settings, including sign-up, login, profile updates, and role assignment (guest or host). It establishes a secure identity foundation necessary for all other interactions like booking and listing.

#### Property Management
This feature allows hosts to create, read, update, and delete their property listings. It includes capturing key details like location, pricing, amenities, and descriptions, which is the core content that guests interact with to find accommodation.

#### Booking System
This is the transactional core of the application, allowing guests to search for properties, check availability against a calendar, and initiate a reservation for a specific date range. It ensures properties are not double-booked and calculates the total cost.

#### Review System
This feature allows guests to leave public ratings and written feedback on properties after their stay. It builds trust within the community, providing social proof for hosts and critical information for future guests.

---
## API Security

Securing the backend APIs is paramount to protecting both the business and its users.

The following key security measures will be implemented:

* **Authentication (Who you are):** Users will be required to prove their identity (e.g., using **Token-Based Authentication**) for access to protected endpoints.
* **Authorization (What you can do):** Role-based permissions will ensure users can only access data they are entitled to (e.g., a guest cannot update a property, and a user can only view their own bookings).
* **Rate Limiting:** This technique restricts the number of requests a user or IP address can make to the API in a given time frame, preventing Denial-of-Service (DoS) attacks and misuse of resources.

Security is crucial for:
* **Protecting User Data:** Strong authentication and authorization prevent unauthorized access to sensitive personal information and account details.
* **Securing Payments:** Protecting the payment gateway integration and transaction data against interception and fraud, which is vital for maintaining user trust and legal compliance.
* **Maintaining Platform Integrity:** Rate limiting and authorization prevent malicious users from spamming listings, making fraudulent bookings, or overloading the server, ensuring a reliable service for all users.

---
## CI/CD Pipeline

A **CI/CD Pipeline** is an automated set of practices that reliably and repeatedly build, test, and deploy code changes to production or staging environments.

**CI/CD Importance:**
* **Continuous Integration (CI):** Automates merging code changes and running tests, helping to **catch bugs early** and ensure all parts of the code work together before deployment.
* **Continuous Delivery (CD):** Automates the deployment process, allowing for **faster, more frequent, and less error-prone releases** to users. This reduces manual effort and increases the stability of the final product.

**Potential Tools:**
* **GitHub Actions:** A flexible tool integrated directly into the repository for defining and running CI/CD workflows (e.g., running tests after every commit and deploying to a server).
* **Docker:** A containerization tool used to **package the application and all its dependencies** into a portable image, ensuring the application runs consistently across all environments.
* **Heroku/AWS/Vercel:** Cloud platforms that the CD portion of the pipeline will deploy the application containers to.
