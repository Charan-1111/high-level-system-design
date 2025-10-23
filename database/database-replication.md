# Database Replication
- Database Replication is the process of copying data from one database ( called the primary or master ) to one or more other databases ( called replicas or slaves ) in real time or periodically.
- Having multiple copies of the same data in different locations to improve availability, reliability and performance.
- Database replication helps to solve, High traffic load, Single point of failure, Geographic latency, Backup and Recovery, Analytics workload.

- ## Components of Replication
	- **Primary ( Master )** - Main database where all writes happen.
	- **Replica ( Slave / Secondary )** - Copy of the primary that receives u[dates/
	- **Replication Log** - Record of all changes ( insert/update/delete ) made to the primary.
	- **Replication Agent** - Process responsible for reading logs and applying them to replicas.

- ## Types of Replication
	1. **Synchronous Replication**
		- Primary waits until all the replicas confirms that they have received and applied the transaction.
		- Guarantees data consistency ( No data loss ). But increases latency ( Slower Writes ).

	2. **Asynchronous Replication**
		- Primary does not wait for replicas to acknowledge.
		- Fast writes. But replicas can lag behind ( known as Replication Lag ).

	3. **Semi-Synchronous Replication**
		- A balance between Synchronous and Asynchronous.
		- Master waits for at least one replica to acknowledge before confirming success.
		- Reduces risk of data loss without major latency hit.

	4. **Multi-Master ( Bi-Directional ) Replication**
		- Multiple nodes can accept writes.
		- Each node replicates changes to others.
		- Complex conflict resolution ( eg :- same row updates in two places ).

	5. **Peer-to-Peer Replication**
		- All nodes are equal ( no master ).
		- Each node can read/write.
		- Requires conflict detection and resolution mechanisms.

- ## Benefits of Replication
	- **High Availability** - If one node fails, another replica can take over . Enables automatic failover.
	- **Scalability** - Offload read traffic to replicas ( read scaling ).
	- **Disaster Recovery** - Maintains near-real-time copies across regions or data centers.
	- **Performance Optimization** - Reduce latency by having replicas geographically closer to users.
	- **Back up / Reporting** - Run analytical or backup operations on replicas without affecting production.

- ## Challenges of Replication
	- Replication Lag.
	- Conflict Resolution
	- Network Latency
	- Data consistency issues.
	- Complex Failover
