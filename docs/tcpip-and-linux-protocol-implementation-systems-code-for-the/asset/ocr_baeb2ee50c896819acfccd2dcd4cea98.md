# Protocol Implementation Framework 173

+   * For 1003.ig we need add clean support for a bind to AF_UNSPEC

+   * break bindings

+   * NOTE: 1003.ig draft 6.3 is broken with respect to AX.25/NetROM and

+   * OTHER SEQPACKET protocols that take time to connect() as it doesn't

+   * include the -EINPROGRESS status for these sockets.

+   * "/"

```
asmlinkage long sys_connect(int fd, struct sockaddr *ervaddr, int addlen)
{
    struct socket *sock;
    char address[MAX_SOCK_ADDR];
    int err;

    sock = sockfd_lookup(fd, &err);
    if (!sock)
        goto out;
    err = move_add_to_kernel(uservaddr, addlen);
    if (err < 0)
        goto out_put;
    err = sock->ops->connect(sock, struct sockaddr *)address, addlen,
        sock->file->f_flags);
out_put:
    sockfd_put(sock);
out:
    return err;
}
```

# ## Bookkeeping of Connection Identifiers

We can ask the socket layer for the addresses that the local, or far end, of a connection is bound to.

**Figure 5.101** Socket glue–the local name (address) of a socket:linux/net/socket.c.

+   */

+   * Get the local address ('name') of a socket object. Move the obtained

+   * name to user space.

+   */

```
asmlinkage long sys_getsockname(int fd, struct sockaddr *usockaddr, int *usockaddr_len)
{
    struct socket *sock;
    char address[MAX_SOCK_ADDR];
    int err;

    sock = sockfd_lookup(fd, &err);
    if (!sock)
        goto out;
    err = sock->ops->getsockname(sock, struct sockaddr *)address, &len, 0);
    return err;
}
```