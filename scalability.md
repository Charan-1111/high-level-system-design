# Scalability

- As the system grows, the performance of the system starts to degrade unless we adapt it to deal with that growth.
- Scalability is the property of a system to handler a growing amount of load by adding resources to the system without sacrificing performance or reliability.
- A system that can continuously evolve to support a growing amount of work is scalable.


- ## How can a system grows
    - A system can grow in serveral dimensions.
        - More users
        - More features
        - More data
        - More complexity
        - More geographics

    1. ### Growth in user base
        - More users starts using the system, leading to increased number of requests.
            - <u>Eg</u>. A social media platform experiencing a surge in new users.

    
    2. ### Growth in features
        - More features were introduced to expand system capabilities.
            - <u>Eg</u>. An e-commerce application adding support for a new payment mehtod.

    3. ### Growth in data volume
        - Growth in the amount of data the system stores and manages due to user activity or logging.
            - <u>Eg</u>. A video streaming platform like youtube storing a lot of information

    4. ### Growth in comlexity
        - The system's architecture evolves to accommodate new features, scale, or integrations, resulting in additional components and dependencies.
            - <u>Eg</u>. A system that started as a simple application is broken into smaller, independent systems.

    5. ### Growth in geographic reach
        - The system is expanded to server users in new regions or contries
            - <u>Eg</u>. An e-commerce company launching websites and distribution in new regions.



- ## How can we scale the system to handle increasing load

    - A system can grow in serveral ways to accommodate the increasing load.

    1. ### Vertical Scaling ( Scale UP )
        - Means adding more power to our existing machines by upgrading server with more RAM, faster CPUs, or additional storage.
        - This approach is good for simple architectures, but it has limitations in how fast we can go.
        - This is simple to implement, but it is limited by hardware capacity and cost.


    2. ### Horizontl Scaling ( Scale Out )
        - Means adding more machines to our system to spread the workload across the multiple servers.
        - This is often considered as the most effective way to scale for large systems.
        - <u>Eg</u>. Netflix uses horizontal scaling for its streaming service, adding more machines to their cluster to handle the growing number of users and data traffic.

    3. ### Load Balancing
        - Load balancing is the process of distributing the load or traffic across multiple servers to ensure no single server is becoming overwhelmed with the increasing traffic.
        - <u>Eg</u>. If we have multiple servers for a service ( horizontal scaling ), then the load balancers distributes the load across the different servers to maintain the system flow smooth.

    4. ### Caching
        - Caching is a technique in which we store the more frequently accessed data in-memory like RAM, to reduce the load on the server or the database
        - Implmenting the cache can lead to improving in the performace or the response times of the service
        - <u>Eg</u>. If we have a service, that is querying the database every time for the information, then in this case we can use the cache to reduce the load on the database.

    5. ### Content Delivery Networks (CDNs)
        - CDN distributes static assets like images, videos, etc. closer to the users.
        - This can result in the reduces latency and faster loading times.
        - [ ] TODO : add an example for this

    6. ### Sharding / Partitioning
        - Partitioning means splitting data or functionality across multiple nodes/servers to distribute workload and avoid bottlenecks.

    7. ### Asynchronous communications.
        - This means deffering the long-running tasks or non-critical tasks to the backgroung queues or message brokers.
        - This ensures our main application remains responsive to users.

    8. ### Microservice Architecture.
        - This breakdowns a service into smaller, independent services that can be scalled independently.
        - This improves resilience and allows teams to work on specific components in parallel.

    9. ### Auto Scaling
        - This means automatically adjusting the number of active servers based on the current load.
        - This ensures that the system can handle the spike in the traffic without manual intervention.

    10. ### Multi-region Deployment.
        - Deploy the application in multiple data centers or cloud regions to reduce latency and improves redundancy.



- [ ] add examples to everyone
