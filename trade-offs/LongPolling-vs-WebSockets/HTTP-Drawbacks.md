# Drawbacks of Traditional HTTP
- HTTP follows a client-driven request-response model
	- Client sends a request to the server.
	- Server processes the request and sends the response to the client
	- Connection closes
- But this model has following limitations
	- **No automatic updates** - With plain HTTP, the server cannot proactively push data to the client. The client has to request the data periodically.
	- **Stateless Nature** - HTTP is stateless, means each request stands alone with no persistant connection to the server. This can be problematic if we need continuous exchange of data.
