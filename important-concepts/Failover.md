# Failover
- Failover is the process of automatically switching to a standby system, server, database or network when the primary system fails or becomes unavailable.
- Failover ensures continuous availability, minimize downtime, maintain data integrity, and user experience.
- Failover is critical for systems when uptime is essential.

- ## Key Components in a Failover System
	- **Primary ( Active ) System** - Main system currently handling all operations.
	- **Secondary ( Standby ) System** - Backup system ready to take over if the primary fails.
	- **Health Monitor/Heartbeat** - A process that continuously checks if the primary system is alive.
	- **Failover Controller** - Component that decides when to trigger failover.
	- **Replication Mechanism** - Keeps the standby nodes data synchronized with primary node.

- ## Working of Failover System
	1. **Health Monitoring** - A monitoring agent ( or heartbeat ) continuously checks the primary systems status ( CPU, memory, network ... ).
	2. **Failure Detection** - If the primary system stops responding ( eg :- missed heartbeats ), the system detects a failure.
	3. **Failover Trigger** - Failover controller automatically initiates the switch to the standby system.
	4. **Role Switch** - Standby takes over as the new primary and starts handling the requests.
	5. **Recovery and Failback** - Once the original primary is repaired and restored, the roles may switch back ( called failback ).

- ## Types of Failover Architecture.
1. **Cool Standby ( Manual Failover )**
	- Backup server is powered off until failure occurs.
	- Manual intervention is needed to start it.
	- Low cost, but high downtime.

2. **Warm Standby ( Semi-Automatic Failover )**
	- Backup server is running, but not actively handling requests.
	- Data is periodically synchronized.
	- Some delay before the switch happens.

3. **Hot Standby ( Automatic Failover )**
	- Backup server is always running and in sync with the primary.
	- Failover happens instantly and automatically.
	- Used in mission-critical systems.

4. **Active-Active Failover**
	- Both severs are active simultaneously.
	- Load is distributed between them.
	- If one fails, the other continues handling all traffic.
	- Ensures zero downtime.

- ## Advantages of Failover
	- **High Availability** - Keeps system operational despite failures.
	- **Reduced Downtime** - Automatic recovery means faster recovery.
	- **Business Continuity** - No loss of critical services.
	- **Improved Reliability** - Confidence that the system won't collapse with one node failure.

- ## Drawbacks of Failover
	- **Data Inconsistency** - If data wasn't fully replicated before failure, some transactions might lost.
	- **Split-Brain Scenario** - Both nodes think they are primary, can corrupt data ( common in poorly configured clusters ).
	- **Failover Loops** - Repeated switching due to unstable network or false alarms.
	- **Cost** - Maintaining hot standbys, and extra infrastructure is expensive.
