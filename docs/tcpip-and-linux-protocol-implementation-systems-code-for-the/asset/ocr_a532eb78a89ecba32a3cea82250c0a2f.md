# Protocol Implementation Framework

```
if (err)
    goto out_freeiov;
err = len;
out_freeiov:
    if (iov != iovstack)
        sock_kfree_s(sock->sk, iov, iov_size);
out_put:
    sockfd_put(sock);
out:
    return err;
}
```

# Other VFS Calls

**Figure 5.109 Socket glue—file control (fcntl): linux/net/socket.c.**

```
/*
 * Perform a file control on a socket file descriptor.
 * Doesn't acquire a fd lock, because no network fcntl
 * function sleeps currently.
 */
int sock_fcntl(struct file *filp, unsigned int cmd, unsigned long arg)
{
    struct socket *sock;

    sock = sock_lock_lookup(filp->f_entry->d_inode);
    if (sock && sock->ops)
        return sock_no_fcntl(sock, cmd, arg);
    return(-EINVAL);
}

/* Argument list lists for sys_socketcall all */
#define Al(x) ((x) sizeof(unsigned long))
static unsigned char nargs[18]={AL(0),AL(0),AL(3),AL(3),AL(3),AL(3),
AL(3),AL(3),AL(4),AL(4),AL(4),AL(4),AL(4),
AL(6),AL(2),AL(2),AL(5),AL(5),AL(3)};

undef Al
```

**Figure 5.110 Socket glue—system call vector: linux/net/socket.c.**

```
/*
 * System call vectors.
 * Argument checking cleaned up. Saved 20% in size.
 * This function doesn't need to set the kernel lock because
 * it is set by the callee.
 */
```