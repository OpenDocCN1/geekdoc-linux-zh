# UNIX Domain Sockets

UNIX domain sockets work on only a single machine, so they are much more like named pipes than a network protocol. The addresses to which UNIX domain sockets bind are actual filenames in the filesystem. However, sockets cannot be opened; they must be accessed using the socket interface.

# Creating a UNIX Domain Socket

Earlier, you learned that the socket_addr structure contains a network address. That was a bit of an oversimplification. Actually, that socket_addr structure is the general format. All the protocol families (domains) have their own protocol-specific versions of socket_addr. The socket_addr structure for UNIX domain sockets is defined in <sys/un.h> as follows:

```
struct sockaddr_un {
  unsigned short int sun_family;  /* AF_UNIX */
  char sun_path[108];     /* pathname */
};
```

sun_family must be set to AF_UNIX to create a UNIX domain socket. sun_path contains the name of the file to be used as the socket. The socket is bound to the file using the bind call as you would expect, but the file is created when bind is called. If the file already exists, bind fails, sets errno to EADDRINUSE, and returns -1 to the calling process. The SUN_LEN macro, also defined in <sys/un.h>, returns the size of a sockaddr_un structure.

The sockconn program illustrated the correct method for a client program to connect to a server socket, so the example will not be repeated again. Pay close attention, however, to how sockconn and mksock cast their protocol's sockaddr_un structure to a generic socket_addr structure for each call to the API's interface.

# Example

![](bbox=[0.05, 0.6, 0.15, 0.7])

# Example

This example shows what happens when you try to open a socket that is already in use. It assumes that you have already created the socket file lpe-sample by running the first two sample programs.

```
$ ls -l lpe-sample
srw-r-xr-x 1 kwall users 0 Aug 17 18:29 lpe-sample=
$ ./mksock lpe-sample
bind: Address already in use
$ rm lpe-sample
$ ./mksock lpe-sample
socket available: lpe-sample
```