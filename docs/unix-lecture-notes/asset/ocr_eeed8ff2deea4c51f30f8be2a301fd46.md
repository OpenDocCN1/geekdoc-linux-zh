4. Enter a loop in which it repeatedly accepts new connections and processes them. It can accept a new connection by calling accept(). The accept() function removes the request at the front of the completed connection queue and creates a second socket that the server can use for talking with this client. The return value of accept() is a file descriptor that represents this socket. The original socket continues to exist. The idea is that the original socket is just for listening, not talking to clients. In fact it is called the listening socket, and the new socket is called the connected socket. When the connection is closed, this connected socket is removed.

That is the essence of the server's tasks. Now what remains is to see how to program this.

# 9.1.6 Programming a Connection Oriented Server

We have already seen how the socket() call works. The step of binding a local protocol address to the socket is carried out with bind(), but before we look at bind() we need to see how these addresses are represented. A generic socket address is defined by the sockaddr structure defined in <sys/socket.h>.

```
struct sockaddr {
    sa_family_t sa_family; /* address family */
    char sa_data[];        /* socket address */
};
```

This is a generic socket address structure because it is not specific to any one address family. When you call bind(), you will be specifying a particular family, such as PF_INET or PF_UNIX. For each of these there is a different form of socket address structure. The address structure for PF_INET, defined in <netinet/in.h>, would be

```
struct sockaddr_in {
    sa_family_t    sin_family; /* internet address family */
    in_port_t      sin_port;   /* port number */
    struct in_addr sin_addr;   /* IP address */
    unsigned char  sin_zero[8]; /* padding */
};
```

The bind() system call takes the socket file descriptor returned by socket() and an address structure like the one above, and "binds" them together to form the end of a socket that can now be used by processes living somewhere in the internet to find this server:

```
#include <sys/types.h>
#include <sys/socket.h>

int bind(int sockfd, const struct sockaddr *address,
         socklen_t addrlen);
```

Putting these few steps together, we might start out with the following code: