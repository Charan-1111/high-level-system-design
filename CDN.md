# Content Delivery Networks ( CDN )
- CDN is a geographically distributed network of servers that works together to deliver web content ( like images, videos, CSS, JavaScript, or HTML pages ) quickly to users based on their geographic location.
- Primary purpose of CDN is to deliver content to end users with high availability and performance by reducing physical distance between server and user.
- When a user request content from a website the CDN redirects the request to the nearest server in its network, reducing latency and improvind load times.

- ## Working of CDN
	- CDN operates using three components.
		1. **Edge Servers** - Located at Point of Presence ( PoP ) locations, these servers cache and deliver content closer to users.
		2. **Origin Servers** - The primary server where the original content is stored.
		3. **DNS ( Domain Name System )** - Directs user requests to the nearest edge server insted of origin server.
	- Step-by-Step working
		1. User requests a webpage ( eg :- www.example.com/image.png ).
		2. DNS resolves the domain to the nearest CDN edge server.
		3. If the edge server has the content cached ( cache hit ) -> sends it immediately.
		4. If no ( cache miss ) -> It fetches from origin server, stores it in cache and then serves it.
		5. Subsequent users nearby get it instantly from the edge server.

	- CDN uses **Time-to-Live ( TTL )** mechanism to determine how long a content remains cached before expiring.
	- To ensure users always gets latest version of data CDN periodically refresh and update cached content from the origin server.

- ## CDN Architecutre.
	- A typical CDN consists of 
		1. **Origin Server** - Main source of truth.
		2. **Edge Servers ( PoPs )** - Globally distributed cache servers.
		3. **Caching Mechanism** - Stores frequently accessed files temporarily.
		4. **Request Routing System** - Directs users to optimal edge server using DNS.
		5. **Load Balancer** - Balancers traffic between servers.
		6. **Monitoring and Analytics** - Tracks latency, cache hit ratio, traffic volumes, errors.

- ## Types of content served by CDNs
	1. **Static Content** -> HTML, CSS, JS, images, fonts, video.
	2. **Dynamic Content** -> Personalized pages ( using CDN acceleration techniques ).
	3. **API/JSON Responses** -> API edge caching and routing.
	4. **Streaming Media** -> Live and on-demand video streaming.
	5. **Software Distribution** -> App updates, downloads.

- ## Benefits of CDN
	- **Reduced Latency** - Content is delivered from nearest location.
	- **Reduced Server Load** - Delivering from nearest edge server offloads traffic from origin servers.
	- **Improved Availability and Reliability** - With multiple servers in different locations, CDN prevents single point of failures.
	- **Scalability** - Handles traffic spikes automatically.
	- **Global Reach** - CDN make it easier to deliver content to users worldwide.
	- **Enhanced Security** - DDos Protection, SSL offload.
	- **Improved SEO and UX** - Faster page loading improves ranking and user experience.

- ## Limitations of CDN
	- **Dynamic Content** - Harder to cache user-specific data.
	- **Cache invalidation** - Must handle content updates carefully.
	- **Cost** - Premium CDNs can be expensive for large traffics.
	- **Configuration complexity** - Requires tuning cache policies and routing roles.

- ## CDN Security Features.
	- Modern CDNs also acts as a security layers.
	- **DDoS Mitigation** - Filters malicious traffic before reaching origin.
	- **Web Application Firewall ( WAF )** - blocks SQL injection, XSS...
	- **TLS Termination** - handles HTTPs at edge nodes.
	- **Bot Proteection** - identifies and blocks scrapers/bots.
	- **Rate Limiting** - limits abuse requests.
