---
created: 2024-01-11T15:22
updated: 2024-01-11T15:29
---
# Protocols
### REST (Representational State Transfer):
REST is an architectural style for designing distributed systems. It was introduced and defined in 2000 by computer scientist Roy Fielding in his doctoral dissertation. REST is based on a set of principles, which include:
1. **Client-Server**: A separation of concerns where the user interface concerns are separated from the data storage concerns, improving the portability of the user interface across multiple platforms and scalability by simplifying server components.
2. **Stateless**: Each HTTP request from a client to a server must contain all the information the server needs to fulfill the request. The server should not store any session information about the client.
3. **Cacheable**: Responses should be implicitly or explicitly labeled as cacheable or non-cacheable so that clients can reuse responses to improve efficiency.
4. **Uniform Interface**: A standardized way of interacting with server resources through HTTP methods (GET, POST, PUT, DELETE, etc.) that simplifies and decouples the architecture, which enables each part to evolve independently.
5. **Layered System**: The architecture is composed of hierarchical layers, which helps to structure an application into layers that have specific functionality, and where each layer can only "see" the immediate layer with which they are interacting.
6. **Code on Demand (optional)**: Servers can extend client functionality by transferring executable code (for instance, JavaScript scripts) to the client.

### RESTful
A RESTful web service or API is one that adheres to the REST architectural principles. An API or web service is considered RESTful when it meets the constraints and design principles of REST.

For example:
- An API that uses HTTP for communication, using standard HTTP methods in a way that follows REST principles, such as using GET for retrieving resources and POST for creating new resources, would be a RESTful API.

- A RESTful API would also be stateless, meaning that each request contains all the necessary information so that the server does not need to maintain session information.
Often, RESTful is used to describe services or APIs that strive to comply with REST principles, whereas REST is more of a conceptual framework. In practice, you'll see APIs and services being labeled as RESTful when they attempt to realize the principles of REST in their operations and design. However, due to the practical constraints and needs of different applications, you may find APIs that are more or less "RESTful" based on how strictly they adhere to REST's constraints.

### SOAP (Simple Object Access Protocol)
SOAP is a protocol for exchanging structured information in the implementation of Web Services in computer networks. It relies heavily on XML, and typically works with HTTP (but can work with other protocols as well). Unlike REST, which is architectural style, SOAP includes a set of rules and standards along with a specification. It provides a robust mechanism for error handling and is often favored in enterprise environments for its security features and transactional reliability.

### gRPC (gRPC Remote Procedure Calls)
gRPC is a high-performance, open-source RPC (remote procedure call) framework initially developed by Google. It uses HTTP/2 for transport, Protocol Buffers as the interface description language, and it is designed for the efficient connection between services in microservices architectures. It has built-in features like authentication, load balancing, retries, and more. gRPC is particularly suited for service-to-service communication and is language-agnostic, meaning clients and servers can be written in different programming languages.

### GraphQL
A query language developed by Facebook for APIs. Unlike the other technologies listed, it allows clients to request only the data they need and nothing more. It's often used as a more flexible and efficient alternative to REST.

### OData (Open Data Protocol):
An ISO/IEC approved, OASIS standard that defines a set of best practices for building and consuming RESTful APIs. It allows for both simple and complex queries and provides a way to help clients consume APIs.

### WebSockets
A protocol providing full-duplex communication channels over a single TCP connection. WebSockets are typically used for real-time applications like live chatting and gaming.

### JSON-RPC and XML-RPC
Protocols that allow for remote procedure calls encoding the calls as JSON or XML. They are simpler than SOAP and are often used in lightweight applications where the overhead of additional features is not necessary.

## Architectures
1. **Monolithic Architecture:**
 - **Description:** Often used for small to medium-sized applications, a monolithic architecture is a single-tiered software application in which different components are combined into a single program on a single platform. All components for a software application are interconnected and interdependent.
 - **Pros:** Easy to develop, test, deploy, and scale horizontally by running multiple copies behind a load balancer.
 - **Cons:** Can become unwieldy, hard to understand and manage as the application grows; challenging to scale certain components independently.

2. **Microservices Architecture:**
 - **Description:** An approach where a single application is composed of many loosely coupled and independently deployable smaller services. Each service runs a unique process and communicates through a well-defined, lightweight mechanism to serve a business goal.
 - **Pros:** Services can be deployed independently, enabling continuous deployment and scalability; allows for using different technologies and languages for different services.
 - **Cons:** Complex to design and deploy; inter-service communication can introduce latency; requires sophisticated management, monitoring, and DevOps practices.

3. **Service-Oriented Architecture (SOA):**
 - **Description:** An architecture pattern in which application components provide services to other components via a communication protocol, usually over a network. SOA emphasizes decoupled components and reusable services.
 - **Pros:** Promotes reuse of existing services, flexibility, and integration with other services; facilitates distributed deployment and scalability.
 - **Cons:** Can be complex with significant overhead; potential performance bottlenecks due to communication overhead.

4. **Serverless Architecture:**
 - **Description:** An architecture where the cloud provider dynamically manages the allocation of machine resources. Developers can build and run applications and services without thinking about servers. It usually refers to Function-as-a-Service (FaaS) platforms.
 - **Pros:** Reduces operational cost and complexity; scales automatically; developers focus solely on the individual functions in their application code.
 - **Cons:** Might have limitations in terms of runtime and memory; can become expensive for high-traffic applications; debugging and monitoring can be challenging.

5. **Event-Driven Architecture:**
 - **Description:** An architecture pattern centered around the production, detection, consumption, and reaction to events. Components are loosely coupled and communicate through events, enabling highly adaptable and scalable systems.
 - **Pros:** Highly flexible and scalable; components can be easily added or removed; conducive to asynchronous processing.
 - **Cons:** Complexity of the system can increase; handling event consistency and order can be challenging.

6. **Layered (N-tier) Architecture:**
 - **Description:** This architecture divides an application into layers, typically including presentation, business logic, persistence, and database layers. Each layer has a specific role and responsibility and communicates with the layers directly above and below it.
 - **Pros:** Organized and easy to maintain; each layer can evolve independently; widely understood and used.
 - **Cons:** Layering can introduce latency and sometimes redundant logic; can become complex if layers are not well-defined.

7. **Jamstack Architecture:**
 - **Description:** A modern web architecture that revolves around client-side JavaScript, reusable APIs, and prebuilt Markup. Jamstack stands for JavaScript, APIs, and Markup. It aims to make websites faster, more secure, and easier to scale.
 - **Pros:** Sites are fast and secure; development is streamlined; hosting and scaling are simplified due to static file serving.
 - **Cons:** Not suitable for highly dynamic web applications; relies on third-party services for backend functionalities.

8. **Progressive Web App (PWA):**
 - **Description:** A PWA is a type of application software delivered through the web, built using common web technologies including HTML, CSS, and JavaScript. It is intended to work on any platform that uses a standards-compliant browser, with a focus on mobile user experience.
 - **Pros:** Provides a native app-like experience, offline usage, and device integration; can be deployed and accessed through a web browser.
 - **Cons:** May not have full access to device capabilities as compared to native apps; browser compatibility issues may arise.