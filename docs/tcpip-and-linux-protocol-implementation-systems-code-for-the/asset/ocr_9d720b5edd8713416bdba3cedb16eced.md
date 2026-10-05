# 150 TCP/IP and Linux Protocol Implementation

Read a block from a file:

**Figure 5.58** Socket glue-socket static super_block *socksfs_read_super(struct super_block *sb, void *data, int silent)

The following operations really very little sense at all on sockets (of any address family).

**Figure 5.59** Socket glue-socket fs vmount, delete_entry: linux/net/socket.c.

```
301 static struct vmount
302 static DECLARE_FYPE(sock_fs_type, "sockfs", socksfs_read_super,
303     FS_NOMOUNT|FS_SINGLE);
304 static int socksfs_delete_dentry(struct dentry *dentry)
305 {
306     return 1;
307 }
308 static struct dentry_operations socksfs_dentry_operations = {
309     d_delete: socksfs_delete_dentry,
310 };
```

Seeking is another thing that we do on storage device type filesystems, but which doesn't make a whole lot of sense on a socket.