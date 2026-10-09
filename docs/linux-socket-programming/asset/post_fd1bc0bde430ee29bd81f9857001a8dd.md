
## Possible Errors

- **MSG_WAITALL**: This flag requests that the operation block until the full request is satisfied. However, the call may still return less data than requested if a signal is caught, an error or disconnect occurs, or the next data to be received is of a different type than that returned.
- **MSG_ERRQUEUE**: Receive packet from the error queue.
- **MSG_NOSIGNAL**: This flag turns off raising of SIGPIPE on stream sockets when the other end disappears.
- **MSG_ERRQUEUE**: This flag specifies that queued errors should be received from the socket error queue. The error is passed in an ancillary message with a type dependent on the protocol (for IP, IP_RECVERR). The error is supplied in a `sock_extended_error` structure.

### Errors

| Error | Description |
| :--- | :--- |
| EBADF | The argument s is an invalid descriptor. |
| ENOTCONN | The socket is associated with a connection-oriented protocol and has not been connected (see `connect()` and `accept()`). |
| ENOTSOCK | The argument sockfd does not refer to a socket. |
| EAGAIN | The socket is marked as non-blocking, and the receive operation would block, or a receive timeout had been set and the timeout expired before data was received. |
| EINTR | A signal interrupted the receive operation before any data was available. |
| EFAULT | The receive buffer pointer points outside the process's address space. |
| EINVAL | An invalid argument was passed. |

### Example

```c
/*** Recv a message (TCP, UDP) from a connected destination ***/
int sockfd;
int bytes, bytes_wrote=0;
/*--- Create socket, connect to server/peer ---*/
if ( (bytes = recv(sockfd, buffer, msg_len, 0)) < 0 )
    perror("recv");

/*** Recv an URGENT message (TCP) from a connected destination ***/
/*** This code is typically in a SIGURG signal handler ***/
int sockfd;
int bytes, bytes_wrote=0;
/*--- Create socket, connect to server ---*/
if ( (bytes = recv(sockfd, buffer, msg_len, MSG_URGENT)) < 0 )
    perror("Urgent message");
```

## recvfrom()

Wait for and receive a message from an unconnected peer (UDP and raw sockets). Please note that T/TCP never uses this call. Instead, the receiver uses `accept()`.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
int recvfrom(int sockfd, void *buf, size_t buf_len, int options,
    struct sockaddr *addr, socklen_t *addr_len);
```

### Return Value

If successful, the number of bytes read. If an error occurred, the return value is -1, and `errno` holds the error code.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The open socket descriptor. |
| `buf` | The byte array to receive the data. |
| `buf_len` | The maximum size of the buffer (message truncated and dropped if buffer too small). |
| `options` | Channel controlling options (same as `recv()`). |
| `addr` | The sending peer's address and port. |
| `addr_len` | The maximum size of `addr` (address truncated if too small). Upon return, this value changes to match the number of bytes used. |

### Possible Errors

(Same as `recv()`)

### Example

```c
struct sockaddr_in addr;
int addr_len=sizeof(addr), bytes_read;
char buf[1024];
int sockfd = socket(PF_INET, SOCK_DGRAM, 0);
/***Bind socket to specific port***/
bytes_read = recvfrom(sockfd, buf, sizeof(buf), 0, &addr, &addr_len);
if ( bytes_read < 0 )
    perror("recvfrom failed");
```

## recvmsg()

Receive several messages at once from the same source. This call is customarily used with `SOCK_DGRAM` sockets (same reasoning as `sendmsg()`). The operation does not have the flexibility to accept from different sources.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
#include <sys/uio.h>
int recvmsg(int sockfd, struct msghdr *msg,
            unsigned int options);
```

### Return Value

Total number of bytes received if no error occurred; otherwise, returns -1.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The socket descriptor waiting for a message |
| `msg` | The data received |
| `options` | Channel controlling options (same as `recv()`) |

### Possible Errors

(Same as `recv()`)

### Example

```c
char buffer[MSGS][1000];
struct sockaddr_in addr;
struct iovec io[MSGS];
struct msghdr msg;
...
bzero(&addr, sizeof(addr));
msg.msg_name = &addr;
msg.msg_namelen = sizeof(addr);
for ( i = 0; i < MSGS; i++ )
{
    io[i].iov_base = buffer[i];
    io[i].iov_len = sizeof(buffer[i]);
}
msg.msg_iov = io;
msg.msg_iovlen = MSGS;
if ( (bytes = recvmsg(sd, &msg, 0)) < 0 )
    perror("recvmsg");
```

## Terminating Connections

The last step a solid program performs after communicating with the external host is to close the connection. This section describes the API for socket termination.

### shutdown()

Closes specific paths or directions of data flow. Socket connections, by default, are bidirectional. If you want to limit the flow to be read-only or write-only, `shutdown` closes the other half of the channel.

#### Prototype

```c
#include <sys/socket.h>
int shutdown(int sockfd, int how);
```

#### Return Value

Zero if everything goes well. If an error occurs, you can find the cause in `errno`.

#### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The open socket descriptor. |
| `how` | A flag indicating which half (or both) of channel to close: <br> `SHUT_RD` (0)—Make the channel output only. <br> `SHUT_WR` (1)—Make the channel input only. <br> `SHUT_RDWR` (2)—Close both halves, functionally same as `close()`. <br> This operates only on connected sockets. |

#### Possible Errors

| Error | Description |
| :--- | :--- |
| EBADF | `sockfd` is not a valid descriptor. |
| ENOTSOCK | `sockfd` is a file, not a socket. |
| ENOTCONN | The specified socket is not connected. |

#### Example

```c
int sockfd;
struct sockaddr_in addr;
sockfd = socket (PF_INET, SOCK_STREAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons (DEST_PORT);
inet_aton (DEST_ADDR, &addr.sin_addr);
connect (sockfd, &addr, sizeof (addr));
if ( shutdown (sockfd, SHUT_WR) != 0 )
    PANIC ("Can't make socket input-only");
```

## Network Data Conversions

While working with data on the network, you must consider the data byte-ordering, converting addresses, and so on. The Socket API includes a sizeable list of tools to help you get the information you need. This section describes the tools that the book has used (and a few others).

### htons() or htonl()

Convert host-byte order binary data to network-byte order. On a little-endian processor, the call swaps the bytes around. A big-endian host does nothing but return the value.

#### Prototype

```c
#include <netinet/in.h>
unsigned short int htons (unsigned short int host_short);
unsigned long int htonl (unsigned long int host_long);
```

#### Return Value

(none)

#### Parameters

| Parameter | Description |
| :--- | :--- |
| `host_short` | The 16-bit host value |
| `host_long` | The 32-bit host value |

#### Possible Errors

(none)

#### Example

```c
/*** Assign #1023 to socket **/
struct sockaddr_in addr;
addr.sin_port = htons(1023);
/*** Assign 128.1.32.10 to the destination address **/
struct sockaddr_in addr;
addr.sin_addr.s_addr = htonl(0x8001200A);
```

### ntohs() or ntohl()

Converts the network byte order to the host's byte order.

#### Prototype

```c
#include <netinet/in.h>
unsigned short int ntohs(unsigned short int network_short);
unsigned long int ntohl(unsigned long int network_long);
```

#### Return Value

The converted value (16 bits or 32 bits).

#### Parameters

| Parameter | Description |
| :--- | :--- |
| `network_short` | The 16-bit value to convert |
| `network_long` | The 32-bit value to convert |

#### Possible Errors

(none)

#### Example

```c
struct sockaddr_in addr;
int client, addrLen = sizeof(addr);
client = accept(sockfd, &addr, &addrLen);
if ( client > 0 )
    printf("Connected %1X:%d\n", ntohl(addr.sin_addr),
           ntohs(addr.sin_port));
```

### inet_addr()

A deprecated conversion tool for converting numeric, dot-notation addresses into the network-byte-order binary form. If it fails, the return value (-1 or 255.255.255.255) is still a legal address. The `inet_aton()` tool has better error handling.

#### Prototype

```c
#include <netinet/in.h>
unsigned long int inet_addr(const char *ip_address);
```

#### Return Value

| Value | Description |
| :--- | :--- |
| Non-zero | If everything goes well, the value is the converted IP address. |
| `INADDR_NONE` (-1) | The parameter is not valid. (This is the call's defect—there is no negative value, and 255.255.255.255 is the general broadcast address.) |

#### Parameters

| Parameter | Description |
| :--- | :--- |
| `ip_address` | The human-readable, dot-notation form (for example, 128.187.34.2) |

#### Possible Errors

(errno not set)

#### Example

```c
if ( (addr.sin_addr.s_addr = inet_addr("128.187.34.2")) == -1 )
    perror("Couldn't convert address");
```

### inet_aton()

Converts a human-readable IP address from the dot-notation to the binary, network-byte ordered form. This call replaces `inet_addr()`.

#### Prototype

```c
#include <netinet/in.h>
int inet_aton(const char* ip_addr, struct in_addr *addr);
```

#### Return Value

Non-zero if everything goes well. If an error occurs, the call returns a zero.

#### Parameters

| Parameter | Description |
| :--- | :--- |
| `ip_addr` | The ASCII string of the IP address (for example, 187.34.2.1). |
