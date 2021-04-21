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
**Ocelot** Ocelot is a lightweight API Gateway, recommended for simpler approaches. Ocelot is an Open Source .NET Core-based API Gateway especially made for microservices architectures that need unified points of entry into their systems.
**Amazon API Gateway**
**GraphQL**

there are many other products in the market offering API Gateways features, such as** Apigee, Kong, MuleSoft, WSO2**


**GRAPHQL**

GraphQL is a query language for APIs and a runtime for fulfilling those queries with your existing data. GraphQL provides a complete and understandable description of the data in your API, gives clients the power to ask for exactly what they need and nothing more, makes it easier to evolve APIs over time, and enables powerful developer tools
**INTRODUCTION **
---------------------------
GraphQL is a query language for your API, and a server-side runtime for executing queries using a type system you define for your data. GraphQL isn't tied to any specific database or storage engine and is instead backed by your existing code and data.

A GraphQL service is created by defining types and fields on those types, then providing functions for each field on each type. For example, a GraphQL service that tells you who the logged in user is (me) as well as that user's name might look like this:

type Query {
  me: User
}
 
type User {
  id: ID
  name: String
}

Along with functions for each field on each type:

function Query_me(request) {
  return request.auth.user;
}
 
function User_name(user) {
  return user.getName();
}

After a GraphQL service is running (typically at a URL on a web service), it can receive GraphQL queries to validate and execute. The service first checks a query to ensure it only refers to the types and fields defined, and then runs the provided functions to produce a result.

For example, the query:

{
  me {
    name
  }
}

Could produce the following JSON result:

{
  "me": {
    "name": "Luke Skywalker"
  }
}
------------------------------------------

Big Picture (Architecture)

**GraphQL has been released only as a specification.** This means that GraphQL is in fact not more than a long document that describes in detail the behaviour of a GraphQL server.

## Use Cases ##

In this section, we’ll walk you through 3 different kinds of architectures that include a GraphQL server:

    GraphQL server with a connected database
    GraphQL server that is a thin layer in front of a number of third party or legacy systems and integrates them through a single GraphQL API
    A hybrid approach of a connected database and third party or legacy systems that can all be accessed through the same GraphQL API

All three architectures represent major use cases of GraphQL and demonstrate the flexibility in terms of the context where it can be used.

**1. GraphQL server with a connected database**

This architecture will be the most common for greenfield projects. In the setup, you have a single (web) server that implements the GraphQL specification. When a query arrives at the GraphQL server, the server reads the query’s payload and fetches the required information from the database. This is called resolving the query. It then constructs the response object as described in the official specification and returns it to the client.

It’s important to note that GraphQL is actually transport-layer agnostic. This means it can potentially be used with any available network protocol. So, it is potentially possible to implement a GraphQL server based on TCP, WebSockets, etc.

GraphQL also doesn’t care about the database or the format that is used to store the data. You could use a SQL database like AWS Aurora or a NoSQL database like MongoDB.

GraphQL server with a connected database
A standard greenfield architecture with one GraphQL server that connects to a single database.

![GraphQL-1](https://user-images.githubusercontent.com/74425320/115612773-3cece000-a2b1-11eb-8b27-a428ce0af5ac.png)

**2. GraphQL layer that integrates existing systems**

Another major use case for GraphQL is the integration of multiple existing systems behind a single, coherent GraphQL API. This is particularly compelling for companies with legacy infrastructures and many different APIs that have grown over years and now impose a high maintenance burden. One major problem with these legacy systems is that they make it practically impossible to build innovative products that need access to multiple systems.

In that context, GraphQL can be used to unify these existing systems and hide their complexity behind a nice GraphQL API. This way, new client applications can be developed that simply talk to the GraphQL server to fetch the data they need. The GraphQL server is then responsible for fetching the data from the existing systems and package it up in the GraphQL response format.

Just like in the previous architecture where the GraphQL server didn’t care about the type of database being used, this time it doesn’t care about the data sources that it needs to fetch the data that’s needed to resolve a query.

GraphQL layer that integrates existing systems
GraphQL allows you to hide the complexity of existing systems, such as microservices, legacy infrastructures or third-party APIs behind a single GraphQL interface.

![GraphQL-2](https://user-images.githubusercontent.com/74425320/115612803-45ddb180-a2b1-11eb-8fa8-6ee9bc8d7699.png)


**3. Hybrid approach with connected database and integration of existing system**

Finally, it’s possible to combine the two approaches and build a GraphQL server that has a connected database but still talks to legacy or third—party systems.

When a query is received by the server, it will resolve it and either retrieve the required data from the connected database or some of the integrated APIs.

![GraphQL-3](https://user-images.githubusercontent.com/74425320/115612900-63ab1680-a2b1-11eb-8716-627d847687fa.png)


Hybrid approach with connected database and integration of existing system
Both approaches can also be combined and the GraphQL server can fetch data from a single database as well as from an existing system - allowing for complete flexibility and pushing all data management complexity to the server.

## Resolver Functions ##

But how do we gain this flexibility with GraphQL? How is it that it’s such a great fit for these very different kinds of use cases?

As you learned in the previous chapter, the payload of a GraphQL query (or mutation) consists of a set of fields. In the GraphQL server implementation, each of these fields actually corresponds to exactly one function that’s called a resolver. The sole purpose of a resolver function is to fetch the data for its field.

When the server receives a query, it will call all the functions for the fields that are specified in the query’s payload. It thus resolves the query and is able to retrieve the correct data for each field. Once all resolvers returned, the server will package data up in the format that was described by the query and send it back to the client.

Screenshot containing some of the resolved field names
The above screenshot contains some of the resolved field names. Each field in the query corresponds to a resolver function. The GraphQL calls all required resolvers when a query comes in to fetch the specified data.

![GraphQL-4](https://user-images.githubusercontent.com/74425320/115612989-7c1b3100-a2b1-11eb-98a4-2199c8ddf5f7.png)


## GraphQL Client Libraries ##

GraphQL is particularly great for frontend developers since it completely eliminates many of the inconveniences and shortcomings that are experienced with REST APIs, such as over- and underfetching. Complexity is pushed to the server-side where powerful machines can take care of the heavy computation work. The client doesn’t have to know where the data that it fetches is actually coming from and can use a single, coherent and flexible API.

Let’s consider the major change that’s introduced with GraphQL in going from a rather imperative data fetching approach to a purely declarative one. When fetching data from a REST API, most applications will have to go through the following steps:

    construct and send HTTP request (e.g. with fetch in Javascript)
    receive and parse server response
    store data locally (either simply in memory or persistent)
    display data in the UI

With the ideal declarative data fetching approach, a client shouldn’t be doing more than the following two steps:

    describe data requirements
    display data in UI

All the lower-level networking tasks as well as storing the data should be abstracted away and the declaration of data dependencies should be the dominant part.

This is precisely what GraphQL client libraries like Relay or Apollo will enable you to do. They provide the abstraction that you need to be able to focus on the important parts of your application rather than having to deal with the repetitive implementation of infrastructure.

