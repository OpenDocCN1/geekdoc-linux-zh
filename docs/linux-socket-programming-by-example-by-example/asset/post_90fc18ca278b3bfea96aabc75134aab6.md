
Listing 7.8 shows an example compile and run session for this demo program.

# **Listing 7.8: Compiling and Running the daytime Client Program**

![](img/961a0296fe36074690a9847b79332eff_197_0.png)

```
$ make daytime
gcc -c -D_GNU_SOURCE -Wall daytime.c
gcc daytime.o -o daytime
$ ./daytime
Date & Time is: Tue Aug 17 18:41:42 1999
$  
```

There is an extra newline emitted by the program, because the server places a `'\n'` at the end of the date and time information that is sent to the client program.

# **Using connect(2) on SOCK_DGRAM Sockets**

The `connect(2)` function was introduced to you in this chapter for use with connection-oriented protocols. Before moving onto the next chapter, however, it should be noted that there is an exception to this rule.

The `connect(2)` function can be used with UDP sockets (`SOCK_DGRAM` for protocol family `PF_INET`). This does not actually imply a connection, however, but instead imposes some restrictions upon how the UDP socket will be used. This function call should be made

- 1. After the `bind(2)` function is called, if used.
- 2. Before any datagrams are read or written on the socket.

When `connect(2)` is used on a UDP socket, this indicates that all packets written will be addressed to the destination indicated in the server address specified (argument 2). This also implies that this socket is only interested in receiving datagrams from the same server. This prevents stray datagrams from being received from other sockets, which is otherwise possible with UDP. The kernel will eliminate unwanted UDP datagrams from being received by your UDP socket.

One other advantage to this technique is that it permits the caller to use the `read(2)` and `write(2)` system calls instead of the `sendto(2)` and `recvfrom(2)` functions. This saves the programmer from having to provide socket address structures and lengths for each I/O operation.

## What's Next

This chapter introduced you to the concept of a connection-oriented form of communication. The client program demonstrated that it must connect to its server before performing any I/O.

The next chapter will introduce you to the server's point of view and the different steps that it must perform. You'll also learn about two new important socket functions that you have yet to see in this book.

![](img/961a0296fe36074690a9847b79332eff_200_0.png)

![](img/961a0296fe36074690a9847b79332eff_200_1.png)

# Connection-Oriented Protocols for Servers

The last chapter showed you how to write a connection-oriented client program. The server program that the client connects to must use a different procedure, however. This chapter will teach you about the role of the server, including the following topics:

- The basic steps used by connection-oriented servers
- Why the `bind(2)` function is necessary for servers
- The `listen(2)` function and its role
- The `accept(2)` function and its role
- How to write a connection-oriented server program

With these topics mastered, you will be equipped to program your own custom server programs.

## Understanding the Role of the Server

In the last chapter you saw how a client program connected to a server process. Compared to connectionless communication, from the client’s point of view, the only new step was the “connect” step. The connection was established by use of the connect (2) function.

You will recall that the client program required five basic steps. In their simplest form, these are shown in Figure 8.1 on the left side of the figure, as steps C1 through C5. Steps S1 through S6 depict the six basic steps that a server program will use. The steps shown flow from top to bottom. Two dotted horizontal lines with arrows in the center of the figure show how these events form a relationship between the client and server programs. Figure 8.1 represents the simplest form that a server can take. This model will be further enhanced as you progress through this chapter.

![](img/961a0296fe36074690a9847b79332eff_201_0.png)

Figure 8.1: Study and compare these connection steps for client and server connections.

The basic steps of the server can now be summarized as follows:

1. Create a socket.
2. Bind a socket address (mandatory).
3. Listen for a connection.
4. Accept a connection.
5. Communicate with the client program.
6. Close the socket.

Notice that, for the server, the bind(2) step 2 (S2 in Figure 8.1) is not optional. The server cannot be contacted by clients unless the client has an address for connecting. On the other hand, the client bind(2) step C2 is optional. In order for a server to be contacted, then, a server address cannot be completely wild.

Notice also that step 3 (S3 in Figure 8.1) is something new. The server must express its interest in accepting connections to the kernel for its socket. This will be discussed further when the listen(2) function is covered.

The process of accepting a connection in step 4 (S4 in Figure 8.1) is another new socket concept. Once a client has connected to the server, the server must then accept the connection. This will be covered in detail when the accept(2) function is covered later in this chapter.

Briefly, the server differs from the client in the following ways:

- The server must bind a server address to the socket.
- The server listens for a connection.
- The server accepts connections.

## The listen(2) Function

The listen(2) function is how the server is able to express its interest in listening for connections. The function is very simple to call, and its function prototype is given as follows:

```c
#include <sys/socket.h>

int listen(int s, int backlog);
```

The two input arguments are the following:

- The socket s to use as the listening socket.
- The backlog, which specifies the connect queue length in entries.

The function returns zero when it is successful. Otherwise -1 is returned, and the reason for the error is posted to `errno`.

## Understanding the Connect Queue

It might seem odd that the application programmer would have to supply something apparently so cryptic as a *backlog* parameter value in the call to the *listen*(2) function. However, there is a sound reason for it. Figure 8.2 shows the general activity of the very popular www.wooho.com Web server.

![](img/961a0296fe36074690a9847b79332eff_203_0.png)

**Figure 8.2:** *The Linux kernel manages the backlog queue when accepting new connections.*

Notice the block in Figure 8.2 that is labeled *listen*(2). This block represents the call to *listen*(2), which establishes a listening queue. A small arrow points up to the queue it established, which resides within the Linux kernel. The length of this queue is determined by the *backlog* argument of the *listen*(2) call.

Now look at the block at the bottom right of Figure 8.2. This block is labeled “Process Client Request.” The arrow labeled as number one represents the very first connection into your server. In Figure 8.2, this connection has just been accepted by the accept(2) function call and is currently being processed by your server code.

However, while server processing is taking place on the first client connection, more connection requests are coming into your server from all over the world. Within the queue that listen(2) established, you have connect requests two through five pending and waiting to be accepted.

Figure 8.2 shows another client request being inserted into the tail end of the queue as request number six by the Linux kernel. Even as that is happening, connect requests seven, eight, and nine are being received. A busy server indeed!

The thrust of Figure 8.2 has been to demonstrate the purpose of the backlog argument, within the listen(2) function call. As you have seen, this parameter sets the length of the incoming queue. Now that you understand its purpose, let’s discuss what practical values should be used in this parameter.

## Specifying a Value for *backlog*

Historically, the value of backlog in the listen(2) call has been less than precise. In the early days of UNIX, the value 5 was commonly used. However, with the faster and busier systems of today, this value might not be suitable for your server application. So how does one determine a reasonable value?

UNIX literature advises not to use a value of 0 in the backlog argument. This is good advice to programmers writing applications that must be ported to various flavors of UNIX, including Linux. The reason is that for some platforms this means no connections are accepted. For others, it means that at least one connection can be pending in accept(2). A negative value does not make sense, and so it should not be used.

The man page for *listen(2)* indicates that the behavior of the backlog argument changed at Linux kernel release 2.2. Previously, this count included connections that were still establishing communications with the listening socket. As of 2.2 and later, this backlog count only pertains to those connections that have been established with the listening socket, but are waiting to be accepted by the server.

It would seem that for small servers, the queue length should be specified as 5 or more. For Web servers, however, you might need to experiment with larger numbers. Some tests published by Richard Stevens suggest that for a Web server that is receiving approximately 45,000 connects per hour, you might want to use a backlog length of 16 or more.
