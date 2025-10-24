# WebSockets
- WebSockets are a communication protocol used to build real-time features by establishing a two-way communication between a client and a server.
- WebSockets enables a full-duplex, bi-directional communication between a client and a server over a single TCP connection.
- WebSockets allows both the client and the server to send messages to each other independently and continuously after a connection is established.
	- Unlike in HTTP, where client sends a request to server and waits for the response.

- ## Working of WebSockets
	- WebSockets connection starts with a standard HTTP request from the client to the server.
	- Instead of completing the request and close the connection, server responds with ***HTTP 101*** status code, indicating that the protocol is switching to WebSockets.
	- After this handshake, a WebSocket connection is established and both the client and server can send messages to each other over the open connection.

	- **Setp-by-Step Communication Process**
		1. **Handshake**
			- Client initiates the connection request using a standard ***HTTP GET*** request with an "Upgrade" header set to "WebSocket".
			- If the server supports WebSockets and accepts the request, it responds with a special 101 status code, indicating that the protocol will be changed to WebSocket.
		
		2. **Connection** 
			- Once the handshake is complete, the WebSocket connection is established. This connection remains open until explicitly closed by either the client or the server.
		
		3. **Data Transfer**
			- Both the client and server can now send and receive messages in real-time.
			- These messages are sent in small packets called frames, and carry minimal overhead compared to traditional HTTP requests.
			
		4. **Closure**
			- The connection can be closed at any time either by the client or the server, typically with a close frame indicating the reason for closure.

- ## Advantages of WebSockets
	- **Real-time Updates** - WebSockets enables instant data transmission, making them perfect for applications that require real-time updates, like live chat, gaming or financial trading platforms.
	- **Reduced Latency** - Since the connection is persistent, there's no need to establish a new connection for each message, significantly reducing latencty.
	- **Efficient Resource Usage** - WebSockets are more efficient than traditional polling techniques, as they don't require the client to continuously as the server for updates.
	- **Bi-directional Communication** - Both the client and server can initiate communication, allowing for more dynamic and interactive applications.
	- **Lower Overhead** - After the initial handshake, WebSocket frames have a small header ( as little as 2 bytes ) reducing the amount of data transferred.

- [ ] Read about challenges of websockets,  WebSockets vs. HTTP, Polling, and Long-Polling
