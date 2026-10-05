# TCP/IP and Linux Protocol Implementation

We need then to map inodes to socket descriptors, and vice versa.

Figure 5.63 Socket glue–get a file descriptor for a sock fd: linux/net/socket.c.

```
static int sock_map_fd(struct *sock)
{
    int fd;
    struct qatr this;
    char name[32];
    /*
     Find a file descriptor suitable for return to the user.
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
out}
```

The next part fills the file function points and other administrative parts of the structure.

Figure 5.64 Socket glue–get a file descriptor for a sock fd: linux/net/socket.c.

```
file->f_dentry->d_op = &sock_dentry_operations;
d_add(file->dentry, sock->inode);
file->f_vfsmnt = mget(sock_mnt);

sock->file = file;
file->f_op = sock->inode->i_fop = sock_file_ops;
file->f_mode = 3;
file->f_flags = 0_RDWR;
```