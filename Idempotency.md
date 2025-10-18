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
		- 
