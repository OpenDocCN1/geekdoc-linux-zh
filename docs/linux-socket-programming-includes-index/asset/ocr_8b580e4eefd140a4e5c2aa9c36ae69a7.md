+   EALREADY
+   The socket is non-blocking, and a previous connection attempt has not yet been completed.
+   EAFNOSUPPORT
+   The passed address didn't have the correct address family in its sa_family field.
+   EACCES
+   The user tried to connect to a broadcast address without having the socket broadcast flag enabled.

# Example

```
/*** Connect to a TCP server ***/
int sockfd;
struct sockaddr_in addr;
sockfd = socket(PF_INET, SOCK_STREAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = 13; /* current time */
inlet_atoi("127.0.0.1", &addr.sin_addr);
if (connect(sockfd, &addr, sizeof(addr)) != 0)
    perror("connect");
```

# socketpair()

Creates a pair of sockets that are linked together like a pipe but uses the socket subsystem. It is nearly identical to a pipe() system call but gives you the added functionality of the Socket API. socketpair() supports PF_UNIX or PF_LOCAL sockets only. You do not need to bind() this socket to a file system filename.

# Prototype

```
#include <sys/socket.h>
#include <resolv.h>
int socketpair(int domain, int type, int protocol,
               int sockfds[2]);
```

# Return Value

Zero (0) if everything goes well. If an error occurs, you can find the cause in errno.

# Parameters

+   domain
+   Must be PF_LOCAL or PF_UNIX.
+   type
+   SOCK_STREAM; This creates a socket like a pipe(). On some UNIX systems the pipe is bidirectional. Posix 1, however, does not require bidirectionality.
+   protocol
+   Must be zero (0).
+   sockfds[2]
+   An array of integers into which the call stores the new socket descriptors if successful.