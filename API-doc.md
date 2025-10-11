# Application Programming Interface ( API )
- An API is a bunch of code that takes an input and gives a predictable outputs.
- An API is a set of rules and protocols that allows two software systems to communicate with each other.
- It defines how requests are made, how responses are structured and what data and functionalities are accessible between systems.
- API follows are request-response model.
	- Client ( web or app ) makes a request to an API.
	- API ( hosted on a server ) processes the request, interacts with the necessary databases, other serviecs and prepares a response.
	- API sends response back to the client in a structured format ( usually JSON/XML ).
- Inputs
	- Every API requires specific type of input, passing wrong data can results in errors.
	- APIs often validate inputs before processing, which helps to maintain accuracy and security.
- Output :- API returns a well structured response.
- Most applications follows ***frontend-backend*** architecture, where :
	- **Backend** :- Consists of APIs, that handles data processing, business logic and communication with databases.
	- **Frontend** :- Graphical User Interface ( GUI ) that interacts with these APIs, making applications user-friendly and accessible without requiring uses to write code.

- ## Components of API
	1. **Endpoint** :- URL or address where api is accessible.
	2. **Method** :- Type of operation ( GET, PUT, POST, DELETE... ).
	3. **Headers** :- Metadata about the request ( eg :- authorization, content type ).
	4. **Body** :- Data sent in the request.
	5. **Response** :- Data returned by the API.
	6. **Status Code** :- Indicates the result.

- ## Types of APIs
	1. **Open APIs** ( Public APIs ) - Accessible to external developers with minimal retrictions.
	2. **Internal APIs** ( Private APIs) - Designed exclusively for internal use within an organization.
	3. **Code Interfaces** ( also called library APIs or programming APIs ) - These APIs don't connect different applications. Instead they provide predefined functions within a programming language or framework to make development easier.

- ## API Communication Methods
	- APIs communicate using different protocols and architectures that define how requests are sent, how responses are structured, and how data is exchanged between systems.

	1. **REST ( Representational State Transfer )**
		- Most widely used communication method.
		- It is lightweight, stateless and scalable making it perfect for web and mobile applications.
		- REST APIs follow a set of design principles and uses HTTP methods ( GET, PUT, POST, DELETE ) to perform operations.
		- REST APIs are based on resources, and each resource is accessed through a URL ( endpoint ).
		- The API follows client-server model.

	2. **SOAP ( Simple Object Access Protocol )**
		- SOAP is older api communication method that relies on XML-based messaging.
		- SOAP is more structured and secure, making it ideal for banking, healthcare, and enterprise applications.
		- SOAP messages are sent using XML format and requires WSDL ( Web Services Description Language ) file, which defines the APIs available functions and request structure.

	3. **GraphQL**
		- GraphQL is alternative to REST that allows client to request exactly the data they need, making it more effiecient for modern applications.
		- GraphQL can fetch the entire required data in a single api request call unlike REST which requires multiple API calls.
		- Instead of predefined endpoints, GraphQL exposes a single endpoint, and client sends queries to request specific fields.

	4. **gRPC ( Google Remote Procedural Call )**
		- High performance API communication method that uses Protocol Buffers ( Protobuf ) instead of JSON or XML, making it faster and more efficient.
		- gRPC uses binary data instead of text-based formats, reducing payload size and it supports bidirectional streaming ( client and server can send data at the same time ).

- ## Benefits of API
	- Decoupling - Frontend and backend can evolve independently.
	- Reusability - Common services can be reused by multiple apps.
	- Scalability - Easy to distribute and load balance services.
	- Integration - Connects different platforms and systems easily.
	- Automation - Enable programatic access for scripts and bots.

- ## API Gateway.
	- In microservices architecture, instead of exposing every service individually, we route them through API gateway.
	- Responsibilities.
		- Central entry point for all APIs
		- Authentication and rate limiting.
		- Load balancing.
		- Request/response transformation.
		- Logging and monitoring.
