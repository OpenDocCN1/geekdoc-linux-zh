
```c
/*
 * 对 socket 文件描述符进行控制。
 * 因为 fcntl 函数目前会睡眠。
 */
int sock_fcntl(struct file *filp, unsigned int cmd, long arg)
{
    struct socket *sock;

    sock = sock_lookup(filp->f_inode);
    if (sock && sock->ops)
        return sock_no_fcntl(sock, cmd, arg);
    return(-EINVAL);
}
```

# sys_call 的参数列表

```c
#define Al(x) ((x) sizeof(unsigned long))
static unsigned char nargs[6]={Al(0),Al(0),Al(3),Al(3),Al(3),Al(3),Al(4),Al(4),Al(4),Al(6),Al(2),Al(3)};
undef Al
```

**图 5.110** Socket glue—system call: linux/net/socket.c。

```c
/*
 * 系统调用清理。
 * 该函数不需要设置内核锁，
 * 由调用者设置。
 */
```

# TCP/IP 和 Linux 协议实现

```c
asmlinkage long sys_socket(int call, unsigned long *args)
{
1521 unsigned long a[6];
1522 unsigned long a0,ai;
1523 int err;
1524 if (copy_from_user(a, args, sizeof(a)))
1526 return -EFAULT;
1527 /* copy_from_user 应该是安全的。 */
1529 a0=a[0];

switch(call)
1532 {
1533 case SYS_SOCKET:
1534 err = sys_socket(a0,ai,a[2]);
1535 break;
1536 case SYS_BIND:
1537 err = sys_bind(a0,(struct sockaddr *)a1,a[2]);
1538 break;
1539 case SYS_CONNECT:
1540 err = sys_connect(a0,(struct sockaddr *)a1,a[2]);
1541 break;
1542 case SYS_LISTEN:
1543 err = sys_listen(a0,ai);
1544 break;
1545 case SYS_ACCEPT:
1546 err = sys_accept(a0,(struct sockaddr *)a1,a[2]);
1547 break;
1548 case SYS_GETOCKSNAME:
1549 err = sys_getockname(a0,(struct sockaddr *)a1,(int *)a[2]);
1550 break;
1551 case SYS_GETPEERNAME:
1552 err = sys_getpeername(a0,(struct sockaddr *)a1,(int *)a[2]);
1553 break;
1554 case SYS_SOCKETPAIR:
1555 err = sys_socketpair(a0,ai,a[2],int *)a[3]);
1556 break;
1557 case SYS_SEND:
1558 err = sys_send(a0,void *)a[1],a[2],a[3]);
1559 break;
1560 case SYS_SENDTO:
1561 err = sys_sendto(a0,void *)a[1],a[2],a[3], (struct sockaddr *)a[4],a[5]);
1562 break;
1563 case SYS_RECV:
1564 err = sys_recv(a0,void *)a[1],a[3]);
1565 break;
1566 case SYS_RECVFROM:
1567 err = sys_recvfrom(a0, (void *)a1, a[2], a[3], (struct sockaddr *)a[4], (int *)a[5]);
1568 break;
```

**图 5.111** Socket glue-system call vector: linux/net/socket.c。

```c
case SYS_SHUTDOWN:
    err = sys_shutdown(a0,a1);
    break;
case SYS_SETSOCKOPT:
    err = sys_setsockopt(a0, a1, a[2], (char *)a[3], a[4]);
    break;
case SYS_GETSOCKOPT:
    err = sys_getsockopt(a0, a1, a[2], (char *)a[3], (int *)a[4]);
    break;
case SYS_SENDMSG:
    err = sys_sendmsg(a0, (struct msghdr *)a1, a[2]);
    break;
case SYS_RECVMSG:
    err = sys_recvmsg(a0, (struct msghdr *)a1, a[2]);
    break;
default:
    err = -EINVAL;
    break;
```

**图 5.112** Socket glue–system call vector: linux/net/socket.c。

# 协议实现框架

# 将协议与 Socket 层关联

我们可以在运行时动态安装协议地址族。

**图 5.113** Socket glue–registering a protocol family with the socket module: linux/net/socket.c。

```c
/*
 * 此函数由协议处理程序调用，该程序想要
 * 移除其地址族，并从 SOCKET 模块中解除链接。
 */
int sock_unregister(int family)
{
    if (family < 0 || family >= NPROTO)
        return -1;

    net_family_lock();
    net_families[family]=NULL;
    net_family_unlock();
    return 0;
}
```

**图 5.115** Socket glue—initializing the socket VFS module: linux/net/socket.c。

```c
void __init_sock_init(void)
{
    int i;

    printk(KERN_INFO "Linux NET4.0 for Linux 2.4\n");
    printk(KERN_INFO "Based upon Swansea University Computer Society NET3.039\n");

    /*
     * 初始化所有地址（协议）族。
     */
    for (i = 0; i < NPROTO; i++)
        net_families[i] = NULL;
}
```

```c
/*
 * 初始化 sock SLAB 缓存。
 */
skk_init();

#ifdef SLAB_SKB
/*
 * 初始化 skbuff SLAB 缓存
 */
ksb_init();
#endif

/*
 * Wan 路由器层。 */
#ifdef CONFIG_WAN_ROUTER
wanrouter_init();
#endif
```

然后，socket VFS 模块本身也可以根据需要运行时进行安装或移除。

# 图 5.116 Socket 粘胶——初始化 socket VFS 模块：linux/net/socket.c。

```c
/*
 * 初始化协议模块。
 */
register_filesystem(&sock_fs_type);
sock_mt = kernel_mount(&sock_fs_type);
/* 真正的协议初始化是在
 * do_initcall 运行时执行的。
 */
/*
 * netlink 设备处理器可能尽早需要。
 */
#ifdef CONFIG_RTNETLINK
rtnetlink_init();
#endif
#ifdef CONFIG_NETLINK_DEV
init_netlink();
#endif
#ifdef CONFIG_NETFILTER
netfilter_init();
#endif
```

## 184 TCP/IP 和 Linux 协议实现
