
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

### 套接字选项 (get/setsockopt())

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
