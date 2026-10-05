# Protocol Implementation Framework 159

Figure 5.74 Socket glue-readv/writev service routine: linux/net/socket.c.

```
605 int sock_readv/writev(int type, struct inode *inode, struct file *file,
606      const struct iovec *iov, long count, long size)
607 {
608     struct msghdr msghdr;
609     struct socket *sock;
610
611     sock = socki_lookup(inode);
612     struct msg_msg *msg_name = NULL;
613     msg_name->namelen = 0;
614     msg_msg->control = NULL;
615     msg_msg->controllen = 0;
616     msg_msg->iov = (struct iovec *) iov;
617     msg_msg->iovlen = count;
618     msg_msg->flags = (file->flags & O_NONBLOCK) ? MSG_DONTWAIT : 0;
619
620     /* does a VERIFY_WRITE */
621     if (type == VERIFY_WRITE)
622         return sock_recvmsg(sock, &msg_msg, size, msg_msg->flags);
623
624     if (type == SOCK_PACKET))
625         msg_msg->flags |= MSG_EHDR;
626
627     return sock_sendmsg(sock, &msg_msg, size);
628 }
```

The preceding function is a service function for the separate handlers here.

Figure 5.75 Socket glue-readv/writev: linux/net/socket.c.

```
631 static size_t sock_readv(struct file *file, const struct inode iovec *vector,
632              unsigned long count, loff_t *ppos)
633 {
634     size_t tot_len = 0;
635     int i;
636     for (i = 0; i < count; i++)
637         tot_len += vector[i].iov_len;
638     return sock_readv/writev(VERIFY_WRITE, file->f_dentry->d_inode,
639                  file, count, tot_len);
640 }
641
642 static size_t sock_writev(struct file *file, const struct inode iovec *vector,
643              unsigned long count, loff_t *ppos)
644 {
645     size_t tot_len = 0;
646     int i;
647     for (i = 0; i < count; i++)
648         tot_len += vector[i].iov_len;
649     return sock_readv/writev(VERIFY_READ, file->f_dentry->d_inode,
650                  file, count, tot_len);
651 }
```