# Distributed Tracing
- Distributed Tracing is a method used to track and observe requests as they propagate across multiple services in a distributed system.
- If follows an interaction and tags it with a unique identifier. This identifier stays with the transaction as it interacts with microservices, containers, and infrastructure.
- This identifier offers real-time visibility into user experience, from the top of the stack to the application layer and the infrastructure beneath.
- In short, if gives a complete end-to-end view of how a single user request moves through all microservices, APIs, databases and queues - helping to understand latency, bottlenecks, and errors.

- ## Need of Distributed Tracing
	- In monolithic architecture systems, all the code lies at a single place, so the debugging is easy.
	- But in microservice architecture, one single request may land of different services, so debugging in this case becomes difficult.
	- Without tracing, we only sees isolated logs from each service, with tracing we can see the entire journey.

- ## Architecture Components
	- Distributed Tracing typically has three layers.
	1 . **Instrumentation Layer** - Code that generates trace data ( spans, trace id's ).
	2. **Collector Layer** - Receives spans from multiple services normalizes and batches data. Sends to backend for Storage or Visualization.
	3. **Visualization Layer** - A UI to view traces, timings, dependencies and logs.

- ## Benefits of Distributed Tracing
	- Detect Performance bottlenecks.
	- Identify service dependencies.
	- Improves incident response time.
	- Provides SLA/SLO compliance data.
	- Enables root cause analysis in microservices.
