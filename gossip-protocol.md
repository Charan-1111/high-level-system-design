# Gossip Protocol
- The popular message broadcasting techniques in a distributed system are
	- point-to-point broadcast
	- eager reliable broadcast
	- gossip protocol
- **Gossip Protocol** ( also known as epidemic protocol ) is a communication style in which nodes in a distributed system exchange information with a small, random subset of other nodes, similar to how a gossip ( or virus ) spreads in a social networks.
- Overtime, the information eventually speads ( or infect ) the entire cluster.

- ## Why Gossip ?
	- In very large distributed systems, global condition is expensive and slow.
	- Gossip provides
		- **Scalability** - Grows well as cluster size increases
		- **Fault Tolerance** - Works even with node failures.
		- **Decentralization** - No single point of failures.
		- **Eventual consistency state across all nodes**.

- ## Working of Gossip Protocol
	1. **Initial State** - A node has some new information ( Eg :- Node X is down )
	2. **Random Peer Selection** - At regular intervals ( gossip rounds ), the node randomly selects one or more peers.
	3. **Information Exchange** - They exchange state information ( push, pull, or push-pull ).
	4. **Spread** - Those peers then continue gossiping to others.
	5. **Convergence** - Eventually, all nodes learn the information.

- ## Types of Gossip Protocol
	- Based on the time required by gossip protocol to propagate a message across the system and the network traffic generated in propagating a message. The gossip protocol is broadly categorized into
		- anti-entropy model
		- rumor-mongering model
		- aggregation model
	- [ ] Read about these models

- ## Communication models in Gossip Protocol
	- The strategy to spread a message through gossip protocol should be chosen based on the service requirements and available network conditions.
	- **Push Gossip**
		- A node sends it know updates to others
		- Works well when information is new and rare

	- **Pull Gossip**
		- A node asks others if they know anything new.
		- Works well when information is common but the node is outdated.

	- **Push-Pull Gossip**
		- Both send updates to each other.
		- Faster convergence.

- ## Properties of Gossip Protocols.
	- **Probabilistic Guarantee** - Gossip protocols don't guarantee instant delivery, but with high probability, all nodes eventually get the update.
	- **Scalability** - Because only a small subset of nodes are contacted per round, the overhead remains small even for very large clusters.
	- **Fault Tolerance** - Even if some nodes crash or message drops, gossip continues spreading via other paths.
	- **Epidemic Convergence** - Spread is logarithmic - information reaches to N nodes in about O(logN) rounds.

- ## Advantages
	- Decentralized, no single point of failure.
	- Scales to thousands of nodes.
	- Tolerant of message loss and failure.
	- Simple and light weight.

- ## Disadvantages
	- Eventual consistency, not strong consistency.
	- Redundant messages increases network chatter.
	- Slower convergence compared to centralized broadcast in small clusters.
	- Difficult to guarantee exact timing of propagation.

- ## Use Cases
	1. **Membership Management**
		- Detecting which nodes are alive or dead in a cluster
		- Eg :- SWIM protocol used in HashiCorps Serf and Consul.

	2. **Failure Detection**
		- Nodes periodically gossip about which nodes they think are alive.
		- Help in quick detection of crashed nodes.

	3. **Configuration Updates**
		- Spread new configuration changes without central coordination.

	4. **Databases**
		- Cassandra and Amazon DynamoDB use gossip to keep track of cluster state and share membership changes.
