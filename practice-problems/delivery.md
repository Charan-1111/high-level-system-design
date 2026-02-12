
# 🛵 Design a Local Delivery Service (like Gopuff)

Gopuff delivers convenience-store items via rapid delivery from micro-fulfillment centers.

---

# 1. Functional Requirements

## 1.1 Item Availability
- Customers should be able to query available items deliverable within **1 hour**.
- Availability should be based on user location and nearby fulfillment centers.
- Results should support pagination.

## 1.2 Order Placement
- Customers should be able to:
  - Add multiple items to an order.
  - Place an order.
  - Receive order confirmation.

---

# 2. Non-Functional Requirements

## 2.1 High Availability
- System must remain highly available.
- Availability checks may tolerate slightly stale inventory data (eventual consistency).

## 2.2 Low Latency
- Availability API latency < **100ms**.
- Order placement must also be low latency.

## 2.3 Consistency
- Availability → **Eventual Consistency**
- Order Placement → **Strong Consistency**

## 2.4 Scalability
- System should scale horizontally as traffic increases.

---

# 3. Scale Assumptions

| Metric | Value |
|--------|-------|
| Items in catalog | 100,000 |
| Fulfillment centers | 10,000 |
| Orders per day | 1,000,000 (~12 orders/sec avg, higher at peak) |

---

# 4. Core Entities

## 4.1 Item (Catalog)

| Field | Description |
|-------|------------|
| itemId | Unique identifier |
| name | Item name |
| category | Category |
| price | Item price |
| metadata | Weight, description, etc |

> Catalog is global. Inventory is maintained per center.

---

## 4.2 Fulfillment Center

| Field | Description |
|-------|------------|
| centerId | Unique identifier |
| latitude | Geographic latitude |
| longitude | Geographic longitude |
| capacity | Storage capacity |
| operatingHours | Operating hours |

---

## 4.3 Inventory

Represents stock of an item at a specific fulfillment center.

| Field | Description |
|-------|------------|
| itemId | Item identifier |
| centerId | Fulfillment center identifier |
| availableQuantity | Available stock |
| reservedQuantity | Reserved stock |

**Primary Key:** `(itemId, centerId)`

---

## 4.4 User

| Field | Description |
|-------|------------|
| userId | Unique identifier |
| name | User name |
| address | Delivery address |
| latitude | User latitude |
| longitude | User longitude |

---

## 4.5 Order

| Field | Description |
|-------|------------|
| orderId | Unique identifier |
| userId | User placing order |
| centerId | Assigned fulfillment center |
| status | CREATED / CONFIRMED / DISPATCHED / DELIVERED / CANCELLED |
| totalAmount | Order total |
| createdAt | Timestamp |

---

## 4.6 OrderItem

| Field | Description |
|-------|------------|
| orderId | Associated order |
| itemId | Ordered item |
| quantity | Quantity ordered |
| price | Price at time of order |

**Primary Key:** `(orderId, itemId)`

---

# 5. API Design

## 5.1 Check Item Availability

```
GET /items/availability?lat=<latitude>&long=<longitude>&page=1&limit=10
```

### Response (200 OK)

```json
[
  {
    "itemId": "123",
    "name": "Coke",
    "price": 40,
    "availableQuantity": 12,
    "centerId": "C45",
    "estimatedDeliveryTime": "45 mins"
  }
]
```

---

## 5.2 Place Order

```
POST /orders
```

### Request Body

```json
{
  "items": [
    {
      "itemId": "123",
      "quantity": 2
    }
  ],
  "lat": "19.0760",
  "long": "72.8777"
}
```

> `customerId` is derived from authentication token.

### Response (200 OK)

```json
{
  "orderId": "ORD789",
  "status": "CONFIRMED",
  "estimatedDeliveryTime": "50 mins"
}
```

---

# 6. High-Level Architecture

## Components

1. **API Gateway**
   - Authentication
   - Rate limiting
   - Routing

2. **Catalog Service**
   - Manages item metadata

3. **Inventory Service**
   - Maintains stock per center
   - Handles reservation logic

4. **Order Service**
   - Handles order creation
   - Ensures strong consistency

5. **Location Service**
   - Finds nearest fulfillment centers
   - Uses geo-indexing (PostGIS / Redis GEO / ElasticSearch)

6. **Fulfillment Service**
   - Assigns delivery partner
   - Tracks delivery status

---

# 7. Data Storage Choices

| Component | Suggested Storage |
|-----------|-------------------|
| Catalog | SQL / NoSQL |
| Inventory | Strongly consistent DB (PostgreSQL / CockroachDB) |
| Orders | SQL with transactions |
| Availability Cache | Redis |
| Geo Search | PostGIS / ElasticSearch / Redis GEO |

---

# 8. Consistency Strategy

## Availability (Eventual Consistency)
- Inventory updates published via event stream (Kafka).
- Availability cached in Redis.
- Slight staleness allowed.

## Order Placement (Strong Consistency)
Within a transaction:
1. Lock inventory row (`SELECT ... FOR UPDATE`)
2. Validate availability
3. Deduct quantity
4. Create order
5. Commit transaction

---

# 9. Optimizations for <100ms Availability

- Precompute nearest centers using geospatial indexing.
- Cache popular items per area.
- Store hot inventory in Redis.
- Use read replicas.
- Limit response size with pagination.

---

# 10. Scaling Strategy

- Horizontally scale stateless services.
- Partition inventory by `centerId`.
- Shard orders by `orderId`.
- Use message queues for async workflows (dispatch, notifications).


# 11 . High Level Design
![HLD](https://raw.githubusercontent.com/Charan-1111/images/refs/heads/main/delivery.png)
