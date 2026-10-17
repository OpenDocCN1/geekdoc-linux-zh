
```c
int optname, char __user *optval, int *optlen);

int (*getsockopt)(struct socket *sock, int level,
 int optname, char __user *optval, int *optlen);

int (*compat_setsockopt)(struct socket *sock, int level,
 int optname, char __user *optval, int *optlen);
```

结构设计用于与系统调用进行通信。换句话说，它们形成了用户端和内核端套接字之间的链接。

## 12.10.2 套接字与文件

一旦建立连接，用户空间就可以普通的文件操作访问套接字。这在内核中是如何实现的？由于 VFS 层的开放结构（在第 8 章讨论），只需要极少数的操作。

虚拟文件系统的 VFS inode 在第 8 章中进行了讨论。每个套接字都被分配此类型的 inode，该 inode 反而又与普通文件相关的其他结构链接在一起。操作文件的函数存储在一个单独的指针表中：

```c
<fs.h>
struct inode {
    struct file_operations *i_fop; /* 称为 -i_op->default_file_ops */
}
```

因此，对套接字描述符的文件访问可以透明地重定向到网络层的代码。套接字使用以下文件操作：

```c
net/socket.c
struct file_operations socket_file_ops = {
    .owner = THIS_MODULE,
    .llseek = no_llseek,
    .aio_read = sock_aio_read,
    .aio_write = sock_aio_write,
    .poll = sock_poll,
    .locked_ioctl = sock_ioctl,
    .compat_ioctl = compat_ioctl,
    .mmap = sock_mmap,
    .open = sock_no_open, /* 用于禁用通过 /proc 打开的特殊代码 */
    .release = sock_close,
    .fsync = sock_fsync,
    .sendpage = sock_sendpage,
    .splice_write = generic_splice_sendpage,
};
```

`sock_functions` 是简单的封装例程，它们调用 `sock_operations` 例程，如下所示的 `sock_mmap` 示例所示：

```c
net/socket.c
```
