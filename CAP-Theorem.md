
# CAP Theorem

- CAP Theorem provides a fundamental framework for understanding the trade-offs that must be made while designing distributed systems.
    - C => Consistency
    - A => Availability
    - P => Parition Tolerance

- CAP Theorem states that : It is impossible for a distributed data store to simultaneously provide all three guarantees.
    - Consistency - Every read reveives the most recent write or an error.
    - Availability - Every request ( read/write ) receives a non-error response, without guarantee that it contains the most recent write.
    - Partition Tolerance - The system continues to operate despite an arbitrary number of messages being dropped or delayed by network between nodes.

## 3-Pillars of CAP
1. ### Consistency
    - Consistency ensures that every read receives the most recent write or an error.
    - Means that all working nodes in a distributed system will return the same data at any given point of time.
    - In consistent distributed system, if we perform write data to node A, a read operation from node B will immediately reflect the write operation on node A.
    - Consistency is crucial for applications where having the most up-to-date data is critical.
        - **Eg**. A financial systems where a balance inquiry must reflect the most up-to-date state of an account.
        
2. ### Availbility
    - Availability gurantees that every request ( read/write ) receives a response, without ensuring that it contains the most recent write.
    - This means that the system is still operational and responsive, even if the response from some of the nodes don't reflect most up-to-date data
    - Availability is critical and important for applications that need to remain operational at all times, such as online retail systems.

3. ### Partition Tolerance
    - Partition Tolerance means that the system continues to function despite the network partitions where nodes cannot communicate with each other.
    - A network partition occurs when a network failure causes a distributed system to split into two or more groups of nodes that cannot communicate with each other.
    - When there is a partition tolerance, the system must choose between consistency and availability.
    - Partition tolerance is essential for distributed systems because network failures can and do happen.
    - A system that tolerates partitions can maintain operations across different network segments.


## The CAP Trade-off
- CAP theorem asserts that in presence of network partition, a distributed system must choose between consistency and availability.

1. ### CP ( Consistency and Partition Tolerance )
    - These systems prioritize consistency and can tolerate network partitions, but at the cost of availability.
    - During a partition, the system may reject some requests to maintain consistency.
    - Traditonally relational databases like MySQL and PostgreSQL when configured for strong consistency, prioritizing consistency over availability during network failures.

    - **Eg**. Banking systems prioritize consistency over availability, due to the data accuracy is more important than availability during network failures.

2. ### AP ( Availability and Partition Tolerance )
    - These systems ensures availability and can tolerate network partitions at the cost of consistency.
    - During a partition, different nodes may return different values for the same data.
    - NoSQL databases like Cassandra and DynamoDB are designed to be highly available and partition-tolerance, potentially at the cose of strong consistency.
    - **Eg**. Amazon's shopping cart system is designed to always accept items, prioritizing availability.

3. ### CP ( Consistency and Availability )
    - In absence of partitions, a system can be both consistence and available.
    - However network partitions are inevitable in distributed systems, making this combination impractical.
    - **Eg**. Single-node databases can provide both consistency and availabilty but aren't partition-tolerant. In a distributed systems this combination is partically impossible.

## Practical Design Strategies
- Designing distributed systems requires carefully these trade-offs based on the application requirements.
- Below are some practical strategies
1. ### Eventual Consistency
	- For many systems strict consistency is not always necessary.
	- Eventual consistency can provide a good balance where updates are propagated to all the nodes eventually, but not immediately.
	- **Eg**. Systems where immediate consistency is not required like DNS, CDN's

2. ### Strong Consistency
	- A model ensuring that once a write is accepted, all the subsequent reads will return that data.
	- **Eg**. System requiring hign data accuracy, like financial applications and inventory management.

3. ### Tunable Consistency
	- Tunable consistency allows systems to adjust their consistency levels based on specific needs.
	- This provides balance between strong and eventual consistencies.
	- Systems like cassandra allows configuring the level of consistency on a per-query basis, providing flexibility.

4. ### Quorum-Based Approaches
	- Quorum-based approaches use voting among a group of nodes to ensure a certain level of consistency and fault tolerance.
	- **Eg**. Systems needing balance between consistency and availabiltity, often used in consensus algorithms like Paxos and Raft.
- [ ] TODO : Read about PACELC theorem
