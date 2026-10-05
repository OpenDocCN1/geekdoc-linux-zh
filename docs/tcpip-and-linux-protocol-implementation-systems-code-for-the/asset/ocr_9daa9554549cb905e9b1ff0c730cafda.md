# TCP/IP and Linux Protocol Implementation

The next piece of code actually fields the asynchronous calls.

**Figure 5.98** Socket glue–finish async events on sockets: linux/net/socket.c.

```
/* This function may be called only under socket lock or callback_lock */
int sock_wake_async(struct socket *sock, int how, int band)
{
    if (!sock || !sock->fsasync_list) {
        return -1;
    }
    switch (how) {
        case 1:
            if (test_bit(SOCK_ASYNC_WAITDATA, &sock->flags)) {
                break;
                goto call_kill;
            }
        case 2:
            if (!test_and_clear_bit(SOCK_ASYNC_NSPACE, &sock->flags)) {
                break;
            }
            /* fall through */
        case 0:
            call_kill:
                kill_fsasync(sock->fsasync_list, SIGIO, band);
                break;
        case 3:
                kill_fsasync(sock->fsasync_list, SIGURG, band);
                break;
    }
    return 0;
}
```

# Creating a Socket

**Figure 5.99** Socket glue–create a socket i: linux/net/socket.c.

```
int sock_create(int family, int type, int protocol, struct socket **res)
{
    int i;
    struct socket *sock;
    /*
     * Check protocol is in range
     */
    if (family<0 || family>=NPROTOMAX)
        return -EAFNOSUPPORT;
    
    /* Compatibility.
     This uglymoron is moved from INET layer here to avoid
     deadlock in module load.
     */
```