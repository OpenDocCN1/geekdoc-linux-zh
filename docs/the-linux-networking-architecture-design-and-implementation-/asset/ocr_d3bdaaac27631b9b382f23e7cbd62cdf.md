# Chapter 27 Network Programming with Sockets

after a close() system call, while the kernel still tries to handle data waiting in the queues.
The only parameter of the close() function is the following:

```
int sockfd is the descriptor of the socket that should be closed. A process that terminates and releases all open sockets automatically.
```

Application Example:

```
#include <sys/socket.h>
int sockfd;
/* Creating a socket. */
/* Communication operations. */
close(sockfd);
```

```
int bind(int sockfd, struct sockaddr *mAddress, int AddrLength)
```

A newly created socket has no allocation to local addresses or port numbers. On the client side, user programs do not necessarily have to care about the local addresses they use, because they can be allocated automatically. In contrast, server processes have to specify the port they are working at, because this port is used to address the corresponding service. This means that the server has to bind a new socket to a local address and a port; this binding is the task of the bind() system call.
The bind() system call requires the following parameters:

```
int sockfd is a socket descriptor.
struct sockaddr *mAddress is a pointer to a structure with the address the socket is to be bound.
int AddrLength specifies the size of the address structure provided in the second parameter. The size of the address structure has to be specified, because different address families use different address formats.
```

The bind() system call is used in three cases:

Servers register their own addresses within the system. They inform the system about the kind of packets to be forwarded at this socket, e.g., packets with a specific port number. Server applications use globally defined port numbers, the socalled well-known ports. They are assigned by IANA upon request and listed in the file /etc/services.
A client itself store a specific address.
A connectionless client has to ensure that the system creates an individual address for it, so that the other end of the communication relationship has a valid return address for replies.