Be careful—this function returns 0 if the name isn’t found, not −1.

To map an index to a name, you call:

```
**if_indextoname** —map network interface index to name

```
#include <net/if.h>

char *if_indextoname(
    unsigned ifindex,       /* interface index */
    char *ifname            /* interface name */
);
/* Returns name or NULL on error (sets errno) */
```
```

The `ifname` argument must be a buffer of at least `IF_NAMESIZE` bytes, which includes space for the terminating NUL byte. It also returns a pointer to that buffer.

# ## 8.9  Miscellaneous System Calls

This section describes some networking system calls that don’t fit into the previous sections.

# ### 8.9.1  send and recv

These two functions behave exactly like `write` and `read`, except they allow you to specify flags. Because they don’t have a socket address argument, they’re normally used with connected sockets. For connectionless sockets, `sendto`, `sendmsg`, `recvfrom`, and `recvmsg` are more convenient.

```
**send** —send data to socket

```
#include <sys/socket.h>

ssize_t send(
    int socket_fd,         /* socket file descriptor */
    const void *data,      /* data to send */
    size_t length,         /* length of data */
    int flags              /* flags */
);
/* Returns number of bytes sent or -1 on error (sets errno) */
```
```