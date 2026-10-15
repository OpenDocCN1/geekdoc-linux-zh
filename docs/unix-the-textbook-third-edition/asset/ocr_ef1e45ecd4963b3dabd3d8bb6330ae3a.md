```
67008  4  S    0:00.00 ./selects
67009  4  R+   0:00.00 ps
% ./udptimec 202.147.169.196 8001 udp
Wed Aug 19 00:11:09 2015
% ./udptimec 127.0.0.1 8001 udp
Wed Aug 19 00:11:13 2015
% ./udp echo 202.147.169.196 8002 udp
Enter text for server : That's all folks!
Text from server : That's all folks!
% kill -9 67008
%
```

# EXERCISE 20.24

Repeat this session on your UNIX system to verify that it works as expected.

# EXERCISE 20.25

At which port is each service offered?

# EXERCISE 20.26

Run the client and server processes in different windows on the same machine and on different machines on the Internet. Verify working of the concurrent server with multiple simultaneous clients.

# 20.10 THE UNIX SUPERSERVER: INETD

When you offer a network service on a system, the corresponding daemon runs on the system. This means that the main memory and several kernel data structures allocated to the daemon are used. If some services are sparingly used, you can offer them through a single server that monitors the client requests on the sockets associated with the services and runs the corresponding server daemons only on demand. This scheme makes efficient use of the main memory and kernel data structures. A server that offers multiple network services is called a superserver.

In UNIX, inetd offers several basic Internet services and is known as the UNIX superserver. It is dynamically configurable; that is, it can reconfigure itself while it runs. It executes as a single master process, creates sockets for each of the services that it is to offer according to the type of communication (SOCK_STREAM, SOCK_DGRAM, etc.) and relevant protocol to be used (TCP, UDP, etc.), binds a name to each socket, and monitors client requests on these sockets using the select() system call. When a client request arrives on a socket, the master server process forks a slave (child) process, hands over the request to it, and goes back to wait for new client requests. The slave process uses a call in the exec() family to overlay itself with the executable code for the corresponding service. The /etc/inetd.conf file specifies complete information about all the services that inetd