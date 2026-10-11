
Then, replace lines 40–45 of `mksock.c` with the following:

```c
/* Accept the first connection that comes in */
if ((infd = accept(sockfd, (struct sockaddr *)&srv, &socklen)) >= 0)
      puts("new connection granted");

/* Read from the socket and write to stdout */
xfer_data(infd, fileno(stdout));
```

Rather than simply accepting every incoming connection, the new code accepts only the first connection, and then calls `xfer_data` to read incoming data from the socket's file descriptor, `infd`, and write it to `stdout`.

Finally, add the following code just above the `exit` statement of `sockconn.c`:

```c
/* Copy stdin to the socket file descriptor */
xfer_data(fileno(stdin), sockfd);
```

The additional code reads input from `stdin` and writes it the file descriptor bound to the socket. The modified files are available as `rdsock.c` and `wrsock.c` from the Web site for this book.

To run these programs, run `rdsock` in one xterm or virtual console, and then start `wrsock` on another one. Each time you press Enter, lines of text entered appear in `rdsock`'s window. Sample output from these programs is illustrated in Figure 18.4.

![](img/be588b36b489136ce784030a08a1d3d4_426_0.png)

Figure 18.4:
Reading and writing UNIX domain sockets.

In Figure 18.4, the reader/server, rdsock, is running in the xterm on the left and the writer/client, wrsock, is running in the xterm on the right. As you can see in the figure, each line of text typed into the writer appears in the reader after you press Enter.

# TCP/IP Programming

TCP/IP is the protocol (actually, the protocol family) that runs the Internet, the largest network of interconnected machines in the world. The current version of the protocol is version 4 (IPv4), but the transition to version 6 (IPv6) has already begun. The specifications extant in current proposals for IPv6 have been integrated in the 2.2.x kernels. Because the new protocol is not in wide use, however, this section covers IPv4 instead. As remarked at the beginning of the chapter, network programming is a big topic about which whole volumes of books are written. However, you can actually write network-capable programs using fewer than 10 function calls.

# Network Numbers

Before jumping into network programming per se, it is important to point out that the TCP/IP protocol is big-endian; that is, it stores the most significant bit of multibyte numbers in the lowest memory address. Many computers are similarly big-endian.

However, other computers, such as Intel's x86 processors, are little-endian, meaning that the least significant bit of multibyte numbers is stored in the lowest memory address (the general term for the arrangement of values in memory is byte ordering). The implication of this is that when feeding numeric values to the TCP/IP functions, they must be converted from the host's byte order to the network's byte order.

Fortunately, the protocol implementation includes four functions to do precisely this. They are declared in `<netinet/in.h>` as follows:

```c
unsigned long int htonl(unsigned long int hostlong);
unsigned short int htons(unsigned short int hostshort);
unsigned long int ntohl(unsigned long int netlong);
unsigned short int ntohs(unsigned short int netshort);
```

`htonl` converts `hostlong`, a long integer, from the host system's byte order to network byte order. Similarly, `htons` converts `hostshort`, a short integer, from the host byte order to network byte order. The other two calls, `ntohl` and `ntohs`, reverse the process and thus convert from network byte order to the host system's byte order.

# Network Addresses

As with UNIX domain sockets, TCP/IP network addresses are stored in a `sockaddr` structure, `struct sockaddr_in`, defined in `<netinet/in.h>` as follows:

```c
struct sockaddr_in {
    short int sin_family;      /* AF_INET */
    uint16_t sin_port;        /* Port number */
    struct in_addr sin_addr;  /* IP address */
};
```

You also must include `<sys/socket.h>` to get the complete socket definition. For TCP/IP (version 4, at least), `sin_family` must be `AF_INET`. `sin_port` is the port number to which to connect, and `sin_addr` is the IP address. Both `sin_port` and `sin_addr` must be in network byte order. However, `sin_addr` is a binary structure, so to convert it into standard dotted decimal form, use the `inet_ntoa` function; conversely, to convert a dotted decimal address to the binary format of `sin_addr`, use `inet_aton`. These calls are prototyped in `<arpa/inet.h>` as

```c
char *inet_ntoa(struct in_addr addr);
int inet_aton(const char *daddr, struct in_addr *ipaddr);
```

`inet_ntoa` converts the binary IP address stored in `addr` and returns it as a string (the returned string is a statically allocated buffer that is overwritten by subsequent calls of `inet_ntoa`). `inet_aton` converts a dotted decimal address stored in `daddr` to the proper binary format, and then stores it in `ipaddr`. If the address is a valid address, `inet_aton` returns nonzero, otherwise it returns zero.

> **CAUTION**
>
> Several TCP/IP API functions return zero on failure and nonzero when they succeed. This behavior is precisely opposite the behavior of almost every library and system call you have seen so far.

> **TIP**
>
> You will occasionally encounter a function named `inet_addr`. It does the same thing as `inet_aton`. It has the prototype `unsigned long int inet_addr(const char *daddr)`. It is an obsolete call because it does not recognize `255.255.255.255` as a valid IP address. If you encounter code that uses this function, do the world a favor and change it to use `inet_aton`.

TCP/IP network addresses are 32-bit numbers, usually expressed in *dotted decimal* notation such as www.xxx.yyy.zzz. Because they are 32-bit numbers, there are a potential 4,294,967,295 (counting from 0) unique network addresses. However, because each unique address might want or need to run multiple TCP/IP applications simultaneously, each address also has up to 65,535 ports to which to connect.

*Ports* are 16-bit numbers that represent a connection or end point on a given system (ports 0-1024 are reserved for use by processes running with root privileges). So, a unique connection point on one system is defined by the combination of the host's IP address and a port number. A complete and unique network connection between two systems is defined by two such connection points. Figure 18.5 graphically illustrates this point.

![](img/be588b36b489136ce784030a08a1d3d4_430_0.png)

As you can see in the figure, HOST1 and HOST2 have four complete connections between them, HOST1:PORT1 to HOST2:PORT2, HOST1:PORT2 to HOST2:PORT3, HOST2:PORT1 to HOST1:PORT3, and HOST2:PORT4 to HOST1:PORT4.

Before looking at the sample programs, you must know about one last function, *setsockopt*. After closing a socket, its address (the IP and port number combination) is unavailable for a certain period of time. To reuse this address, you must set an option on the socket that allows it to be reused. It is declared in `sys/socket.h` as

```c
int setsockopt(int sockfd, int level, int optname,
               const void *optval, socklen_t optlen);
```

*setsockopt* sets the option stored in *optname* to *optval* for the socket that opened on the file descriptor *sockfd*. For sockets, *level* must be *SOL_SOCKET*.

Set *optname* to *SO_REUSEADDR* and *optval* to *1*. That is, the *setsockopt* call should resemble the following:

```c
int i = 1;
setsockopt(sockfd, SOL_SOCKET, SO_REUSEADDR, &i, sizeof(i));
```

# Examples

![](img/be588b36b489136ce784030a08a1d3d4_431_0.png)

# Example

1. The example that follows, *mynet*, creates a *TCP/IP* socket, and then waits for and accepts all connections. It uses port number *50000*, which is not likely to be used by another program.

```c
/*
 * mynet.c - Bind to and wait on a TCP/IP socket
 */
#include <sys/socket.h>
#include <netinet/in.h>

#include <arpa/inet.h>
#include <unistd.h>
#include <stdlib.h>
#include <stdio.h>
#include "helper.h"

int main(void)
{
    int sockfd;
    struct sockaddr_in srv; /* Server's socket structure */
    socklen_t socklen;
    int i = 1;               /* For setsockopt */

    /* Create the socket */
    if ((sockfd = socket(PF_INET, SOCK_STREAM, 0)) < 0)
        err_quit ("socket");

    /* Want to reuse the local address */
    setsockopt (sockfd, SOL_SOCKET, SO_REUSEADDR, &i, sizeof (i));

    /* Initialize and set up the server structure */
    memset (&srv, 0, sizeof (srv));
    srv.sin_family = AF_INET;
    srv.sin_port = htons (50000); /* Don't forget network byte order */
```
