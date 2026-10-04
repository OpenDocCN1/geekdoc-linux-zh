# Using the xinetd Super Server 603

A quick look through the entries in the /etc/services file shows the breadth of networking services available under TCP/IP.

Note: Port number 80 is designated for Web service. In other words, if you set up a Web server on your system, that server listens to port 80. By the way, IANA — the Internet Assigned Numbers Authority (www.iana.org) — is the organization responsible for coordinating the assignment of port numbers below 1,024.

![](bbox=[0.123, 0.193, 0.186, 0.258])

# Using the xinetd Super Server

The client/server architecture of Internet services requires that the server be up and running before a client makes a request for service. A simplistic idea would be to run all the services all the time — impractical each server process would use system resources in the form of memory and processor besides. Besides, you don't need all the services up and ready at all times. A smart solution to this problem is to run a single server, xinetd, that listens to all the ports and then starts the appropriate server when a client requests in. (The xinetd server is a replacement for an older server named inetd, offering improved access control and logging. The name xinetd stands for extended index.)

For example, when a client tries to connect to the TELNET port, xinetd starts the TELNET server and lets it communicate directly with the client (and the TELNET server exits when the client disconnects).

Because it starts various servers on demand, xinetd is known as the Internet super supper. The xinetd server starts a configuration file named /etc/xinetd.conf when the system boots. This file fills xinetd which listens to port all and what server to start for each port. This file can contain instructions that include other configuration files. In Fedora Core, the /etc/xinetd.conf file looks like the following:

```
# Simple configuration file for xinetd
# Some defaults, and include /etc/xinetd.d/
defaults {
    instances = 60
    log_type = SYSLOG authpriv
    log_on_success = HOST PID
    log_on_failure = HOST
    cps = 25 30
}
includedir /etc/xinetd.d
```

Book VIII
Chapter 1

Managing the Servers