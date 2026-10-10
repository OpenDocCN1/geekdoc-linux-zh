➢ **TFTP (Trivial File Transfer Protocol)** is for transferring files from one system to another. (It’s typically used by X terminals and diskless workstations to download boot files from another host on the network.) TFTP data transfer takes place on port 69.

Each service is provided by a *server process* — a computer program that runs on a system awaiting client requests that arrive at the well-known port associated with its service. Thus the Web server expects client requests at port 80, the standard port for HTTP service.

The `/etc/services` text file on your Linux system stores the association between a service name and a port number (as well as a protocol). Here is a small subset of entries in the `/etc/services` file from a Linux system:

```
`ftp-data      20/tcp`
`ftp         21/tcp    fsp   21/udp`
`ssh         22/tcp    fspd  22/udp    # SSH Remote Login Protocol`
`ssh         22/udp`
`telnet      23/tcp`
`satp        25/tcp    mail`
`time        37/tcp    timerserver`
`time        37/udp    timerserver`
`rhp         39/tcp    resource    # resource location`
`nameserver  42/tcp    name        # IEN 116`
`whos        43/udp    nicname`
`tacacs      49/tcp            # Login Host Protocol (TACACS)`
```

A quick look through the entries in the `/etc/services` file shows the breadth of networking services available under TCP/IP.

> **Note:** Port number 80 is designated for Web services. In other words, if you set up a Web server on your system, that server listens to *port* 80. By the way, IANA — the Internet Assigned Numbers Authority (*www.iana.org*) — is the organization responsible for coordinating the assignment of port numbers below 1,024.

![](bbox=[0.08, 0.6, 0.2, 0.68])

![](bbox=[0.88, 0.5, 0.96, 0.55])

![](bbox=[0.88, 0.52, 0.96, 0.54])

![](bbox=[0.88, 0.55, 0.96, 0.58])

![](bbox=[0.88, 0.58, 0.96, 0.61])

# ## Using the *Internet Super Server*

The client/server architecture of Internet services requires that the server is up and running before a client makes a request for service. It’s probably a bad idea to run all the servers all the time — impractical because each server process uses up system resources in the form of memory and processor time. Besides, you don’t really need *all* the services up and ready at all times. A smart solution to this problem is to run a single server that listens to all the ports and then starts the appropriate server when a client request comes in. Such a server is known as the *internet super server* because it starts various services on demand.