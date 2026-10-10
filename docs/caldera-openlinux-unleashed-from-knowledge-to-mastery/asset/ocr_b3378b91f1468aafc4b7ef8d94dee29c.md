+   Class C: 192.168.0.0 through 192.168.255.0. (All addresses beginning with 192.168.)

# Background Material

Linux features IP masquerading, which allows translation between real IP addresses and private IP addresses to take place on a firewall, without either the outside or inside host being aware of it. Always pick private IP addresses for internal networks.

# TCP

The Transmission Control Protocol is a transport protocol built on IP. It creates a virtual error-free channel for two processes to communicate.

TCP adds the concept of a port to the addressing scheme. When a TCP connection is made from one host to another, the originating end is associated with an IP address and a 16-bit port number. Similarly, the destination end has an IP address and port number. One analogy is that of a telephone conversation: The telephone numbers correspond to IP addresses and identify the hosts (or houses). Ports are like names of particular people; a given house may might have more than one person who uses the telephone just as a host might have more than one process that uses TCP.

Note that a TCP connection is fully identified by four pieces of information: the source address, source port, destination address, and destination port. It is quite possible (in fact, very common) for different TCP connections to have the same destination address and port. They are distinguished by the source address and port.

The *telnet* program allows you to remotely log in to another machine. It works as follows: On the destination machine, a telnet daemon (a program that runs in the back-ground) “listens” for incoming connections on a “well-known” port number (port 23). The telnet client picks any available port and initiates a connection to port 23 on the destination machine. The telnet daemon responds and lets you log in. You can open another telnet session to the same machine; although both telnet clients talk to destination port 23, they have different source ports, and the destination TCP code keeps track of both connections.

The telnet client picks any available port and initiates a connection to port 23 on the destination machine. The telnet daemon responds and lets you log in.