
improve it. In our experience with many customers in the field, many of the problems uncovered can be fixed by making changes in the application alone.

The two main reasons for a badly performing application are as follows:

-   *Bad application design.* Not even the smartest application server can help if the design of the enterprise application is very bad to begin with. Architectural designs and design patterns are one of the leading areas of expertise today. Software architects should be sure to consider performance early in the design of an application.
-   *Poor programming practices.* Bad programming habits can easily lead to poor performance. Programmers should be educated and understand well the programming model and language they are using. Many papers and presentations cover best practices for J2EE application development and Java programming.

## The Application Server

The application server can be written in native code, but J2EE is essentially a Java framework. For easier interaction and integration with other Java-based frameworks, such as JMX, JDBC, and JNDI, most application servers are written in Java. This is also favorable for application server vendors because they can easily port their product to different platforms.

As a Java application, the application server is subjected to the same assessments as enterprise applications. A badly designed application server will very likely exhibit poor performance. In this market, vendors compete as to who has the best-performing application server. Thus, every ounce of improvement in the design and implementation of an application server can go a long way. A good design is one that is performance-oriented from the start.

**Figure 18-2** shows the generic architecture of a J2EE application server. Note that the diagram is not a software architecture; instead, it simply shows what components are included and the interactions of those components.

**Figure 18-2. The application server that is shown here is based mainly on the J2EE specifications, which require two containers: the web and EJB containers.**

![](img/08b574e80eed8279bfda286dbd25d40d_482_0.png)

![](img/08b574e80eed8279bfda286dbd25d40d_483_0.png)

Requests can be channeled to the application server from two possible types of clients: the HTTP client and the thick Java client. The HTTP client is usually done through a web browser that transmits an HTTP request to a web server that is a front end to the application server. A plug-in is typically installed into the web server to enable communication with the application server. This installation can be done during the installation of the application server. When an application server receives an HTTP request from the web server, it determines which web application must handle the request by examining the Uniform Resource Identifier (URI). For dynamic HTML pages, the request is served by a servlet (Java Server Pages are converted to servlets after compilation). Per the J2EE specification, web requests are processed in a web container inside the application server. Meanwhile, servlets can also call an EJB, which resides in the EJB container of the application server. Depending on the business logic, the request may involve accessing resources, such as a data source, through a JDBC provider or a message queue through JMS.

A thick client is a complete Java application running somewhere in its own Java runtime environment. EJB lookups, creations, and calls to EJB methods are coded in the application. This is similar to Remote Procedure Calls (RPC), a mechanism used in distributed systems prior to the creation of Java. The protocol used to execute the remote method is typically the Remote Method Interface over Internet Inter-Orb Protocol (RMI/IIOP), which allows the capabilities of the Common Object Request Broker Architecture (CORBA) for distributed systems to be implemented on the Java 2 platform. CORBA is a specification by the Object Management Group (OMG). Some vendors, such as BEA, use a proprietary protocol, but RMI/IIOP is the expected protocol by most J2EE application servers. Java clients communicate directly with EJBs; requests are routed through the EJB container of the application server.

The dominant type of client remains the HTTP client (or web client). Most J2EE enterprise applications have a web module and EJB modules. The Java-based clients are catching up, but the web clients are likely to remain the dominant interface in the coming years. This is especially true now that web services are the cutting-edge technology. Most web services use the SOAP protocol with HTTP as the transport mechanism.

In summary, the critical, major components in an application server for performance are the web container, the web server plug-in, the EJB container, the ORB, and the interfaces within the various resources.

### The Java Virtual Machine

From a performance perspective, the Java Virtual Machine (JVM) is one of the most critical components of the application server because most, if not all, of the application server's code is executed by the JVM. The application server must be written in such a way that it leverages the best features of the JVM.

Some vendors offer several JVMs to run the application server and allow the user to select his preference, while others ship and prepackage their JVM. Ideally, however, users should be able to manually change their JVM (possibly with extra steps that are specific to the application server configuration). The ability to change the JVM is advantageous because it lets you use the best-performing JVM that is currently available.

The SPEC organization provides a standard benchmark application called SPECjbb2000 that can be used to evaluate the performance of servers running typical Java business applications. The evaluation takes into consideration both hardware and software aspects of JVM servers. SPECjbb2000 represents an order-processing application for a wholesale supplier. For more information, visit SPEC at http://www.spec.org/jbb2000.

The specific components of the JVM that are critical to application servers include the networking libraries, the garbage-collection mechanism, the memory management subsystem, and the JIT compiler. Extensions to JVM, such as RMI/IIOP and Java security, are also important components.

Another important area to consider is the set of flags that are available for the JVM. You can use these flags to tune the JVM based on the characteristics of the J2EE application and the application server itself.

### Native Code

In the performance stack, some native code has to be executed one way or another. Native code is closest to the operating system. In the case of the application server, the JVM is written in a third-generation language such as C or C++ and is directly compiled to produce the native code that is then executed by the host machine. Other components, such as back-end resources and enterprise applications, might contain some native code as well.

We believe that native application performance also depends heavily on how the application is written. The JVM itself is an application program that has been architected, designed, and implemented. A critical component of the JVM is the JIT (just-in-time) compiler, in which some methods of a Java application might be compiled to native code at runtime. In general, features (the JIT compiler and C++ compiler, for example) contain code optimization features so that the code they produce performs as well as possible. To achieve high performance, compiler writers need to have a deep understanding of the host machine's architecture as well as the underlying operating system. They also need to understand the resources and system calls available from the operating system, as well as its policies. In this case, understanding how the Linux kernel works and the major features and fixes that come with every release of the kernel is very important.

### The Hardware and the Operating System

The choice of hardware platform on which to run your application server is a big factor to consider because it is the hardware that executes all instructions. It is almost superfluous to discuss hardware in this section, but some things need to be emphasised.

First, choosing a hardware platform is a task that every business owner must do at an early stage. This task may or may not be easy, depending on many factors and their impact, such as the existing hardware the business currently has and the legacy applications on these assets.

Second, business owners are constantly faced with the many challenges of rapid advances in hardware performance. For example, processor speeds continue to go up, and performance techniques, such as hyperthreading, are on the rise. Computer architecture continues to evolve toward better performance and higher capacity. 64-bit machines are on their way, Non-Uniform Memory Access (NUMA) is getting a lot of attention, and blade servers are currently very popular because they have the advantage of being small and yet are very powerful and scalable.

The third and probably most important issue is the choice of operating system on these machines. The purpose of the operating system is to manage the hardware resources and the processes that run on the machines. Bad and inefficient operating systems can waste a lot of what the hardware has to offer. Thus, the operating system is a key contributor to the performance stack.

An operating system is essentially a software application, and its performance depends heavily on its overall design and implementation. The Linux operating system started as a UNIX-like operating system for the personal computer. It has now matured to the operating system for many enterprise-level systems, such as IBM's eServers that span the Intel, PowerPC, and 390 architectures; the Sun Fire systems from Sun; the SGI Altix systems; the HP ProLiant Servers; and the HP Integrity Superdome (based on Itanium processors).

One of the advantages of application servers using Java is portability. Portability is ideal for a heterogeneous environment. Portability lets you write applications without worrying about the target platform ahead of time. Heterogeneity gives you the flexibility to mix and match available hardware and operating system platforms that you may already have or are planning to requisition.

Because the application server is just one component of a bigger enterprise system, you need to plan which platform and operating system each component should run on. For example, most systems use Intel servers for their web servers and big UNIX systems for their application servers. The back-end data sources are typically mainframe systems or legacy systems.
