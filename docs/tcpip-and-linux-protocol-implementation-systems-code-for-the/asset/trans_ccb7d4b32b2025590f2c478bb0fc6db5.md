

# TCP/IP 与 Linux 协议实现

我们需要将 inode 映射到套接描述符（socket descriptors），反之亦然。

图 5.63 Socket 粘层——为 sock fd 获取文件描述符：linux/net/socket.c。

```c
static int sock_map_fd(struct sock *sock)
{
    int fd;
    struct qatr this;
    char name[32];
    /*
     找到一个适用于返回给用户的文件描述符。
     */
    fd = get_unused_fd();
    if (fd > 0) {
        struct file *file = get_empty_filp();
        if (!file) {
            put_unused_fd(fd);
            fd = -ENFILE;
            goto out;
        }
        sprintf(name, "[%Xu]", sock->inode->i_ino);
        this.name = name;
        this.len = strlen(name);
        this.hash = strlen(sock->inode->i_ino);
        file->f_entry = d_alloc(sock_mnt->mnt_sb->s_root, &this);
        if (!file->f_entry) {
            put_filp(file);
            put_unused_fd(fd);
            fd = -ENOMEM;
            goto out;
        }
    }
out:
    return fd;
}
```

下部分填充文件函数点以及该结构体的其他管理部分。

图 5.64 Socket 粘层——为 sock fd 获取文件描述符：linux/net/socket.c。

```c
file->f_dentry->d_op = &sock_dentry_operations;
d_add(file->dentry, sock->inode);
file->f_vfsmnt = mget(sock_mnt);

sock->file = file;
file->f_op = sock->inode->i_fop = sock_file_ops;
file->f_mode = 3;
file->f_flags = O_RDWR;
```

```c
369   file->_pos = 0;
370   fd_install(fd, file);
371  }
372 
373  out:
374   return fd;
375 }
```

我们也需要反向的映射。

# 图 5.65 Socket 粘层——通过文件描述符查找 sock fd：linux/net/socket.c。

```c
377  extern __inline_ struct socket *sock_lookup(struct inode *inode)
378  {
379    return inode->u.socket_i;
380  }
```

# 图 5.66 Socket 粘层——通过文件描述符查找 sock fd：linux/net/socket.c。

```c
382 /**
383  *   sock_lookup - 从文件号到其套接字槽位
384  *   fd: 文件句柄
385  *   err: 指向返回错误码的指针
386  *
387  *   传入文件句柄，并返回其绑定的套接字。
388  *   如果发生错误，err 指针将被覆盖为负的 errno 码并返回 NULL。
389  *   该函数会检查无效句柄以及传入非套接字的句柄。
390  *
391  *
392  *   成功时，返回套接字对象指针。
393  */
394 
395  struct socket *sockfd_lookup(int fd, int *err)
396  {
397    struct file *file;
398    struct inode *inode;
399    struct socket *sock;
400 
401    if (!(file = fget(fd)))
402    {
403      *err = -EBADF;
404      return NULL;
405    }
406 
407    inode = file->f_dentry->d_inode;
408    if (!inode->i_sock || !(sock_lookup(inode)))
419    {
410      *err = -ENOTSOCK;
411    fput(file);
```

```c
412      return NULL;
413  }
414 
415  if (sock->file != file) {
416      printk(KERN_ERR, "socki_lookup: socket file changed!\n");
417      sock->file = file;
418  }
419  return sock;
420  }
```

我们需要允许在 inode 和套接字描述符空间之间自由通过。这里是我们分配并关联相关数字。

**图 5.67** 粘层——分配套接字 inode：linux/net/socket.c。

```c
422  extern __inline__ void sockfd_put(struct socket *sock)
423  {
424      fput(sock->file);
425  }
426 
427  /**
428   * sock_alloc      分配一个套接字
429   *
430   配分配一个新的 inode 和套接字对象。两者被绑定
431   *   并初始化。然后返回该套接字。如果 inode 耗尽，
432   *   则返回 NULL。
433   */
434 
435  struct socket *sock_alloc(void)
436  {
437      struct inode *inode;
438      struct socket *sock;
439 
440      inode = get_empty_inode();
441      if (!inode)
442          return NULL;
443 
444      inode->i_ab = sock_mnt->mnt_sb;
445      sock = socki_lookup(inode);
446 
447      inode->i_mode = S_IFSOCK|S_IRWXUGO;
448      inode->i_sock = sock;
449      inode->i_uid = current->uid;
450      inode->i_gid = current->sgid;
451 
452      sock->inode = inode;
453      init_waitqueue_head(&sock);
454      sock->file = NULL;
455      sock->state = SOCK_CONNECTED;
456      return sock;
457  }
```

