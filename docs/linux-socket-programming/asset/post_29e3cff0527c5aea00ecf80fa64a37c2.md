
## bind()

`bind()` defines a port or name to a socket. If you want a consistent port for an incoming connection, you have to bind your socket to a port. In most instances, the kernel automatically calls `bind()` for the socket if you do not call it explicitly. The kernel-generated port assignment can be different from execution to execution.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
int bind(int sockfd, struct sockaddr* addr, int addrlen);
```

### Return Value

Zero if everything goes well. If an error occurs, you can find the cause in `errno`.

### Parameters

| Parameter | Description |
|:---|:---|
| `sockfd` | The socket descriptor to bind. |
| `addr` | The port assignment or name. |
| `addrlen` | The length of `addr` because `addr` can be different sizes. |

### Possible Errors

| Error | Description |
|:---|:---|
| `EBADF` | `sockfd` is not a valid descriptor. |
| `EINVAL` | The socket is already bound to an address. This may change in the future; see `../linux/unix/socket.c` for details. |
| `EACCES` | The address is protected, and the user is not the superuser. |
| `ENOTSOCK` | Argument is a descriptor for a file, not a socket. |

### Example

```c
/* ** Bind port #9999 to socket from any Internet Address ** */
int sockfd;
struct sockaddr_in addr;
sockfd = socket(AF_INET, SOCK_STREAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(9999); /* or whatever port you want */
/* to bind any network interface */
addr.sin_addr.s_addr = INADDR_ANY;
/* -or- to bind a specific interface, use this: */
/* inet_aton("128.1.1.1", &addr.sin_addr); */
if ( bind(sockfd, &addr, sizeof(addr)) != 0 )
    perror("bind");
```

## listen()

`listen()` converts the socket into a listening socket. This option is available only to `SOCK_STREAM` protocols. The call creates a queue of incoming connections.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
int listen(int sockfd, int queue_len);
```

### Return Value

Zero if everything goes well. If an error occurs, you can find the cause in `errno`.

### Parameters

| Parameter | Description |
|:---|:---|
| `sockfd` | A `SOCK_STREAM` socket that has been bound to a port. |
| `queue_len` | The maximum number of pending connections. |

### Possible Errors

| Error Code | Description |
|:---|:---|
| `EBADF` | The argument `sockfd` is not a valid descriptor. |
| `ENOTSOCK` | The argument `sockfd` is not a socket. |
| `EOPNOTSUPP` | The socket is not of a type that supports the `listen()` operation. If you supply any socket that is not `SOCK_STREAM`, you get this error. |

### Example

```c
/*** Convert a socket to a listening socket with 10 slots ***/
int sockfd;
sockfd = socket(PF_INET, SOCK_STREAM, 0);
/*----set up address with bind()----*/
listen(sockfd, 10);  /* create a 10-pending queue */
```

## accept()

### Return Value

| Return | Description |
|:---|:---|
| If >= 0 | A new socket descriptor. |
| If < 0 | Error; `errno` has details. |

### Parameters

| Parameter | Description |
|:---|:---|
| `sockfd` | The bound and listening socket descriptor. |
| `addr` | If nonzero, the call places the address definition in this region. While it should match the `sockfd`'s family (`AF_INET`), do not assume it. |
| `addr_len` | You pass the length by reference so that the call can tell you exactly how much of `addr`'s data block it used. This means that you need to reset the value for each call. |

### Possible Errors

| Error | Description |
|:---|:---|
| `EBADF` | The socket descriptor is invalid. |
| `ENOTSOCK` | The descriptor references a file, not a socket. |
| `EOPNOTSUPP` | The referenced socket is not of type `SOCK_STREAM`. |
| `EFAULT` | The `addr` parameter is not in a writable part of the user address space. |
| `EAGAIN` | The socket is marked non-blocking and no connections are present to be accepted. |
| `EPERM` | Firewall rules forbid connection. |
| `ENOBUFS`, `ENOMEM` | Not enough free memory. |

### Examples

```c
/**** Accept a connection, ignoring the origin ****/
int sockfd = socket(PF_INET, SOCK_STREAM, 0);
/*---bind address to socket with bind()---*/
/*---convert it to a listening socket with listen()---*/
for (; ; )
{
    int client;
    client = accept(sockfd, 0, 0);
    /*---interact with client---*/
    close(client);
}
```

```c
/**** Accept a connection, capturing the origin in a log ****/
int sockfd = socket(PF_INET, SOCK_STREAM, 0);
/*---bind address to socket with bind()---*/
/*---convert it to a listening socket with listen()---*/
for (; ; )
{
    struct sockaddr_in addr;
    int client, addr_len = sizeof(addr);
    client = accept(sockfd, &addr, &addr_len);
    printf("Connected: %s:%d\n", inet_ntoa(addr.sin_addr), ntohs(addr.sin_port));
    /*---interact with client---*/
    close(client);
}
```

## connect()

Connect to a peer or server. You can use this function for either `SOCK_DGRAM` or `SOCK_STREAM` protocols. For UDP, it merely remembers the port to which you connected. This allows you to use `send()` and `recv()`. For TCP (`SOCK_STREAM`), this call starts the three-way handshake for stream communications.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
int connect(int sockfd, struct sockaddr *addr, int addr_len);
```

### Return Value

Zero (0) if everything goes well. If an error occurs, you can find the cause in `errno`.

### Parameters

| Parameter | Description |
|:---|:---|
| `sockfd` | The freshly created socket. You could optionally call `bind()` before this to assign the local port. If you do not, the kernel assigns the next available port slot. |
| `addr` | The address and port of the destination address. |
| `addr_len` | The length of addr data block. |

### Possible Errors

| Error | Description |
|:---|:---|
| `EBADF` | Bad descriptor. |
| `EFAULT` | The socket structure address is outside the user's address space. This is caused by a bad addr structure reference. |
| `ENOTSOCK` | The descriptor is not associated with a socket. |
| `EISCONN` | The socket is already connected. You cannot reconnect a connected socket. Instead, you have to close the socket and create a new one. |
| `ECONNREFUSED` | Connection refused at server. |
| `ETIMEDOUT` | Timeout while attempting connection. |
| `ENETUNREACH` | Network is unreachable. |
| `EADDRINUSE` | Address is already in use. |
| `EINPROGRESS` | The socket is non-blocking, and the connection cannot be completed immediately. It is possible to `select()` or `poll()` for completion by selecting the socket for writing. After `select()` indicates writeability, use `getsockopt()` to read the `SO_ERROR` option at level `SOL_SOCKET` to determine whether the connection was successful (`SO_ERROR` is zero) or unsuccessful (`SO_ERROR` is one of the usual error codes previously listed, explaining the reason for the failure). |
| `EALREADY` | The socket is non-blocking, and a previous connection attempt has not yet been completed. |
| `EAFNOSUPPORT` | The passed address didn't have the correct address family in its `sa_family` field. |
| `EACCES` | The user tried to connect to a broadcast address without having the socket broadcast flag enabled. |

### Example

```c
/** Connect to a TCP server **/
int sockfd;
struct sockaddr_in addr;
sockfd = socket(PF_INET, SOCK_STREAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = 13; /* current time */
inet_aton("127.0.0.1", &addr.sin_addr);
if ( connect(sockfd, &addr, sizeof(addr)) != 0 )
    perror("connect");
```

## socketpair()

Creates a pair of sockets that are linked together like a pipe but uses the socket subsystem. It is nearly identical to a `pipe()` system call but gives you the added functionality of the Socket API. `socketpair()` supports `PF_UNIX` or `PF_LOCAL` sockets only. You do not need to `bind()` this socket to a file system filename.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
int socketpair(int domain, int type, int protocol, int sockfds[2]);
```

### Return Value

Zero (0) if everything goes well. If an error occurs, you can find the cause in `errno`.

### Parameters

| Parameter | Description |
|:---|:---|
| `domain` | Must be `PF_LOCAL` or `PF_UNIX`. |
| `type` | `SOCK_STREAM`; This creates a socket like a `pipe()`. On some UNIX systems the pipe is bidirectional. `Posix 1`, however, does not require bidirectionality. |
| `protocol` | Must be zero (0). |
| `sockfds[2]` | An array of integers into which the call stores the new socket descriptors if successful. |

### Possible Errors

| Error | Description |
|:---|:---|
| `EMFILE` | Too many descriptors are in use by this process. |
| `EAFNOSUPPORT` | The specified address family is not supported on this machine. |
| `EPROTONOSUPPORT` | The specified `protocol` is not supported on this machine. |
| `EOPNOSUPPORT` | The specified `protocol` does not support creation of socket pairs. |
| `EFAULT` | The address `sockfds` does not specify a valid part of the process address space. |

### Example

```c
/*** Create a socket pair ***/
int sockfd[2];
struct sockaddr_un addr;
if ( socketpair(PF_LOCAL, SOCK_STREAM, 0, sockfd) != 0 )
    perror("socketpair");
```

## Communicating on a Channel

After establishing the socket and connection, you can use the API for sending and receiving messages. This section defines the calling API for all socket I/O.

## send()
