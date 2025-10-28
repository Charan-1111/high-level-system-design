# Distributed Locking
- Distributed Locking is a mechanism that ensures only one process or node in a distributed system can access a shared resource like a database record, file, or cache entry at a time.
- It is similar to mutex ( mutual exclusion lock ) in single-node application.

- ## Need for Distributed Locking
	- In distributed systems multiple nodes often perform tasks in parallel ( sometimes on a shared data ).
	- Without coordination they could
		- Update the same record simultaneously.
		- Execute the same Job multiple times.
		- Cause race conditions.

- ## Working of Distributed Locking
	1. A node requests a lock for a resource from a lock manager ( like redis, zookeeper...)
	2. If the resource is not locked, the lock manager grants the lock and associates a unique LockID with it.
	3. The node performs its critical section ( the protected code ).
	4. When done, the node releases the lock using the same LockID.
	5. If another node requests the lock during this time it must wait ( or fail if its non-blocking lock ).

- ## Challenges in Distributed Locking
	- **Clock Skew** - different machines may have unsynchronized clocks, breaking TTL-based locks.
	- **Network Partitions** - a node may think it holds a lock but is actually isolated from the rest.
	- **Performance Overhead** - Communication with external systems ( like Redis/Zookeeeper) adds latency.
	- **Split-Brain Scenarios** - Two nodes both think they own the lock due to network issues.

- [ ] Read about the best practices for Distributed Locking
