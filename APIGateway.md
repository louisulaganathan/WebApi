## API GATEWAY ##

Amazon API Gateway is a fully managed service that makes it easy for developers to create, publish, maintain, monitor, and secure APIs at any scale. 
APIs act as the "front door" for applications to access data, business logic, or functionality from your backend services. 
Using API Gateway, you can create RESTful APIs and WebSocket APIs that enable real-time two-way communication applications. 
API Gateway supports containerized and serverless workloads, as well as web applications.

API Gateway handles all the tasks involved in accepting and processing up to hundreds of thousands of concurrent API calls, including traffic management, CORS support, authorization and access control, throttling, monitoring, and API version management.

![direct-client-to-microservice-communication](https://user-images.githubusercontent.com/74425320/115600002-d3190a00-a2a1-11eb-99b7-f55832d6f1fb.png)


Consider the following questions when developing a large application based on microservices:

    How can client apps minimize the number of requests to the back end and reduce chatty communication to multiple microservices?

Interacting with multiple microservices to build a single UI screen increases the number of round trips across the Internet. This approach increases latency and complexity on the UI side. Ideally, responses should be efficiently aggregated in the server side. This approach reduces latency, since multiple pieces of data come back in parallel and some UI can show data as soon as it's ready.

    How can you handle cross-cutting concerns such as authorization, data transformations, and dynamic request dispatching?

**Implementing security and cross-cutting concerns like security and authorization on every microservice can require significant development effort. A possible approach is to have those services within the Docker host or internal cluster to restrict direct access to them from the outside, and to implement those cross-cutting concerns in a centralized place, like an API Gateway.**

    How can client apps communicate with services that use non-Internet-friendly protocols?

Protocols used on the server side (like AMQP or binary protocols) are not supported in client apps. Therefore, requests must be performed through protocols like HTTP/HTTPS and translated to the other protocols afterwards. A man-in-the-middle approach can help in this situation.

##Why API GATEWAY ##

In a microservices architecture, the client apps usually need to consume functionality from more than one microservice. If that consumption is performed directly, the client needs to handle multiple calls to microservice endpoints. 

aving an intermediate level or tier of indirection (Gateway) can be convenient for microservice-based applications. If you don't have API Gateways, the client apps must send requests directly to the microservices and that raises problems, such as the following issues:

  Coupling: Without the API Gateway pattern, the client apps are coupled to the internal microservices. 
  Too many round trips: A single page/screen in the client app might require several calls to multiple services
  Security issues: Without a gateway, all the microservices must be exposed to the "external world"
  Cross-cutting concerns: Each publicly published microservice must handle concerns such as authorization and SSL.

## API GATEWAY ##

The API gateway sits between the client apps and the microservices. It acts as a reverse proxy, routing requests from clients to services. It can also provide other cross-cutting features such as authentication, SSL termination, and cache.

![custom-service-api-gateway](https://user-images.githubusercontent.com/74425320/115600782-aa454480-a2a2-11eb-97cd-376e5d7b1346.png)

Apps connect to a single endpoint, the API Gateway, that's configured to forward requests to individual microservices.

You need to be careful when implementing the API Gateway pattern. Usually it isn't a good idea to have a single API Gateway aggregating all the internal microservices of your application. If it does, it acts as a monolithic aggregator or orchestrator and violates microservice autonomy by coupling all the microservices.

Therefore, the API Gateways should be segregated based on business boundaries and the client apps and not act as a single aggregator for all the internal microservices.

When splitting the API Gateway tier into multiple API Gateways, if your application has multiple client apps, that can be a primary pivot when identifying the multiple API Gateways types, so that you can have a different facade for the needs of each client app. This case is a pattern named "Backend for Frontend" (BFF)

![multiple-custom-api-gateways](https://user-images.githubusercontent.com/74425320/115601395-63a41a00-a2a3-11eb-9a13-d3c4b2a72dcd.png)

An API Gateway can offer multiple features. Depending on the product it might offer richer or simpler features, however, the most important and foundational features for any API Gateway are the following design patterns:

Reverse proxy or gateway routing. The API Gateway offers a reverse proxy to redirect or route requests (layer 7 routing, usually HTTP requests) to the endpoints of the internal microservices. 

Cross-cutting concerns or gateway offloading. Depending on the features offered by each API Gateway product, 


    Authentication and authorization
    Service discovery integration
    Response caching
    Retry policies, circuit breaker, and QoS
    Rate limiting and throttling
    Load balancing
    Logging, tracing, correlation
    Headers, query strings, and claims transformation
    IP allowlisting

## Products: ##

**Azure API Management**  not only solves your API Gateway needs but provides features like gathering insights from your APIs. 
**Amazon API Gateway**
**GraphQL**
