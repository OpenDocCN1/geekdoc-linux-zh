[SUS2002] defines some options for these six protocols, but implementations typically define additional ones. Unfortunately, it’s not easy to get a list of all the options—you’ll have to read through the documentation for the protocol you’re using. For example, on Solaris, typing *man ip* brings up a manual page that describes options for *IPPROTO_IP*.

We’ll just describe the standardized *SOL_SOCKET* options here; for the rest, consult your system’s documentation or [Ste003].

There’s a matching call to get options, with almost the same arguments:

```
**getsockopt**—get socket options

```c
#include <sys/socket.h>

int getsockopt(
    int socket_fd,      /* socket file descriptor */
    int level,          /* level to be accessed */
    int option,         /* option to get */
    void *value,        /* returned value */
    socklen_t *value_len/* length of value */
);
/* Returns 0 on success or -1 on error (sets errno) */
```
```

The one thing different between *setsockopt* and *getsockopt* is that with the latter the *value_len* argument is a pointer to the length, and it must be set before the call to the size of the buffer pointed to by the *value* argument. On return it’s set to the size of the returned value.

Here’s a quick example that sets a socket’s *SO_REUSEADDR* option (I’ll get to what that actually means below):

```
```c
int socket_option_value = 1;

ec_neg1( setsockopt(fd, SOL_SOCKET, SO_REUSEADDR,
    &socket_option_value, sizeof(socket_option_value)) )
```
```

I’ll briefly describe all of the portable *SOL_SOCKET* options. Most of the option values are integers, in which case *value* must point to an *int*, and *value_len* will be *sizeof(int)*. Some integers are Boolean values, for which *1* is true and *0* is false. Don’t use the C constant *true* in place of a *1* because *true* may have the value *−1*, which is fine for C but not acceptable to *setsockopt*. In the following list, the notation *(B)* indicates a Boolean value, *(I)* indicates an integer, and *(X)* indicates a type that’s explained further. The letter is followed by an “*s*” and/or a “*g*” to indicate whether it’s used with *setsockopt*, *getsockopt*, or both.