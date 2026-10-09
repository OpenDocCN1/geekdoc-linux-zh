```
EC_CLEANUP_BGN
    exit(EXIT_FAILURE);
EC_CLEANUP_END
}
```

Running this produced the same output that we showed before in Section 8.2.3.

If your system, your DNS server, and the host you’re accessing support it, you can use getaddrinfo to access more than SOCK_STREAM AF_INET addresses on port 80. You can use NULL for either the nodename or servname arguments (but not both) and/or use an address “family” of AF_UNSPEC in the hint to find out what’s available. Then you search through the returned addresses to find what you want to work with. For example, you might want to use an AF_INET6 (IPv6) address if one is there. For the details on this advanced use of getaddrinfo, see [SUS2002], your system’s documentation, or Chapter 11 of [Ste2003].

One more thing before we leave this section: You should free the list returned by getaddrinfo when you no longer need it with a call to freeaddrinfo:

```
freeaddrinfo—free socket-address information
#include <sys/socket.h>
#include <netdb.h>

void freeaddrinfo(
    struct addrinfo *infop    /* list to free */
);
```

We didn’t call freeaddrinfo in our examples because they were main functions that were going to exit anyway.

# 8.2.7 gethostname

Sometimes, such as in the example Web server in Section 8.4.4, a program needs the name of its own host. Usually the generic name “localhost” will work, but if other machines need to connect to the name, what’s needed is the public name assigned by the system administrator. That’s what gethostname is for.

```
gethostname—get name of host
#include <unistd.h>

int gethostname(
    char *name,          /* returned name */
    size_t namelen      /* size of name buffer */
);
/* Returns 0 on success or -1 on error (errno not defined) */
```