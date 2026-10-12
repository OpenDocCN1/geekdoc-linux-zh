
    struct `file_ra_state`  `f_ra`;              /* 预读状态 */

    unsigned long         `f_version`;         /* 版本号 */

    void                  *`f_security`;      /* 安全模块 */

    void                  *`private_data`;     /* tty 驱动钩子 */

    struct `list_head`      `f_ep_links`;        /* eventpoll 链接列表 */

    spinlock_t            `f_lock`;            /* eventpoll 锁 */

    struct `address_space`  *`f_mapping`;         /* 页缓存映射 */

};

## 文件操作

与其他的 VFS 对象一样，文件操作表也非常重要。与 `struct file` 关联的操作是我们熟悉的系统调用，它们构成了标准 Unix 系统调的基础。

文件对象方法在 `file_operations` 中指定，并在 `<linux/fs.h>` 中定义：

```c
struct file_operations {
  struct module *owner;
  loff_t (*llseek) (struct file *, char *, loff_t, int);
  ssize_t (*read) (struct file *, char *, size_t, loff_t);
  ssize_t (*aio_read) (struct kiocb *, const char *, size_t, loff_t);
  ssize_t (*write) (struct file *, const char *, size_t, loff_t);
  ssize_t (*aio_write) (struct kiocb *, const char *, size_t, loff_t);
  int (*readdir) (struct file *, void *, filldir_t *);
  unsigned int (*poll) (struct file *, struct poll_table_struct);
  int (*ioctl) (struct inode *, struct file *, unsigned int, unsigned long);
  int (*mmap) (struct file *, struct vm_area_struct *);
  int (*open) (struct inode *, struct file *);
  int (*flush) (struct file *);
  int (*release) (struct file *, struct dentry *);
  int (*fsync) (struct file *, int);
  int (*aio_fsync) (struct kiocb *, int);
  int (*lock) (struct file *, struct file_lock_struct *);
  ssize_t (*readv) (struct file *, const iovec *, unsigned long, loff_t *);
  ssize_t (*writev) (struct file *, const iovec *, unsigned long, loff_t *);
  ssize_t (*sendfile) (struct file *, loff_t *, size_t, read_actor_t, void *);
  ssize_t (*sendpage) (struct file *, struct page *, int, size_t, int);
  unsigned long (*get_unmapped_area) (struct file *, unsigned long, unsigned long, unsigned long);
  int (*check_flags) (int flags);
  int (*dir_notify) (struct file *, struct filp, unsigned long arg);
  int (*lock) (struct file *, struct filp, int cmd, struct file_lock *fl);
};
```
