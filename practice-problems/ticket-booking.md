
# 🎟️ Design a Ticket Booking Site (Ticketmaster-like Service)

## 📌 Problem Statement
Design a Ticketmaster-like service that allows users to discover and purchase tickets for concerts, sporting events, theater shows, and other live entertainment.

---

## ✅ Functional Requirements
- Users should be able to view available events.
- Users should be able to search for events.
- Users should be able to book tickets for events.

---

## 📈 System Scale
- **100M** daily users  
- **100K** events per day

---

## ⚙️ Non-Functional Requirements
1. Strong consistency for critical operations (especially bookings).
2. High availability for read operations. Temporary inconsistencies in event listings are acceptable.
3. Low latency for search operations (≈ 150–200 ms).
4. Low latency for booking operations (≈ 100–150 ms).
5. High scalability to handle increasing traffic and peak loads.

---

## 🧩 Core Entities

### 🗓️ Event
| Field            | Description |
|------------------|-------------|
| eventId          | Unique identifier for the event |
| eventDate        | Date and time of the event |
| ticketsAvailable | Number of tickets remaining |
| performers       | Artists / teams performing |
| eventDetails     | Description and metadata |

---

### 🎫 Booking
| Field      | Description |
|-----------|-------------|
| bookingId | Unique identifier for the booking |
| eventId   | Associated event |
| userId    | User who made the booking |
| bookedOn  | Timestamp of booking |

---

### 👤 User
| Field     | Description |
|----------|-------------|
| userId   | Unique user identifier |
| userInfo | User profile information |

---

## 🔌 API Routes

### Get Events
**Description :** Fetch all events (paginated)
**PATH** : **GET** /events?page=1&limit=10
**Query Parameters:**
- `page` (default: 1)
- `limit` (default: 10)

**Response:**
- `200 OK → []events`

### Search Events
**Description :** Search events by keyword (paginated)
**PATH** : **GET** /events?searchText={searchText}&page=1&limit=10
**Query Parameters:**
- `searchText`
- `page`
- `limit`

**Response:**
- `200 OK → []events`

### Book Tickets
**Description :** Book the tickets for the event

**Request Body:**
```json
{
  "userId": "string (derived from authentication)",
  "eventId": "string"
}
```

**Response**
```json
{
	"booking Details" : "bookingDetails"
}
```

---

### 🏗️ High-Level Design
![Ticket Booking HLD](https://raw.githubusercontent.com/Charan-1111/images/refs/heads/main/ticket-booking.png)

### Component Overview
### **User**
-   End user accessing the system via web or mobile.
-   Performs event discovery, search, and ticket booking.
### **CDN**
-   Serves static assets (UI, images).
-   Reduces latency and load on backend services.
### **API Gateway**
-   Entry point for all client requests.
-   Responsibilities:
    -   Authentication & authorization
    -   Rate limiting
    -   Request routing
    -   Idempotency key validation for booking requests
### **Load Balancer**
-   Distributes traffic across multiple service instances.
-   Ensures horizontal scalability and fault tolerance.
### **Ticket Service**
-   Handles:
    -   Event listing
    -   Event details
    -   Search queries
-   Reads data from:
    -   **Redis Read Cache** (fast reads)
    -   **ElasticSearch** (search use cases)
    -   **Read replicas** of the database (fallback)
### **ElasticSearch**
-   Stores indexed event data for full-text search.
-   Optimized for low-latency search queries.
### **Read Cache (Redis)**
-   Caches frequently accessed event data.
-   Reduces database read load.
-   Updated or invalidated when bookings occur.
### **Booking Service**
-   Handles the full booking lifecycle.
-   Responsible for:
    -   Seat locking
    -   Payment coordination
    -   Booking confirmation
    -   Cache invalidation
### **Seat Lock Cache (Redis)**
-   Temporarily locks seats during booking.
-   Uses TTL-based locks to prevent double booking.
### **Payment Service (External)**
-   Processes user payments.
-   Booking is finalized only after successful payment.
### **Database**
-   Source of truth.
-   **Primary DB**: Handles all writes (bookings, seat updates).
-   **Read Replicas**: Serve read-heavy traffic.
---
### 🔄 Request Flow

### **Event Listing / Search Flow**
1.  User sends request → API Gateway.
2.  API Gateway authenticates and routes request.   
3.  Ticket Service:
    -   Checks Redis Read Cache.
    -   On cache miss, fetches from DB read replicas.
    -   Search requests go to ElasticSearch.
4.  Response is returned to the user.
5.  Data is cached for future reads.
### **Booking Flow**
1.  User initiates booking → `POST /events/book` with **Idempotency-Key**.
2.  API Gateway validates idempotency and forwards request.
3.  Booking Service performs:
    -   **Step 1:** Lock seat in Redis
        `SET seat:{seatId} userId NX EX 300` 
    -   **Step 2:** Call Payment Service.
    -   **Step 3:** On success, write booking to Primary DB.
4.  Booking Service:
    -   Invalidates event and seat caches.
    -   Releases seat lock.
5.  Booking confirmation is returned to the user.
---
## 🧹 Expiration & Cleanup
### **Seat Lock Expiration**
-   Seat locks are stored in Redis with TTL (2–5 minutes).
-   If:
    -   User abandons booking
    -   Service crashes
    -   Payment times out  
        → Redis automatically releases the lock.
### **Payment Failure Handling**
-   If payment fails:
    -   Seat lock is explicitly released.
    -   Booking is not persisted.
### **Cache Cleanup**
-   On successful booking:
    -   `ticketsAvailable`
    -   `seatStatus`
-   Are invalidated or updated in Redis.
-   Ensures fresh data for subsequent reads.
### **Idempotency Cleanup**
-   Idempotency keys stored in Redis with TTL.
-   Prevents duplicate bookings due to retries.
-   Auto-expires after safe duration.
---
## ⚖️ Consistency & Trade-offs
### **Strong Consistency (Where It Matters)**
-   Booking operations:
    -   Seat locking
    -   Payment confirmation
    -   Booking persistence
-   Always go through:
    -   Redis locks
    -   Primary DB writes
✅ Guarantees **no double booking**.
### **Eventual Consistency (Where Acceptable)**
-   Event listings
-   Search results
-   Cached event data
