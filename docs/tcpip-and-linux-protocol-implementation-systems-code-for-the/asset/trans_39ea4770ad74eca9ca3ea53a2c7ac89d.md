

## TCP/IP 与 Linux 协议实现

```
564  iov.iov_len=size;
565  flags = !(file->f_flags & O_NONBLOCK) ? 0 : MSG_DONTWAIT;
566
567  return sock_recvmsg(sock, &msg, size, flags);
568 }
```

同样，还有一个 `write()` 系统调用。

图 5.73 Socket 粘合–write: linux/net/socket.c。

```
571  /*
572   * 向 socket 写数据。我们验证用户区域 ubuf..ubuf+size-1
573   * 是否可供用户进程。
574  */
575
576  static size_t t_sock_write(struct file *file, const char *ubuf,
577                               size_t size, loff_t *ppos)
578  {
579      struct socket *sock;
580      struct msghdr msg;
581      struct iovec iov;
583
584      if (ppos != &file->f_pos)
585          return -ESPIPE;
586      if(size==0)                    /* 匹配 SysV5行为 */
587          return 0;
588
589
590      sock = sock_lookup(file->f_dentry->d_inode);
591      msg.msg_name=NULL;
592      msg.msg_len=0;
593      msg.iov=iov;
594      msg.iov_len=1;
595      msg.control=NULL;
596      msg.controllen=0;
597      msg.flags=(file->f_flags & O_NONBLOCK) ? 0 : MSG_DONTWAIT;
598      if (sock->type == SOCK_PACKET)
599          msg.msg_flags |= MSG_HDR;
600      iov.iov_base=(void *)ubuf;
601      iov.iov_len=size;
602
603      return sock_sendmsg(sock, &msg, size);
604  }
```

## 非连续 I/O 缓冲区参数

以下例程管理用户使用非连续缓冲区（iovec 结构体）时的调用。

图 5.74 Socket 粘合-readv/writev 服务例程: linux/net/socket.c。

```
605 int sock_readv/writev(int type, struct inode *inode, struct file *file,
606      const struct iovec *iov, long count, long size)
607 {
608     struct msghdr msghdr;
609     struct socket *sock;
610
611     sock = sock_lookup(inode);
612     struct msghdr *msg_name = NULL;
613     msg_name->namelen = 0;
614     msg_name->control = NULL;
615     msg_name->controllen = 0;
616     msg_name->iov = (struct iovec *)iov;
617     msg_name->iovlen = count;
618     msg_name->flags = (file->flags & O_NONBLOCK) ? MSG_DONTWAIT : 0;
619
620     /* VERIFY_WRITE */
621     if (type == VERIFY_WRITE)
622         return sock_recvmsg(sock, &msg_name, size, msg_name->flags);
623
624     if (type == SOCK_PACKET)
625     msg_name->flags |= MSG_HDR;
626
627     return sock_sendmsg(sock, &msg_name, size);
628 }
```

前面的函数在此处是一个服务函数。

图 5.75 Socket 粘合-readv/writev: linux/net/socket.c。

```
631 static size_t sock_readv(struct file *file, const struct iovec *vector,
632              unsigned long count, loff_t *ppos)
633 {
634     size_t tot_len = 0;
635     int i;
636     for (i = 0; i < count; i++)
637         tot_len += vector[i].iov_len;
638     return sock_readv/writev(VERIFY_WRITE, file->f_dentry->d_inode,
639                  file, tot_len);
640 }
641
642 static size_t sock_writev(struct file *file, const struct iovec *vector,
643              unsigned long count, loff_t *ppos)
644 {
645     size_t tot_len = 0;
646     int i;
647     for (i = 0; i < count; i++)
648         tot_len += vector[i].iov_len;
649     return sock_readv/writev(VERIFY_READ, file->f_dentry->d_inode,
650                  file, tot_len);
651 }
```

## TCP/IP 与 Linux 协议实现

当用户进程调用 `sendto()` socket API 时，它映射到此处。

图 5.76 Socket 粘合-sendto: linux/net/socket.c。

```
/*
 * 向给定地址发送数据报文。我们将地址移动到内核空间，
 * 在调用协议之前检查用户区域是否可读。
 */
asmlinkage long sendto(int fd, void *buf, size_t len, unsigned flags,
         struct sockaddr *addr, int addr_len)
{
	struct socket *sock;
	char address[MAX_SOCK_ADDR];
	int err;
	struct msghdr *msg;
	struct iovec iov;

	sock = sock_lookup(fd, &err);
	if (!sock) {
		goto out;
	}
	iov.iov_base = buf;
	iov.iov_len = len;
	msg.msg_name = NULL;
	msg.msg_iov = iov;
	msg.msg_iovlen = 1;
	msg.msg_control = NULL;
	msg.msg_controllen = 0;
	msg.namelen = addr_len;
```

此 `sendto()`（可能是数据报文）后续如下：

图 5.77 Socket 粘合-sendto ii: linux/net/socket.c。

```
if (addr)
{
	err = move_addr_to_kernel(addr, addr_len, address);
	if (err < 0)
		goto out_put;
	msg.msg_name = address;
}
if (sock->file->f_flags & O_NONBLOCK)
	flags |= MSG_DONTWAIT;
	msg.msg_flags = flags;
	err = sock_sendmsg(sock, msg, len);

out_put:
	sockfd_put(sock);
out:
```

## 协议实现框架

```
return err;
}
/*
 * 向 socket 发送数据报文。
 */
asmlinkage long sys_send(int fd, void *buf, size_t len, unsigned long)
{
    return sys_sendto(fd, buf, len, NULL);
}
```

当用户进程调用 `recvfrom()` 时，它映射到此代码。这意味着我们有一个想要接收包（通常是数据报文）的用户。

图 5.78 Socket 粘合--recvfrom: linux/net/socket.c。

```
/*
 * 从 socket 接收帧并可选地记录发送者的地址。
 * 我们验证缓冲区是否可写，如果需要，将发送者信息移动到用户空间。
 */
asmlinkage long recvfrom(int fd, void *buf, size_t len, unsigned flags,
         struct sockaddr *addr, int addr_len)
{
	struct socket *sock;
	struct iovec iov;
	struct msghdr *msg;
	int err;

	sock = sock_lookup(fd, &err);
	if (!sock) {
		goto out;
	}
	iov.iov_base = buf;
	iov.iov_len = len;
	msg.msg_name = NULL;
	msg.msg_iov = iov;
	msg.msg_iovlen = 1;
	msg.msg_control = NULL;
	msg.msg_controllen = 0;
	msg.namelen = addr_len;
```

