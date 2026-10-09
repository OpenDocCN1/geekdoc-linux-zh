
to the server, which interpreted it as a request for a Web page, which it sent back to us. How the path is treated depends on the scheme; for HTTP, it's the argument to the GET command (a single slash in our example). None of the socket system calls care about the path or the scheme.

We don't need to get into HTTP, HTML, FTP, or any other scheme-related subjects in this book beyond the minimum that we need to understand some simple examples. The best way to learn about the various schemes is to read the RFC (Request for Comments) documents [RFC].

### 8.2.6 getaddrinfo

Rather than construct a *sockaddr_in* or *sockaddr_in6* address from scratch, it's easier to call *getaddrinfo*, which builds a socket address for you:

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

Typically, you call *getaddrinfo* with *nodename* set to the host name you want, *servname* set to the port number (as a string), and *hint* set to the address family and socket type you want. You get back, through the *info* argument, a linked list of *addrinfo* structures that contain socket addresses and other information that match your hint. You pick a suitable socket address and use it directly in a call to *connect* or *bind*, casting the *ai_addr* member to *struct sockaddr*.

The “host name” can be a name to be looked up using a DNS server, a name defined in the local machine’s /etc/hosts file, an IPv4 address in dotted notation (as a string), or an IPv6 address in colon notation (as a string).

The one critical flag is AI_PASSIVE, which means that the socket addresses returned are for use with accept; that is, the call to getaddrinfo is from a server. Otherwise, with the flag clear, the call is from a client and the socket address will be used with connect. For a connectionless protocol (e.g., SOCK_DGRAM), it can also be used with sendto or sendmsg.

getaddrinfo returns its own kind of error code that you can’t treat as an errno value, which means that you can’t use standard functions like perror or strerror in case of an error. Instead, there’s a special function just for the error code returned by getaddrinfo and another function, getnameinfo (Section 8.8.1):

**gai_strerror**—get error-code description

```c
#include <netdb.h>

const char *gai_strerror(
         int code    /* error code */
);
/* Returns string (no error return) */
```

In our examples, we’ll use the error-checking macro ec_ai, which knows how to deal with the return from getaddrinfo and getnameinfo, so we won’t call gai_strerror directly.

Here’s a simple example using getaddrinfo:

```c
int main(void)
{
 struct addrinfo *infp = NULL, hint;

 memset(&hint, 0, sizeof(hint));
 hint.ai_family = AF_INET;
 hint.ai_socktype = SOCK_STREAM;
 ec_ai( getaddrinfo("www.yahoo.com", "80", &hint, &infp) )
 for ( ; infp != NULL; infp = infp->ai_next) {
 struct sockaddr_in *sa = (struct sockaddr_in *)infp->ai_addr;

 printf("%s port: %d protocol: %d\n", inet_ntoa(sa->sin_addr),
 ntohs(sa->sin_port), infp->ai_protocol);
 }
 exit(EXIT_SUCCESS);
}

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

**The output:**

- 66.218.70.48 port: 80 protocol: 0
- 66.218.70.49 port: 80 protocol: 0
- 66.218.71.88 port: 80 protocol: 0
- 66.218.71.86 port: 80 protocol: 0
- 66.218.70.50 port: 80 protocol: 0
- 66.218.71.91 port: 80 protocol: 0
- 66.218.71.80 port: 80 protocol: 0
- 66.218.71.84 port: 80 protocol: 0
- 66.218.71.90 port: 80 protocol: 0
- 66.218.71.93 port: 80 protocol: 0
- 66.218.71.94 port: 80 protocol: 0
- 66.218.71.92 port: 80 protocol: 0
- 66.218.71.89 port: 80 protocol: 0

So it seems that www.yahoo.com is associated with several different IP numbers. Because of the hint, we know that all of them are AF_INET addresses of type SOCK_STREAM, so any of them are suitable for access to Web pages. To see this, let's pair up the retrieval of the socket address via getaddrinfo with the connection and display code from the example in Section 8.2.3:

```c
#define REQUEST "GET / HTTP/1.0\r\n\r\n"

int main(void)
{
    struct addrinfo *infop = NULL, hint;
    int fd_skt;
    char buf[1000];
    size_t nread;

    memset(&hint, 0, sizeof(hint));
    hint.ai_family = AF_INET;
    hint.ai_socktype = SOCK_STREAM;
    ec_ai( getaddrinfo("www.yahoo.com", "80", &hint, &infop) )
    ec_negl( fd_skt = socket(infop->ai_family, infop->ai_socktype,
            infop->ai_protocol) )
    ec_negl( connect(fd_skt, (struct sockaddr *)infop->ai_addr,
            infop->ai_addrlen) )
    ec_negl( write(fd_skt, REQUEST, strlen(REQUEST)) )
    ec_negl( nread = read(fd_skt, buf, sizeof(buf)) )
    (void)write(STDOUT_FILENO, buf, nread);
    ec_negl( close(fd_skt) )
    exit(EXIT_SUCCESS);
}

EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

Running this produced the same output that we showed before in Section 8.2.3.

If your system, your DNS server, and the host you’re accessing support it, you can use getaddrinfo to access more than SOCK_STREAM AF_INET addresses on port 80. You can use NULL for either the nodename or servname arguments (but not both) and/or use an address “family” of AF_UNSPEC in the hint to find out what’s available. Then you search through the returned addresses to find what you want to work with. For example, you might want to use an AF_INET6 (IPv6) address if one is there. For the details on this advanced use of getaddrinfo, see [SUS2002], your system’s documentation, or Chapter 11 of [Ste2003].

One more thing before we leave this section: You should free the list returned by getaddrinfo when you no longer need it with a call to freeaddrinfo:

**freeaddrinfo**—free socket-address information

```c
#include <sys/socket.h>
#include <netdb.h>

void freeaddrinfo(
    struct addrinfo *infop    /* list to free */
);
```

We didn’t call freeaddrinfo in our examples because they were main functions that were going to exit anyway.

### 8.2.7 gethostname

Sometimes, such as in the example Web server in Section 8.4.4, a program needs the name of its own host. Usually the generic name “localhost” will work, but if other machines need to connect to the name, what’s needed is the public name assigned by the system administrator. That’s what gethostname is for.

**gethostname**—get name of host

```c
#include <unistd.h>

int gethostname(
    char *name,          /* returned name */
    size_t namelen      /* size of name buffer */
);
/* Returns 0 on success or -1 on error (errno not defined) */
```

See Section 8.4.4 for an example of gethostname in use.

## 8.3 Socket Options

One reason why the `socket` system call is so simple, even though sockets are complicated, is that all of the options are handled by a separate system call:

**setsockopt**—set socket options

```c
#include <sys/socket.h>

int setsockopt(
    int socket_fd,       /* socket file descriptor */
    int level,           /* level to be accessed */
    int option,          /* option to set */
    const void *value,   /* value to set */
    socklen_t value_len  /* length of value */
);
/* Returns 0 on success or -1 on error (sets errno) */
```

Four of the five arguments are pretty easy to explain: `socket_fd` is the socket file descriptor, `option` is the name of the option, `value` points to the value to set it to, and `value_len` is the length of the value that `value` points to. The value is usually an integer, but sometimes it's a structure specific to the option, as we'll see.

The second argument, `level`, identifies the protocol level to which the option belongs. One level, `SOL_SOCKET`, applies to the socket level itself, and it's the one you'll probably use the most. [SUS2002] defines six additional protocol levels in `<netinet/in.h>`:

- `IPPROTO_IP` Internet protocol
- `IPPROTO_IPV6` Internet Protocol Version 6
- `IPPROTO_ICMP` Control message protocol
- `IPPROTO_RAW` Raw IP Packets Protocol
- `IPPROTO_TCP` Transmission control protocol
- `IPPROTO_UDP` User datagram protocol
