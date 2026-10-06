
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

By default (with no parameters), **netstat** will provide all established connections for both network and domain connections. That means we'll see not only the connections that are actually working over the network, but also (which, from a security monitoring standpoint, might not be immediately obvious). In the command we just illustrated, netstat to show all ports (-a)—whether they are listening or actually connected—for TCP (-t) and UDP (-u). We now have netstat to prevent any time resolving IP addresses to hosts (-n).

In the **netstat** output, each line represents either a TCP or UDP network port, as indicated by the first column of the output. The Recv-Q (receive queue) column lists the number of bytes received by the kernel but not read. Next, the Send-Q (send queue) column tells us the number of bytes sent to the other side of the connection but not acknowledged.

The fourth, fifth, and sixth columns are the most interesting in terms of system security. The Local address column tells us server's IP address and port number. Remember that our server recognizes itself as 127.0.0.1 and 0.0.0.0, as well as its normal IP address. In case of multiple interfaces, each port listened to will usually show up on all interfaces, and thus, as IP addresses. The port number is separated from the IP address by a colon (:). In the output, the Ethernet device has the IP address 192.168.1.4.

The fifth column, Foreign Address, identifies the other side of the connection. In the case of a port being listened to for new connections, the default value will be 0.0.0.0. This IP address means nothing, since we're still waiting for a host to connect!

The sixth column tells us the state of the connection. The man page for netstat lists all of the ports, but you'll see most often are LISTEN and ESTABLISHED. The LISTEN state means that a process on your server is listening on the port number and ready to accept new connections. The ESTABLISHED state means just—a connection is established between a client and server.

# Security Implications of netstat's Output

By listing all of the available connections, you can get a snapshot of what the system is doing. You should be able to explain and account for all ports listed. If your system is listening to a port you cannot explain, this would raise suspicion.

Just in case you've forgotten all the well-known services and their associated port numbers (all 25 thousand of them!), you can look up the matching information you need in the /etc/services file. However, some services (most notably those that use the portmapper) don't have port numbers but are valid services.

# CHAPTER 15 Network Security 409

To see which process is associated with a port, use the -p option with netstat. For example, if you are looking for odd or unusual processes using the network sockets, if the Bourne Again Shell (Bash) is listening to a network port, you can be fairly certain that something is going on!

Finally, remember that you are mostly interested in the destination port of a connection; this tells you which service is being connected and whether it is legitimate. The source address and source port are, of course, important, too—especially if somebody has opened an unauthorized back door into your system. Unfortunately, netstat does not explicitly tell you who originated a connection, but you can easily figure out by becoming familiar with the applications that you use and their use of network ports is the best way to determine which connection originated to where. In general, you'll find that the rule of thumb is that the side whose port number is greater than 1024 is the side that originated the connection. Obviously, this general rule doesn't apply to all services. Some oddballs run on ports higher than 1024, such as the X Window System (6000).

# Binding to an Interface

A common approach to improving the security of a service running on your server is to make sure that it binds only to a specific network interface. By default, applications will bind to all interfaces (as 0.0.0.0 in the netstat output). This will allow a connection to that service from any interface—so long as the connection makes past any Netfilter rules (built-in Linux kernel firewall stack) you have configured. However, if you need a service to be available only on a particular interface, you should configure that service to bind to the specific interface.

For example, let us assume there are three interfaces on your server:

- eth0, with the IP address 192.168.1.4
- eth1, with the IP address 172.16.1.1
- lo, with the IP address 127.0.0.1

And also assume that your server does not have forwarding (/proc/sys/net/ipv4/ip_forward) enabled. In other words, machines on the 192.168.1.0/24 (eth0) side cannot communicate with machines on the 172.16/16 side. The 172.16/16 (eth1) network represents the “safe” or “inside” network, and of course, 127.0.0.1 (lo or loopback) represents itself.

If the application binds to 172.16.1.1, then only those hosts on the 172.16/16 network will be able to reach the connection and connect to it. If you do not trust the hosts on the 192.168.1/24 side (for example, it is a demilitarized zone, or DMZ), this is a safe way to provide services to one segment without exposing yourself to another. For even less exposure, you can bind to 127.0.0.1. By doing so, you can almost guarantee that connections will have to originate from the server itself to communicate with the service.

# 410 Linux Administration: A Beginner's Guide

For example, if you need to run the MySQL database for a web-based application and the application runs on the server, configuring MySQL to accept only connections from 127.0.0.1 makes any risk associated with remotely exploiting the service significantly mitigated. The attacker would have to compromise your web-based application and somehow make it query the database on the attacker's behalf (perhaps via a SQL injection attack) in order to circumvent this.

# SSH Tunneling Tricks

If you need to temporarily provide a service to a group of users across the Internet, binding the service to the loopback address (localhost) and then forcing the group to use SSH tunnels is a great way to provide authenticated and encrypted access to the service. For example, if you have a Post Office Protocol 3 (POP3) service running on your server, you can bind the service to the localhost address. This, of course, nobody will be able to connect to the POP3 server via a remote interface. But if you run an SSH server on the system, authenticated users can connect via SSH and set up a port-forwarding tunnel to the remote server. Here's a sample command to do this from the remote SSH client:

```
ssh -l <username> -L 1110:127.0.0.1:1110 <REMOTE_SSH_SERVER>
```

After successfully establishing an SSH connection to the server using the previous command, any POP3 e-mail client can then be configured to connect to the POP3 server at the IP address 127.0.0.1 via port 1110.

# Shutting Down Services

Striking a reasonable balance between ease of installation/manageability of Linux servers and providing a secure out-of-box experience in Linux distros is a delicate process. One of the side effects can be seen in some distributions that aim to oversimplify things for end users by adopting unsafe default settings, as to provide convenience for the end user. The task of seeking out these unsafe default settings is thus left to the system administrator.

When you're evaluating which services should stay and which should go, answer the following questions:

- Do we need the service? The answer to this question is important. In most situations, you should be able to disable a great number of services that start up by default. A stand-alone web server, for example, does not need to run Network File System (NFS).
