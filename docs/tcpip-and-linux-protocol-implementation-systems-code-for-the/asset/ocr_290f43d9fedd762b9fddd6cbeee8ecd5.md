# Protocol Implementation Framework 157

```
507 if (err >= 0) {
508     err = sock->ops->sendmsg(sock, msg, size, &scm);
509     scm_destroy(&scm);
510 }
511 return err;
512 }
513 
514 int sock_recvmsg(struct socket *sock, struct msghdr *msg, int size, int flags)\)
515 {
516     struct scm_cookie scm;
517 
518     memset(&scm, 0, sizeof(scm));
519 
520     size = sock->ops->recvmsg(sock, msg, size, flags, &scm);
521     if (size >= 0) {
522         scm_recv(sock, msg, &scm, flags);
523 }
524     return size;
525 }
```

We also need to support the read() call.

Figure 5.72 Socket glue-read: linux/net/socket.c.

```
537 /*
538  * Read data from a socket. ubuf is a user node pointer. We make sure the we
539  * area abuf...ubuf*size-i is writable before asking the protocol.
540  */
541 
542 static size_t sock_read(struct file *file, char *ubuf,
543                             size_t size, loff_t *ppos)
544 {
545     struct socket *sock;
546     struct iovec iov;
547     struct msghdr *msg;
548     int flags;
549 
550     if (ppos == &file->f_pos)
551         return -EPIPE;
552     if (size==0) {
553         /* Match behaviour of SYSS * */
554         return 0;
555     }
556     sock = sock_lookup(file->f_dentry)->d_inode;
557 
558     msg.msg_name=NULL;
559     msg.msg_namelen=0;
560     msg.msg_iov=iov;
561     msg.msg_iovlen=1;
562     msg.msg_control=NULL;
563     msg.msg_ctrlrollen=0;
564     iov.iov_base=ubuf;
```