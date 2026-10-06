

## B.3 /proc 目录中的信息

tcp_keepalive_probes: 在连接被认为失败之前，TCP 发送的 KeepAlive 探测包数量。

tcp_retries1: 在放弃某个数据包之前接收的确认包数量。

tcp_retries2: 发送数据包的最大尝试次数。

tcp_fin_timeout: 在终止连接之前，等待连接关闭确认包的时间。

tcp_max_syn_backlog: 为套接字缓冲的 TCP 连接建立请求数。

tcp_window_scaling: 启用或禁用 TCP 窗口缩放（如 RFC 1323 规范）。

tcp_timestamps: 启用或禁用 TCP 时间戳（如 RFC 1323 规范）。

tcp_sack: 选择性确认（TCP ACK）的开关。

tcp_sturg: 根据 RFC 793 规范启用紧急优先级数据。

tcp_retrans_collapse: 打印机中的某些 TCP 栈存在缺陷。你可以激活此选项来规避此问题。

ip_local_port_range 指定了 TCP 和 UDP 协议本地端口的范围。第一个数字指定间隔的起始位置，第二个数字指定结束位置。

/proc/sys/net/ipv4/conf 目录被细分：让我们看看 conf 子目录。它包含以下子目录：每个注册的网络设备各一个，以及一个名为 all 的目录。所有这些目录都包含相同的条目，在此介绍：

- * accept_redirects 显示是否接受 ICMP 重定向。此选项在路由器中默认禁用，但在终端系统中禁用。
- * accept_source-route 启用或禁用接受源路由数据包。此选项在路由器中通常启用，但在终端系统中禁用。
- * forwarding 启用或禁用在此网络设备上转发数据包。
- * log_martians 启用或禁用记录“不可能”的地址（包括 IP 中的类 E 地址）。
- * mc_forwarding 启用或禁用多播路由。如果激活，则应额外为内核编译 CONFIG_ROUTE 选项，并安装一个多播路由守护进程。
- * proxy_arp: 支持 ARP 代理。
- * rp_filter 启用或禁用仅允许默认网关列表中的路由器接受 ICMP 重定向消息的选项。

/proc/sys/net/ipv4/route

error_burst, error_cost: 这些参数用于限制内核中路由代码的日志消息。error_cost 越大，创建日志消息的时间越早，error_burst 限制警告消息的拒绝。

## 附录 B 调试 Linux 内核

ush: 访问此文件会导致路由缓存被删除。
gc_elastic, gc_interval, gc_min_interval, gc_thresh, gc_timeout:
这些参数控制路由表的自动垃圾回收（即条目从表中移除的速度有多快和严格程度有多高）。

max_size 指定路由缓存的大小。一旦达到此大小，旧的条目将被删除。

max_delay, min_delay: 删除整个缓存的数值。
redirect_load, redirect_number: 这些因素指定了可以发送多少 ICMP 数据包。如果超过 redirect_load 或 redirect_number，则不再发送重定向包。

redirect_silence 是重定向包的超时值。一旦过期，尚未被确认的重定向包将重新发送。此过程在重定向被禁用、超过 redirect_load 或超过 redirect_number 运行时运行。

max_size: 路由缓存中条目的最大数量。如果超过此值，最少使用的条目将被覆盖。

/proc/sys/net/ipv4/neigh/[net_dev] 以下参数定义了直接网络邻居；它们位于各自网络设备的 /proc/sys/net/ipv4/neigh/[net_dev] 目录下：

- * base_reachable_time: 用于计算随机可达时间（参见 RFC 2461）。
- * retrans_time: 两个连续的邻居请求包之间的时间，用于地址解析和检查本地计算机的可达性。该时间以刻（ticks）为单位。
- * q_len: 等待特定地址的高层层数据包的最大队列长度（参见第 15 章）。
- * ucast_solicit: 用于解析单播地址发送的最大数据包数量。
mcast_solicit: 解析多播地址的最大尝试次数。
delay_first_probe_time: 有效邻居过期后再次进入的等待时间（参见 gc_stale_time）。
- * locktime: ARP/邻居表中的条目一旦旧条目锁定刻，将被新条目替换。
- * proxy_delay: ARP 代理中 ARP 请求响应的最大等待时间。
- proxy_len: 延迟 ARP 代理计时器的最大队列长度。
- arp_solicit: 指定在用户级别发送到 ARP 守护进程的请求数。
- gc_stale_time: 指定检查 ARP 表的间隔。如果条目处于 NUD_STALE 状态，将尝试查找它（通过广播请求）。如果尝试失败且 mcast_solicit > 0，则使用单播请求。

## 在内核中使用调试器

调试器允许你在执行期间停止程序并单步执行以监控状态——变量值和内存内容——并在需要时进行修改。调试器也可用于内核。然而，停止内核会导致系统立即无法使用。

内核与调试器之间的接口

核心文件作为调试器与状态之间的接口也可用于内核。为此，/proc/kcore 将系统内存映射到核心文件的格式。因此，我们可以检查系统状态。

 编译器选项

除了核心文件，调试器还需要一个可执行程序文件。对于 Linux 内核，它在编译目录下名为 vmlin。在编译要调试的程序时，编译器应插入调试信息（变量的文本名称以及对源代码相关位置的引用）。如果这些信息可用，调试器允许你通过名称查询变量。

 gcc 提供了 -g 选项在编译期间嵌入调试信息。此选项必须输入 Makefile 中的适当位置，以确保在编译 Linux 内核时使用。如果我们想对整个内核实现这一点，可以在主目录文件中的 CFLAGS 变量。在包含这些区域文件的 Makefile 中添加一个 EXTRA_CFLAGS=-g 行即可。例如，使用 /ip4/Makefile。

gdb 和 ded UNIX 中受欢迎的调试器之一是 gdb 调试器，它在自由软件基金（FSF）的支持下开发。gdb 只为用户提供文本界面，因此使用起来并不方便。最近，开发了一些前端来消除这一缺点（例如提供图形用户界面）。FSF 也开发了两个此类代表工具：数据调试器 d，以及 emacs 编辑器的全局统一调试器（gud）模式 dd 具有数据结构的可视化表示选项，使其特别适用于 Linux 内核中的此类数据结构。

