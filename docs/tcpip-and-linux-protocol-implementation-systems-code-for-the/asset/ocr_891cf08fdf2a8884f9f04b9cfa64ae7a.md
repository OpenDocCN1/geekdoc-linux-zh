# Protocol Implementation Framework

```
if (ctl_len)
  if (ctl_len > sizeof(ctl))
    ctl_buf = sock_kmalloc(sock->sk, ctl_len, GFP_KERNEL);
    if (ctl_buf == NULL)
      goto out_freeiov;
  err = -EFAULT;
  if (copy_from_user(ctl_buf, msg_sys.msg_control, ctl_len))
    goto out_freeiov;
  msg_sys.msg_control = ctl_buf;
  msg_sys.msg_flags = flags;
  if (sock->file_f_flags & O_NONBLOCK)
    msg_sys.msg_flags = MSG_DONTWAIT;
  err = sock_sendmsg(sock, &msg_sys, total_len);
out_fctrl:
  if (ctl_buf != NULL)
    sock_kfree_s(sock->sk, ctl_buf, ctl_len);
out_freeiov:
  if (iov != iostack)
    sock_kfree_s(sock->sk, iov, iov_size);
out_put:
  sockfd(sock);
  return err;
```

**Figure 5.107** Socket glue-recvmsg : linux/net/socket.c.

```
/*
BSD recvmsg interface
*/
smlinkage long sys_recvmsg(int fd, struct msghdr *msg, unsigned int flags)
(
  struct socket *sock;
  struct iovec iostack[UIO_FASTIOV];
  struct iovec *iov = iostack;
  struct msghdr *msg_sys;
  unsigned long cmsg_ptr;
  int err, iov_size, total_len, len;
  /* kernel mode address */
  char addr[MAX_SOCK_ADDR];
  /* user mode address pointers */
  struct sockaddr *uaddr;
  int *uaddr_len;
\  err = -EFAULT;
```