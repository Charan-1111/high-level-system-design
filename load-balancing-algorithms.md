# Load Balancing
- Load Balancing distributes the incoming network traffic across multiple servers to ensure that no single server is overwhelmed.
- Load balancing aims to
	- Prevent overload on a single server.
	- Improves performance by reducing response time.
	- Improves availability by rerouting traffic incase of server failures.

# Load Balancing Algorithms
1. ## Round Robin
	- **Working**
		- A request is sent to the first server in the list.
		- Next request is sent to second sever, and so on.
		- After the last server in the list, the algorithm loops back to the first server.
	- **When to Use**
		- When all servers have similar processing capabilities and are equally capable of handling requests.
		- When simplicity and even distribution.
	- **Benefits**
		- Simple to implement and understand.
		- Ensures even distribution of traffic.
	- **Drawbacks**
		- Does not consider server load or response time.
		- Can lead to inefficient if servers have different processing capabilities.
	- [ ] Implement the algorithm.

2. ## Weighted Round Robin
	- **Working**
		- Each server is assigned a weight based on their processing power or available resources.
		- Servers with higher weights receive a proportionally larger share of incoming requests.
	- **When to Use**
		- When servers have different processing capabilities or available resources.
		- When we want to distribute the load based on the capacity of each server.
	- **Benefits**
		- Balances load according to server capacity.
		- More efficient use of server resources.
	- **Drawbacks**
		- Slightly more complex to implement than simple Round Robin.
		- Does not consider current server load or response time.
	- [ ] Implement the Algorithm

3. ## Least Connections
	- **Working**
		- Monitor the number of active connections on each server.
		- Assigns the incoming requests to the server with the least number of active server connections.
	- **When to Use**
		- When we want to distribute the load based on the current number of active server connections.
		- When servers have similar processing capabilities but may have different level of concurrent conenctions.
	- **Benefits**
		- Balances load more dynamically based on current sever load.
		- Helps prevent any server from becoming overloaded with a high number of active connections.
	- **Drawbacks**
		- May not be optimal if servers have different processing capabilities.
		- Requires tracking of active connections for each server.

4. ## Least Response Time
	- **Working**
		- Monitors the response time of each server.
		- Assigns incoming requests to the server with the fastest response time.
	- **When to Use**
		- When we have servers with varying response times and want to route requests to the fastest server.
	- **Benefits**
		- Minimizes overall latency by selecting the server with fastest response time.
		- Can adapt dynamically to changes in server response times.
		- Helps to improve the user experience by providing quick responses.
	- **Drawbacks**
		- Requires accurate measurement of server response times, which can be challenging in distributed systems.
		- May not consider other factors such as server load or connection count.
	- [ ] Implement the Algorithm

5. ## IP Hash
	- **Working**
		- Calculates a hash value from the client's IP address and uses it to determine the server to route the request.
	- **When to Use**
		- When we need session persistence, as requests from the same client are always directed to the same server.
	- **Benefits**
		- Simple to implement
		- Useful for applications that require sticky.
	- **Drawbacks**
		- Can lead to uneven load distribution if certain IP addresses generate more traffic than others.
		- Lacks flexibility if a server goes down, as the hash mapping may need to be reconfigured.
	- [ ] implement the algorithm
