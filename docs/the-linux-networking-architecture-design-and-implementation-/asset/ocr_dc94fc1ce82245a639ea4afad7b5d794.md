# 27.2 Functions of the Socket API 543

```
if (childpid = fork()) < 0
    printf("ERROR: Creating child process");
else if (childpid == 0)
{
    /* Child process */
    close(sockfd);
    doit(newsockfd);
    exit(0);
}
/* Parent socket */
/* Handle client request */
/* Parent closes the new socket */

```

```
int connect(int sockfd, struct sockaddr *ServAddr, int AddrLength)
```

A newly created socket is not connected (i.e., it is not associated with a destination address or a communication partner). However, a user program has to establish a connection before data can be sent over a reliable connection. Once a connection has been successfully established, no destination address needs to be specified to transmit data in a connection-oriented communication (e.g., SOCK_STREAM). Sockets for connectionless datagram services not have to be connected; they can transmit directly.
For the connection-oriented TCP protocol, the connect() system call returns the actual setup of a connection from the local system to a (remote) communication partner.

The following parameters are required to open a connection:

+   * int sockfd: Socket descriptor.
* struct sockaddr *ServAddr: Pointer to a structure that specifies the destination address to which the socket should be connected.
* int AddrLength: Length of the address structure in bytes.

Application Example: Once it has opened a socket, the client fills the data structure for the server address. If the IP address is available in dotted decimal notation, it can be converted by the inet_addr function. The port number of the server is brought into network byte order by the htons() routine. Again, it is useful to first initialize the entire address memory.

```
#include <sys/types.h>
#include <sys/socket.h>

#define SERVER_TCP_PORT 2001
#define SERVER_HOST_ADDR "129.13.35.77"

struct sockaddr_in serv_addr;
/* A sockfd was already created ... */
/* Initialize data space. */
memset(&serv_addr, 0, sizeof(serv_addr));
```