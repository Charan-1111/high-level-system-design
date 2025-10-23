# Proxy vs Reverse Proxy
- When we visit a website, the request doesn't always directly go to the server, sometimes it passes through a proxy or a revrese proxy first.
- Proxies and reverse proxies are servers that sit between clients and servers to imrpove, security. privacy and performance.
- A proxy ( Forward Proxy ) acts on behalf of clients, while a Reverse Proxy acts on behalf of servers.

- ## Proxy Server
	- A Proxy server acts as a middleman between the device and the server.
	- When a request ( like opening a webpage ) the proxy server intercepts it and forwards the request to the target server, retrieves the response and sends it back to the user.
	- Proxy server hides the IP address of the user, keeping location and identity private.
	
	- **Benefits of Proxy Servers**
		- **Privacy and Anonimity** - Proxy servers hide users IP address by using their own, so the destination server cannot know the users real identity.
		- **Access Control** - Organizations use proxies to enforce content restrictions, monitor internet usage.
		- **Security** - Proxies can filter out malicious content and blocks suspicious sites, providing additional layer of security.
		- **Improved Performance** - Proxies cache frequently accessed content, reducing latency and improving load times for websites.

- ## Reverse Proxy
	- Reverse proxy works the otherway. It intercepts client requests and forwards them to backend servers based on predefined rules.
	- It is like a gate keeper, instead of hiding clients from servers, it hides servers from clients.
	- Allowing direct access to the servers can pose security risks, exposing them to threat, like hackers or DDoS attacks.
	- A reverse proxy mitigates these risks by acting as a controlled entry point that regulates the incoming traffic and hides server IPs.
	- With a reverse proxy inplace, clients cannot directly talks with the servers, they can only talk through the proxy.
	- It can also acts as a load balancer, ditributing traffic across multiple servers.

	- **Benefits of Reverse Proxy**
		- **Enhanced Security** - By acting as a protective layer, a reverse proxy hides backend servers from clients, reducing the risk of attacks directly targetting the backend infrastructure.
		- **Load Balancing** - A reverse proxy can distribute incoming requests, evenly across multiple backend servers, improving system reliability and preventing server overloading.
		- **Caching Static Content** - Reverse proxies can cache static content like images, css, js , reducing the need to fetch these files.
		- **SSL Termination** - Reverse proxies can handle SSL encryption, offloading this from backend servers.
		- **Web Application Firewall ( WAF )** - Reverse proxies can inspect incoming requests, acting as a firewll to detect and block malicious traffiic.

	- We can setup reverse proxy using ***Nginx***
