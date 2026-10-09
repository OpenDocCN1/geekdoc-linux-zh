to the server, which interpreted it as a request for a Web page, which it sent back to us. How the path is treated depends on the scheme; for HTTP, it's the argument to the GET command (a single slash in our example). None of the socket system calls care about the path or the scheme.

We don't need to get into HTTP, HTML, FTP, or any other scheme-related subjects in this book beyond the minimum that we need to understand some simple examples. The best way to learn about the various schemes is to read the RFC (Request for Comments) documents [RFC].

# 8.2.6  getaddrinfo

Rather than construct a *sockaddr_in* or *sockaddr_in6* address from scratch, it's easier to call *getaddrinfo*, which builds a socket address for you:

```
**getaddrinfo**—get socket-address information

```c
#include <sys/socket.h>
#include <netdb.h>

int getaddrinfo(
    const char *nodename,        /* node name */
    const char *servname,       /* service name */
    const struct addrinfo *hint, /* hint */
    struct addrinfo **info      /* returned info as linked list */
);
/* Returns 0 on success or error number on error (errno not set) */
```
```

```
**struct addrinfo**—structure for getaddrinfo

```c
struct addrinfo {
    int ai_flags;               /* input flags */
    int ai_family;             /* address family */
    int ai_socktype;           /* socket type */
    int ai_protocol;           /* protocol */
    socklen_t ai_addrlen;      /* length of socket address */
    struct sockaddr *ai_addr;   /* socket address */
    char *ai_canonname;         /* canonical name of service location */
    struct addrinfo *ai_next;   /* pointer to next structure in list */
};
```
```

Typically, you call *getaddrinfo* with *nodename* set to the host name you want, *servname* set to the port number (as a string), and *hint* set to the address family and socket type you want. You get back, through the *info* argument, a linked list of *addrinfo* structures that contain socket addresses and other information that match your hint. You pick a suitable socket address and use it directly in a call to *connect* or *bind*, casting the *ai_addr* member to *struct sockaddr*.