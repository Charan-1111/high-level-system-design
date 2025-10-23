# Consensus in Distributed Systems
- Consensus is the process by which multiple distributed node ( machines, servers or processes ) agree on a single value of state, even in the presence of failures ( crashes, delays or malicious behaviour ).
- In short, if multiple computers are working together, consensus ensures they all agree on what's true at a given time.

- ## Importance of Consensus
	- In distributed systems.
		- Machines can fail, restart or lose connectivity.
		- Messages can be delayed or dropped.
		- Nodes can hold different views of the system state.

	- Consensus algorithms solves problems like.
		- **Leader Election** ( who coordinates tasks ?).
		- **State Machine Replication** ( all nodes must agree on logs / transactions )
		- **Commit Decisions** - (eg :- in databases, commit or abort )

- ## How to achieve consensus in distributed system.
	- To achieve consensus all the nodes in the distributed system should follow the same protocol when communicating.
	- There are three basic conditions that need to be satisfied by the system for consensus algorithms.
		- **Agreement** :- All non-faulty nodes should agree on the same value.
		- **Validity** :- If a system has decided on a value *v* then that value should be suggested by one of the non-faulty nodes of the system and all other non-faulty nodes must decide that value *v*.
		- **Termination** :- Every non-faulty node should agree upon some value. If one of the non-faulty nodes agrees upon value *v*, consensus cannot be achieved.

- ## Challenges in Distributed consensus
	1. Asynchronous Communication - Messages may be delayed indefinitely.
	2. Network Partitions - Some nodes can't communicate with others.
	3. A distributed system can mainly face 2 problems
		1. **Crash Failures**
			- Occurs when a node is not responding to other nodes of the system due to some hardware or software or network fault.
			- This is very common issues in distributed systems and it can be easily handled by simply ignoring the nodes existance.
		2. **Byzantine Failures**
			- Byzantine failures is a situation where one or more nodes is not crashed but behaves abnormally and forward a different message to different peers, due to an internal or external attack.
			- Handling this kind of situation is complicated in the distributed system.

		- A consensus algorithm, if it can handle byzantine failures, then it can handle any type of consensus problem in a distributed systems.


- [ ] Learn about the consensus algorithms 
