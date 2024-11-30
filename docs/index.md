# Welcome to Trade-Tix Docs

Trade-Tix: Don't waste your tickets.


&nbsp;





## How to run

To run the project locally, follow these steps:

&nbsp;


### Frontend

1. **Clone the repo**:
    ```
    git clone https://github.com/pravin-pk/TradeTix-frontend.git
    ```
2. **Start the Development Server**:
    ```
    npm run start
    ```

 &nbsp;


### Backend

1. **Clone the repo**:
    ```
    git clone https://github.com/pravin-pk/TradeTix-backend.git
    ```
2. **Move to k8s**:
    ```
    cd tradetix-backend/k8s
    ```
3. **Run the Docker command**:
    ```
    docker-compose up -d
    ```
4. **Move back to the main folder**:
    ```
    cd ..
    ```
5. **Run the app**:
    ```
    npm run dev
    ```

&nbsp;





## Project Structure

| File or Folder | Purpose                                |
|----------------|----------------------------------------|
| `controllers/` | Controller for the resource           |
| `middlewares/` | Auth Middleware                       |
| `models/`      | Domain Model                          |
| `providers/`   | External services                     |
| `routers/`     | Routing for resource                  |




&nbsp;
## Technology Stack
We agreed to use the following technology stack:

- **Node.j, Express, TypeScript**: Programming languag for backend.
- **Angular**: For the Frontend.
- **MongoDB**: For the Database.
- **GitHub**: For source code management.
- **MetaMask, SmartContract**: For crypto transaction.


&nbsp;

**Trade-Tix API Documentation**

The Trade-tix platform facilitates a secure and user-friendly marketplace for reselling concert tickets. The platform connects buyers, sellers, and admins, streamlining ticket transactions and event management.

---

### **Key Stakeholders:**

1. **Buyers:**
   * Browse and purchase tickets for available events.
   * Make payments via Razorpay or blockchain.
2. **Sellers:**
   * List tickets for events already on the platform.
   * Request the creation of new events if not listed.
3. **Admins:**
   * Oversee platform operations, ensuring smooth transactions and policy compliance.
   * Create events and manage event requests from sellers.
   * Earn a commission from transactions.

---

### **Stakeholder Goals Defined**

#### **1\. Admin Goals**

* As an admin, I want to **create and manage events** so buyers and sellers can interact seamlessly.
* As an admin, I want to **approve or reject seller event requests** so that the platform only features relevant and legitimate events.
* As an admin, I want to **earn a commission on transactions** so that the platform generates revenue.
* As an admin, I want to **monitor user transactions** so that the platform complies with policies and prevents fraud.
* As an admin, I want to **manage seller roles and listings** to ensure high-quality and authentic ticket sales.

---

#### **2\. Seller Goals**

* As a seller, I want to **list tickets for resale** so that I can monetize my unused or extra tickets.
* As a seller, I want to **set and update ticket prices** so that I can maximize profits based on demand.
* As a seller, I want to **request new events** so that I can list tickets for events not already on the platform.
* As a seller, I want to **manage my listings** so that I can update ticket availability and details as needed.
* As a seller, I want to **receive timely payments** for sold tickets to maintain trust and business continuity.

---

#### **3\. Buyer Goals**

* As a buyer, I want to **browse and filter events** so that I can easily find tickets for concerts of interest.
* As a buyer, I want to **purchase tickets securely** so that I can attend events without worrying about fraud.
* As a buyer, I want to **view event details and ticket prices** so that I can make informed purchasing decisions.
* As a buyer, I want to **track my purchase history** so that I can reference past transactions when needed.

---

### **Resources**

This section provides a detailed explanation of each resource in the system, its purpose, key attributes, and associated actions (CRUD operations). Each resource connects the stakeholders (Admin, Seller, Buyer) to the platform's functionality.

---

### **1\. Events**

#### **Purpose:**

Represents concerts or shows listed on the platform. Events can be created by admins or requested by sellers for approval.

#### **Key Attributes:**

* **name**: The title of the event (e.g., "Rock Fest 2024").
* **date**: The scheduled date of the event.
* **venue**: Location where the event is held.
* **performers**: List of artists or bands performing at the event.
* **categories**: Tags (e.g., "music", "rock").
* **isAvailable**: Whether the event is open for ticket listings.
* **validFrom / validTo**: The validity period for ticket sales.
* **createdBy / updatedBy**: References to the user who created or updated the event.

#### **Actions:**

* **GET `/events`: Fetch all available events (Buyers).**
* **POST `/events`: Create an event (Admins only).**
* **POST `/events/:id/tickets`: *Create new tickets for a specific event. (Sellers)***
* **GET `/events/:id`: *Fetch details of an event by its ID.***
* **GET `/events/:id/tickets`: *Retrieve all tickets associated with a specific event. (Buyers)***
* **PUT `/events/:id`: Update event details (Admins only).**
* **DELETE `/events/:id`: Remove an event (Admins only).**

---

### **2\. Tickets**

#### **Purpose:**

Represents individual tickets tied to specific events. Each ticket has an owner (Seller) and a seat assignment.

#### **Key Attributes:**

* **eventID:** Reference to the associated event.
* **ownerID:** The seller who owns the ticket.
* **seatNumber:** The assigned seat (optional).
* **createdBy / updatedBy:** References to the user who created or updated the ticket.

#### **Actions:**

* **GET `/tickets/:id/listings`: *Retrieve all listings of a specific ticket by its ID.***
* **POST `/tickets/:id/listing`: *Create a listing for a specific ticket by its ID.***
* **PUT `/tickets/:id`: Update ticket details (Sellers or Admins).**
* **DELETE `/tickets/:id`: Remove a ticket (Sellers or Admins).**

---

### **3\. Listings**

#### **Purpose:**

Represents tickets put up for resale by sellers. Each listing includes ticket details and price.

#### **Key Attributes:**

* **ticketID:** Reference to the ticket being listed.
* **price:** Sale price for the ticket.
* **status:** Whether the listing is "open" (available) or "closed" (sold or withdrawn).
* **createdBy / updatedBy:** References to the seller managing the listing.

#### **Actions:**

* **POST `/listings/:id/buy`: *Purchase the listed ticket by its ID.***
* **PUT `/listings/:id`: *Update the details of a ticket listing by its ID***
* **DELETE `/listings/:id`: *Delete a specific ticket listing by its ID.***

---

### **4\. Transactions**

#### **Purpose:**

Represents completed purchases where buyers buy tickets from sellers.

#### **Key Attributes:**

* **ticketID:** Reference to the ticket sold.
* **sellerID:** Reference to the seller of the ticket.
* **salePrice:** The final transaction amount.
* **createdBy / updatedBy:** References to users initiating and recording the transaction.

#### **Actions:**

* **GET `/transactions`: View all transactions (Buyers or Sellers).**
* **POST `/transactions`: Record a new transaction (Buyers).**

---

### **5\. Users**

#### **Purpose:**

Represents platform participants, including admins, buyers, and sellers. Users can authenticate and perform actions based on their roles.

#### **Key Attributes:**

* **username:** Unique identifier for the user.
* **password:** Encrypted user password.
* **role:** Either "admin", "seller", or "buyer".
* **tokens:** Array of authentication tokens for session management.
* **accountNumber / IFSCCode:** Seller's bank details for payouts.

#### **Actions:**

* **POST `/users`: Register a new user.**
* **GET `/users`: *Retrieve all users.***
* **POST `/users/login`: Authenticate a user and retrieve a token.**
* **GET `/users/:id`: *Fetch details of a user by their ID.***
* **PUT `/users/:id`: Update user details by their ID**
* **DELETE `/users/:id`: Remove a user account.**
* **POST `/users/logout`: logout a user**

---

### **Authentication**

* The platform uses **JWT (JSON Web Token)** for authentication.

---

### **Authorization**

* The platform implements two scopes for access control:
   1. **User Scope**: For Buyers and Sellers to perform actions related to tickets, listings, and their accounts.
   2. **Admin Scope**: For Admins to manage events, users, and platform-wide operations.

---









