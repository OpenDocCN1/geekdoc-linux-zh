We will begin by looking at the fundamental network interface, the socket. With that as a foundation, we will go on to examine how common application-level network protocols can be used in embedded devices.

# ## Sockets

The “socket” interface, first introduced in the Berkeley versions of Unix, forms the basis for most network programming in Unix systems. Sockets are a generalization of the Unix file access mechanism that provides an endpoint for communication, either across a network or within a single computer. A socket can also be thought of as an extension of the named pipe concept that explicitly supports a client/server model, wherein multiple clients may be attached to a single server.

The principal difference between file descriptors and sockets is that a file descriptor is bound to a specific file or device when the application calls `open()`, whereas sockets can be created without binding them to a specific destination. The application can choose to supply a destination address each time it uses the socket, for example when sending datagrams, or it can bind the destination to the socket to avoid repeatedly specifying the destination, for example when using TCP.

Both the client and server may exist on the same machine. This simplifies the process of building client/server applications. You can test both ends on the same machine before distributing the application across a network. By convention, network address 127.0.0.1 is a “local loopback” device. Processes can use this address in exactly the same way they use other network addresses.

> **Try it out**
> 
> Execute the command `/sbin/ifconfig`. This will list the properties and current status of network devices in your system. You should see at least two entries: one for the Ethernet interface, and the other for lo, the local loopback device.
> 
> This command should work on both your development host and your target with similar results. `ifconfig`, with appropriate arguments, is also the command that sets network interface properties.

# ## The Server Process

Fig. 10.1 illustrates the basic steps that the server process goes through to establish communication. We start by creating a socket and then `bind()` it to a name or destination address. For local sockets, the name is a file system entry, often in `/tmp` or `/usr/tmp`. For