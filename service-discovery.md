# Service Discovery
- Service discovery is a mechanism that allows serviecs in a distributed system to find and communicate with each other dynamically.
- Service discovery hides the complex details where services are located, so they can interact without knowing each other's exact network spots.
- Service discovery registers and maintains a record of all the services in a service registry. This service registry acts as a single source of truth that allows services to query and communicate with each other.
- A service registry typically stores.
	- **Basic Details** - Service name, IP, Port and status.
	- **Metadata** - Version, environment, region, tags, etc...
	- **Health Information** - Health status, last health check.
	- **Load Balancing Info** - Weights, priorities.
	- **Secure Communication** - Protocols, certificates.

- **Key benefits of Service Discovery**
	- **Reduced Manual Configuration** - Services can automatically discover and connect to each other, eliminating the need for manual configuration and hardcoding of network locations.
	- **Improved Scalability** - As new service instances are added or removed, service discovery ensures that other services can seamlessly adapt to the changing environment.
	- **Fault Tolerance** - Service discovery offers including health checks, enabling systems to automatically reduce traffic away from failing service instances.
	- **Simplified Management** - Having a central registry of services makes it easier to monitor, manage, and troubleshoot the entire system.

- ## Service Registration Options
	- Service Registration is the process where a service announces its availability to a service registry, making it discoverable by other services.
	- Most common service registration options are as follows.
	
		1. **Manual Registation**
			- Service details are added to the registry manually by a developer or operator.
			- This approach is simple but not suitable for dynamic systems where services scales or moves frequently.

		2. **Self-Registration**
			- Service is responsible for registering itself with service registry when it starts.
			- Service includes logic to interact with the registry, such as sending API requests to register its details.
			- **Working**
				1. When a service or an instance starts, it receives its own network information ( eg :- IP address, Port...)
				2. It sends a registration request to the servie registry ( via HTTP / gRPC )
				3. To ensure the registry has up-to-date information, the service may periodically send heartbeat signals to confirm it is active and healthy.

		3. **Third-Party Registration ( Sidecar Pattern )**
			- An external agen or sidecar process handles service registration.
			- Service itself doesnot directly interacts with the registry. Instead sidecar detects the service and registers it.
			- **Working**
				1. The sidecar runs alongside the service ( eg :- in the same container or on the same host )
				2. The sidecar detects when the service starts and gathers its network details.
				3. It sends the registration request to the service registry.

		4. **Automatic Registration by Orchestration**
			- In orchestratos ( like Kubernetes ), service registration happens automatically.
			- Orchestration platform manages the lifecycle of services and updates the service registry as service starts, stops or scales.
			- **Working**
				1. Orchestrator ( like Kubernetes ) detects when a service or a container is deployed.
				2. It assigns the service an IP address and Port.
				3. It registers the service automatically with its built-in service discovery mechanism ( like kubernetes DNS ).

		5. **Configuration Management Systems**
			- Some systems use configuration management tools ( eg :- Chef, Puppet, Ansible ) to register services.
			- These tools manage the service lifecycle and update the service registry whenever services are added or removed.

- ## Types of Service Discovery.
	- There are two primary types of service discovery :- client-side discovery and server-side discovery.
	1. **Client-Side Discovery**
		- In this model, the responsibility for discovering and conneting to a service lies entirely with the client.
		- Client is responsible for
			- Discovering healthy service instances.
			- Load balancing between them.
		- **Working**
			1. **Service Regristration**
				- Services register themselves with a centralized service registry.
				- They provide their network details ( IP address and Port ) along with metadata like service health or version.
			2. **Client Queries the Registry**
				- Client ( a micro service or API gateway ) sends a request to the service registry to find the instances of a target service.
				- The registry responds with a list of available instances, including their IP address and Ports.
			3. **Client Routes the Request** - Based on the information retrieved, the client selects one of the service instances ( often using a load balancing algorithm ) and connects directly to it.
		- Client maintains control over how requests are routed, such as distributing traffic evenly across instances or prioritizing the closest instance.

		- **Advantages**
			- Simple to implement and understood.
			- Reduces the load on a central load balancer.
		- **Disadvantages**
			- Consumers need to implement discovery logic.
			- Changes in the registry protocol requires changes in the client.

	2. **Server-side Discovery**
		- In this model, the client delegates the responsibility of discovering and routing requests to a specific service instance to a centralized server or load balancer.
		- Unlike, the client-side discovery, the client does not need to query the service registry directly or perform any load balancing itself.
		- Instead, client simply sends a request to a central server ( load balancer or api gateway ) which handler the rest.
		- **Working**
			1. **Service Registration**
				- Services register themselves with a centralized service registry, similar to client-side discovery.
				- The service registry keeps track of all service instances, their IP addresses, Ports, and metadata.
			2. **Client sends requests**
				- Client sends a request to a load balancer or API gateway, specifying the service it wants to communicate with.
				- The client does not query the service registry or know the specific location of the service instances.
			3. **Server Queries the Service Registry** - The load balancer or gateway queries the service registry to find available instances of the requested service.
			4. **Routing** - The load balancer selects a suitable service instance ( based on factors like load, proximity, or health ) and routes the clients request to that instance.
			5. **Response** - The service instance processes the request and sends the response back to the client via the load balancer or gateway.

		- **Advantages**
			- Centralizes discovery logic, reducing the complexity for consumers.
			- Easier to manage and update discovery protocols.

		- **Disadvantages**
			- Introduces an additional network hop.
			- The load balancer can become a single point of failure.

- ## Best practices for implementing Service Discovery
	1. **Choose the Right Model** :- Use client-side discovery for custom load balancing and server-side for centralized routing.
	2. **Ensure High Availability** :- Replicate the service registry and test failover scenarios to prevent downtime. Deploy multiple instances of the service registry to avoid single points of failures.
	3. **Automate Registration** :- Use self-registration, sidecars or orhestration tools for dynamic environments. Ensure proper deregistration of stale services.
	4. **Use Health Checks** :- Monitor service health and remove failing instances automatically.
	5. **Follow Naming Conventions** :- Use clear, unique service names with versioning to avoid conflicts.
	6. **Caching** :- Use caching mechanisms to reduce the load on the service registry and improve discovery performances.
	7. **Scalability** :- Ensure that the service discovery system can scale with the growth of our services.
