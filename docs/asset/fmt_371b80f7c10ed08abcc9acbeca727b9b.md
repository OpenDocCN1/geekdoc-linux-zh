
## 17.4 文件操作

下一组请求以 `FIO` 开头，除了 socket 外，还可能适用于某些类型的文件。我们仅涵盖了适用于 socket 的请求（TCPv2 第 553 页）。这五个请求都要求 `ioctl` 的第三个参数指向一个整数：

- `FIONBIO`: socket 的非阻塞标记被清除或开启，取决于 `ioctl` 的第三个参数指向零值还是非零值。此请求的效果与 `O_NONBLOCK` 文件状态标记相同，可以通过向 `fcntl` 函数发送 `F_SETCTL` 命令来设置和清除该标记。
- `FIOASYNC`: 控制 socket 接收异步 I/O 信号 `SIGIO` 的标记被清除或开启，取决于 `ioctl` 的第三个参数指向零值还是非零值。该标记与 `O_ASYNC` 文件状态标记相同，可以通过向 `fcntl` 函数发送 `F_SETCTL` 命令来设置和清除该标记。
- `FIONREAD`: 通过 `ioctl` 的第三个参数指向的整数返回 socket 接收缓冲区中当前包含的字节数。此功能也适用于文件、管道和终端。我们在第 14.7 节中详细讨论过此请求。
- `FISETOWN`: 等同于 socket 的 `SIOCGRP`。
- `FIOGETOWN`: 等同于 socket 的 `SIOCPGRP`。

## 17.5 接口配置

许多处理系统网络接口的程序采用的早期步骤之一是从内核获取系统上配置的所有接口。这是通过 `ifconf` 请求完成的，它使用了 `ifconf` 结构，而该结构又使用了 `ifreq` 结构，两者如图 17.2 所示。

在调用 `ioctl` 之前，我们分配一个缓冲区和一个 `ifconf` 结构并初始化后者。我们在图 17.3（第 470 页）中展示了这一点，假设我们的缓冲区大小为 1024 字节。`ioctl` 的第三个参数指向我们的 `ifconf` 结构。

如果我们假设内核返回了两个 `ifreq` 请求，当 `ioctl` 返回时，我们可以得到如图 17.4（第 470 页）所示的布局。阴影区域已被 `ioctl` 修改。缓冲区已填充了这些结构，`ifconf` 结构中的 `if_len` 成员已更新，以反映存储的信息量。

一个 `ifreq` 结构指针也用于图 17.1 所示的 `ioctl` 参数，我们在第 17.7 节中描述它。注意 `ifconf` 许多 `ifreq` 结构包含一个联合体，取决于具体实现。

```
struct ifconf {
    int if_len;
    union {
        u_char if_buf[];
        struct ifreq *if_req;
    };
    /* 缓冲区 */
    /* 接口 */
};
```

将在第 24 章更详细地描述带外数据。POSIX 用 `socketmark` 函数替换了此请求，我们将在第 24.3 节中展示使用 `ioctl` 实现该函数的实现。

通过第三个参数所指向的整数返回设置用于该 socket 接收 `SIGIO` 或 `SIGUR` 信号的进程 ID 或进程组 ID。此请求与 `fcntl` 的 `F_GETOWN` 相同，我们在图 7.20 中提到 POSIX 标准化了 `fcntl`。

通过第三个参数所指向的整数设置用于该 socket 接收 `SIGIO` 或 `SIGUR` 信号的进程 ID 或进程组 ID。此请求与 `fcntl` 的 `F_SETOWN` 相同，我们在图 7.20 中提到 POSIX 标准化了 `fcntl`。

> 图 17.1 网络 ioctl 请求摘要。

| SIOCGETWIN | 获取文件的进程 ID 或进程组 ID | int |
| Interface | SIOCGIFCONF | 获取所有接口的列表 | struct ifreq |
| SIOCIFADDR | 设置接口地址 | struct ifreq |
| SIOCGIFADDR | 获取接口地址 | struct ifreq |
| SIOCSIFFLAGS | 设置接口标志 | struct ifreq |
| SIOCGIFLAGS | 获取接口标志 | struct ifreq |
| SIOCIFSTADDR | 设置点对点地址 | struct ifreq |
| SIOCGIFSTADDR | 获取点对点地址 | struct ifreq |
| SIOCSIBCADDR | 设置广播地址 | struct ifreq |
| SIOCGFBDADDR | 获取广播地址 | struct ifreq |
| SIOCIFNETMASK | 设置子网掩码 | struct ifreq |
| SIOCGETNETMASK | 获取子网掩码 | struct ifreq |
| SIOCIFTMETRIC | 设置接口权重 | struct ifreq |
| SIOCGIFMETRIC | 获取接口权重 | struct ifreq |
| SIOCGIFMTU | 获取 MTU（多个；取决于具体实现） | struct ifreq |
| SIOCXXX | | | |
| ARP | SIOCARP | 创建/修改 ARP 条目 | struct arpreq |
| SIOCARP | 获取 ARP 条目 | struct arpreq |
| SIOCDARP | 删除 ARP 条目 | struct arpreq |
| Routing | SIOCADDRT | 添加路由 | struct rtentry |
| SIOCDELRT | 删除路由 | struct rtentry |
| STREAMS | I_xxx | (见第 31.5 节) | |
