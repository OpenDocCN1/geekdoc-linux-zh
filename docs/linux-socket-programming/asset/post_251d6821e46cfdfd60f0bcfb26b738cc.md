
![](img/03334662da8fdfb8d95a02f270c522f6_67_0.png)

The server replies with its own connection request, a close request, and an acknowledgment of the client's close. (The connection request acknowledgment is implied.) This packet includes the data that the server generated. Lastly, the client acknowledges the server's close.

T/TCP can be very fast. There is one problem: All the information must be transmitted within TCP's MSS (Maximum Segment Size), which is only 540 bytes. However, you can change that setting up to 64KB. Also, the program is not limited to sending one message; it can send several messages.

The server program does not have to do any more work to support T/TCP. The algorithm for a normal TCP connection serves T/TCP as well, because all the server-side support is programmed in the network subsystem. All the work is on the client side. You may use the following algorithm in the client:

```c
/***** ... *******/
/*** T/TCP basic algorithm. ***
/***** ... *******/
```

```c
int flag=1;
int sd;
sd = socket( PF_INET, SOCK_STREAM, 0);
if ( setsockopt( sd, IPPROTO_TCP, TCP_NOPUSH, &flag,
sizeof( flag) ) != 0 )
    PANIC( "TCP_NOPUSH not supported" );
/** Set up addr to destination ****/
if ( sendto( sd, buffer, bytes, MSG_FIN, &addr, sizeof( addr) )
< 0 )
    PANIC( "sendto" );
...
```

With T/TCP you have to disable TCP from flushing its buffers too quickly. That is what the `setsockopt()` system call is doing in the example. Also, you can send as many messages as you want, but the last message must have MSG_FIN (see above) in the `sendto()` system call.

# NOTE

## T/TCP and Linux

Linux, unfortunately, does not currently support T/TCP. In the future it will, but for now, you may use these techniques on other UNIX operating systems. You can see some flags that indicate a work in progress in the Linux kernel (for example, MSG_EOF and MSG_FIN are defined in linux/socket.h). Still, you can try out the T/TCP programs found on the Web site.

TCP, as mentioned before, requires you to re-create a TCP socket for every new connection, because you can close a connection only by closing the socket itself. T/TCP may have a side benefit of not requiring you to re-create a socket like TCP, because its connection and shutdown are implicit.

T/TCP gives you the benefit of short bursts of interaction with any supporting server, while minimizing startup and shutdown times. The benefits of T/TCP help your program respond faster to servers.

## Sending a Direct Message

Up to this point you have worked with a connected channel to send and receive messages that is best compared to using a telephone. A directed message is unconnected, meaning that it does no handshaking. Creating a directed message (not a pipe) to a peer requires a sender and a receiver. The sender transmits the message, and the receiver accepts the message. It's that simple.

Each message needs a destination (the kernel places the return address in the packet for you). The `send()` and `recv()` assume that they have a connected channel, which automatically defines the destination. Instead, you must use the `recvfrom()` and `sendto()` system calls, because both provide the addressing each message requires.

Prior to sending the message, you build the destination address, which includes the host address and the port number. As described in previous chapters, if your program skips selecting a port, the operating system assigns one to the socket randomly. This is not a good idea for peer programs. The calling peer must know the destination port to address the message properly.

# NOTE

## Checking Linux sockaddr Support

The Linux kernel supports several different types of addressing protocols, but not all protocols are directly included in the distribution kernels. For example, the distribution kernels often omit the amateur radio protocols. If you are uncertain which binding protocols your compiled kernel supports, simply run your program. The bind(), sendto(), connect(), and recvfrom() system calls complain if they receive a sockaddr they don't understand. You can find a list of the supported sockaddr in Appendix A, "Data Tables."

The UDP/TCP senders must know what port the receiver is listening on so that the operating system routes the packet to the correct program. This port is usually an agreed-upon port number between sender and receiver. For example, the /etc/services file lists the published port numbers that provide standard services.

## Binding the Port to Your Socket

You can request a specific port number from the operating system using the bind() system call. You may have seen this call before, and regrettably most UNIX manual pages define it as a way to "name the socket." This definition refers to PF_LOCAL or PF_UNIX sockets that use the file system. A better description is "to bind a port number or other publishable interface to the socket."

# NOTE

## Name and Port Binding

The port assignment and socket naming vary dramatically between each sockaddr family member. Some, such as AF_LOCAL and AF_AX25, are alphanumeric names; others, like AF_INET and AF_IPX, use ports. The port numbers must be unique, so in general no two TCP or UDP sockets can have the same port numbers (at least with AF_INET). However, you can have a UDP socket and a TCP socket share the same port number. That is how some services (in /etc/services) offer you both connections.

The prototype definition of the bind() system call is

```c
#include <sys/socket.h>
#include <resolv.h>
int bind(int sd, struct sockaddr *addr, int addr_size);
```

This section only introduces bind(); for an in-depth description, see Chapter 6. The use is similar to the connect() system call where you need to initialize the addr parameter first:

```c
/*****\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/
/***** Bind() example.
/*****\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*/
struct sockaddr addr;
int sd;
sd = socket(PF_INET, SOCK_STREAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(MY_PORT); /* request specific port */
addr.sin_addr.s_addr = INADDR_ANY; /* any IP interface */
```

```c
if ( bind(sd, &addr, sizeof(addr)) != 0 )
    perror("bind");
...
```

If you compare this bind() system call example with that of the connect() system call, you may note two main differences: Here, the code snippet is requesting MY_PORT, and the address is INADDR_ANY. Your program needs a specific port number for your peers to connect to.

The INADDR_ANY is a special flag (essentially 0.0.0.0) that indicates that any peer can connect from any interface. Some computers have more than one network interface (for example, two LAN cards, a modem with a LAN card, aliased IP addresses). Each hardware or logical interface has its own IP address. Using the bind() system call, you can specify whether to serve any one or all of these interfaces. You can use this feature for cross-firewall translations or filters, and it applies to both TCP and UDP protocols. To indicate a specific interface, you can use the following:

```c
if ( inet_aton("128.48.5.161", &addr.sin_addr) == 0 )
    perror("address error");
...
```

This makes the request that the port listen on 128.48.5.161. You could use the network byte-ordering conversions like htonl():

```c
addr.sin_addr.s_addr = htonl(0x803005A1);   /* 128.48.5.161 */
```

Either way, it functions the same. You may note that INADDR_ANY does not use the htonl() conversion call. It doesn't need it, since it is all zeros, and it is guaranteed to be in network byte order.

## Tossing the Message Around

Sending and receiving UDP messages looks a little like playing catch in the fog. The players take turns tossing and catching, even though they can't see each other. The sender is the first to toss the ball. The receiver must have a known location and port number, established with the bind() system call. The sender does not need to establish its port number, because each message includes the return address. The potential exists for a player to toss the ball to an empty space.

The sender does very little initialization and often does no more than one message request. You could place this in a loop, if you want to toss messages back and forth. The code for the sender is seen in Listing 4.4 and on the Web site in connectionless-sender.c.

### Example 4.4. Datagram Sender Example

```c
/********************************************************
/**  Sender example.
/**  (Excerpt from connectionless-sender.c)
/**
****/struct sockaddr addr;int sd, bytes, reply_len, addr_len=sizeof(addr);
```
