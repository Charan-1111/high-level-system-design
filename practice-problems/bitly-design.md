
# Design a URL Shortener (Bit.ly-like Service)

## 📌 Problem Statement
Design a Bit.ly–like service that converts long URLs into short, manageable URLs.

---

### ✅ Functional Requirements
- Users should be able to submit a **long URL** and receive a **shortened URL**.
- Users can optionally provide:
  - A **custom alias**
  - An **expiration time** for the shortened URL.
- Users should be able to access the original URL using the shortened URL.

---

### 📈 System Scale
- **1 Billion** shortened URLs stored
- **100 Million DAU (Daily Active Users)**

---

### ⚙️ Non-Functional Requirements
1. **Low Latency**  
   - Redirects should happen in under **100 ms**.
2. **High Availability**  
   - The system is **read-heavy**.  
   - Occasional wrong redirections are acceptable.
3. **High Scalability**  
   - Should scale **horizontally** as traffic grows.
4. **Consistency Model**  
   - Eventual consistency is acceptable to ensure availability.
5. **Uniqueness**  
   - Each short URL must map to **exactly one** long URL.

---

### 🧩 Core Entities

### URLs Table
| Field       | Type                 | Description |
|------------|----------------------|-------------|
| shortUrl   | string               | Generated short URL |
| longUrl    | string               | Original long URL |
| alias      | string               | Custom alias (optional) |
| expiryTime | timestamp / epoch    | Expiration time |
| userId     | string               | Owner of the URL |

### Users Table
| Field       | Type   | Description |
|------------|--------|-------------|
| userId     | string | Unique user identifier |
| userDetails| user   | User metadata |

---

### 🔌 API Routes

### Create Short URL
**POST** `/urls`  
**Response:** `200 OK`
#### Request Body
```json
{
  "longUrl": "string",
  "alias": "string",
  "expiryTime": "timestamp"
}

### Response
{
    "shortUrl" : "shortUrl"
}
```
### Redirect Short URL
**GET** `/urls/{shortUrl}`
**Response:** 302 Found

---

### 🏗️ High-Level Design
### Component Overview
-  **CDN**
	-   Serves requests from nearest geo-location
	-   Caches hot redirects using **TTL-based eviction**
-   **API Gateway**
    -   Authentication
    -   Rate limiting
    -   Request routing (read vs write)
    -   Handles HTTP redirection responses
-   **URL Shorten Write Service**
    -   Handles `POST /urls`
    -   Generates unique short URLs using:
        -   `hash(longUrl + timestamp)`
        -   Base62 encoding
        -   First 8 characters
    -   Persists mappings to the database
-   **Load Balancer**
    -   Distributes read traffic across multiple read service instances
-   **URL Shorten Read Service**
    -   Handles `GET /urls/{shortUrl}`
    -   Stateless and horizontally scalable
    -   Implements cache-first lookup
-   **Cache Service (Redis / Memcached)**
    -   Stores `{ shortUrl → longUrl }` mappings
    -   Uses **LRU eviction policy**
    -   Read-through cache pattern:
        -   Cache hit → redirect
        -   Cache miss → fetch from DB, update cache, redirect
-   **Database**
    -   Stores all URL mappings
    -   Supports high write and read throughput
    -   Periodic cleanup of expired URLs via background job / cron
---
### 🔄 Request Flow
### URL Creation Flow

1.  User sends `POST /urls`
2.  Request passes through CDN → API Gateway
3.  Write service generates a unique short URL
4.  Mapping is stored in the database
5.  Short URL is returned to the user

### URL Redirection Flow
1.  User accesses `GET /urls/{shortUrl}`
2.  Request passes through CDN → API Gateway → Load Balancer
3.  Read service checks cache:
    -   **Cache hit** → redirect immediately
    -   **Cache miss** → fetch from DB, update cache, redirect
4.  If URL is expired → return `404 Not Found`

---
## 🧹 Expiration & Cleanup
-   URLs with `expiryTime < now` return `404`
-   Background cron job periodically deletes expired URLs
-   Cache entries expire automatically via TTL
---
## ⚖️ Consistency & Trade-offs
-   Eventual consistency between cache and database
-   Prioritizes availability and low latency over strict consistency
-   Rare cache inconsistencies are acceptable
