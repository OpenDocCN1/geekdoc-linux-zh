```
        EC_CLEANUP_BGN
           EC_FLUSH("gethostbyaddr_ex")
        EC_CLEANUP_END
}
```

The output:

name: wl5.www.scd.yahoo.com; type: 2; len: 4
    66.218.71.94

What happened is that when we got the IP addresses for `www.yahoo.com`, `66.218.71.94` was on the list, but when we asked for that IP’s name we got `wl5.www.scd.yahoo.com`. That’s the way DNS works—apparently Yahoo uses a lot of servers, which, of course, it must.

`gethostbyaddr` is just as obsolete as `gethostbyname`. The modern function is the counterpart to `getaddrinfo` (Section 8.2.6), called `getnameinfo`:

```
**getnameinfo**—get name information

```
#include <sys/socket.h>
#include <netdb.h>

int getnameinfo(
     const struct sockaddr *sa,    /*  socket address */
     socklen_t sa_len,            /*  socket-address length */
     char *nodename,              /*  node name */
     socklen_t nodelen,           /*  node-name buffer length */
     char *servname,             /*  service name */
     socklen_t servlen,          /*  service-name buffer length */
     unsigned flags             /*  flags */
);
/* Returns 0 on success or error number on error */
```
```

`getnameinfo` takes a whole socket address, not just a bare IP address, because it potentially works with lots of different families. Most importantly, it works with IPv6 addresses, which `gethostbyname` doesn’t. The answers come back into two buffers: `nodename`, of length `nodelen`, for the node (or host) name, and `servname`, of length `servlen`, for the service name. If a buffer pointer is NULL or its length is 0, you don’t get that information back.

Like `getaddrinfo`, the error numbers returned by `getnameinfo` aren’t `errno` codes, but special “EAI” codes, and you can use the function `gai_strerror` (Section 8.2.6) on them if you want. Or, use the `ec_ai` macro that we’ve provided just for these two functions.

Various flags that you can OR together control what `getnameinfo` returns: