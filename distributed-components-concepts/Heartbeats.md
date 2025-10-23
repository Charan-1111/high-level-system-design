# Heart Beats
- In distributed system heartbeat is a periodic message sent from one component to another to monitor each other's health and status.

- ## Need for Heart Beat
	- Without heartbeats it is hard to quickly detect failures in distributed system. Leading to
		- Delayed fault detection and recovery.
		- Increased downtime and errors.
		- Decreased overall system reliability.
	- Heartbeats helps with
		- **Monitoring** - Helps in monitoring health and status of different parts of distributed system.
		- **Detecting Failures** - It enables a system to identify when a component becomes unresponsive. If a node misses several expected heartbeats, it is a sign that something might wrong.
		- **Triggering Recovery Actions** - Heartbeats allows the system to take corrective actions. This could mean moving tasks to a healthy node, restarting a failed component, or letting the system administrator about the failure.
		- **Load Balancing** - By monitoring heart beats of different nodes, a load balancer can distribute the load more effectively across the network based on the responsiveness and health of each node.

- Heartbeat mechanism involves two primary components.
	- **Heartbeat Sender ( Node )** - This is the node that sends periodic heartbeat signals.
	- **Heartbeat Receiver ( Monitor )** - This component receives and monitors the heartbeat signals.

- There are two primary types of heartbeats.
	- **Push Heartbeat** - Nodes actively send heartbeat singals to the monitor.
	- **Pull Heartbeat** - Monitor periodically queries nodes for their status.

- [ ] Read about challenges in heartbeats
