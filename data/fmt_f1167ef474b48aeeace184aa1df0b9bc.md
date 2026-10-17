
```c
/*
 * BSD sendmsg 接口
 */
asmlinkage long sys_sendmsg(int fd, struct msghdr *msg, unsigned flags)
{
    struct socket *sock;
    char address[MAX_SOCK_ADDR];
    struct iovec lock[UIO_FASTIOV], *iov = iovack;
    unsigned char ctl[sizeof(struct msghdr) + 20]; // 20是 ipv6_pktinfo 的大小
    unsigned char *ctl_buf = ctl;
    struct msghdr msg_sys;
    int err, iov_len, total_len;

    err = -EFAULT;
    if (copy_from_user(msg_sys, msg, sizeof(struct msghdr)))
        goto out;

    sock = sockfd_lookup(fd, &err);
    if (!sock)
        goto out;

    /* 在 msg_sys 有效前不要移动 */
    err = -EINVAL;
    if (msg_sys.msg_iovlen > UIO_MAXIOV)
        goto out_put;

    /* 是否需要分配 iovec 区域 */
    err = -ENOMEM;
    iov_size = msg_sys.msg_iovlen * sizeof(struct iovec);
    if (msg_sys.msg_iovlen > UIO_FASTIOV)
        iov = kmalloc(sock->sk, iov_size, GFP_KERNEL);
    if (!iov)
        goto out_put;

    }
}
```

# 协议实现框架

```c
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

**图 5.107** Socket glue-recvmsg : linux/net/socket.c。

```c
/*
BSD recvmsg 接口
*/
smlinkage long sys_recvmsg(int fd, struct msghdr *msg, unsigned int flags)
(
  struct socket *sock;
  struct iovec iostack[UIO_FASTIOV];
  struct iovec *iov = iostack;
  struct msghdr *msg_sys;
  unsigned long cmsg_ptr;
  int err, iov_size, total_len, len;
  /*内核态地址 */
  char addr[MAX_SOCK_ADDR];
  /* 用户态地址指针 */
  struct sockaddr *uaddr;
  int *uaddr_len;
  err = -EFAULT;
```

# TCP/IP 与 Linux 协议实现

```c
1422
if (copy_from_user(msg_sys.msg,sizeof(struct msgghdr))
1423
	togo out;
1424
1425
    sock = sockfd_lookup(fd,err);
1426
    if (!sock)
1427
	togo out;
1428
1429
    err = -EINVAL;
1430
    if (msg_sys.msg_iovlen > UI_MAXIOV)
1431
	togo out_put;
1432
1433
    /* 检查是否分配 iovec */
1434
    err = -ENOMEM;
1435
    iov_size = msg_sys.msg_iovlen * sizeof(struct iovec);
1436
    if (msg_sys.msg_iovlen > UI_FASTIO) {
1437
        iov = sock_malloc(sock->sk, iov_size, GFP_KERNEL);
1438
        if (!iov)
            	togo out_put;
1439
    }
```

```c
1442
    /*
1443
     * 保存用户态地址（verify_iovec 将内核
1444
     * 的 msgghdr 改为使用内核地址空间）
1445
     */
1446
1447
    uaddr = msg_sys.msg_name;
1448
    uaddr_len = msg_sys->msg_namelen;
1449
    err = verify_iovec(iovec, iov, VERIFY_WRITE);
1450
    if (err < 0)
        	togo out_freeiov;
1451
    total_len;
1452
1453
    cmsg_ptr = (unsigned long)msg_sys.msg_control-cmsg_ptr;
1455
    msg_sys.msg_flags = 0;
1457
    if (sock->file->flags & 0_NONBLOCK)
1458
        flags |= MSG_DONTWAIT;
1459
        err = sock_recvmsg(sock, &msg_sys, total_len, flags);
1460
        if (err < 0)
            	togo out_freeiov;
1461
    len = err;
1463
    if (uaddr != NULL && msg_sys.msg_namelen) {
1464
        err = move_add_to_user(uaddr, msg_sys.msg_namelen, uaddr, uaddr_len);
1465
        if (err < 0)
            	togo out_freeiov;
1466
    }
1468
1469
    err = __put_user(msg_sys.msg_flags, &msg_sys->msg_flags);
1470
    if (err)
        	togo out_freeiov;
1472
    err = __put_user((unsigned long)msg_sys.msg_control,
1473
        &msg_sys->msg_control);
```

**图 5.108** Socket-recvmsg: linux/net/socket.c。

# 协议实现

```c
if (err)
    goto out_freeiov;
err = len;
out_freeiov:
    if (iov != iostack)
        sock_kfree_s(sock->sk, iov, iov_size);
out_put:
    sockfd(sock);
out:
    return err;
```

**图 5.109** Socket glue-file control (fcntl): linux/net/socket.c。
