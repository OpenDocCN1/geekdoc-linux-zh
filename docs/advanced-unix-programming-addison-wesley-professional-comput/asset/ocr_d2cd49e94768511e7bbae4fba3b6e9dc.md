Like *accept*, *connect* usually blocks until the connection request is accepted, but it doesn't return a file descriptor—the client does I/O on the socket file descriptor.

If the *O_NONBLOCK* flag is set, *connect* won't block waiting for a connection but will return −1 with *errno* set to *EINPROGRESS*. The connection request isn't abandoned but remains on the queue to be eventually satisfied. Further calls to *connect* during that period also return −1 but with *errno* now set to *EALREADY*. When the connection is made, the socket file descriptor can be used. If you want, you can use *select* or *poll* to wait for it to be ready for writing (not reading). A typical use for this would be an application that has some initialization to do. It issues a nonblocking *connect*, does the initialization, and then issues a *select* or *poll* to block.

# 8.1.3 Handling Multiple Clients

Now let's extend the example from Section 8.1.1 so the server can handle multiple clients. Here's a replacement for the server-side code in that example:

```
```
static bool run_server(struct sockaddr_un *sap)
{
  int fd_skt, fd_client, fd_hwm = 0, fd;
  char buf[100];
  fd_set set, read_set;
  ssize_t nread;

ec_neg1( fd_skt = socket(AF_UNIX, SOCK_STREAM, 0) )
ec_neg1( bind(fd_skt, (struct sockaddr *)sap, sizeof(*sap)) )
ec_neg1( listen(fd_skt, SOMAXCONN) )
  if (fd_skt > fd_hwm)
    fd_hwm = fd_skt;
  FD_ZERO(&set);
  FD_SET(fd_skt, &set);
  while ( true ) {
    read_set = set;
    ec_neg1( select(fd_hwm + 1, &read_set, NULL, NULL, NULL) )
    for (fd = 0; fd<= fd_hwm; fd++)
      if (FD_ISSET(fd, &read_set)) {
        ec_neg1( fd_client = accept(fd_skt, NULL, 0) )
        FD_SET(fd_client, &set);
        if (fd_client > fd_hwm)
          fd_hwm = fd_client;
```

```