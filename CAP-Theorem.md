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
