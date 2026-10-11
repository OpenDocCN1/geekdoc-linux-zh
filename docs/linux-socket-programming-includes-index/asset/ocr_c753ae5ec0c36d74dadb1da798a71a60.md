# **LISTING 4.2 Continued**

```
`{ bytes_read = recv(sd, buffer, sizeof(buffer)-1, 0); buffer[bytes] = 0; if ( bytes_read > 0 ) printf("%s", buffer); } while ( bytes_read > 0 );`
```

The program in Listing 4.2 opens the connection, sends the command-line request, and displays everything it gets until the server closes the connection. Later versions of the HTTP protocol (1.1 and the proposed HTTP-NG) include the capability to leave the channel open, taking advantage of the TCP connection. Again, this feature emphasizes the need to tell the receiver when the sender is done talking. You can read much more about the new versions of HTTP in the RFCs found at www.w3c.org.

# What Are Connectionless Sockets?

Not every communication requires having a full bi-directional channel open between peers. If the telephone is an example of a streaming connection, the postal system best represents a message-based (or connectionless) system. Like the postal system, UDP composes messages, assigns a destination, and ships it off without any tracking of the message as it travels to the destination. (Just to reiterate: A datagram’s unreliability means that it offers no guarantee of delivery. That does not mean it does not work.)

# Setting the Socket’s Address

The full installation of a Linux distribution usually includes tools that allow you to send and receive notes from other workstations on the network. The tools require only a machine address and maybe a username. You could implement this kind of tool on your own using a UDP socket. To do this, you need to see if the current user is the recipient of the message.

These messenger-style tools use the two pieces of data (hostname and username) to identify the recipient uniquely. The tool has no streamed data, so your implementation could use a connectionless interface.

The connectionless interface does not make the connect() system call, but you can’t call send() or recv() without a connection. Instead, the operating system offers two lower-level system calls that include the destination address: recvfrom() and sendto(). These calls act similarly to recv() and send(), but you provide the destination as part of the call:

```
#include <sys/socket.h> #include <resolv.h>
```