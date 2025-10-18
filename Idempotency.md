# Idempotency in Distributed Systems
- In mathematics, an operation is idempotent if applying it multiple times produces the same result as it applying once.
- Idempotency is a property of certain operations where by executing the same operation multiple times produces the same result as executing once.

- ## Need for Idempotency
	- Distributed systems often require fault tolerance to ensure high availability. When a network issue causes a timeout or an error, the client might retry the request.
	- If the system handles retries without idempotency, every retry could change the system's state unpredictably.

- ## Strategies to implement Idempotency
	1. **Unique Request Identifier**
		- One of the simplest techniques to achieve idempotency is by attaching a unique identifier, often called a idempotency key to each request.
		- When client makes a request it generates a uniqueID, that the server uses to track the request. If the server receives a request with same ID later, it knows it's a duplicate and discards it.
	2. **Database Design Adjustments ( Upsert Operations )**
	3. **Idempotency in Messaging systems** - In a messaging system, we can enforce idempotency by storing a log of processed message IDs and checking against it for every incoming message.
	4. **Idempotency in HTTP Methods**
		- GET, PUT, DELETE -> These are idempotent methods.
		- POST -> Non-idempotent method.

- ## Challenges
	- **Performance Overhead** - Storing idempotency keys or checking for duplicate operations can add overhead and increase the overall latency.
	- **State Management** - Idempotency often requires maintaining state, which can be challenging in stateless architectures.
	- **Distributed Systems** - Ensuring idempotency across distributed systems can be challenging and may require distributed locking or consensus algorithms.
	- **Time Window** - How long should idempotency guarantees be maintained.
	- **Database Constraints** - Not all operations are idempotent by default, unique constraints or upsert logic may necessary to avoid duplication.
