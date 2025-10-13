# Caching
- Caching is a technique used to temporarily store copies of data in high-speed storage layers ( such as RAM ) to reduce the time taken to access data.
- The primary goal of caching is to improve system performance by storing frequently accessed data, reducing latency, offloading the main data store, and providing faster data retrieval.

- ## Benefits of Caching
	- **Improved Performance** - By storing frequently accessed data in a cache, the time required to retieve that data is significantly reduced.
	- **Reduced Load on Backend Systems** - Caching reduces the number of requests that need to processed by the backend, freeing up the resources for other operations.
	- **Increased Scalability** - Cache helps in handling a large number of read requests, making the system more scalable.
	- **Enhanced User Experience** - Faster response times lead to a better user experience, particularly for web and mobile applications.

- ## Types of Caching
	1. **In-Memory Cache**
		- In-memory caches store data in the main memory ( RAM ) for extremely fast access.
		- These caches are typically used for session management, storing frequently accesed objects, and as a front for databases.
		- Eg :- Redis, Memcached.
	2. **Distributed Cache**
		- A distributed cache spans multiple servers and is designed to handle large-scale systems.
		- It ensures that cached data is available across different nodes in a distributed system.
		- Eg :- Redis Cluster, Amazon ElastiCache.
	3. **Client-Side Cache**
		- Client-Side caching involves storing data on the client device, typically in the form of cookies, local storage or application-specific caches.
		- This is commonly used in web browsers to cache static assets like images, scripts and stylesheets.
	4. **Database Cache**
		- Database caching involves storing frequently queried database results in cache.
		- This reduces the number of queries made to the database for improving performance and scalability.
	5. **Content Delivery Network ( CDN )**
		- CDN is used to store copies of content in servers distributed across different geographic locations.
		- This reduces latency by serving content from a server closer to the user.

- ## Caching Strategies.
	- **Read-Through Cache** - Application first checks the cache for data. If it's not there ( a cache miss ), it retrieves data from database and updates the cache.
	- **Write-Through Cache** - Data is written to both the cache and the database simultaneously, ensuring consistency but potentially impacting write performance,
	- **Write-Back Cache** - Data is written to the cache first and later synchronized with the database, improving write performance but risking data loss.
	- **Cache-Aside ( Lazy Loading )** - Application is responsible for reading and writing from both the cache and the database.

- ## Cache Eviction Policies.
	- To manage the limited size of a cache, eviction policies are used to determine which data should be removed when cache is full.
	1. **Least Recently Used ( LRU )** - LRU evicts least recently accessed data when the cache is full. It assumes that recently used data will likely be used again.
	2. **Least Frequently Used ( LFU )** - LFU evicts data that has been accessed the least number of times, under the assumption that rarely accessed data is less likely to be needed.
	3. **First-In-First-Out ( FIFO )** - FIFO evicts the oldest data in the cache first, regardless of how often or recently it has been accessed.
	4. **Time-to-Live ( TTL )** - TTL is time-based eviction policy where data is removed from the cache after a specified duration, regardless of usage.

- [Read about Caching Strategies here](https://blog.algomaster.io/p/top-5-caching-strategies-explained)
