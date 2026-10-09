selection if the type offers a choice, but in most cases the default will do, so it’s zero.

Next, the server has to name the socket with `bind`:

```
```
bind—bind name to socket
#include <sys/socket.h>

int bind(
    int socket_fd,                    /* socket file descriptor */
    const struct sockaddr *sa,         /* socket address */
    socklen_t sa_len                   /* address length */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

Socket addresses get a whole section to themselves (Section 8.2). We’ve already seen an example for `AF_UNIX`, which is just for communication within a single machine, as were the IPC mechanisms in Chapter 7. Later we’ll see how to set up addresses for other domains, including `AF_INET`.

Remember that on most systems, for `AF_UNIX`, `bind` will make a fresh socket file; it can’t reuse an existing file.

The server also has to call `listen` to set the socket up for accepting connections:

```
```
listen—mark socket for accepting and set queue limit
#include <sys/socket.h>

int listen(
    int socket_fd,                    /* socket file descriptor */
    int backlog                       /* maximum connection queue length */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

Our example in the last section didn’t show it, but a server can accept connections from lots of clients. Also, as it can only issue `accepts` at a certain rate, requests for connections can queue up. The second argument to `listen` limits the length of that queue. Usually an attempt by a client to connect when the queue is full causes its `connect` to return –1 with `errno` set to `ECONNREFUSED`. In my examples I use the constant `SOMAXCONN`, which is a system-defined maximum.

Next, the server accepts a connection: