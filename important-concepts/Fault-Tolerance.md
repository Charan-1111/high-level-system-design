# Fault Tolerance
- Fault tolerance is the system ability to continue operate correctly even in the presence of hardware failures, software bugs or unexpected conditions.
- Instead of entire system going down when a failure occurs fault-tolerant systems detect the problem, isolate it, and recover to maintain availability and reliability.
- Fault tolerance involves designing systems that can automatically recover from failures, ensuring minimal disruptions to services.

- ## Techniques to Achieve Fault Tolerance
	- Fault tolerance can be achieved in many ways.
		1. **Hardware Level**
			- RAID Storage ( mirroring, parity-based application )
			- Redundant power supplies, network cards and servers.
		2. **Software Level**
			- Exception handling and retires.
			- Checkpointing ( saving system state periodically to resume after failure ).
		3. **Network Level**
			- Load balancers distributing requests across healthy servers.
			- Multiple ISPs for network redundancy.
		4. **Data Level**
			- Replication ( Synchronous / Asynchronous ).
			- Sharding with redundancy.
			- Backups and snapshots.
		5. **Distributed System Level**
			- Consensus protocols ( Paxos, Raft ) to maintain consistency in the face of failures.
			- Leader election for failover handling.
			- CAP theorem considerations ( availability vs consistency trade-offs ).

- ## Key characterstics of Fault Tolerance
	1. **Redundancy**
		- Duplicate components ( hardware, software, data ) are maintained so if one fails, another takes over.
		- Eg :- Two servers running the same service with a load balancer.

	2. **Graceful Degradation**
		- The system continues to work, though with reduced functionality, instead of complete failures.
		- Eg :- An e-commerce site disables product recommendations if the recommendation service fails but still allows purchases.
	
	3. **Failover Mechanisms**
		- Automatic switching from a failed component to a standby replica.
		- Eg :- Active-passive database replication.

	4. **Replication**
		- Multiple copies of services or data across nodes to ensure availability.
		- Eg :- Distributed database like cassandra or mongodb keep data replicated across nodes.

	5. **Error Detection and correction**
		- Mechanisms like checksums, parity bits or heartbeats to detect and fix errors.
		- Eg :- TCP re-transmission of lost packets.
