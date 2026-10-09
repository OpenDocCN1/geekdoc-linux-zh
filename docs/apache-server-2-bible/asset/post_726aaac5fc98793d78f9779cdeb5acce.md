
# 14 Configuring Apache for FastCGI

This chapter discusses FastCGI and how it solves the performance problems inherent in CGI, without introducing the overhead and complexity of proprietary APIs. FastCGI is fast, open, and maintainable. It offers features such as in-memory caching, persistent connections, and distributed architecture. The migration path from CGI to FastCGI is also reasonably simple.

## What is FastCGI?

Simply speaking, a FastCGI application acts like a server application, which is often called a daemon in the Unix world. Unlike a CGI script, a FastCGI application is persistent and services all incoming requests by using a single instance, eliminating the overhead of starting a new process per request as in the CGI version. For example, if you need to generate a set of dynamic pages by using contents from a database, a CGI script has to connect to the database every time it is run per request. On the other hand, a FastCGI application can connect once and keep the connection alive for all the subsequent requests, and this time-saving results in higher performance. Hence, FastCGI is considered a high-performance alternative to CGI for writing Web-server applications in a variety of languages, including Perl, C, C++, Java, and Python.

The existence of CGI, FastCGI, and the Server API creates a great deal of confusion for developers and server administrators. To shed some light on this murky subject, Table 14-1 provides some key feature comparisons among these technologies.

### In This Chapter

- Explaining FastCGI
- Describing the basic architecture of a FastCGI application
- Compiling and installing the FastCGI module for Apache
- Configuring httpd.conf to run FastCGI applications

Table 14-1: Comparing CGI, Server API, and FastCGI

| Feature | CGI | Server API | FastCGI |
| :--- | :--- | :--- | :--- |
| Programming language dependency | Language independent. CGI applications can be written in almost any programming language (usually C/C++). | Applications have to be written in a language supported by the vendor API programming language. | Language independent. Like CGI, FastCGI applications can be written in any programming language. |
| Process isolation | Applications separate processes; buggy applications cannot crash the Web server or access the server’s private internal state and compromise security. | Feature not supported. Because the FastCGI applications run in the server’s address space, buggy applications can corrupt the core server. | A buggy application cannot crash or corrupt the core server or other applications. |
| Type of standard | Open standard. Some form of CGI has been implemented on every Web server. | Proprietary. Coding your application to a particular API locks you into a particular vendor’s server. | Nonproprietary, proposed open standard. Support is under development for other Web servers, including commercial servers from Microsoft and Netscape. Apache currently supports FastCGI as a third-party module. |
| Platform dependency | Platform independent. CGI is not tied to any particular server architecture (single-threaded, multithreaded, threaded, and so on). | Tie-in to server architecture. API applications have to share the same architecture as the server. If the Web server is multi-threaded, the application has to be thread safe. If the Web server has single-threaded processes, multithreaded applications don’t gain any performance advantage. | Platform independent. The FastCGI is not tied to any particular server architecture. Any Web server can implement the FastCGI interface. |
| Performance | A new process is created for each request and thrown away whether request is done; efficiency is poor. | Applications run in the server process and are persistent across requests. The CGI startup/initialization problem is absent. | FastCGI processes are persistent; they are reused to handle multiple requests. The CGI startup/initialization problem is absent. |
| Complexity | Easy to understand. | Very complex. Vendor APIs introduce a steep learning curve, with increased implementation and maintenance costs. | Simple, with easy migration from CGI. |
| Distributed architecture | Not supported. To run CGI applications on a remote system, a Web server is needed on that system, because CGI applications are run by Web servers. | Depends on vendor. | Supported. FastCGI applications can be run on any host that supports TCP/IP. |

### Achieving high performance by using caching

How fast is FastCGI? The answer depends on the application. If an application reads data from files and the data can be cached into memory, the FastCGI version of this application provides better performance than either CGI or an API-based Web-server application. A CGI application by specification cannot make use of in-memory cache because a new instance of the application runs per request and exits after request processing is complete. Similarly, most widely used API-based Web-server applications run on child processes that do not share memory, and therefore no caching can be applied. Even if in-memory caching is implemented per child process in this model, it works very poorly because each child process has to have a copy of the cache in memory, which wastes a great deal of memory.

FastCGI is designed to enable effective in-memory caching. Requests are routed from any child process to a FastCGI application server. The FastCGI application process maintains an in-memory cache. Note that in some cases a single FastCGI application server would not provide enough performance. With multithreading you run an application process designed to handle several requests at the same time. The threads handling concurrent requests share process memory, so they all have access to the same cache.

### Scalability through distributed applications

Unlike CGI applications, FastCGI applications do not get the CGI environment variables from their process environment table. Instead, a full-duplex connection between the application and the Web server is used to communicate the environment information, standard input and output, and errors. This enables FastCGI applications to run on remote machines using TCP/IP connections to the Web server, as shown in Figure 14-1. This figure shows that requests from the Internet are handled by www.nitec.com (the Web server), which connects remotely via TCP connection to fcgi.nitec.com where requests are then handled by Fast CGI scripts.

## Putting FastCGI through its paces

The developers of FastCGI performed tests that used three versions of an application (based on CGI, FastCGI, and a popular Web server-based API specification) that interacted with a database server. What the developers learned was that when the FastCGI version of the application used in-memory caching and persistent connection to the database server, it outperformed both CGI and the API-based versions of the application by a large margin.

When the in-memory cache was disabled for the FastCGI application, and persistent connection was used for the API-based application, the API-based application performed slightly better than the FastCGI version. This means that only when a level playing field is used (that is, FastCGI advantages such as the in-memory caching feature are disabled) the API version wins. But why would you disable caching? In other words, as long as you do not write a crippled FastCGI application, it is likely to outperform both CGI and API versions.

The tests demonstrated that the FastCGI-based application’s architectural advantage resulted in a performance that was three times faster than the API counterpart. This factor is likely to be more dramatic if the applications have to connect to remote resources such as a remote database server. However, they also point out that a multithreaded Web server capable of maintaining cache and persistent connections for its API application threads is likely to outperform FastCGI applications. This is caused by the absence of interprocess communication overhead in a threaded environment. Developing multithreaded applications requires very careful design and programming, as a single faulty thread can shut down the entire Web server system.

On the other hand, FastCGI processes take advantage of the process isolation model, where they run as external processes. This provides a safety net for the Web server system. In case of a faulty FastCGI application, the Web server will still function. If you just love multithreading and can’t live without it, you can always write your FastCGI applications in a multithreaded model, which still takes advantage of the process isolation model.
