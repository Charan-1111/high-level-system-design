# Distributed Caching
- Distributed cache is a technique where cached data is stored across multiple servers ( nodes ) in a distributed network, rather than on a single machine.
- This helps applications access frequently used data quickly and scale horizontally without overloading databases or backend services.

- ## Need for Distributed Caching.
	- **Scalability** - Distributed caching allows applications to scale horizontally by adding more cache nodes. This helps to manage more traffic without a significant drop in performance.
	- **Fault Tolerance** - Since data is spread across multiple nodes, failure of a single node doesn't result in the loss of the entire cache. Remaining nodes can continue to serve requests allowing the system to recover gracefully.
	- **Load Balancing** - By distributing the cache across several nodes, the load is spread evenly. This helps prevent any single node becoming a bottleneck.

- ## Distributed Caching Components.
	- **Cache Nodes** - These are the individual servers where the cache data is stored. Each node is part of the overall cache cluster.
	- **Client Library/Cache Client** - Applications use a client library to talk to the distributed cache. This library handles the logic of connecting to cache nodes, distributing data, and retrieving cached data.
	- **Consistent Hashing** - This method spreads data evenly across cache nodes. It ensures that adding or removing nodes has minimal impact on the system.
	- **Replication** - To make the system more reliable, some distributed caches replicate data across multiple nodes.
	- **Sharding** - Data is split into shards, and each shard is stored on a different cache node. It helps distribute the data evenly and allows the cache to scale horizontally.
	- **Eviction Policies** - Caches implement eviction policies like LRU, LFU, TTL to get rid of old or less used data and make space for new ones.
	- **Coordination and Synchronization** - Coordination mechanisms like distributed locks or consensus protocols ensures that cache nodes remains synchronized, especially when multiple nodes try to change the same data at the same time.

- [ ] Read about distributed cache working and challenges with distributed caching
- [ ] 
