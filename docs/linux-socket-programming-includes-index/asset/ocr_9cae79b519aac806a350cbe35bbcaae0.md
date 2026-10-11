# connect( )

Connect to a peer or server. You can use this function for either SOCK_DGRAM or SOCK_STREAM protocols. For UDP, it merely remembers the port to which you connected. This allows you to use send( ) and recv( ). For TCP (SOCK_STREAM), this call starts the three-way handshake for stream communications.

# Prototype

```
#include <sys/socket.h>
#include <resolv.h>
int connect(int sockfd, struct sockaddr *addr, int addr_len);
```

# Return Value

Zero (0) if everything goes well. If an error occurs, you can find the cause in errno. ·

# Parameters

+   *   `sockfd` The freshly created socket. You could optionally call bind() before this to assign the local port. If you do not, the kernel assigns the next available port slot.
+   *   `addr` The address and port of the destination address.
+   *   `addr_len` The length of addr data block.

# Possible Errors

| Error | Description |
| :--- | :--- |
| EBADF | Bad descriptor. |
| EFAULT | The socket structure address is outside the user's address space. This is caused by a bad addr structure reference. |
| ENOTSOCK | The descriptor is not associated with a socket. |
| EISCONN | The socket is already connected. You cannot reconnect a connected socket. Instead, you have to close the socket and create a new one. |
| ECONNREFUSED | Connection refused at server. |
| ETIMEDOUT | Timeout while attempting connection. |
| ENETUNREACH | Network is unreachable. |
| EADDRINUSE | Address is already in use. |
| EINPROGRESS | The socket is non-blocking, and the connection cannot be completed immediately. It is possible to select( ) or poll( ) for completion by selecting the socket for writing. After select( ) indicates writability, use getsockopt( ) to read the SO_ERROR option at level SOL_SOCKET to determine whether the connection was successful (SO_ERROR is zero) or unsuccessful (SO_ERROR is one of the usual error codes previously listed, explaining the reason for the failure). |