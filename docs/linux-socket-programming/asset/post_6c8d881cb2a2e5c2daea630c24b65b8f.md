
Send a message to the connected peer, client, or server. This call is like the `write()` system call, but `send()` permits you to define additional options for channel control.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>

int send(int sockfd, void *buffer, int msg_len, int options);
```

### Return Value

Like `write()`, the call returns the number of bytes written. The byte count can be less than `msg_len`. If the call does not succeed in writing all required bytes, you can use a loop for successive writes. If negative, the call stores the error detail in `errno`.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The socket channel. This can be a connected `SOCK_DGRAM` or `SOCK_STREAM` socket. |
| `buffer` | The data to send. |
| `msg_len` | The number of bytes to send. |
| `options` | A set of flags to enable special message handling:<br>• `MSG_OOB`: Send message out-of-band (urgent).<br>• `MSG_DONTROUTE`: Send the message bypassing all routers. If unsuccessful, the network sends an error back.<br>• `MSG_DONTWAIT`: Don't allow blocking. Similar to the `fcntl()` option call, but only applies to this call. If the call would block, the call returns with `EWOULDBLOCK` in `errno`.<br>• `MSG_NOSIGNAL`: If the peer severs the connection, don't raise a `SIGPIPE` signal locally. |

### Possible Errors

| Error | Description |
| :--- | :--- |
| `EBADF` | An invalid descriptor was specified. |
| `ENOTSOCK` | The argument `sockfd` is not a socket. |
| `EFAULT` | An invalid user space address was specified for `buffer`. |
| `EMSGSIZE` | The call can't complete because the socket requires that the message be sent atomically, and the size of the message to be sent has made this impossible. |
| `EAGAIN` | The socket is marked non-blocking and the requested operation would block. |
| `ENOBUFS` | The system was unable to allocate an internal memory block. The operation may succeed when buffers become available. |
| `EINTR` | A signal occurred. |
| `ENOMEM` | No memory available. |
| `EINVAL` | Invalid argument passed. |
| `EPIPE` | The local end has been shut down on a connected socket. In this case, the process will also receive a `SIGPIPE` unless `MSG_NOSIGNAL` is set. |

### Example

```c
/*** Send a message (TCP, UDP) to a connected destination ***/
int sockfd;
int bytes, bytes_wrote=0;
/*--- Create socket, connect to server/peer ---*/
while ( (bytes = send(sockfd, buffer, msg_len, 0)) > 0 )
    if ( (bytes_wrote += bytes) >= msg_len )
        break;
if ( bytes < 0 )
    perror("send");

/*** Send an URGENT message (TCP) to a connected destination ***/
int sockfd;
int bytes, bytes_wrote=0;
/*--- Create socket, connect to server ---*/
if ( send(sockfd, buffer, 1, MSG_OOB) != 1 )
    perror("Urgent message");
```

## sendto()

Send a message to a specific destination without connecting. Typically, you use this system call for UDP and raw sockets. Using this call for TCP sockets is Transaction TCP (T/TCP). (Linux, however, does not yet support T/TCP.)

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>

int sendto(int sockfd, void* msg, int len, int options,
           struct sockaddr *addr, int addr_len);
```

### Return Value

Returns the number of bytes sent or −1 if an error occurred.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The socket descriptor |
| `msg` | The data to send |
| `len` | The number of bytes to send |
| `options` | Message-controlling flags (same as `send()`) |
| `addr` | The address of the destination |
| `addr_len` | The size of the destination data body |

### Possible Errors

(Same as `send()`)

### Example

```c
/*** Send a message (TCP, UDP) to an unconnected destination ***/
int sockfd;
struct sockaddr_in addr;
if ( (sd = socket(PF_INET, SOCK_DGRAM, 0)) < 0 )
    perror("socket");

bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(DEST_PORT);
inet_aton(DEST_ADDR, &addr.sin_addr);

if ( send(sockfd, buffer, msg_len, 0, &addr, sizeof(addr)) < 0 )
    perror("sendto");
```

## sendmsg()

Assemble a message from several blocks of data. This routine takes the data in the `iovec` structure and creates a single message. If the `msg_name` points to a real `sockaddr`, the routine sends the message connectionless. If `NULL`, the routine assumes that the socket is connected.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>
#include <sys/uio.h>

int sendmsg(int sockfd, const struct msghdr *msg, unsigned int options);
```

### Return Value

This call returns the total number of bytes sent or -1 if error (check `errno` for more information).

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The open socket descriptor. |
| `msg` | This is a reference to a `msghdr` structure that holds destination, flags, and messages. The structure definitions are as follows:<br><br>```c<br>struct iovec {<br>    void *iov_base;        /* Buffer start */<br>    __kernel_size_t iov_len; /* Buffer length */<br>};<br><br>struct msghdr {<br>    __ptr_t msg_name;      /* Dest address */<br>    socklen_t msg_namelen; /* Address length */<br>    struct iovec *msg_iov; /* Buffers vector */<br>    size_t msg_iovlen;     /* Vector length */<br>    __ptr_t msg_control;   /* Ancillary data */<br>    size_t msg_controllen; /* Ancillary data len */<br>    int msg_flags;         /* Received msg flags */<br>};<br>```<br><br>The ancillary data allows the program to transfer special data like file descriptors. |
| `options` | Message-controlling flags (same as `send()`). |

### Possible Errors

(Same as `send()`)

### Example

```c
int i, sd, len, bytes;
char buffer[MSGS][100];
struct iovec io[MSGS];
struct msghdr msg;
struct sockaddr_in addr;

sd = socket(PF_INET, SOCK_DGRAM, 0);
bzero(&addr, sizeof(addr));
addr.sin_family = AF_INET;
addr.sin_port = htons(8080);
inet_aton("127.0.0.1", &addr.sin_addr);

bzero(&msg, sizeof(msg));
msg.msg_name = &addr;
msg.msg_namelen = sizeof(addr);

for ( i = 0; i < MSGS; i++ )
{
    io[i].iov_base = buffer[i];
    sprintf(buffer[i], "Buffer #%d: this is a test\n", i);
    io[i].iov_len = strlen(buffer[i]);
}

msg.msg_iov = io;
msg.msg_iovlen = MSGS;

if ( (bytes = sendmsg(sd, &msg, 0)) < 0 )
    perror("sendmsg");
```

## sendfile()

A fast way to transmit a file through a socket. The call reads the data from `in_fd` and writes it out to `out_fd`. The call does not change the file pointer in `in_fd`, but `out_fd`'s file pointer is changed. The call begins reading from `*offset` for `count` bytes. When done, `*offset` points to the byte after the last byte read. If you need to add header information, refer to the `TCP_CORK` option in `TCP(4)` to improve performance.

### Prototype

```c
#include <unistd.h>

int sendfile(int out_fd, int in_fd, off_t *offset, size_t count);
```

### Return Value

If successful, the call returns the total number of bytes copied. If error, the call returns -1 and sets `errno` to the error code.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `out_fd` | The destination descriptor (file pointer modified) |
| `in_fd` | The source descriptor (file pointer not modified) |
| `offset` | A pointer to a variable that holds the starting offset |
| `count` | The number of bytes to send |

### Possible Errors

| Error | Description |
| :--- | :--- |
| `EBADF` | Input file was not opened for reading or output file was not opened for writing. |
| `EINVAL` | Descriptor is not valid or locked. |
| `ENOMEM` | Insufficient memory for reading from `in_fd`. |
| `EIO` | Unspecified error while reading from `in_fd`. |

### Example

```c
#include <unistd.h>
#include <sys/stat.h>
#include <fcntl.h>

...
struct stat fstat;
int client = accept(sd, 0, 0);
int fd = open("filename.gif", O_RDONLY);
fstat(fd, &fstat);
sendfile(client, fd, 0, fstat.st_size);
close(fd);
close(client);
```

## recv()

Wait for and accept a message from a connected peer, client, or server. The system call behaves similarly to `read()` but adds control flags. UDP can use this call if connected to a peer.

### Prototype

```c
#include <sys/socket.h>
#include <resolv.h>

int recv(int sockfd, void* buf, int maxbuf, int options);
```

### Return Value

The number of bytes read or -1 if an error occurred.

### Parameters

| Parameter | Description |
| :--- | :--- |
| `sockfd` | The open socket descriptor |
| `buf` | The byte array to accept the incoming message |
| `maxbuf` | The size of the array |
| `options` | A set of flags that can be arithmetically ORed together:<br>• `MSG_OOB` This flag requests receipt of out-of-band data that would not be received in the normal data stream. Some protocols place expedited data at the head of the normal data queue, and so this flag cannot be used with such protocols.<br>• `MSG_PEEK` This flag causes the receive operation to return data from the beginning of the receive queue. |
