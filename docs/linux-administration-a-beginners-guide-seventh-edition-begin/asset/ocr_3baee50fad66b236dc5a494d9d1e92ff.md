# 408 Linux Administration: A Beginner's Guide

```
tcp      0 192.168.1.4:22     192.168.1.135:52248       ESTABLISHED
tcp      0 ::::111                     ::*                          LISTEN
udp      0 0.0.0.0:776               0.0.0.0:*
udp      0 0.0.0.0:68                0.0.0.0:*
udp      0 0.0.0.0:42827           0.0.0.0:*
udp      0 0.0.0.0:56781           0.0.0.0:*
udp      0 ::::111                       ::*
```

By default (with no parameters), **netstat** will provide all established connections for both network and domain connections. That means we'll see not only the connections that are actually working over the network, but also (which, from a security monitoring standpoint, might not be immediately). In the command we just illustrated, netstat to show all ports (-a)—whether they are listening or actually connected—for TCP (-t) and UDP (-u). We now have netstat to prevent any time resolving IP addresses to hosts (-n).

In the **netstat** output, each line represents either a TCP or UDP network port, as indicated by the first column of the output. The Recv-Q (receive queue) column lists the number of bytes received by the kernel but not read. Next, the Send-Q (send queue) column tells us the number of bytes sent to the other side of the connection but not acknowledged.

The fourth, fifth, and sixth columns are the most interesting in terms of system security. The Local address column tells us server's IP address and port number. Remember that our server recognizes itself as 127.0.0.1 and 0.0.0.0, as well as its normal IP address. In case of multiple interfaces, each port listened to will usually show up on all interfaces, and thus, as IP addresses. The port number is separated from the IP address by a colon (:). In the output, the Ethernet device has the IP address 192.168.1.4.

The fifth column, Foreign Address, identifies the other side of the connection. In the case of a port being listened to for new connections, the default value will be 0.0.0.0. This IP address means nothing, since we're still waiting for a moment host to connect!

The sixth column tells us the state of the connection. The man page for netstat lists all of the ports, but you'll see most often are LISTEN and ESTABLISHED. The LISTEN state means that a process on your server is listening on the port number and ready to accept new connections. The ESTABLISHED state means just—a connection is established between a client and server.

# Security Implications of netstat's Output

By listing all of the available connections, you can get a snapshot of what the system is doing. You should be able to explain and account for all ports listed. If your system is listening to a port you cannot explain, this would raise suspicion.

Just in case you've forgotten all the well-known services and their associated port numbers (all 25 billion of them!), you can look up the matching information you need in the /etc/services file. However, some services (most notably those that use the portmapper) don't have port numbers but are valid services.