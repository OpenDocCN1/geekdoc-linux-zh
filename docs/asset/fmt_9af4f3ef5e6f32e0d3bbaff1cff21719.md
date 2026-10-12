
## HTTP 1.1 状态码

如果您想编写自己的 Web 服务器，就需要理解并使用 HTTP 1.1（RFC2616、RFC2817）的标准状态码。表 A.3 列出了这些状态码。

**表 A.3** HTTP 结果码

| 代码类别值 | 类别名称 | 具体代码及描述 |
| :--- | :--- | :--- |
| 1xx | 信息 | 100 继续 |
| | | 101 切换协议 |
| 2xx | 成功 | 200 确定 |
| | | 201 已创建 |
| | | 202 已接受 |
| | | 203 非权威信息 |
| | | 204 无内容 |
| | | 205 重置内容 |
| | | 206 部分内容 |
| 3xx | 重定向 | 300 多种选择 |
| | | 301 永久移动 |
| | | 302 临时移动 |
| | | 303 查看其他 |
| | | 304 未修改 |
| | | 305 使用代理 |
| 4xx | 客户端错误 | 400 错误请求 |
| | | 401 未授权 |
| | | 402 需要支付 |
| | | 403 禁止 |
| | | 404 未找到 |
| | | 405 方法不允许 |
| | | 406 不可接受 |
| | | 407 需要代理身份验证 |
| | | 408 请求超时 |
| | | 409 冲突 |
| | | 410 已删除 |
| | | 411 需要长度 |
| | | 412 先决条件失败 |
| | | 413 请求实体过大 |
| | | 414 请求-URI 过长 |
| | | 415 不支持的媒体类型 |
| 5xx | 服务器错误 | 500 内部服务器错误 |
| | | 501 未实现 |
| | | 502 坏网关 |
| | | 503 服务不可用 |
| | | 504 网关超时 |
| | | 505 HTTP 版本不支持 |

## 套接字选项 (get/setsockopt())

表 A.4 至 A.7 列出了各种套接字选项及其所需参数。并非所有选项在 UNIX 类型之间都具有大小兼容性。例如，Linux 中的 `IP_TTL` 允许使用 `int` 类型，但只填充第一个字节。而 IBM 的 AIX 将同一选项限制为 `char` 类型。

| 层级 | 选项 | 描述 | * | 读 | 写 | 值 | 类型 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_SOCKET | SO_ATTACH_FILTER | 附加过滤器 | ? | ? | ? | 整数 | int |
| SOL_SOCKET | SO_BINDTODEVICE | 绑定到设备 | ? | ? | ? | 字符串 | char* |
| SOL_SOCKET | SO_BROADCAST | 启用广播 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_BSDCOMPAT | 请求 BSD 逐 bug 兼容性 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_DEBUG | 启用套接字调试 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_DETACH_FILTER | 分离过滤器 | ? | ? | ? | 整数 | int |
| SOL_SOCKET | SO_DONTROUTE | 禁止路由 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_ERROR | 最近错误 | Y | Y | Y | 整数 | int |

**表 A.4 续**

| 层级 | 选项 | 描述 | 读 | 写 | 值 | 类型 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_SOCKET | SO_KEEPALIVE | 启用保持连接 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_LINGER | 滞留直至数据发送 | Y | Y | Y | 滞留 | struct linger |
| SOL_SOCKET | SO_NO_CHECK | 不检查 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_OOBINLINE | 将带外数据内联放置 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_PASSCRED | 启用传递用户凭证 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_PEERCREDS | 对端凭证 | Y | Y | Y | 凭证 | struct ucred |
| SOL_SOCKET | SO_PRIORITY | 设置队列优先级 | Y | Y | Y | 整数 | int |
| SOL_SOCKET | SO_RCVBUF | 接收缓冲区大小 | Y | Y | Y | 整数 | int |
| SOL_SOCKET | SO_RCVLOWAT | 接收低水位标记 | Y | Y | N | 整数 | int |
| SOL_SOCKET | SO_RCVTIMEO | 接收超时 | Y | Y | Y | 时间 | struct timeval |
| SOL_SOCKET | SO_REUSEADDR | 重用地址 | Y | Y | Y | 布尔值 | int |
| SOL_SOCKET | SO_REUSEPORT | 重用地址（多播） | N | - | - | 布尔值 | int |
| SOL_SOCKET | SO_SECURITY_AUTHENTICATION | 安全身份验证 | N | - | - | 整数 | int |
| SOL_SOCKET | SO_SECURITY_ENCRYPTION_NETWORK | 安全网络加密 | N | - | - | 整数 | int |
| SOL_SOCKET | SO_SECURITY_ENCRYPTION_TRANSPORT | 安全传输加密 | N | - | - | 整数 | int |
| SOL_SOCKET | SO_SNDBUF | 发送缓冲区大小 | Y | Y | Y | 整数 | int |
| SOL_SOCKET | SO_SNDLOWAT | 发送低水位标记 | Y | Y | Y | 整数 | int |
| SOL_SOCKET | SO_SNDTIMEO | 发送超时 | Y | Y | Y | 时间 | struct timeval |
| SOL_SOCKET | SO_TYPE | 套接字类型 | Y | Y | Y | 整数 | int |

**表 A.5 IP 层套接字选项**

| 层级 | 选项 | 描述 | * | 读 | 写 | 值 | 类型 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_IP | IP_ADD_MEMBERSHIP | 添加多播组成员资格 | Y | Y | Y | IPv4 多播地址 | struct in_addr |
| SOL_IP | IP_DROP_MEMBERSHIP | 删除多播组成员资格 | Y | Y | Y | IPv4 多播地址 | struct in_addr |
| SOL_IP | IP_HDRINCL | 启用手动 IP 报头创建 | Y | Y | Y | 布尔值 | int |
| SOL_IP | IP_MTU_DISCOVER | MTU 发现 | Y | Y | Y | 整数 | int |
| SOL_IP | IP_MULTICAST_IF | 出站多播接口 | Y | Y | Y | IPv4 地址 | struct in_addr |
| SOL_IP | IP_MULTICAST_LOOP | 启用多播回环 | Y | Y | Y | 布尔值 | int |
| SOL_IP | IP_MULTICAST_TTL | IP 多播生存时间 | Y | Y | Y | 整数 | int |
| SOL_IP | IP_OPTIONS | IP 选项 | Y | Y | Y | 选项 | int [] |
| SOL_IP | IP_PKTOINFO | 启用获取数据包信息 | Y | Y | Y | 布尔值 | int |
| SOL_IP | IP_RECPOPTNS | 数据包选项 | N | - | Y | 选项 | int [] |
| SOL_IP | IP_RECVERR | 启用接收错误数据包 | Y | Y | Y | 布尔值 | int |
| SOL_IP | IP_RECVOPTS | 启用接收选项 | Y | Y | Y | 布尔值 | int |
| SOL_IP | IP_RECVTOS | 获取接收到的 TOS | Y | Y | Y | 整数 | int |
| SOL_IP | IP_RECVTTL | 获取接收到的 TTL | Y | Y | Y | 整数 | int |
| SOL_IP | IP_MULTICAST_IF | 多播接口 | * | Y | Y | 整数 | int |
| SOL_IP | IP_MULTICAST_TTL | 多播生存时间 | * | Y | Y | 布尔值 | int |
| SOL_IP | IP_MULTICAST_LOOP | 多播回环 | * | Y | Y | 布尔值 | int |
| SOL_IP | IP_TOS | 服务类型 (TOS) | * | Y | Y | 整数 | int |
| SOL_IP | IP_TTL | 生存时间 (TTL) | * | Y | Y | 整数 | int |

**表 A.6 IPv6 层套接字选项**

| 层级 | 选项 | 描述 | * | 读 | 写 | 值 | 类型 |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| SOL_IPV6 | IPV6_ADD_MEMBERSHIP | 加入多播组成员资格 | ? | ? | ? | IPv6 多播地址 | struct ip_mreq6 |
| SOL_IPV6 | IPV6_ADDRFORM | 更改套接字地址 | ? | ? | ? | 整数 | int |
| SOL_IPV6 | IPV6_AUTHHDR | AUTHHDR 偏移量 | ? | ? | ? | 整数 | int |
| SOL_IPV6 | IPV6_CHECKSUM | 原始套接字的原始校验和偏移量 | ? | ? | ? | 整数 | int |
| SOL_IPV6 | IPV6_DROP_MEMBERSHIP | 删除多播组成员资格 | ? | ? | ? | IPv6 多播地址 | struct ip_mreq6 |
| SOL_IPV6 | IPV6_DSTOPTS | 启用获取目标选项 | ? | ? | ? | 布尔值 | int |
| SOL_IPV6 | IPV6_HOPLIMIT | 启用获取跳数限制 | ? | ? | ? | 布尔值 | int |
| SOL_IPV6 | IPV6_HOPOPTS | 启用获取逐跳选项 | ? | ? | ? | 布尔值 | int |
| SOL_IPV6 | IPV6_MULTICAST_HOPS | 指定多播跳数 | ? | ? | ? | 整数 | int |
| SOL_IPV6 | IPV6_MULTICAST_IF | 指定出站多播接口 | ? | ? | ? | IPv6 地址 | struct in6_addr |
| SOL_IPV6 | IPV6_MULTICAST_LOOP | 启用多播回环 | ? | ? | ? | 整数 | int |
| SOL_IPV6 | IPV6_NEXTHOP | 启用指定下一跳 | ? | ? | ? | 布尔值 | int |
| SOL_IPV6 | IPV6_PKTINFO | 接收数据包信息 | ? | ? | ? | 整数 | int |
| SOL_IPV6 | IPV6_RCVTCLASS | 指定数据包类 | ? | ? | ? | 选项 | int [] |
| SOL_IPV6 | IPV6_ROUTER_ALERT | 启用路由器警报 | ? | ? | ? | 布尔值 | int |
| SOL_IPV6 | IPV6_RSRCRT | 接收源路由 | ? | ? | ? | 布尔值 | int |
| SOL_IPV6 | IPV6_UNICAST_HOPS | 指定跳数限制 | ? | ? | ? | 整数 | int |

### 表 A.7 TCP 层套接字选项

| 层级 | 选项 | 描述 | * | R | W | 值 | 类型 |
|---|---|---|---|---|---|---|---|
| SOL_TCP | TCP_KEEPALIVE | 保持连接延迟（已替换为 sysctl 调用） | N | - | - | 整数 | int |
| SOL_TCP | TCP_MAXRT | 最大重传时间 | N | - | - | 整数 | int |
| SOL_TCP | TCP_MAXSEG | 设置最大分段（发送缓冲区）大小 | Y | Y | Y | 整数 | int |
| SOL_TCP | TCP_NODELAY | 启用 Nagle 算法 | Y | Y | Y | 布尔值 | int |
| SOL_TCP | TCP_STDURG | 指定紧急字节的位置（已替换为 sysctl 调用） | N | - | - | 布尔值 | int |
| SOL_TCP | TCP_CORK | 永不发送部分完成的数据段 | Y | Y | Y | 布尔值 | int |
| SOL_TCP | TCP_KEEPIDLE | 在此时间段后开始保持连接探测 | Y | Y | Y | int |
| SOL_TCP | TCP_KEEPINTVL | 保持连接探测之间的间隔 | Y | Y | Y | int |
| SOL_TCP | TCP_KEEPCNT | 连接断开前的保持连接探测次数 | Y | Y | Y | int |
| SOL_TCP | TCP_SYNCNT | SYN 重传次数 | Y | Y | Y | int |
| SOL_TCP | TCP_LINGER2 | 孤立的 FIN-WAIT-2 状态的生存时间 | Y | Y | Y | int |
| SOL_TCP | TCP_DEFER_ACCEPT | 仅在数据到达时唤醒监听者 | Y | Y | Y | int |
| SOL_TCP | TCP_WINDOW_CLAMP | 限制通告窗口 | Y | Y | Y | int |

## 信号定义

表 A.8 列出了标准信号及其含义。

### 表 A.8 标准 Linux 信号代码

| 信号 | 值 | 动作 | 注释 |
| :--- | :--- | :--- | :--- |
| SIGHUP | 1 | A | 检测到控制终端挂断或控制进程终止 |
| SIGINT | 2 | A | 来自键盘的中断 |
| SIGQUIT | 3 | A | 来自键盘的退出 |
| SIGILL | 4 | A | 非法指令 |
| SIGABRT | 6 | C | 来自 abort(3) 的中止信号 |
| SIGFPE | 8 | C | 浮点异常 |
| SIGKILL | 9 | AEF | 杀死信号 |
| SIGSEGV | 11 | C | 无效内存引用 |
| SIGPIPE | 13 | A | 管道破裂：向没有读者的管道写入 |
| SIGALRM | 14 | A | 来自 alarm(2) 的定时器信号 |
| SIGTERM | 15 | A | 终止信号 |
| SIGUSR1 | 30,10,16 | A | 用户自定义信号 1 |
| SIGUSR2 | 31,12,17 | A | 用户自定义信号 2 |
| SIGCHLD | 20,17,18 | B | 子进程停止或终止 |
| SIGCONT | 19,18,25 | | 如果已停止则继续 |
| SIGSTOP | 17,19,23 | DEF | 停止进程 |
| SIGTSTP | 18,20,24 | D | 在终端上输入的停止 |
| SIGTTIN | 21,21,26 | D | 后台进程 tty 输入 |
| SIGTTOU | 22,22,27 | D | 后台进程 tty 输出 |
| SIGIOT | 6 | CG | IOT 信号：SIGABRT 的同义词 |
| SIGEMT | 7,-,7 | G | |
| SIGBUS | 10,7,10 | AG | 总线错误 |
| SIGSYS | 12,12 | G | 例程参数错误 (SVID) |
| SIGSTKFLT | -,16,- | AG | 协处理器栈故障 |
| SIGURG | 16,23,21 | BG | 套接字上的紧急状况 (4.2 BSD) |
| SIGIO | 23,29,22 | AG | I/O 现在可能 (4.2 BSD) |
| SIGPOLL | | AG | SIGIO 的同义词 (System V) |
| SIGCLD | --,18 | G | SIGCHLD 的同义词 |
| SIGXCPU | 24,24,30 | AG | CPU 时间限制超出 (4.2 BSD) |
| SIGXFSZ | 25,25,31 | AG | 文件大小限制超出 (4.2 BSD) |
| SIGVTALRM | 26,26,28 | AG | 虚拟闹钟 (4.2 BSD) |
| SIGPROF | 27,27,29 | AG | 性能分析闹钟 |
| SIGPWR | 29,30,19 | AG | 电源故障 (System V) |
| SIGINFO | 29,-, | G | SIGPWR 的同义词 |
| SIGLOST | -,-,- | AG | 文件锁丢失 |
| SIGWINCH | 28,28,20 | BG | 窗口大小改变信号 (4.3 BSD, Sun) |
| SIGUNUSED | -,31,- | AG | 未使用的信号 |

- A—默认动作是终止进程。
- B—默认动作是忽略信号。
- C—默认动作是转储核心。
- D—默认动作是停止进程。
- E—信号不能被捕获。
- F—信号不能被忽略。
- G—非 POSIX.1 兼容信号。

## ICMP 代码

表 A.9 显示了不同类型的 ICMP (RFC792) 数据包及其含义。

### 表 A.9 ICMP 代码描述

| 类型 | 代码 | 描述 |
| --- | --- | --- |
| 0 | 0 | 回显应答 |
| 3 | | 目的站不可达 |
| | 0 | 网络不可达 |
| | 1 | 主机不可达 |
| | 2 | 协议不可达 |
| | 3 | 端口不可达 |
| | 4 | 需要分片但设置了 DF 位 |
| | 5 | 源路由失败 |
| | 6 | 目的网络未知 |
| | 7 | 目的主机未知 |
| | 8 | 源主机隔离（已废弃） |
| | 9 | 目的网络在管理上被禁止 |
| | 10 | 目的主机在管理上被禁止 |
| | 11 | 网络不可达（针对 TOS） |
| | 12 | 主机不可达（针对 TOS） |
| | 13 | 通信在管理上被禁止 |
| | 14 | 主机优先级违规 |
| | 15 | 优先级截断生效 |
| 4 | 0 | 源站抑制——网关请求主机降低传输速率 |
| 5 | | 重定向 |
| | 0 | 针对网络的重定向 |
| | 1 | 针对主机的重定向 |
| | 2 | 针对服务类型和 network 的重定向 |
| | 3 | 针对服务类型和 host 的重定向 |
| 8 | 0 | 回显请求 |
| 9 | 0 | 路由器通告 |
| 10 | 0 | 路由器请求 |
| 11 | | 超时 |
| | 0 | 传输过程中 TTL 等于 0 |
| | 1 | 分片重组过程中 TTL 等于 0 |
| 12 | | 参数问题 |
| | 0 | IP 头部错误 |
| | 1 | 缺少必需选项 |
| 13 | 0 | 时间戳请求 |
| 14 | 0 | 时间戳应答 |
| 15 | 0 | 信息请求 |
| 16 | 0 | 信息应答 |
| 17 | 0 | 地址掩码请求 |
| 18 | 0 | 地址掩码应答 |

## IPv4 组播分配

表 A.10 定义了当前组播地址分配 [RFC2365] 在频谱顺序中的排列。

### 表 A.10 建议的组播分配

| 地址范围 | 范围 | 典型 TTL |
| :--- | :--- | :--- |
| 224.0.0.0–224.0.0.255 | 集群 | 0 |
| 224.0.1.0–238.255.255.255 | 全球 | <= 255 |
| 239.0.0.0–239.191.255.255 | （未定义） | |
| 239.192.0.0–239.195.255.255 | 组织 | < 128 |
| 239.196.0.0–239.254.255.255 | （未定义） | |
| 239.255.0.0–239.255.255.255 | 站点 | < 32 |

## 建议的 IPv6 地址分配

表 A.11 列出了以位为单位的建议 IPv6 地址分配。

### 表 A.11 建议的 IPv6 地址分配

| 分配 | 地址前缀 |
| :--- | :--- |
| （保留） | 0000 0000 |
| （未分配） | 0000 0001 |
| NSAP | 0000 001 |
| IPX | 0000 010 |
| （未分配） | 0000 011 |
| （未分配） | 0001 1 |
| （未分配） | 0001 |
| 聚合全球单播地址 | 001 |
| （未分配） | 010 |
| （未分配） | 011 |
| （未分配） | 100 |
| （未分配） | 101 |
| （未分配） | 110 |
| （未分配） | 1110 |
| （未分配） | 1111 0 |
| （未分配） | 1111 10 |
| （未分配） | 1111 110 |
| （未分配） | 1111 1110 0 |
| 链路本地单播地址 | 1111 1110 10 |
| 站点本地单播地址 | 1111 1110 11 |
| 组播地址 | 1111 1111 |

## ICMPv6 代码

表 A.12 显示了用于 IPv6 的新 ICMPv6 [RFC2463]。

### 表 A.12 ICMPv6 代码描述

| 类型 | 代码 | 描述 |
|---|---|---|
| 1 | 0 | 目的站不可达 |
| | 1 | 在管理上被禁止（防火墙过滤） |
| | 2 | 不是邻居（错误的严格源路由） |
| | 3 | 地址不可达（通用） |
| | 4 | 端口不可达 |
| 2 | 0 | 数据包过大 |
| 3 | 0 | 超时 |
| | 1 | 传输过程中跳数限制超出 |
| | | 分片重组时间超时 |
| 4 | 0 | 参数问题 |
| | 1 | 头部字段错误 |
| | 2 | 无法识别的下一个头部 |
| | | 无法识别的选项 |
| 128 | 0 | 回显请求（ping） |
| 129 | 0 | 回显应答（ping） |
| 130 | 0 | 组成员身份查询 |
| 131 | 0 | 组成员身份报告 |
| 132 | 0 | 组成员身份减少 |
| 133 | 0 | 路由器请求 |
| 134 | 0 | 路由器通告 |
| 135 | 0 | 邻居请求 |
| 136 | 0 | 邻居通告 |
| 137 | 0 | 重定向 |

## IPv6 组播范围字段

表 A.13 定义了 IPv6 组播地址中范围字段的不同值。

### 表 A.13 IPv6 组播范围字段描述

| 范围 | 区间 | 描述 |
| :--- | :--- | :--- |
| 0 | （未定义） | |
| 1 | 节点 | 在同一主机上本地使用（类似于 127.0.0.1）。 |
| 2 | 链路 | 消息保留在路由器的组内。路由器绝不让这些消息通过。 |
| 3–4 | （未定义） | |
| 5 | 站点 | 由网络管理员定义，消息保留在站点的局部范围内。 |
| 6–7 | （未定义） | |
| 8 | 组织 | 由网络管理员定义，消息保留在组织的局部范围内。 |
| 9–13 | （保留） | |
| 14 | 全球 | 所有路由器允许消息通过全球网络，直到它们过期。 |
| 15 | （保留） | |

## IPv6 多播标志字段

表 A.14 展示了 IPv6 多播地址中当前定义的标志字段。

**表 A.14** IPv6 多播标志字段描述

| 位 # | 描述 |
| :--- | :--- |
| 0 | 临时性 |
| | 0= 知名地址 |
| | 1= 临时地址 |
| 1 | （保留） |
| 2 | （保留） |
| 3 | （保留） |

## 附录 B

### 本附录内容

- 连接到网络 422
- 在通道上通信 428
- 终止连接 437
- 网络数据转换 438
- 网络寻址工具 442
- 套接字控制 446

本附录汇总了所有网络库和系统调用。

## 连接到网络

Sockets API 提供工具帮助你创建套接字并连接到其他主机。本节描述了与套接字创建和连接相关的 API。

### socket()

`socket()` 创建一个双向通道，通常用于连接网络。你可以使用此通道配合网络特定的系统调用或通用文件 I/O 进行操作。

#### 原型

```c
