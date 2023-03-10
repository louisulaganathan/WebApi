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

## WebApi 20 Features:##
External Auth
Attribute based routing
OData support
Cors Cross Origin Resource Sharing support
Passing Complex types using newtonsoft Jarray arraylist

HttpAuthenticationContext in OnAuthentication
HttpActionContext in ActionExecuted

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
    
 ## TEST WEB API ##
 
 Web api can be debugged and tested using fiddler, postman, swagger doc[open API spec].
 
 https://www.tutorialsteacher.com/webapi/test-web-api
    
## Web API Filters ##

Web API includes filters to add extra logic before or after action method executes. Filters can be used to provide cross-cutting features such as logging, exception handling, performance measurement, authentication and authorization.

Filters are actually attributes that can be applied on the Web API controller or one or more action methods. Every filter attribute class must implement IFilter interface included in System.Web.Http.Filters namespace.

## Dependency Injection concepts ##

![principles-and-patterns](https://user-images.githubusercontent.com/74425320/115464705-19636000-a1f3-11eb-991f-5b64ab795adb.png)


## Inversion of Control ##

IoC is a design principle which recommends the inversion of different kinds of controls in object-oriented design to achieve loose coupling between application classes. In this case, control refers to any additional responsibilities a class has, other than its main responsibility, such as control over the flow of an application, or control over the dependent object creation and binding (Remember SRP - Single Responsibility Principle). If you want to do TDD (Test Driven Development), then you must use the IoC principle, without which TDD is not possible. Learn about IoC in detail in the next chapter.


## Dependency Inversion Principle ##

The DIP principle also helps in achieving loose coupling between classes. It is highly recommended to use DIP and IoC together in order to achieve loose coupling.

DIP suggests that high-level modules should not depend on low level modules. Both should depend on abstraction.

The DIP principle was invented by Robert Martin (a.k.a. Uncle Bob). He is a founder of the SOLID principles. Learn more about DIP in the DIP chapter.

## Dependency Injection ##

Dependency Injection (DI) is a design pattern which implements the IoC principle to invert the creation of dependent objects. We will learn about it in the DI chapter.


## IoC Container ##

The IoC container is a framework used to manage automatic dependency injection throughout the application, so that we as programmers do not need to put more time and effort into it. There are various IoC Containers for .NET, such as Unity, Ninject, StructureMap, Autofac, etc. 

![ioc-steps](https://user-images.githubusercontent.com/74425320/115465187-d2299f00-a1f3-11eb-9e57-a6e9c60f9750.png)


## Versioning ##

Approaches:
-----------

    1.URI 
    2.Query string
    3.Request Header.  -> Good

### URI Versioning ###

```
    [Route("api/V1/[controller]")]
    public class CatalogController:ControllerBase
    {
        :
        :
    }
    or
    [ApiVersion("2.0")]
    [Route("Api/Helloworld")
    public class HelloWorld: controller
    {
    }
    
    
    **WebAPIConfig.cs**
    Register(HttpConfiguration config)
    {
        config.MapHttpAttributeRoutes();
        config.MapHttpRoute(name:"Emp1",
            RouteTemplate: "api/V1/Employee/{id}",
            defaults: new { controller = "Employee1", id = RouteParam.Optional});
        config.MapHttpRoute(name:"Emp2",
            RouteTemplate: "api/V2/Employee/{id}",
            defaults: new { controller = "Employee2", id = RouteParam.Optional});
    }
    
```

## ASP.NET CORE API versioning ##

** Query String **

Below config services code is required for querystring and url based versioning.
```
public void ConfigureServices( IServiceCollection services)
{
    services.UseMVC();
    services.AddApiVersioning();
}
```
```
services.AddApiVersioning(config =>
{
  config.DefaultApiVersion = new ApiVersion(1, 0);
  config.AssumeDefaultVersionWhenUnspecified = true;
  config.ReportApiVersions = true;
});
```

**Controller impln**

```
[Route("api/[controller]")]
    [ApiController]
    [ApiVersion("1.0")]
    [ApiVersion("1.1")]
    [ApiVersion("2.0")]
    public class DefaultController : ControllerBase
    {
        string[] authors = new string[]
        { "Joydip Kanjilal", "Steve Smith", "Anand John" };
        [HttpGet]
        public IEnumerable<string> Get()
        {
            return authors;
        }
    }
    
    //[ApiVersion("1.0", Deprecated = true)]
    
    //Below method will serve only uri /v2/id not v1/id
    [HttpGet("{id}")]
    [MapToApiVersion("2.0")]
    public string Get(int id)
    {
       return authors[id];
    }
 ```
 
 URL Pattern:
 
 http://localhost:25718/api/default?api-version=1.0
 
 
 
 ### URL Pattern ###
 
 ```
 [Route("api/v{version:apiVersion}/[controller]")]
[ApiController]
[ApiVersion("1.0")]
[ApiVersion("1.1")]
public class DefaultController : ControllerBase
    {
        string[] authors = new string[]
        { "Joydip Kanjilal", "Steve Smith", "Stephen Jones" };
        [HttpGet]
        public IEnumerable<string> Get()
        {
            return authors;
        }
        [HttpGet("{id}")]
        [MapToApiVersion("2.0")]
        public string Get(int id)
        {
            return authors[id];
        }
    }
    
```

** URL Pattern** 
http://localhost:25718/api/v2.0/default/1
http://localhost:25718/api/v1.0/default



### Request Header ###

```
services.AddApiVersioning(config =>
{
   config.DefaultApiVersion = new ApiVersion(1, 0);
   config.AssumeDefaultVersionWhenUnspecified = true;
   config.ReportApiVersions = true;
   config.ApiVersionReader = new HeaderApiVersionReader("api-version");
});
```

http://localhost:25718/api/default/1


## Exception Handling in WebAPI ##

HttpResponseException
Exception Filters
Registering Exception Filters
HttpError

## HttpResponseException ##

```
public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        throw new HttpResponseException(HttpStatusCode.NotFound);
    }
    return item;
}

public Product GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var resp = new HttpResponseMessage(HttpStatusCode.NotFound)
        {
            Content = new StringContent(string.Format("No product with ID = {0}", id)),
            ReasonPhrase = "Product ID Not Found"
        };
        throw new HttpResponseException(resp);
    }
    return item;
}
```

## Exception Filters ##
An exception filter is executed when a controller method throws any unhandled exception that is not an HttpResponseException exception.

```
namespace ProductStore.Filters
{
    using System;
    using System.Net;
    using System.Net.Http;
    using System.Web.Http.Filters;

    public class NotImplExceptionFilterAttribute : ExceptionFilterAttribute 
    {
        public override void OnException(HttpActionExecutedContext context)
        {
            if (context.Exception is NotImplementedException)
            {
                context.Response = new HttpResponseMessage(HttpStatusCode.NotImplemented);
            }
        }
    }
}
```
## Registering Exception Filters ##
There are several ways to register a Web API exception filter:

By action
By controller
Globally

```
public class ProductsController : ApiController
{
    [NotImplExceptionFilter]
    public Contact GetContact(int id)
    {
        throw new NotImplementedException("This method is not implemented");
    }
}
```
```
[NotImplExceptionFilter]
public class ProductsController : ApiController
{
    // ...
}
```
```
GlobalConfiguration.Configuration.Filters.Add(
    new ProductStore.NotImplExceptionFilterAttribute());
```

```
public static class WebApiConfig
{
    public static void Register(HttpConfiguration config)
    {
        config.Filters.Add(new ProductStore.NotImplExceptionFilterAttribute());

        // Other configuration code...
    }
}
```
## HttpError ##
The HttpError object provides a consistent way to return error information in the response body. The following example shows how to return HTTP status code 404 (Not Found) with an HttpError in the response body.
```
public HttpResponseMessage GetProduct(int id)
{
    Product item = repository.Get(id);
    if (item == null)
    {
        var message = string.Format("Product with id = {0} not found", id);
        return Request.CreateErrorResponse(HttpStatusCode.NotFound, message);
    }
    else
    {
        return Request.CreateResponse(HttpStatusCode.OK, item);
    }
}
```





