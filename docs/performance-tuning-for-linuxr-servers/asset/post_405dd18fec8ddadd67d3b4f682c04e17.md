
- Distributable. A number of application servers must be able to be created and grouped in a cluster.
- Heterogeneous. Application servers running on different platforms should be able to interoperate.
- Multiple services in one. Although the application server's main function is to execute web and Enterprise Java Beans applications, many services are componentized within the server itself. These services include transaction services, security services, web services, and naming services. Thus, the application server is much more complicated than it first appears.
- Multiple applications in one. An application server must be able to serve many applications. In other words, business owners should be able to deploy as many applications as they deem necessary. The direct effect of this is a greater workload for the application server itself, especially when these applications are made available at the same time to their respective target users.
- Non-uniform, unpredictable requests. The incoming flow of requests to the application server can fluctuate. Because of the nature of the web, there are often high and low volume times that can vary from day to day and from hour to hour within a day. The application server must be able to handle situations where there is a sudden avalanche of requests.
- High volume. The high volume of transactions that need to be processed is what really separates application servers from other servers. The exposure to the world via the Internet is what made transaction processing transcend to a different level. Transactions can be on the order of thousands or even millions each day.

## Application Servers on Linux

Commercial application servers that run in Linux exist today and have become undeniably popular. Vendors of application server products, including those known to support only the powerhouse servers, now have Linux in their platform portfolio. Table 18-1 is just a short list of these vendors. Notice that even the major application server vendors, such as IBM, BEA, and Oracle, are major supporters of Linux.

### Table 18-1. Application Server Vendors with Linux Support.

| Vendor | Product | JDK Version | EJB Version | JSP Version | Linux Distribution |
| :--- | :--- | :--- | :--- | :--- | :--- |
| BEA | WebLogic | 1.4 | 2.0 | 1.2 | RH AS 2.1 |
| Borland | Enterprise Server | 1.3, 1.4 | 2.0 | 1.2 | Linux |
| Bull | JonAS | 1.2, 1.3, 1.4 | 1.1, 2.0 | | Linux |
| CauchO | Resin | 1.1, 1.2, 1.3 | | 1.2 | Linux |
| Fujitsu Software Corp. | Interstage | 1.3 | 2.0 | 1.2 | Linux |
| IBM | WebSphere | 1.3 | 2.0 | 1.2 | RH Linux, SUSE, Turbo Linux, Linux/390 |
| IONA | Orbix ASP | 1.3, 1.4 | 2.0 | 1.2 | RH 7.2 |
| Ironflae | Orion | 1.4 | 2.0 | 1.2 | Linux |
| JBoss.org | JBoss | 1.3, 1.4 | 2.0 | 1.2 | Linux |
| Macromedia | JRun | 1.3 | 2.0 | 1.2 | SUSE Linux, RH Linux |
| Novell | extend Application Server | 1.3 | 2.0 | 1.2 | Linux |
| Oracle | Oracle9i AS | 1.3, 1.4 | 2.0 | 1.1, 1.2 | Linux |
| Persistence | Power Tier for J2EE | 1.2, 1.3 | 1.1 | 1.1 | Linux |
| Prmati Technologies | Prmati Server | 1.3 | 2.0 | 1.1 | Linux |
| SAP AG | Web Application Server | 1.3 | 1.1 | 1.1 | Linux |
| Sun Microsystems | Sun ONE | 1.4 | 2.0 | 1.2 | RH 7.2, Sun Linux 5.0 |
| Sybase | EAServer | 1.2, 1.3 | 1.1, 2.0 | 1.1, 1.2 | Linux |
| Trifork | Enterprise Application Server | 1.4 | 2.0 | 1.2 | RH Linux 6.2 |

Data was taken from TheServerSide.com web site at http://theserverside.com.

Enterprize businesses are investing seriously on Linux-based applications. Future predictions from Giga and Gartner are all in favor of Linux. For example, the Gartner group thinks that by 2006, Linux will be a key foundation for a strategic cross-development platform environment creating a powerful alternative to Microsoft's .NET on Windows. Reports like these are just one of the strong reasons why people migrate to Linux, not to mention the attractive cost-effectiveness of the platform. The good thing is that although application servers are not lightweight servers, they are small enough to run in small and less-expensive machines. Thus, a network of Linux servers can provide the necessary horsepower.

## The Software Performance Stack

This section focuses on the performance needs of application servers and is centered on three major topics:

- Major contributors to the overall performance
- Ways to improve performance
- The influence of Linux on performance

Unlike the performance characterization of other systems, such as network servers and file server, the performance characterization of application servers is much more involved because of the complex nature of application servers. Network and file servers are easier to understand and control because they are stand-alone and very lightweight, and the interactions involved with them are very minimal or limited only to the operating system. The J2EE specification continues to evolve to include more services and functional requirements and enhancements. For example, the latest specification, J2EE 1.4, includes web services, among other things, which necessitates more computations and processing (for example, SOAP protocol processing, XML parsing, and JAX-RPC, to name a few). For more information on J2EE specifications, visit the J2EE web site at http://java.sun.com/j2ee.

Application servers are also very high-level applications whose scope encompasses many, if not all, of the subsystems discussed in this book. For that matter, application servers can serve as excellent end-to-end benchmark applications for Linux servers.

## The Complexity of the J2EE Framework

Under the hood, the J2EE-based application server is a complex aggregate of components that correspond to numerous services. To characterize the application server’s overall performance, the individual performance of these components and their underlying infrastructure must be taken into account. Because this is not an easy task, the most common and accepted approach is to benchmark the application server with a representative J2EE application. Different benchmark applications can be written, with each focusing on a certain aspect of the application server. For example, one application can exercise HTTP session performance, while another can exercise persistence performance of entity beans. An industry-standard benchmark application by the Standard Performance Evaluation Corporation (SPEC; http://www.spec.org ), called SPECjAppServer, is frequently used to benchmark application servers.

What happens beneath the application is transparent when benchmarking an application server. Figure 18-1 shows the layers of components that are involved in a J2EE environment where the performance of one layer affects that of the next layer. We call this layered model the software performance stack.

![](img/08b574e80eed8279bfda286dbd25d40d_480_0.png)
![](img/08b574e80eed8279bfda286dbd25d40d_481_0.png)

At the very top of the stack are the J2EE enterprise applications that are executed by the application server. The application server strictly provides the runtime and threads of execution for the applications as defined by the J2EE specifications. Notice that applications can interact with other back-end resources either through the application server or directlythe application can call special libraries that provide a wrapper for accessing databases, or the application can use data sources via JDBC. Nothing prohibits application developers from writing some parts of their applications in native code. The same is true with back-end resources and other software services.

The application server itself is a Java application (although some parts of it can be written in native code), which means that the JVM's performance plays a major part. The enterprise applications coexist with the application server in the JVM's runtime environment. From the JVM's perspective, the enterprise applications are just part of the application server because the latter executes the former.

The remaining layers, of course, are typical in many other systems. Note that as the method or function calls go down the stack, some overhead is accrued and the overall performance of the application is affected by how good or bad the underlying layers performed.

## The Enterprise Application

Many performance analysts say that at least 75% of the time the leading cause of bad performance is the enterprise application itself. If the problem in the performance stack is at the uppermost layer, the lower layer cannot do much to help
