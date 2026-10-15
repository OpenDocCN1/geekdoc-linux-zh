
图 6.26 使用 `poll()` 的 TCP 服务器后半部分。

### 调用 poll，检查新连接

我们调用 `poll` 来等待新连接或现有连接上的数据。当接受一个新连接时，我们通过寻找第一个描述符为负数的项找到 `client` 数组中的第一个可用条目。注意我们从索引 1 开始搜索，因为 `client[]` 用于监听套接字。找到可用条目后，我们保存描述符并设置 `POLLRDNORM` 事件。

### 检查现有连接上的数据

我们检查的两个返回事件是 `POLLRDNORM` 和 `POLLERR`。我们没有在 `events` 成员中设置后者，因为当条件为真时它总是返回。我们检查 `POLLERR` 的原因是某些实现会返回 `POLLRDNORM`。无论哪种情况，我们调用 `read`，如果发生错误，它将返回错误。当现有连接被客户端终止时，我们将 `fd` 成员设置为 -1。

## 6.12 总结

Unix 提供了五种不同的 I/O 模型：

- 阻塞（Blocking）
- 非阻塞（Nonblocking）
- I/O 多路复用（I/O multiplexing）
- 信号 I/O（Signal-driven I/O）
- 异步 I/O（Asynchronous I/O）

默认是阻塞 I/O，这也是最常用的。我们将在稍后的章节中介绍非阻塞 I/O 和信号驱动 I/O，在本章中已经涵盖了 I/O 多路复用。真正的异步 I/O 由 POSIX 规范定义，但很少有实现。

最常用的 I/O 多路复用函数是 `select`。我们告诉 `select` 函数我们感兴趣的内容（读取、写入和异常）、等待的最长时间，以及服务器支持的最大描述符数量。大多数对 `select` 的调用都指定了可读性，我们注意到在处理套接字时，唯一的情况是带外数据的到达（第 24 节）。由于 `select` 为函数运行时间提供了时间限制，我们将在图 43 中使用这一特性为输入操作设置时间限制。

我们使用 `select` 以批模式运行我们的回显客户端，并发现尽管遇到了用户输入的结束符，数据仍可能留在管道中或尚未发送到服务器中。为了处理这种情况，我们使用了 `shutdown` 函数，它允许我们利用 TCP 的半关闭特性。

将缓冲（以及我们的 `readline` 缓冲）与 `select` 混合的危险导致我们生成了按行缓冲区操作的回显客户端和服务器版本。

POSIX 定义了 `pselect` 函数，它将精度从微秒提高到纳秒，并接受一个指向信号集指针的新参数。这允许我们能够在捕获信号时避免竞态条件，我们将在 20.5 节中详细讨论这一点。

## 练习

System V 的 `poll` 函数提供了与 `select` 类似的功能，并提供了关于 STREAMS 设备的额外信息。POSIX 要求 `select` 和 `poll`，但后者常用。

- 6.1 我们说描述符集可以用 C 语言中的等号赋值另一个描述符集。描述符如何设置整数数组？（提示：查看你系统的 `<sys/select.h>` 或 `<sys/types.h>` 头文件）。
- 6.2 在第 6.3 节描述 *select* 返回“可写”的条件时，为什么我们需要套接字必须是非阻塞的，写入操作才能返回正值的限定条件？
- 6.3 在图 6.9 中，如果在第 19 行的“if” 之前加上“else”会发生什么？
- 6.4 POSIX 定义了 `pselect` 函数，它将精度从微秒提高到纳秒，并接受一个指向信号集指针的新参数。这允许我们能够在捕获信号时避免竞态条件，我们将在 20.5 节中详细讨论。
- 6.5 如果我们发现尽管遇到了用户输入的结束符，数据仍可能留在管道中或尚未发送到服务器，会发生什么？为了处理这种情况，我们使用了 `shutdown` 函数，它允许我们利用 TCP 的半关闭特性。
- 6.6 将缓冲（以及我们的 `readline` 缓冲）与 `select` 混合的危险导致我们生成了按行缓冲区操作的回显客户端和服务器版本。
- 6.7 如果我们使用 `select` 函数为输入操作设置时间限制会发生什么？
- 6.8 最常用的 I/O 多路复用函数是 `select`。

# 第 7.2

# getsockopt 和 setockopt 函数

| level | optname | get | set | Description | Flag | Datatype |
| --- | --- | --- | --- | --- |
| SO_SOCKET | SO_BROADCAST | * | * | 允许发送广播数据报 | | int |
| | SO_DEBUG | * | * | 启用调试 | | int |
| | SO_CONTROUTE | * | * | 绕过路由表查找 | | int |
| | SO_ERROR | * | * | 获取等待错误并清除 | | int |
| | SO_KEEPPALIVE | * | * | 定期测试连接是否仍然存 | | int |
| | SO_LINGER | | * | 关闭时发送带外数据 | | linger |
| | SO_RCBUF | * | * | 接收缓冲区大小 | | int |
| | SO_SNDBUF | * | * | 发送缓冲区大小 | | int |
| | SO_SNDWMT | * | * | 接收缓冲区低水位线 | | int |
| | SO_RCVTIMEO | | * | 接收超时 | | timeval() |
| | SO_SNDTIMEO | | * | 发送超时 | | timeval() |
| | SO_REUSEADDR | | * | 允许地址重用 | | int |
| | SO_REUSEPORT | | * | 允许本地端口重用 | | int |
| | SO_TYPE | | * | 获取套字类型 | | int |
| | SO_TIMEOUT | | * | 返回套字发送的内容 | | int |
| IPPROTO_IP | IP_INDEX | | * | 数据包含 IP 头部 | | (text) |
| | IP_OPTIONS | | * | IP 头部选项 | | int |
| | IP_REVDSTADDR | | * | 返回目的 IP 地址 | | int |
| | IP_RECVIF | | * | 返回接收到的接口 ID | | int |
| | IP_TOS | | * | 服务类型和优先级 | | int |
| | IP_TTL | | * | 存时间 (TTL) | | int |
| | IP_MULTICAST_IF | | * | 指定接口 | | in_addr() |
| | IP_MULTICAST_TTL | | * | 指定多播 TTL | | u_char |
| | IP_MULTICAST_LOOP | | * | 指定环回 | | char |
| | IP_ADD_MEMBERSHIP | | * | 加入/离开多播组 | | ip_mreq() |
| | IP_BLOCK_SOURCE | | * | 阻塞或取消阻塞多播 | | ip_mreq() |
| | IP_LEAVE_SOURCE_MEMBERSHIP | | * | 加入或离开特定多播组 | | ip_mreq() |
| IPPROTO_IPV6 | IP6_CHECKSUM | | * | 要通过的特定 IPv6 消息类型 | | icmp_filter() |
| IPPROTO_IPV6 | IP6_DONTFRAG | | * | 原始套字校验和偏移量 | | |
| | IP6_NEXTHOP | | * | 指定下一跳地址 | | sockaddr_in6() |
| | IP6_ROUTHDR | | * | 获取带有 MTU 的路径 | | ip6_routeinfo() |
| | IP6_REVDSTOPT | | * | 接收目的选项 | | int |
| | IP6_RECVHOPLIMIT | | * | 接收单播跳数限制 | | int |
| | IP6_RECVHOPS | | * | 接收逐跳选项 | | int |
| | IP6_REVPKINFO | | * | 接收数据包信息 | | int |
| | IP6_RECVHTDR | | * | 接收源路由 | | int |
| | IP6_RECVCLASS | | * | 接收路由类 | | int |
| | IP6_UNIC_HOPS | | * | 默认单播跳数限制 | | int |
| | IP6_USE_MTU | | * | 使用最小 MTU | | int |
| | IP6_V6ONLY | | * | 禁用 v4 兼容性 | | int |
| | IP6_KEY | | * | 粘性键 | | (见正文) |
| | IP6_MULTICAST_IF | | * | 指定接口 | | u_int |
| | IP6_MULTICAST_HOPS | | * | 指定输出跳数限制 | | u_int |
| | IP6_MULTICAST_LOOP | | * | 指定环回 | | u_int |
| | IP6_JOIN_GROUP | | * | 加入多播组 | | ip6_mreq() |
| | IP6_LEAVE_GROUP | | * | 离开多播组 | | ip6_mreq() |
| IPPROTO_IP | MAST_JOIN_GROUP | | * | 加入多播组 | | group_req() |
| IPPROTO_IPV6 | MAST_LEAVE_GROUP | | * | 离开多播组 | | group_source_req() |
| | MAST_UNBLOCK_SOURCE | | * | 阻塞取消阻塞多播 | | group_source_req() |
| | MAST_JOIN_SOURCE_GROUP | | * | 加入特定源多播 | | group_source_req() |
| | MAST_LEAVE_SOURCE_GROUP | | * | 离开特定源多播 | | group_source_req() |

图 7.1 用于 `getsockopt` 和 `setockopt` 的套字和 IP 层选项摘要。

| level | optname | get | set | Description | Datatype |
| --- | --- | --- | --- | --- |
| IPPROTO_TCP | TCP_MAXSEG | * | | TCP 分段大小 | int |
| | TCP_NODELAY | * | | 禁用 Nagle 算法 | int |
| IPPROTO_SCTP | SCTP_ADAPTATION_LAYER | * | | 适配层 | sctp_adaptation() |
| | SCTP_ASSOCINFO | * | | 获取关联信息 | sctp_assocparams() |
| | SCTP_OUTCLOSE | * | | 自动关闭 | int |
| | SCTP_DEFAULT_SEND_PARAM | * | | 默认发送参数 | sctp_sndinfo() |
| | SCTP_DISABLE_FRAGMENTS | * | | 分段 | int |
| | SCTP_GET_PEER_ADDR | * | | 注意通知 | sctp_event() |
| | SCTP_SUBSCRIBE | * | | 获取对端状态 | sctp_paddrinfo() |
| | SCTP_ANT_MAP_ADDR | | | 映射 v4 地址 | int |
| | SCTP_INITMSG | * | | 默认参数 | sctp_initmsg() |
| | SCTP_WINDOW | * | | 最大窗口大小 | int |
| | SCTP_MAXSEG | * | | 最大分段大小 | int |
| | SCTP_NODELAY | * | | 禁用 Nagle | int |
| | SCTP_PEER_ADDR | * | | 添加对端地址 | |
| | SCTP_PRIMARY_PARAMS | * | | 目的地址 | sctp_paddams() |
| | SCTP_PRIMARY_ADDR | * | | 目的地址 | sctp_setprim() |
| | SCTP_RTO_INFO | * | | RTO 信息 | sctp_rtolinfo() |
| | SCTP_SET_PEER_ADDR | * | | 对端地址 | sctp_set_prim() |
| | SCTP_STATUS | * | | 获取关联状态 | sctp_status() |

图 2 传输层套字选项。

## 7.3 检查选项是否支持并获取默认值

我们编写一个程序来检查图 7.1 和 7.2 中定义的大多数选项是否支持，如果是，打印它们的默认值。图 7.3 包含了该程序的声明。

### 定义可能的联合体

我们的联合体包含了 `getsockopt` 的每个可能的返回值。

### 定义函数原型

我们定义了四个用于打印给定套字值的函数原型。

### 定义结构并初始化数组

我们的 `sock_opts` 结构包含了调用 `getsockopt` 每个套字选项并打印其当前值所需的信息。最后的 `opt_val` 指向打印选项值的函数。我们分配了这些结构的数组，每个元素一个。

并不是所有实现都支持套字选项。确定给定选项是否支持的方法是使用我们在 `SO_REUSE` 中所示 `#ifdef` 或 `#if`。为了完整性，数组的每个元素都应该按照我们显示 `SO_REUSE` 的方式编译，但我们将省略此部分，因为 `#ifdef` 只增加了我们显示的代码长度，对讨论没有帮助。

```c
```
