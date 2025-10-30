# Vertical vs Horizontal Scaling
- ## Vertical Scaling ( Scaling UP )
	- Vertical Scaling ( scaling up ) involves boosting the power of an existing machine within the system to handle increased loads.
	- This means upgrading the CPU, RAM, Storage or other hardware components to boost the servers capacity.
	- **Pros**
		- **Simplicity** - Vertical scaling is relatively simple to implement as it doesn't require changes to the application architecture.
		- **Lower Latency** - Since all the resources are located on a single machine, vertical scaling can eliminate the need of inter-server communication thus lowering the latency.
		- **Reduced Software Costs** - In the initial phase, vertical scaling may be more cost-efficient than horizontal scaling, especially when dealing with moderate increases in demand.
		- **No Major Code Changes** - Often requires little to no adjustments to out applications codebase.
	- **Cons**
		- **Limited Scalability** - There is a limit to how much a single machine can upgrade.
		- **Single Point of Failure** - With all resources on one server any hardware failures can bring down the entire system.
		- **Downtime** - Upgrading hardware often requires taking the server offline, which can be a significant disadvantages.
		- **Higher Costs in the Long Run** - High-end servers with powerful CPUs and large amounts of RAM can get very expensive as we scale.
	
- ## Horizontal Scaling ( Scaling Out )
	- Horizontal scaling ( scaling out ) involves adding more servers or nodes to the system to distribute the load across multiple machines.
	- Each server runs the copy of a application and load balanced between them by using a load balancer.
	- **Pros**
		- **Near-Limitless Scalability** - We can continue to add nodes as long as the architecture supports it, providing the ability to handle larger loads.
		- **Improved Fault Tolerance** - Failure of one node will not bring down the entire system, minimizing down time.
		- **Cost-Effective** - Horizontal scaling can be more cost-effective as it uses commodity hardware instead of expensive high-end servers.
	- **Cons**
		- **Complexity** - Distributing the application across multiple servers introduces complexity in terms of data consistency load balancing and inter-server communication.
		- **Increased Latency** - Communication between servers can introduce additional latency compared to a single machine.
		- **Cost** - Initial setup and maintenance costs can be higher due to the complexity of the infrastructure.
		- **Application Complexity** - Applications code might need adjustments to work effectively in a distributed environments.

- ## When to choose Vertical vs Horizontal Scaling
	- **When to Choose Vertical Scaling**
		1. **Limited Scalability** - Small to medium sized applications with a limited growth forecast and the needs are easily met by hardware updates.
		2. **Legacy Applications** - When there is a tight coupling between components, making it difficult to distribute across multiple servers.
		3. **Low Latency** - When low latency is critical requirement and inter-server communication overhead is unacceptable.
		4. **Cost-Sensitive Projects** - When the budget does not allow for a complex infrastructure and the cost of scaling horizontally out-weights the benefits, such as in the case of expensive software licenses.
	- **When to Choose Horizontal Scaling**
		- **Rapid Growth** - When experiencing rapid growth and requiring the ability to handle increasing traffic.
		- **High Availability Needs** - When the application needs to be highly available and resilient to node failures.
		- **Easily Distributable** - When the application can be easily distributed across multiple servers without significant modifications.
		- **Microservices Architectures** - When applications are designed around microservices, which naturally lend themselves to horizontal scaling
		- **Cost-Effectiveness** - When cost-effectiveness is a priority, and the use of commodity hardware is preffered.

- ## Combining Vertical and Horizontal Scaling
	- In some cases a combination of vertical and horizontal scaling can be used to optimize system performance and cost-effectiveness.
	- Many successful systems use a combination of both
		- Vertically scaled clusters - Powerful individual machines form the nodes of a horizontally scaled cluster.
		- Database Sharding - Data is partitioned across multiple database servers ( horizontal ), while each database server might be vertically scaled.
