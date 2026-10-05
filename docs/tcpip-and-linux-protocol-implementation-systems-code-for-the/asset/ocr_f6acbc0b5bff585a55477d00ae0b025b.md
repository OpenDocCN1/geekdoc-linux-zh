# Protocol Implementation Framework 153

```
369   file->_pos = 0;
370   fd_install(fd, file);
371  }
372 
373  out:
374   return fd;
375 }
```

We need to map the other way, too.

# Figure 5.65 Socket glue-look up a file descriptor to a sock fd: linux/net/socket.c.

```
377  extern __inline_ struct socket *sock_lookup(struct inode *inode)
378  {
379    return inode->u.socket_i;
380  }
```

# Figure 5.66 Socket glue-look up a file descriptor to a sock fd: linux/net/socket.c.

```
382 /**
383  *   sock_lookup - Go from a file number to its socket slot
384  *   fd: file handle
385  *   err: pointer to an error code return
386  *
387  *   The file handle is passed in the locked and the socket it is bound
388  *   to returned. If an error occurs the err pointer is overwritten
389  *   with a negative errno code and NULL is returned. The function checks
390  *   for both invalid handles and passing a handle which is not a socket.
391  *
392  *   On a success the socket object pointer is returned.
393  */
394 
395  struct socket *sockfd_lookup(int fd, int *err)
396  {
397    struct file *file;
398    struct inode *inode;
399    struct socket *sock;
400 
401    if ((file = fget(fd))
402    {
403      *err = -EBADF;
404      return NULL;
405    }
406 
407    inode = file->f_dentry->d_inode;
408    if (!inode->i_sock || !(sock_lookup(inode)))
409    {
410      *err = -ENOTSOCK
411    fput(file);
```