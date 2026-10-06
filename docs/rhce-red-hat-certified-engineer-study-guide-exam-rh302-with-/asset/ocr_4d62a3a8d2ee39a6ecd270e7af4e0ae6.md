TCP/IP Model 89

# UDP

The UDP enables applications to send finite-length messages from one host to another. Like IP, UDP is a connectionless, unreliable protocol. Its main virtue is low overhead, which makes it suitable for short, infrequent host-to-host interactions and interactions in which dropping a message now again is less important than sending data quickly. When error detection and recovery are needed, TCP is used.

# TCP

The TCP enables applications to send streams of data from one host to another. Unlike IP and UDP, TCP is a connection-oriented protocol. Before hosts exchange data via TCP, a session is initiated. The service provides error control by such means as sequence-checking of the discrete messages that compose the data stream. Creating a session and performing error-checking and recovery entails some overhead; consequently, TCP is preferred over UDP only when these considerations are important.

# Application Protocols

TCP/IP provides many application protocols, known as services. Moreover, programmers can easily create new services based on the UDP or TCP protocols. A service is associated with a port, a 16-bit number that identifies the service. UDP and TCP ports are distinct; a service based on UDP can have the same port as one based on TCP without confusion. Accessing ports 0–123 under UNIX requires root privileges. Consequently, these ports are known as privileged ports. The remaining ports are known as non-privileged ports.

Certain ports are associated with long standing practice with specific services. Certain ports are associated with long standing practice with specific services. For example, port 7 is associated with the echo service (used by the ping command). Such ports are called well-known ports. Under UNIX, the file /etc/services identifies the well-known ports. Table 4.1 summarizes important TCP/IP services and their port numbers. You will find additional services listed in the /etc/services file distributed with Red Hat Linux.

Copyright ©2000 SYBEX, Inc., Alameda, CA      www.sysex.com