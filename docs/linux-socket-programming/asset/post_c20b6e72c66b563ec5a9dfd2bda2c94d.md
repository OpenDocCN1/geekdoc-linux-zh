
## Getting Fragmented Packets

Your programs are going to execute much faster than the network does. Sometimes a packet arrives at the computer in pieces, because the network routers fragmented it to fit more limited networks. If you call `recv()` when this occurs, you may get an incomplete message. This is one reason why MSG_PEEK could give you different results with consecutive calls: The first call may yield 500 bytes, and the second could be 750 bytes. Likewise, this is why there's a MSG_WAITALL flag.

The `recv()` system call is more flexible than `read()`, letting you use the different flags to modify behavior. Do a normal read from socket pipe (equivalent to `read()`):

```
int bytes_read;
bytes_read = recv(sd, buffer, MAXBUF, 0);
...
```

Read nondestructively from socket pipe:

```
int bytes_read;
bytes_read = recv(sd, buffer, MAXBUF, MSG_PEEK);
...
```

Read nondestructively out of band data from socket:

```
int bytes_read;
bytes_read = recv(sd, buffer, MAXBUF, MSG_OOB | MSG_PEEK);
...
```

The first statement gets the information from the server supplying a buffer, length, and no flags. The next statement displays the information. There is an intentional flaw here: What if the server sends more information than the buffer can accept? This is not a critical defect; nothing is going to crash. The algorithm simply may lose the data it doesn't read.

The `recv()` system call yields similar error codes to `read()` along with the following extensions:

- `ENOTCONN` sd not connected. The supplied socket descriptor is not connected to the peer or server.
- `ENOTSOCK` sd not a socket. The supplied socket descriptor does not have the signatures indicating that it came from a `socket()` system call.

Note that if you use the `read()` system call, you can still get these error codes when using a socket descriptor, because the `read()` call is just a portal to the `recv()` call.

## Closing the Connection

You have the information you need from the server, everything went well, and now you want to close the connection. There are again two ways you can close the connection. Most programs use the standard I/O `close()` system call:

```
#include <unistd.h>
int close(int fd);
```

Again, the socket descriptor (*sfd*) may substitute for the file descriptor (*ffd*). It works the same. If successful, the return value is zero.

### Always Close Socket Descriptors

Make it a point always to close descriptors manually, particularly sockets. By default, the operating system closes all descriptors and flushes buffers for you. If the descriptor refers to a file, the process works without affecting other systems. Sockets, on the other hand, can linger longer than necessary, tying up resources and making it difficult for other clients to connect.

This call yields only one error:

- *EBADF* *fd* isn’t a valid open file descriptor.

The *shutdown()* system call gives you more control over closing the channels, because you can close either the incoming or outgoing channels. This call is especially helpful when using sockets to replace *stdin* or *stdout*.

### Confusing Shutdown Commands

The *shutdown()* system call is different from the shutdown command (section 8 of online UNIX manuals) for bringing down the operating system.

With the *shutdown()* system call, you can close different directions of data flow in the communication path, making the path read-only or write-only:

```
#include <sys/socket.h>
int shutdown(int s, int how);
```

The *how* parameter can have three values:

| Value | Function |
|---|---|
| 0 (zero) | Write only (think of "O" in "output") |
| 1 (one) | Read only (think of "I" in "input") |
| 2 | Close both input and output |

## Summary: What’s Going On Behind the Scenes?

Several things occur behind the scenes when the program opens a socket and connects to a TCP server. All the socket call does is create a message queue. Things really happen when the program connects. (You can get the complete program listing on the companion CD.) Table 1.2 shows what happens on the client and server sides.

### Table 1.2, Steps of Creating a Socket and Connecting

| **Client's Actions** | **Server's Actions** |
| :--- | :--- |
| 1. Calls `socket()`: Creates a queue; sets flags for communication protocols. | (Waiting for connection) |
| 2. Calls `connect()`: The operating system assigns a temporary port number if the socket doesn't have an assigned port number through `bind()`. | (Waiting) |
| 3. Sends a message to the server requesting a connection, telling the server which port the client is using. | 4. Places the connection request on the listening queue. |
| (Waiting for server) | 5. Reads the connection queue, accepts a connection, and creates a unique socket channel. |
| (Waiting) | 6. Creates (sometimes) a unique task or thread to interact with your program. |
| (Waiting) | 7. Sends back a confirmation that the connection is accepted. Either sends a message to your port or awaits a request from your program. The server may close the channel after sending the data, if it provides simple bulletin messages (like time-of-day). |
| 8. Begins data correspondence. | |

That's quite a bit for a simple `connect()` call. This process could get much more complicated, especially for the routing computers in between (such as routing management, packet verification, fragmentation and defragmentation, protocol translation, tunneling, and so on). The Socket API considerably simplifies network communication.

The network requires a particular language and algorithm in order to establish a connection. First and foremost, the `socket()` system call starts the ball rolling by creating the telephone handset. This handset allows a program to send and receive messages it is connected to. The program may use regular `read()` and `write()` as used in pipes and file descriptors. Alternatively, you can use the more specialized system calls like `recv()` .

The IP network has several features that require further explanation. The next chapter expands IP numbering, ports, and byte ordering. It explains very useful tools to convert the information, simplifying your programming efforts.

## Chapter 2. TCP/IP Network Language Fluency

### IN THIS CHAPTER

- An IP Numbering Overview
- IP Host Port Numbers
- Network Byte Ordering
- Different Kinds of `sockaddr`
- UNIX Named Pipes
- Summary: Applying IP Numbering and Tools

Working with the Internet requires you to know how to address messages so that they arrive correctly. Addressing is an important part of creating messages. Like the telephone, a computer must have an address or ID so that it can get the right messages and other computers can direct the traffic accordingly.
