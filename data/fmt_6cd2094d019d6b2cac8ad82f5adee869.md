
每当注册一个新的 PPP 网络设备时，Linux 内核会调用此函数。它初始化 `net_device` 结构；特别设置了下面描述的函数指针。

## 8.3 Linux 内核中的 PPP 实现

```
ppp_start()
drivers/net/ppp_generic
```

此函数由 IP 层 `net_device` 结构中的函数指针 `hard_start_xmit()` 调用，用于通过 PPP 设备输出 IP 数据包。首先添加所需的第一个 PPP 头部，然后通过 `skb_queue_tail()` 将完整的数据包添加到发送队列（类似于函数指针 `ppp_write()`），最后由 `ppp_xmit_process()` 将数据包输出到底层网络设备。

```
ppp_xmit_process()
drivers/net/ppp_generic
```

此函数负责将所有在发送队列 `ppp->file` 中等待的包包输出到底层设备。辅助函数 `ppp_send_frame()`（可以可选地压缩 PPP 数据包）被用于实际输出。

```
ppp_input()
drivers/net/ppp_generic
```

每当接收到 PPP 数据包时，底层 TTY 规范（异步或同步）的驱动程序调用此函数。在对数据包进行去分处理后，如有必要，将调用函数 `ppp_do_recv()` 进行进一步处理；然后此函数将数据包转发到 `ppp_receive_frame()`。

```
ppp_receive_frame()
drivers/net/ppp_generic
```

此函数检查 multilink PPP 是否激活，并将入站的 PPP 数据包转发到函数 `ppp_receive_frame()`（带 multilink）或 `ppp_receive_nonmp_frame()`（无 multilink）。

```
ppp_receive_nonmp_frame()
drivers/net/ppp_generic
```

当 PPP 数据包到达时，此函数首先取消压缩，然后检查它是数据包还是子协议的控制包（第 8.1.1 节）。如果是控制包，`skb_queue_tail()` 将数据包添加到接收队列中供 PPP 守护进程通过设备 `/dev/ppp` 读取。如果是数据包，则载荷位于 `sk_buffer` 中，通过调用 `netif_rx()` 传递给网络层。

### 8.3.2 异步 PPP 的函数和数据结构

异步 PPP 模块本质上通过名称 `N_PPP` 提供了一种新的 TTY 规范（第 7.2 节），代表了通用 PPP 驱动与底层 TTY 规范之间的中间层。

图 8-5 提供了重要数据结构的概述。驱动程序的状态维护在 `asyncio` 结构中。作为 SLIP 实现（第 7.2.3 节），它指向底层 TTY 设备的 `tty_struct`，其中包含 PPP TTY 规范的 `tty_id` 结构。

`ppp_channel` 结构（此处定义）用于访问通用 PPP 驱动的 `ppp` 结构以及 `ppp_channel_ops` 类型结构，后者包含了指向其他函数的指针。

![](img/5a25b942ec332b879f2b5de64f6177_0.png) 图 8-5 异步 PPP 驱动的重要数据结构。下文描述了 `ppp_async_send()`。相反，通用 PPP 驱动的 `ppp` 结构可以用于通过跳转访问相关的 `ppp_channel` 结构（以及 `ppp_channel_ops` 中的函数指针，此处将不描述以保持简单）。这对于在异步 PPP 的情况下将数据包传递给 `ppp_async_send()` 函数非常重要。

```
ppp_async_init()
drivers/net/ppp_async.c
```

每当 `ppp_async.o` 模块加载时，都会调用此函数。它使用 `tty_register_ldisc()` 向 Linux 内核注册 PPP TTY 规范。

```
ppp_async_cleanup()
drivers/net/ppp_async.c
```

每当 `ppp_async.o` 模块移除时，都会调用此函数。它调用 `tty_unregister_ldisc(N_PPP, NULL)` 注销 PPP TTY 规范。

```
ppp_async_send()
drivers/net/ppp_async.c
```

当 PPP 数据包准备好发送时，此函数由通用 PPP 驱动通过 `ppp_channel_ops` 结构（见图 8-5）中的函数指针 `start_xmit()` 调用。它将数据包转发到函数 `ppp_async_push()`。

```
ppp_async_push()
drivers/net/ppp_async.c
```

此函数由 `ppp_async_send()` 调用以传输 PPP 数据包。该函数使用辅助函数 `ppp_async_encode()` 准备异步传输的数据包，并通过反复调用 `tty->driver.write()` 将其发送到底层 TTY 设备的驱动。

```
ppp_async_encode()
drivers/net/ppp_async.c
```

此函数使用第 7.1.1 节描述的字符填充技术在异步设备上传输 PPP 数据包。

```
ppp_async_input()
drivers/net/ppp_async.c
```

每当底层 TTY 设备提供新数据时，`ppp_asynctty_receive()` 会调用此函数。本质上，通过 SLIP 函数（见 7.1.1 节），它会取消字符填充并检测 PPP 数据包的开始和结束。一旦数据包被完整读取，它就会被转发到函数 `process_input_packet()`。

```
process_input_packet()
drivers/net/ppp_async.c
```

每当 PPP 数据包被完整读取时，`ppp_async_input()` 会调用此函数。检查第一个数据包校验和（帧-FCS）。在经过若干额外检查后，最终调用 `ppp_input()`，将数据包转发到通用 PPP 驱动。

```
ppp_asynctty_open(), ppp_asynctty_close()
drivers/net/ppp_async.c
```

每当用户程序将 TTY 设备切换到 PPP 行规范或将其重置为另一个行规范时，`tty_ldisc` 结构的函数 `open()` 和 `close()` 会调用这些函数。本质上，在 `ppp_asynctty_open()` 中为 TTY 行规范的状态数据创建了一个 `asyncio` 结构，然后进行初始化，最后在 `ppp_asynctty_close()` 中释放。

```
ppp_asynctty_read(), ppp_asynctty_write()
drivers/net/ppp_async.c
```

# 第 8 章 点对点协议 (PPP)

### 8.3.3 初始化

当 PPP 模块 `ppp_generic_o` 加载时，`ppp_init` 首先注册一个主设备号为 108 的字符设备，这通常会将 `/dev/ppp` 嵌入到系统中。接下来，该模块使用 `ppp_async_init()` 为异步 PPP 驱动（`ppp_async.`）注册一个名为 'ppp' 的新 TTY 线路规范（见第 7.2.1 节）。该 TTY 线路规范是设备与底层设备以及 `ppp_async_c` 模块之间的中间层，便于对所有入站数据包进行访问。一旦 `/dev/tty` 设备和 PPP TTY 行规范注册完成，第一阶段初始化即告完成。

第二阶段通过调用 `ppp` 启动。在简短测试其版本号是否匹配内核驱动版本后，它打开设备 `/dev/ppp`。然后它会打开一个文件描述符，这是与通用 PPP 驱动通信所必需：但最初，PPP 设备的引用指针 `USAGE_COUNT` 会递增。

接着，用户需要建立物理连接（例如，`chat` 程序可以拨打拨号服务器的号码）。如果此操作成功，则 PPP 使用系统的 `ioctl(tty_fd, TIOCSREED, N_PPP)` 将 TTY 线路规范更改为 `N_PPP`。然后它使用 `ioctl(ppp_fd, PPPOCNEWUNIT)` 请求通用 PPP 驱动创建一个网络设备，然后使用 `ioctl(fd, PPPOCGCATATCH)` 将新网络设备绑定到底层 TTY 设备。

这些步骤完成了实际 PPP 连接的建立：现在 PPP 协议（如 LCP）可以开始验证用户身份并配置高层（见第 8.4 节）。

### 8.3.4 发送 IP 数据包

通用 PPP 驱动通过两条路由接收待传输的数据包：网络层通过匹配的网络设备 (`pppX`) 发送负载包，而 PPP 守护进程通过字符设备 `/dev/ppp` 控制数据包。
