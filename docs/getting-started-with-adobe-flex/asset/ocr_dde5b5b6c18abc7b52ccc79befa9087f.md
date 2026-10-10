![](bbox=[0.16, 0.17, 0.84, 0.29])

Figure 7.1 – Flex application communicating with a server

In the figure you can see how a typical Flex application communicates with the application server. On the left hand side is the browser that uses HTML or other client-side scripting language to communicate with the server. The Flex application, app.swf in the figure is embedded within the HTML file and contains the logic to communicate with the server using either a Web service using SOAP (Simple Object Access Protocol) and XML or HTTP Service using simple text or XML. Flex can also communicate directly with the server and access the remote objects directly using its remote object invocation APIs which in turn uses AMF (Action Message Format).

# 7.2 Working with Web services

As defined by oas-is-open, “a Web Service is a software component that is described via WSDL and is capable of being accessed via standard network protocols such as but not limited to SOAP over HTTP”. The underlying implementation can be either, Java, .Net, PHP, Ruby or other language.

In Figure 7.2 below you can see that the service provider can expose the list of services that it wants to make available to the service requester.

![](bbox=[0.2, 0.59, 0.74, 0.65])

![](bbox=[0.2, 0.66, 0.74, 0.79])

Figure 7.2 – Web Service Architecture

The business logic can be in Java, .Net or any other language. In order to expose the application to the outside world, Web services are used by the service provider which uses standard protocols like HTTP and SOAP (Simple Object Access Protocol). The function of