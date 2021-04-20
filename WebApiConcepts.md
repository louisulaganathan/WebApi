## API ##

API is some kind of interface which has a set of functions that allow programmers to access specific features or data of an application, 
operating system or other services.

## WEB API ##

Web API as the name suggests, is an API over the web which can be accessed using HTTP protocol. 
It is a concept and not a technology. 
We can build Web API using different technologies such as Java, .NET etc. 

## ASP.NET WEB API ##

The ASP.NET Web API is an extensible framework for building HTTP based services that can be accessed in different applications 
on different platforms such as web, windows, mobile etc. 
It works more or less the same way as ASP.NET MVC web application except that it sends data as a response instead of html view. 
It is like a webservice or WCF service but the exception is that it only supports HTTP protocol.

![webapi-overview](https://user-images.githubusercontent.com/74425320/115456519-dc926b80-a1e8-11eb-9975-df34a3a35a57.png)

## ASP.NET Web API Characteristics ##

    1. ASP.NET Web API is an ideal platform for building RESTful services.
    2. ASP.NET Web API is built on top of ASP.NET and supports ASP.NET request/response pipeline
    3. ASP.NET Web API maps HTTP verbs to method names.
    4. ASP.NET Web API supports different formats of response data. Built-in support for JSON, XML, BSON format.
    5. ASP.NET Web API can be hosted in IIS, Self-hosted or other web server that supports .NET 4.0+.
    6. ASP.NET Web API framework includes new HttpClient to communicate with Web API server. HttpClient can be used in ASP.MVC server side, 
    Windows Form application, Console application or other apps.
    
## ASP.NET Web API Versions ##
|Web API Version 	|Supported .NET Framework 	|Coincides with 	|Supported in|
|-----------------|---------------------------|-----------------|------------|
|Web API 1.0 	|.NET Framework 4.0 	|ASP.NET MVC 4 	V|S 2010|
|Web API 2 	|.NET Framework 4.5 	|ASP.NET MVC 5 	|VS 2012, 2013|
|.Core Web API| .Net Core 3.1| ASP.NET Core 3.1|VS2017, VS2019|

## ASP.NET Web API vs WCF ##
|Web API 	|WCF|
|---------|----|
|Open source and ships with .NET framework. 	|Ships with .NET framework|
|Supports only HTTP protocol. 	|Supports HTTP, TCP, UDP and custom transport protocol.|
|Maps http verbs to methods 	|Uses attributes based programming model.|
|Uses routing and controller concept similar to ASP.NET MVC. 	|Uses Service, Operation and Data contracts.|
|Does not support Reliable Messaging and transaction. 	|Supports Reliable Messaging and Transactions.|
|Web API can be configured using HttpConfiguration class but not in web.config. 	|Uses web.config and attributes to configure a service.|
|Ideal for building RESTful services. 	|Supports RESTful services but with limitations. |


### When to choose WCF? ###

    Choose WCF if you use .NET Framework 3.5. Web API does not support .NET 3.5 or below.
    Choose WCF if your service needs to support multiple protocols such as HTTP, TCP, Named pipe.
    Choose WCF if you want to build service with WS-* standards like Reliable Messaging, Transactions, Message Security.
    Choose WCF if you want to use Request-Reply, One Way, and Duplex message exchange patterns.

### When to choose ASP.NET Web API? ###

    Choose Web API if you are using .NET framework 4.0 or above.
    Choose Web API if you want to build a service that supports only HTTP protocol.
    Choose Web API to build RESTful HTTP based services.
    Choose Web API if you are familiar with ASP.NET MVC.
    


