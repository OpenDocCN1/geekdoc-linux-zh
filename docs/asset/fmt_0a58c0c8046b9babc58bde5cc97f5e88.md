
为了查看 `rtnetlink` 是如何使用的，让我们来看一个例子。如果运行在应用层的实用程序想向路由表添加路由，它会调用 `recvmsg` 并传递一个 `nmsghdr` 指针，同时将 `nmsg_type` 字段设置为 `RTM_NEWROUTE`。socket 层会将消息汇接到 `sk_buff` 结构中并发送到 netlink 协议，协议随后将其放入 `PF_NETLINK` socket 的接收队列。

# rtnetlink Socket 注册

`linux/net/core/rtnetlink.c` 文件中的 `rtnetlink_recv` 函数在消息从 socket 取出时获取消息。netlink 使用了一个特殊的 "lite" socket。netlink 成员协议如 `rtnetlink` 向 netlink 族注册，并通过这个特殊 socket 与用户交换消息。这种机制与普通 socket 的注册机制相似。然而，`rtnetlink` 通过调用 `netlink_kernel_create` 向 `AF_NETLINK` 族注册其接收函数。在 `linux/net/core/rtnetlink.c` 的初始化函数代码片段中，我们可以看到 `rtnetlink` 初始化函数是如何向 netlink "lite" socket 注册的。

```c
rtnl1 = rtnetlink_kernel_create(NETLINK_ROUTE, RTNLGRP_MAX,
rtnetlink_recv, THIS_MODULE);
```

### netlink_recv 函数

netlink 是完全异步的，因此 `netlink_recv` 函数会移除 netlink socket 中所有的入站消息。它调用 `rtnetlink_recv_msg` 执行实际工作。

```c
static void rtnetlink_recv(struct sock *sk, int len)
{
    unsigned int qlen = 0;
    do {
        rtnl_lock();
        rtnetlink_run_queue(sk, &qlen, &rtnetlink_recv_msg);
        up(&rtnl_sem);
        netdev_run_todo();
    } while (qlen);
}
```
