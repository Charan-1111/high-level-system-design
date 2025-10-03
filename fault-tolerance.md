# Fault Tolerance
- Fault tolerance is the system ability to continue operate correctly even in the presence of hardware failures, software bugs or unexpected conditions.
- Instead of entire system going down when a failure occurs fault-tolerant systems detect the problem, isolate it, and recover to maintain availability and reliability.
- Fault tolerance involves designing systems that can automatically recover from failures, ensuring minimal disruptions to services.
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
