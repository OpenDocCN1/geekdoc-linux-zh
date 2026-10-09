
Now you have two Apache parent daemons (that is, run as root) running two sets of child processes where one services static pages and uses the proxy module to fetch the dynamic mod_perl script pages by using the ProxyPass directive. This allows you to service the static pages using a set of child servers that are not running any Perl code whatsoever. On the other hand, the server on port 8080 only services dynamic requests; thus, you effectively have a configuration that is very performance-friendly.

## Going with FastCGI instead of mod_perl

Scripts running under mod_perl run fast because they are loaded within each child-server's code space. Unlike its CGI counterpart, a mod_perl script can maintain a persistent connection to an external database server. This means that database-driven dynamic content generation becomes fast with mod_perl scripts.

However, a new problem introduces itself if you run a very large Web server. When you run 50 or more Apache server processes to service many simultaneous requests, it is possible for Apache to eventually open up that many database connections and to keep each connection persistent for the duration of each child. Say that you run a Web server system through which you run 50 Apache child processes so that you can service approximately 50 requests per second and you happen to have a mod_perl-based script that opens a database connection in the initialization stage. As requests come to your database script, Apache services such requests by using each of its child processes and thus opening up 50 database connections. Because many database servers allocate expensive resources on a per-connection basis, this could be a major issue on the database side.

For example, when making such connections to an IBM Universal Database Server (UDB) Enterprise Edition running on a remote Linux system, each Apache child has a counterpart connection-related process on the database server. If such environment uses load-balancing hardware to balance incoming requests among a set of mod_perl-enabled Apache Web servers, there is likely to be a scenario when each Web-server system, which is running 50 Apache child processes, has all of the child processes opened and connected to the database server. For example, if such an environment consists of 10 Web servers under the load-balancing hardware, then the total possible connections to the database server is 10 × 50, or 500 connections, which might create an extensive resource load on the database server.

One possible solution for such a scenario is to find a way to have the database time-out idle connections, make the mod_perl script code detect stale connections, and have the code reinitiate connection. Another solution is to create a persistent database proxy daemon that each Web server uses to fetch data from the database.

Fortunately, FastCGI or Java Servlets has a more native solution for such problems and should be considered for heavily used database-driven applications. The next section discusses another performance-boosting Web technology called FastCGI.

Like `mod_perl` scripts, FastCGI applications run all the time (after the initial loading) and therefore provide a significant performance advantage over CGI scripts. Table 22-3 explains the differences between a FastCGI application and a `mod_perl` script.

![](img/e11fcbd2818a3495ac70085e5d8d1c26_664_0.png)

To learn more about FastCGI, see Chapter 14.

**Table 22-3**
**Difference Between a FastCGI Application and `mod_perl` Scripts**

| Topic | FastCGI Applications | `mod_perl` Scripts |
| :--- | :--- | :--- |
| Apache platform dependent | No. FastCGI applications can run on non-Apache Web servers such as IIS, Netscape Web Server, and the like. | Yes. Only Apache supports `mod_perl` module. |
| Perl only solution | No. FastCGI applications can be developed in many languages including C, C++, and Perl. | Yes |
| Runs as external process | Yes | No |
| Can run on remote machine | Yes | No |
| Multiple instances of the application/script are run | Typically, a single FastCGI application is run to respond to many requests that are queued. However, if the load is high, multiple instances of the same application are run. | Number of instances of `mod_perl` script that run is equal to the number of child Apache server processes. |
| Wide support available | Yes. However, I sometimes get the impression that FastCGI development is slowing down but I can't verify this or back this up. | Yes. There are a great deal of `mod_perl` sites on the Internet and support via Usenet or Web is available. |
| Database connectivity | Because all requests are sent to a single FastCGI application, you only need to maintain a single database connection with the back-end database server. However, this can change when Apache FastCGI process manager spawns additional FastCGI application instances because of heavy load. Still, the number of FastCGI instances of an application is likely to be less than the number of Apache child processes. | Because each Apache child process runs the `mod_perl` script, each child can potentially have a database connection to the back-end database. This means that you can end up with hundreds of database connections from even a single Apache server system. |

![](img/e11fcbd2818a3495ac70085e5d8d1c26_667_0.png)

# CHAPTER

## Creating a High-Availability Network

### In This Chapter

In this chapter, you learn about design considerations for building a Web network. A Web network is a network of Web server nodes that create a Web service. For example, Yahoo! uses a large number of Web servers, application servers, and database servers to create a multitude of Yahoo! Web services.

- Understanding the features of a Web network
- Enhancing DNS reliability
- Load balancing a Web network
- Managing Web storage
- Creating a back-end network for maintenance
- Fortifying your Web network

If you have decided to integrate the Web into your business, you must consider a Web solution that can grow beyond a single Web server or a shared Web drive space on an ISP. A Web network is one solution. In this chapter, you learn to use proven networking and system management concepts regarding design considerations for building successful Web network. Although the chapter focuses on Apache-on-Linux-based solutions, most of the solutions are applicable to other platforms as well.

## Features of a High-end Web Network

A high-end Web network serves thousands to millions of pages per day. To serve a large number of Web requests it must have these features:

- **Reliable DNS servers.** If your Domain Name Service (DNS) servers are down, no one can easily access your Web sites. So, reliable DNS is a big consideration in Web network design.
- **Load-balanced Web access.** Users connect to one or more Web servers, which are automatically selected based on system loads, and availability.
- **A manageable storage architecture.** Anyone considering a Web network is likely to have a large amount of content, which needs to be made available on all the Web servers in a reliable and manageable manner. Having many Web servers and managing each server’s hard drives can be a nightmare without proper planning and solid storage architecture.
- **Efficient back-end networks.** Large Web sites run many applications and perform millions of database queries, as well as many other back-end tasks, to produce high-quality, personalized content for their visitors. Therefore a solid back-end network is a must. A *back-end network* is a network that is not accessible for Web visitors but serves as the backbone for keeping each server updated and synchronized with the latest contents. Back-end networks also allow administrator to perform various system administration tasks such as backup, software upgrade, and so on.
- **High degree of security.** Designers must pay close attention to security concerns when designing Web networks because hackers often target Web networks that are easy to break in and use them as platforms for attacking other sites. This can result in serious legal hassle.

## Enhancing DNS Reliability

When a site’s DNS is down, it is unreachable by most users. Yes, if you know the IP address of a Web site you can probably access it, but most people don’t even know how to find out what a Web site’s IP address is, so expecting users to visit while your DNS is down is unrealistic.

This is why two DNS servers are required for registering new domains. However, you should consider this requirement as the absolute minimum and you should use more than two servers to increase redundancy and the reliability of your DNS service. Following is the DNS strategy that I often recommend:

- Deploy at least two DNS servers for your Web site(s) as required by most domain name registrars, and preferably more than two.
- Deploy an off-site secondary DNS server. This means that if your local DNS server goes out, the off-site secondary DNS server should still be reachable. For example, if your primary DNS server sits on a network that is temporarily out of order, the off-site secondary server will respond and direct traffic to the appropriate resources. If you do not wish to deploy an off-site DNS server and maintain it yourself, consider using services such as secondary.com.
- Use at least one dedicated DNS server if possible because systems that run multiple services are more likely to be down frequently than the one that runs a single service.
