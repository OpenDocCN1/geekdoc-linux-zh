# Chapter 10 • PROVIDING HIGH AVAILABILITY IN YOUR UNIX SYSTEM 259

# **TABLE 10.1** Continued

| Application | Notes | Balancing Scheme |
|---|---|---|
| BIND (DNS) | | Round robin |
| IMAP server | | Least connections |
| LDAP server | Mostly reads | Round robin |
| POP server | | Least connections |
| sendmail (SMTP) | | Least connections |

# **Load-Balancing Software**

You can choose from many methods to implement load balancing for your applications, some of which are available in the applications themselves. Although using load-balancing software is economical, remember that the underlying application must provide the load-balancing functionality—the servers themselves are responsible for distributing the load. If the application or the server runs on fails, do you have options for redundant balancers to prevent an outage?

That said, the load-balancing methods that some enterprise software packages employ are quite effective. The most common of these methods are master-slave and shared scheduling.

# **Master-Slave**

The master-slave method designates one machine in a pool of servers as the “master.” The master is responsible for receiving all network requests and distributing them evenly among the resources in the pool (see Figure 10.4). This methodology is also used in dedicated load-balancing hardware, but the difference is that the master server also participates in the pool—it runs the application software as well as performing load-balancing duties. Although this simple method is quite effective, the master server does introduce a single point of failure.

# **FIGURE 10.4**

A master-slave load-balancing scheme. Note how the master, server1, also participates in the pool by handling some of the requests itself.

![](bbox=[0.305, 0.683, 0.775, 0.915])