
## 8.2.3 AF_INET Socket Addresses

As I mentioned earlier, the AF_INET domain is for communicating with sockets over the Internet. Here’s the $sockaddr_{-}in$ structure:

```
struct sockaddr_in—structure for AF_INET socket addresses

#include <netinet/in.h>
struct sockaddr_in {
    sa_family_t sin_family;    /* AF_INET */
    in_port_t sin_port;        /* port number (uint16_t) */
    struct in_addr sin_addr;   /* IPv4 address */
};

struct in_addr {
    in_addr_t s_addr;          /* IPv4 address (uint32_t) */
};
```

An IPv4[^5] address (usually called just an “IP address”) is a 32-bit binary number assigned to a network interface on a machine. Instead of referring to these numbers the usual way (e.g., 1,182,625,240), we use dotted notation, in which each byte is expressed as a separate decimal number, as in 216.109.125.70. Even that isn’t very convenient, so there’s a system using descriptive names instead that allows us to say www.yahoo.com instead of 216.109.125.70 (Section 8.2.5), but I’ll use dotted notation for now.

Each IP can be associated with lots of different services, each of which is assigned a 16-bit port number. Many of the port numbers are, by convention, assigned to well-known services. For example, HTTP (Web) servers are on port 80, FTP servers are on port 21, Telnet servers are on port 23, and so on. You can see how the ports are assigned on your machine by looking at the /etc/services file. For example, here are selected parts of the file (over 2000 lines in all) on my FreeBSD system:

```
... 
ftp             21/tcp    #File Transfer [Control]
ftp             21/udp    #File Transfer [Control]
ssh             22/tcp    #Secure Shell Login
ssh             22/udp    #Secure Shell Login
telnet          23/tcp    #Telnet
telnet          23/udp    #Telnet
...
finger          79/tcp    #Finger
finger          79/udp    #Finger
http            80/tcp    www www-http #World Wide Web HTTP
http            80/udp    www www-http #World Wide Web HTTP
...
```

[^5]: It’s Version 4 of the Internet Protocol.

The types for the port and IP number, in_port_t and in_addr_t, are defined to be uint16_t and uint32_t, respectively, and must be in network byte order, which means you can use the htons and htonl functions, like this:

```c
struct sockaddr_in sa;

sa.sin_family = AF_INET;

sa.sin_port = htons(80);

sa.sin_addr.s_addr = htonl((216UL << 24) + (109UL << 16) +
                           (125UL << 8) + 70UL); /* 216.109.125.70 */
```

But for dotted IP numbers, there's an even better function that goes directly from a string to a 32-bit IP number in network byte order:

```
**inet_addr**—convert dotted IPv4 address string to integer

#include <arpa/inet.h>

in_addr_t inet_addr(
    const char *cp             /* dotted IP address */
);

/* Returns IP address or (in_addr_t)-1 on error (errno not defined) */
```

The return value, −1 cast to an unsigned 32-bit number, is the same as what we would get if we converted 255.255.255.255. But this is OK because that's an illegal IP address.

The reverse function is also sometimes handy:

```
**inet_ntoa**—convert integer IPv4 address to dotted string

#include <arpa/inet.h>

char *inet_ntoa(
    struct in_addr in          /* integer address */
);

/* Returns string (no error return) */
```

Instead of `inet_addr` and `inet_ntoa`, you can use the more general functions `inet_ntop` and `inet_pton` (Section 8.9.5), which also work for IPv6 addresses.

Going back to our example, let’s use `inet_addr` instead of `hton` for the IP address and add some code that connects to the HTTP server on port 80, sends a request for a Web page, and displays part of what comes back:

```c
#define REQUEST "GET / HTTP/1.0\r\n\r\n"

int main(void)
{
    struct sockaddr_in sa;
    int fd_skt;
    char buf[1000];
    ssize_t nread;

    sa.sin_family = AF_INET;
    sa.sin_port = htons(80);
    sa.sin_addr.s_addr = inet_addr("216.109.125.70");
    ec_negl( fd_skt = socket(AF_INET, SOCK_STREAM, 0) )
    ec_negl( connect(fd_skt, (struct sockaddr *)\&sa, sizeof(sa)) )
    ec_negl( write(fd_skt, REQUEST, strlen(REQUEST)) )
    ec_negl( nread = read(fd_skt, buf, sizeof(buf)) )
    (void)write(STDOUT_FILENO, buf, nread);
    ec_negl( close(fd_skt) )
    exit(EXIT_SUCCESS);

    EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
    EC_CLEANUP_END
}
```

The request is a GET command, which is defined by the HTTP protocol that defines Web communication (see Section 8.4.2). Here’s part of the output that came back, which you may recognize as the HTML source for Yahoo’s home page. It begins with a status line, followed immediately by the HTML (shown greatly abbreviated):

```
HTTP/1.1 200 OK
Date: Sat, 19 Jul 2003 18:51:56 GMT
P3P: policyref="http://p3p.yahoo.com/w3c/p3p.xml", CP="CAO DSP COR CUR ADM ...
Cache-Control: private
Connection: close
Content-Type: text/html

<html><head>
<title>Yahoo!</title>...
```

## 8.2.4 AF_INET6 Socket Addresses

If all 32 bits of an IPv4 address could be used, there would be addresses for 4.3 billion network interfaces, which is probably enough for a while. Because of the way IPv4 addresses are assigned, however, there can be only 534 million so-called Class B addresses (those that begin with 192 through 223), which are used by large organizations, and around 1992 it looked like these would run out by mid-1995. Another problem was that routing tables used by Internet backbone sites were growing too large to fit in the memory of routers available at that time.

The proposed solution was Version 6 of the Internet Protocol, called IPv6, which, among other improvements, expands the address from 4 bytes to 16, which allows $2^{128}$ addresses.[^6]

[^6]: This expansion allows for a vastly larger number of unique addresses.

The preferred way of writing an IPv6 address is as 8 groups of 2 bytes each, such as FEDC:BA98:7654:3210:FEDC:BA98:7654:3210.

You use a `sockaddr_in6` structure to set up an `AF_INET6` socket address; there's more to it than for `AF_INET`, as you would expect:

```
struct sockaddr_in6—structure for AF_INET6 socket addresses

#include <netinet/in.h>
struct sockaddr_in6 {
    sa_family_t sin6_family;    /* AF_INET6 */
    in_port_t sin6_port;        /* port number (uint16_t) */
    uint32_t sin6_flowinfo;    /* traffic class and flow information */
    struct in6_addr sin6_addr; /* IPv6 address */
    uint32_t sin6_scope_id;    /* set of interfaces for a scope */
};

struct in6_addr {
    uint8_t s6_addr[16];       /* IPv6 address */
};
```

The two new members here that have no equivalent in a `sockaddr_in` structure are `sin6_flowinfo`, which is intended to hold a “flow label” and priority but whose use is currently unspecified, and `sin6_scope_id`, which identifies a set of interfaces that are used with certain addresses and is implementation dependent. If you're setting up your own `sockaddr_in6` structure, set these to zero. In fact, you're supposed to initialize the whole structure to zeros before setting the members you're interested in because some implementations have members in addition to those listed in the synopses above.

In practice, you won't be initializing a `sockaddr_in6` structure directly; instead, you'll get one from `getaddrinfo`, which is described in Section 8.2.6.

You can't use `inet_addr` and `inet_ntoa` with IPv6 addresses. Instead you use `inet_ntop` and `inet_pton`, which are in Section 8.9.5.

## 8.2.5 The Domain Name System (DNS)

Of course, you seldom type a numeric IP address into your Internet browser or FTP client—you type a mnemonic name like www.yahoo.com or www.basepath.com. These host names are translated to IP addresses by a world-wide distributed database called DNS. There are several standardized functions for accessing the DNS from a UNIX application. The newest and most powerful is called `getaddrinfo`, which is the one we'll use in our examples. Section 8.8.1 briefly describes some older functions (such as `gethostbyname`).

In a URL like http://www.basepath.com/aup (the URL for this book's site), the host name is just the middle part. That is, the overall syntax is:[^7]

`scheme` // `hostname`/`path`

where *scheme* specifies the method of access to the resource (e.g., HTTP, FTP), *hostname* is the name of the host as recorded in the DNS database, and *path* is a path within the host's file system.

In our examples, we use the socket system calls to connect to the host. Once we have a connection, we interact with the host according to the scheme. For instance, in the example in Section 8.2.3, the scheme was HTTP, so we sent the request

```
GET / HTTP/1.0
```

[^7]: This is a simplified view, but it will suffice for our purposes. The complete syntax for Uniform Resource Identifiers is more complicated.
