```
**recv**—receive data from socket
```c
#include <sys/socket.h>

ssize_t recv(
    int socket_fd,    /* socket file descriptor */
    void *buffer,     /* buffer to receive data */
    size_t length,    /* length of buffer */
    int flags         /* flags */
);
/* Returns number of bytes received, 0, or -1 on error (sets errno) */
```
```

You can use the `MSG_OOB` flag with both `send` and `recv`; it was explained in Section 8.7. In addition, for `recv`, you can specify `MSG_PEEK` and/or `MSG_WAITALL`, which were explained in Section 8.6.2. We could have used `MSG_WAITALL` with `recv` instead of calling `readall` in the SMI implementation in Section 8.5.

# 8.9.2  `getsockname` and `getpeername`

`getsockname` gets the socket address that a socket has been bound to with a previous call to `bind`:

```
**getsockname**—get socket address
```c
#include <sys/socket.h>

int getsockname(
    int socket_fd,      /* socket file descriptor */
    struct sockaddr *sa,/* socket address */
    socklen_t *sa_len   /* address length */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

As usual for socket-address-returning functions, on input `sa` should point to a buffer big enough for the socket address and `sa_len` should be the size of that buffer. On output `sa_len` is the actual size of the address.

A similar function gets the socket address of the socket connected to a socket:

```
**getpeername**—get socket address of connected socket
```c
#include <sys/socket.h>

int getpeername(
    int socket_fd,      /* socket file descriptor */
    struct sockaddr *sa,/* socket address */
    socklen_t *sa_len   /* address length */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

If the connected socket is unbound, as is often the case, then what `getpeername` returns is unspecified. You don’t get an error return in this case.