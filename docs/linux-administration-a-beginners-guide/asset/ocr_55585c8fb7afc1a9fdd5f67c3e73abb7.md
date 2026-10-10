of bytes received by the kernel but not read by the process. Next, the Send-Q column tells us the number of bytes sent to the other side of the connection but not acknowledged. 

The fourth, and sixth columns are the most interesting in terms of system security. The Local Address column tells you your own server's IP address and port number. Remember that your server recognizes itself as 127.0.0.1 and 0.0.0.0 as well as its normal IP address. In the case of multiple interfaces, each port being listened to will show up on both interfaces and thus as two separate IP addresses. The port number is separated from the IP address by a colon. In the output from the netstat example shown above, one Ether- net device has the IP address 192.168.1.1, and the PPP connection has the address 209.179.251.53. Your IP addresses will vary depending on your setup.

The fifth column, Foreign Address, identifies the other side of the connection. In the case of a port that is being listened to for new connections, the default value will be 0.0.0.0.*. This IP address means nothing since we're still waiting for a remote host to connect to us!

The sixth column tells us the State of the connection. The man page for netstat lists all of the states, but the two you'll see most often are LISTEN and ESTABLISHED. The LISTEN state means there is a process on your server listening for the port and ready to accept new connections. The ESTABLISHED state means just that—a connection is established between a client and server.

# Security Implications of netstat's Output

By listing all of the available connections, you can get a snapshot of what the system is doing. You should be able to explain and justify all ports listed. If your system is listening to a port that you cannot explain, this should raise suspicions.

If you've been using your memory shell for other purposes and haven't memorized the services and their associated port numbers, you can look up the matching info you need in the /etc/services file. Some services, however (most notably those that use the portmapper), don't have set port numbers but are valid services. To see which process is associated with a port, use the -p option with netstat. On the lookout for odd or unusual processes using the network. For example, if the BASH shell is listening to a network port, you can be fairly certain that something odd is going on.

Finally, remember that you are only interested in the destination part of a connection; this tells you which service is being connected to and whether it is legitimate. Unfortunately, netstat doesn't explicitly tell us who originated a connection, but with a little thinking we can usually figure it out. The general rule of thumb is that the side whose port number is greater than 1024 is the side that originated the connection. Obviously, this general rule doesn't apply to services typically running on ports higher than 1024, such as X Windows (port 6000).

# Shutting Down Services

One purpose for the netstat command is to determine what services are enabled on your servers. Making Linux easier to install and manage right out of the box has led to more and more default settings that are unsafe, so keeping track of services is especially important.