The “routed” routing daemon automatically finds all active network ports when it starts and sends and listens for messages on each of the network devices to allow it to determine and update the routing table on the host.

This has been a very brief explanation of dynamic routing and where you would use it. If you want more information then you should refer to the suggested references listed at the top of the document.

The important points relating to dynamic routing are:

+   You only need to run a dynamic routing protocol daemon when your Linux machine has the possibility of selecting multiple possible routes to a destination.

+   The dynamic routing daemon will automatically modify your routing table to adjust to changes in your network.

+   RIP is suited to small-to-medium sized networks.

# ## Configuring Your Network Servers and Services

Network servers and services are those programs that allow a remote user to make user of your Linux machine. Server programs listen on network ports. Network ports are a means of addressing a particular service on any particular host and are how a server knows the difference between an incoming telnet connection and an incoming ftp connection. The remote user establishes a network connection to your machine and the server program, the network daemon program, listening on that port accepts the connection and executes. There are two ways that network daemons may operate. Both are commonly employed in practice. The two ways are:

**standalone** The network daemon program listens on the designated network port and when an incoming connection is made it manages the network connection itself to provide the service.

**slave to the inetd server** *The inetd server* is a special network daemon program that specializes in managing incoming network connections. It has a configuration file that tells it what program needs to be run when an incoming connection is received. Any service port may be configured for either of the tcp or udp protocols. The ports are described in another file that we will talk about soon.