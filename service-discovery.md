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
