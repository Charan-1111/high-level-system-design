# API Gateway
- An API Gateway acts as a central server that sits between clients ( eg :- browser, mobile apps ) and backend services.
- Instead of clients directly interacts with multiple microservices, they send their requests to the API Gateway. The gateway processes these requests, enforces security, and forwards them to the appropriate microservice.
- API Gateway acts as a single entry point for all clients to access backend services.
- API Gateway handles authentication, rate limiting, logging, monitoring and request routing.

- ## Need for API Gateway
	- **Without API Gateway**
		- Each client directly communicates with multiple microservices.
		- Clients must know each services address and APIs.
		- Each service must handle.
			- Authentication
			- Rate Limiting
			- Logging
			- Security
			- Load Balancing
		- This causes
			- Tight coupling between client and microservices.
			- Complex maintenance.
			- Repeated logic across services.
	- **With API Gateway**
		- Client talks to only one endpoint ( the gateway ).
		- Gateway routes and transforms requests.
		- Backend services remain isolated and focused on business logic.
		- **Benefits**
			- Centralized, security, authentication, and monitoring.
			- Simplified client-side logic.
			- Enables microservices decoupling.
			- Better scalability and reliability.

- ## Core features of API Gateway
	1. **Authentication and Authorization**
		- API Gateway secures the backend services by ensuring only authorized users and clients can access the backend services.
		- It handles tasks like
			- **Authentication** - Verifying the identity of the client using token ( eg :- OAuth, JWT ), API keys, or certificates.
			- **Authorization** - Checking the client's permissions to access specific services or resources.
		- By centralizing these tasks, API Gateway eliminates the need for individual services to handle authentication, reducing redundancy, and ensuring consistent access control across systems.

	2. **Rate Limiting**
		- To prevent abuse and ensure fair usage of resources, mos API Gateways implements rate limiting.
		- This features
			- Controls the frequency of requests a client can make within a given time frame.
			- Protects backend services from being overwhelmed by excessive traffic or potential denial-of-service ( DoS ) attacks.

	3. **Load Balancing**
		- High traffic applications rely on load balancing to distribute the incoming requests evenly across multiple instances of a service.
		- API Gateway can
			- Redirect requests to a healthy service instances while avoiding the ones that are down or overwhelmed.
			- Uses algorithms like Round-Robing, least connections, or weighted distribution to manage traffic intelligently.

	4. **Caching**
		- Most API Gateways also provide caching, to improve performance and response times, and reduces the strain on backend services.
		- They temporarily stores frequently accessed data like
			- Responses to commonly accessed endpoints.
			- Static resources like images or metadata.

	5. **Request Transformation**
		- In systems with diverse clients and backend services request transformation is essential for compatibility.
		- An API Gateway can
			- Modify the structure or format of incoming requests to match the backend service requirements.
			- Transform responses before sending them back to the client, ensuring they meet the clients expectations.

	6. **Service Discovery**
		- Modern services often involves microservices that scales dynamically.
		- Service discovery feature of API Gateway dynamically identifies the appropriate backend service instances to handle each request.
		- This ensures seamless request routing even in environments where services frequently scales up and down.

	7. **Circuit Breaking**
		- Circuit breaking is a mechanism that temporarily stops sending requests to backend services when it detects persistent failures such as
			- Slow responses or timeouts.
			- Server errors ( eg ;- HTTP 500 status code )
			- High latency or unavailability of a service
		- API Gateway continuously monitors health and performance of backend services and uses circuit breaking to block requests to a failing services.

	8. **Monitoring and Logging**
		- API Gateways provide robust monitoring and logging capabilities to track and analyze system behaviour.
		- These capabilities include
			- Logging detailed information about each request, such as source, destination, and response time.
			- Collecting metrics like request rates, error rates and latency.
		- This data helps system administrators to detect anomalies, troubleshoot issues and optimize the system's performance.
		- Many API Gateways also integrate with monitoring tools like Prometheus, Grafana, or AWS CloudWatch
