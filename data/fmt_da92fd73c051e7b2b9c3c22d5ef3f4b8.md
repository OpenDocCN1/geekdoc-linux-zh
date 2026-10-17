
# FreeBSD 系统调优参数与索引

## 网络端口范围配置

`net.inet.ip.portrange.lowfirst: 1023`
`net.inet.ip.portrange.lowmost: 600`

运行时变量。某些程序或协议要求从低号端口建立连接，这表明它们启动了特权进程。记住，发出的 TCP/IP 连接使用本地系统上的端口。还要记住，端口 0 到 1023 只能由 root 打开。这意味着如果连接来自低号端口，从理论上讲它是以 root 身份运行的（这涉及到信任发起连接的机器没有被攻破）。FreeBSD 使用位于 `net.inet.ip.portrange.lowfirst`（默认值为 123）和 `net.inet.ip.portrange.lowlast`（默认值为 600）之间的端口。我只知道过一个更改此设置有意义的例子：Intel 网卡上的 IPMI 总是会拦截针对 623 和 664 端口的 UDP 数据包。如果你没有其中一类网卡，请不要动它。

`net.inet.ip.portrange.first: 49152`
`net.inet.ip.portrange.last: 65535`

运行时变量。当 FreeBSD 为非特权进程发出的连接分配随机端口时，它使用的端口位于 `net.inet.ip.portrange.first`（默认值为 49152）和 `net.inet.ip.portrange.lowlast`（默认值为 65535）之间。

`net.inet.ip.portrange.hfirst: 49152`
`net.inet.ip.portrange.highlast: 65535`

运行时变量。某些程序专门为传出连接请求高号端口。默认情况下，此端口范围与 `net.inet.ip.portrange.first` 到 `net.inet.ip.portrange.last` 指定的端口重叠，但你可以通过使用 `hfirst` 和 `highlast` sysctl 分隔这些范围。

`net.inet.ip.portrange.reservedhigh: 1023`
`net.inet.ip.portrange.reservedlow: 0`

运行时变量。这指定了只能由 root 打开的端口范围。

`net.inet.ip.portrange.randomized: 1`

运行时变量。默认情况下，FreeBSD 在为该类型连接分配的范围内分配随机端口。

`net.inet.ip.portrange.randomps: 10`

运行时变量。这是每秒内随机端口分配的最大数量。如果需要许多端口，FreeBSD 将切换到顺序端口分配，以避免耗尽系统的随机性。

`net.inet.ip.portrange.randomtime: 45`

运行时变量。这是 FreeBSD 在恢复随机端口分配之前使用顺序 TCP/UDP 端口分配的秒数。

## IP 转发与重定向

`net.inet.ip.forwarding: 0`

运行时开关。你可能希望 FreeBSD 充当路由器、网关或防火墙。设置此项后，系统将在接口之间转发数据包。

`net.inet.ip.redirect: 1`

运行时开关。设置此项后，作为路由器或网关的 FreeBSD 系统将向网络上的其他系统发送 ICMP 重定向包。如果系统未进行路由，则此项不起作用。

`net.inet.ip.ttl: 64`

运行时变量。这是任何数据包可以经过的最大跳数（hops）。

`net.inet.ip.source: 0`

运行时开关。源路由被认为是一个坏主意。

`net.inet.ip.accept_source: 0`

运行时开关。这允许接受源路由包。

`net.inet.ip.fastforward: 0`

运行时开关。这允许转发源包。

`net.inet.ip.check_interface: 0`

运行时开关。这提供了基础的反欺骗保护。

## ICMP 配置

`net.inet.icmp.iclim: 200`

运行时变量。这是系统每秒允许的最大 ICMP 请求。

`net.inet.icmp.redirect: 0`

运行时开关。这启用响应 ICMP 重定向。将此设置为 0 以禁用它。

`net.inet.icmp.drop_redirect: 0`

运行时变量。这告诉 FreeBSD 忽略 ICMP 重定向。

`net.inet.icmp.log_redirect: 0`

运行时开关。如果设置，FreeBSD 将记录所有 ICMP 重定向。（你其实并不真的需要这个，对吧？）

`net.inet.icmp.bmcast: 0`

运行时开关。这启用广播响应。现在默认禁用。

## TCP 协议栈配置

`net.inet.tcp.rfc3223: 1`
`net.inet.tcp.rfc3042: 1`
`net.inet.tcp.rfc3390: 1`

运行时开关。这些启用了 RFC 中描述的各种 TCP 方法。

`net.inet.tcp.sendspace: 32768`
`net.inet.tcp.recvspace: 65536`

运行时变量。这是新 TCP/IP 连接的默认缓冲区大小。

`net.inet.tcp.log_in_vain: 0`

运行时开关。这启用记录任何到未监听 TCP 端口的连接尝试。

`net.inet.tcp.blackhole: 0`

运行时开关。默认情况下，尝试连接关闭端口时 TCP/IP 会返回错误。这显示为“被端重置连接”（Connection reset by peer）。如果你将其设置为 1，尝试连接关闭的 TCP 端口将被丢弃而不发送错误。

`net.inet.tcp.delayed_ack: 1`

运行时开关。这告诉 FreeBSD 尝试在数据包中包含 TCP ACK 信息，而不是发送额外的包。

`net.inet.tcp.recvbuf_auto: 1`

运行时开关。这启用接收缓冲器的自动调整。

`net.inet.tcp.recvbuf_inc: 16384`

运行时变量。这是自动调整时接收缓冲区变化的增量大小。

`net.inet.tcp.recvbuf_max: 262144`

运行时变量。这是系统中任何一个接收缓冲器的最大值。

`net.inet.tcp.slowstart_flightsize: 1`

运行时变量。这指定了 FreeBSD 在跨宽网络 TCP 事务的慢启动阶段将发送的数据包数量。

`net.inet.tcp.local_slowstartsize: 4`

运行时变量。这指定了 FreeBSD 在跨本地网络 TCP 事务的慢启动阶段将发送的数据包数量。

`net.inet.tcp.newreno: 1`

运行开关。此项用于切换 RFC2582 连接恢复，也称为 TCP NewReno 算法。

`net.inet.tcp.tso: 1`

运行开关。某些网络硬件可以处理将网络请求拆分为适合介质适当大小的数据包。例如，对于某些网卡，FreeBSD 只需要将一大块数据交给网卡并要求其将其拆分为包。这允许与网卡进行更优化的通信，并减少 CPU 的工作。这告诉 FreeBSD 使用硬件执行支持的分段操作。

`net.inet.tcp.sndbuf_auto: 1`

运行开关。这启用 TCP 连接缓冲区的自动大小调整。

`net.inet.tcp.sndbuf_inc: 8192`

运行时变量。这规定了每次需要更改时增加或减少 TCP 缓冲的量。

`net.inet.tcp.sndbuf_max: 262144`

运行时变量。这是单个 TCP 缓冲区的最大大小。

`net.inet.tcp.sack.enable: 1`

运行开关。FreeBSD 默认使用选择性确认（ACK），但偶尔非常老旧的主机会在该功能上遇到问题。

`net.inet.do_tcpdrain: 1`

运行开关。这告诉 FreeBSD 在 mbufs 不足时从重组队列中刷新数据包。现在 FreeBSD 自动从内核内存分配 mbufs，因此此设置比以前用处小得多。

`net.inet.tcp.always_keepalive: 1`

运行开关。默认情况下，FreeBSD 会检查所有 TCP 连接以查看它们是否存活。通常，如果两个主机之间的连接断开，这些心跳包将告诉系统关闭连接。如果你禁用了此行为，FreeBSD 将不会检查主机之间的连接是否在线；相反，它将假设连接是通的，直到无法传递数据为止。

## UDP 配置

`net.inet.udp.log_in_val: 0`

运行开关。这记录连接到任何没有程序监听的 UDP 端口的尝试。

`net.inet.udp.blackhole: 0`

## 链路层与调试配置

`net.link.log_link_state_change: 1`

运行时开关。如果启用，FreeBSD 将在网络接口每次启动或关闭时记录日志。

`debug.debugger_on_panic: 1`

运行时开关。如果设置，FreeBSD 在发生内核崩溃（panic）时进入调试器。

`debug.trace_on_panic: 0`

运行时开关。如果设置，FreeBSD 在发生崩溃后进入调试器时会自动打印堆栈回溯。

`debug.witness.watch: 1`

运行时变量，可调。在将 WITNESS 编译进内核后，FreeBSD 会对所有内核锁执行额外的完整性检查。将其设置为 0 可禁用这些检查。一旦你关闭 WITNESS，在不重启的情况下无法重新开启。当你禁用它时，将无法获得 WITNESS 的益处；如果你的系统由于高负载下的锁定问题发生崩溃，你将无法获得告诉 FreeBSD 开发者可以在哪里找到问题的锁信息。

`debug.witness.skippin: 1`

启动开关。这告诉 WITNESS 不要对自旋锁（spin locks）执行任何检查。使用 WITNESS 检查自旋锁会让几乎任何机器变得难以忍受地缓慢。跳过自旋锁但在所有其他情况下使用 WITNESS，会使 WITNESS 从难以忍受的缓慢变为仅是缓慢。这与内核选项 `WITNESS_SKIPPIN` 相同。

`debug.minidump: 1`

运行时开关，可调。默认情况下，FreeBSD 只在崩溃时转储内核内存。将其设置为 0 以在崩溃时转储物理内存的所有内容。

## 硬件配置

`hw.ata_dma: 1`

启动开关。启用 IDE 设备中的 DMA。如果你的硬件使用 PIO 而不是 DMA，请将其设置为 0。如果你的硬件老到需要 PIO，你可能已经知道这一点了。

`hw.ata_api_dma: 1`

启动开关。启用 ATAPI 设备中的 DMA。如果你的硬件使用 PIO 而不是 DMA，或者你的硬件的 DMA 实现存在 Bug，请将其设置为 0。再次，如果你的硬件老到需要 PIO，你可能已经知道这一点了。

### `hw.ata.wc: 1`

启动开关。这启用 IDE 写入缓存，某些硬盘支持此项功能。写入缓存使用硬盘上的一个小缓冲区将写入操作缓存到磁盘上，以牺牲可靠性为代价来提高性能。将其设置为 0 以禁用写入缓存并增强数据安全。见第 8 章。

### `hw.syscons.kbd_reboot: 1`

运行开关。启用此项后，传统的 CTRL-ALT-DELETE 将重启系统。设置为 0 以禁用此行为。

### `compat.linux.osrelease: 2.4.2`

运行时变量。这定义了 Linux 模式支持的 Linux 版本。某些 Linux 程序在更改此项时行为会有不同。虽然你可以动态更改它，但如果在使用任何 Linux 程序，系统将崩溃。最好让 Linux 模式为你处理这一点。

## Jail 安全配置

### `security.jail.set_hostname_allowed: 1`

运行时变量。这决定 jail 管理员是否可以更改其 jail 的主机名。见第 9 章。

### `security.jail.socket_unixiproute_only: 1`

运行时变量。这控制 jail 所有者是否可以使用 TCP/IP 的协议。

### `security.jail.sysvic_allowed: 0`

运行时变量。这决定 jail 所有者是否可以使用 System V IPC。

### `security.jail.enforce_staff: 2`

运行时变量。设置为 0 时，jailed 用户可以看到系统内外所有的挂载点和分区。设置为 1 时，仅可见 jail 下的挂载点。设置为 2 时，仅可见 jail 的 root 挂载点。

### `security.jail.allow_sockets: 0`

运行时变量。设置后，jail 中的 root 可以创建原始套接字（raw sockets）。

### `security.jail.chflags_allowed:`

jail 管理员可以使用 `chflags(1)`。见第 9 章。

### `security.jail.list:`

只读。列出系统中所有活跃的 jail。FreeBSD 在启动和停止 jail 时更改，但无法通过 `sysctl(8)` 修改。

### `security.jail.jailed: 0`

只读。如果设置为 1，该程序位于 jail 内部。见第 9 章。

## 进程可见性与安全配置

### `security.bsd.see_other_uids: 1`

运行时开关。默认情况下，用户可以通过 `ps(1)` 查看其他用户的进程。设置为 0 可禁用此项。

### `security.bsd.see_other_gids: 1`

运行时开关。默认情况下，用户可以通过 `ps(1)` 查看其他组的进程。设置为 0 可禁用此项。

### `security.bsd.unprivileged_read_msgbuf: 1`

运行时开关。默认情况下，非特权用户可以通过 `dmesg(8)` 读取系统缓冲区，包括 jail 内部的用户。设置为 0 可禁用此项。

### `security.bsd.hardlink_check_uid: 0`

运行时开关。默认情况下，用户可以为任何文件创建硬链接。设置为 1 时，用户无法为其他用户的文件创建硬链接。

### `security.bsd.hardlink_check_gid: 0`

运行时开关。默认情况下，用户可以为任何组创建硬链接。设置为 1 时，用户只能为其所属组的文件创建硬链接。

### `security.bsd.overworked_admin: 3.1415925`

只读。如果你真的读了这个附录，说明你工作太累了。放下书。出去。去呼吸一两小时新鲜空气。你会感觉好受。如果你认为这是一个真实的 sysctl MIB，至少在外面待两天。

# INDEX 符号与数字

- 星号 (`*`)，在 crontabs 中，464
- `@reboot`，466
- 美元符号 (`$`)，环境字段中的用户名，200
- `$BLOCKSIZE` 变量，216
- `$EDITOR` 环境变量，185
- `$header` 字符串，113
- `$HOME/.bash` 文件，249
- `$Id` 字符串，113
- `$log` 字符串，113
- `$TAPE` 变量，91–92
- 点 (`.`)，名字中的隐藏文件，38
- 井号 (`#`)，注释，130
- `+IGNORE_ME`，408
- 问号 (`?`)，loader 的命令，66
- 斜杠 (`/root`) 分区，38
- 双斜杠 (`//`)，注释，424
- 波浪号 (`~`) 用户环境字段中的，200
- `tip` 程序，75
- 3Ware，542
- 4BSD 调度器，349
- 32-位计算，369
- 64-位计算，369
- 11hn.sh 插件，用于 FreeSBIE，635
- 380BSD，4
- 账户过期字段，在 `/etc/master.passwd` 文件中，187
- ACPI (高级配置电源接口)，启动时，62–63
- Active Directory，513
- 活跃内存，577
- `add` 关键字，在 `/etc/nsmb.conf` 中，250
- 地址解析协议 (ARP)，146, 160, 表格，169
- `adduser` 命令，181
- `adduser-plugin` 用于 FreeSBIE，634
- 管理组，创建，192–193
- Adobe Acrobat Reader，365
- 高级配置电源接口 (ACPI)，启动时，62–63
- 聚合协议 (aggregation protocols)，175–176
- `_REG_PRETTY_PRINT` 选项，用于内核，133
- `ARP_PRETTY_PRINT` 选项，用于内核，133
- AIX，200
- syslog 协议的警报级别，588
- `alias` 语句，用于 Apache，511
- `alias`，配给网卡，84，以及输出连接，164
- `ALL EXCEPT` 选项，在 `login.access` 中，197
- Apache `ALL` 选项，509，在 `login.access` 中，197，在 TCP wrappers 中，267, 268
- `AllowGrows` 变量，用于 SSH，444–445
- `Allowoverride` 关键字，用于 Apache，510，用于虚拟主机，519
- `Allowcpforwarding`，用于 SSH，443
- `Allowusers` 变量，用于 SSH，444–445
- 屏幕标志变量，86
- Alpha 服务器，7
- amd64 平台，34
- 匿名 FTP 服务器，526
- 反垃圾邮件黑名单，473, 485–486
- `a.out` 格式，357
- Apache Web 服务器，500–506
  - 配置文件，501
  - 控制，521
  - 核心配置，501–503
  - 目录与权限，507–515
  - HTTPS 网站，520
  - 包含其他配置文件，515–516
  - 日志，503–505
  - 模块，398–506
  - 密码保护，517–519
  - 虚拟主机，521
  - `apachectl` 程序，521
- 应用二进制接口 (ABI)
  - 重新实现，363
  - 支持，364
- 应用程序，148
- `apropos`，用于 man 搜索，23
- 架构，FreeBSD 构建的
  - 差异，399
- 归档
  - 检查内容，101–102
  - 列出文件，95
  - 恢复文件，从 102–103
  - 恢复文件系统，103
- Areca，542
- ARP 平台，140
- ARP (地址解析协议)，446, 160
  - `arp -a` 命令，160
- ASCI 文件传输，523
- 星号 (`*`)，在 crontabs 中，464
- FFS 中的异步手段，219
- 异步传输模式 (ATM)，147
- AT&T，与 BSD，24
- AT UNIX，364
- ATA 磁盘驱动器，编号，212
- `atatamican` 内核模块，230
- `atime`，229
- ATM (异步传输模式)，147
- 原子时钟，448
- 附加规则，用于 `devdt`，257
- 审计组，194
- 认证设施，587
- `AuthConfig` 覆盖，在 `it.conf` 文件中，510
- 身份认证
  - PAM (可插拔认证模块)，310
  - Radius 用户认证，513–515
  - 使用 SASL，491–493
- 权威名称服务器，412
  - 链式，415
- `auth` 组，194
- `authpriv` 设施，587
- `AuthRadiusCache` 选项，用于 Apache，514
- `AuthRadiusCacheTimeout`，用于 Apache，514
- `autoboot_delay` 变量，70
- 自动登录插件，用于 FreeBSD，634
- 系统崩溃后的自动重启，638, 642
- 可用内存，启动信息中的列出，77

# B

- 后台 `fck`，81, 223–224
- 回溯，643–645
- 镜像备份服务器，565
- 备份
  - 磁盘禁用的，538
  - 安装驱动器前，240
  - 从中提取文件，95
  - `nerkel`，128
  - 同一情况下的多个，105–106
  - 旧版本软件的，407
- 程序
  - `dump-`，98–101
  - `tar`，97
  - 从中恢复，101–104
  - 磁带卷绕，91
  - 切片表，533
  - 指定磁带驱动器，用于 96
  - 系统的，90
- 页面，90-
- 带宽，571
- PF 控制，276
- 头部设置，用于 SSH，444
- 进制2，150
- `BASE638` 选项，用于 FreeBSD，632
- `bash-shell`，安装，537
- 基本输入输出系统 (BIOS)，62
  - 设置为从 CD 启动，45
- `beastie` 变量，70
- Beck, Hob，487
- Begemont SNMPD (`bsnpd`)，598–602
- 互联网名称守护进程 (BIND)
  - `chroot` 环境，437
  - 配置文件，423–424
  - 主/从服务器，423
  - 安全，436
- 伯克利软件发行版 (BSD)，2–3
  - 许可证，3
- 版本控制中的最佳实践，106
- 大锁 (BGL)，345
- `/bin` 命令 (FTP)，523
- 命令中的 `/bin` 目录，64–65
- `bin` 组，194
- `/bin/sh` shell，58, 64
- `/bin/tsh` shell，58, 64
- 二进制文件，格式，357
- 品牌，364
  - 识别与设置，367
  - 文件传输，523
  - 数学，150–151
  - 更新，378–380
  - 数值，作为值，121
  - BIND (伯克利名称守护进程)
- 伯克利名称守护进程 (BIND)
  - `bin` 组，194
  - 网络绑定到端口，157
  - BIAS (基本输入系统)，62
    - 设置从 CD 启动，45
  - `bist`，150
  - 黑名单，473, 485–486
  - 空闲系统的屏幕，85
  - `blanktime` 变量，85
  - FreeBSD-current 的激进版本，373–374
  - 块大小，41, 236–237
  - 磁盘阻塞，574
  - FFS 中的块，217
  - `BRSIZE` 变量，216
  - 蓝牙，302
  - 启动块，62
  - 启动 CD，准备，47–48
  - 启动镜像，549–550
  - 软盘，准备，47
  - 网络无磁盘，607
  - 启动服务器，609
  - 启动媒体，45–46
  - 备内核，137–138
  - 启动默认文件，68–69
  - 启动配置，69–70
  - 启动提示符，67–68
  - 启动内核模块，125–126
  - 多用户启动，79–88
  - 启动串口控制台，70–75
  - 单模式用户，63–66
  - 启动信息，76–79
  - FreeBSD 的可启动 CD，630
  - 可启动磁盘，标记，229
  - `/boot/loaders/loader.file`，68–69
  - `/boot/kernel` 目录，119, 124
  - `/boot/kernel` 目录，67
  - `/boot/kernel` 良好目录，128
  - `/boot/kernel-old-version` 目录，128
  - `/boot/loader.conf` 文件，69–70
  - 禁用缓存，从 72
  - 启动 `load_kernel` 模块，549
  - 启动可调优 `sysctls`，123
  - 启动元组，609
  - `boot_verbose` 变量，70
  - 网络，179
  - BOOTP (互联网引导协议)，607
  - 瓶颈，586
  - 使用 `vmstat` 分析，571–574
  - 磁盘速度，作为 574
  - 输入/输出，作为 570
  - 定位，570
  - 边界消息，469
  - 分支端口，405
  - 品牌二进制文件，识别与设置，367
  - `bsmnd` 的桥接模块，602
  - 广播地址，155
  - 广播池，以太网，作为 159
  - BSD (伯克利软件发行版)，2–3
    - BSD 4.4-Lite，4
  - BSDStats 项目，7
  - `bdtvar`，94
  - `bsmnpd` (Begem SNMPD)，598–602
  - `bsmnpd` 配置，602
  - 缓冲区溢出，178
  - 缓冲区：用于传入连接，174–175
  - 缺陷跟踪系统 (GNATS)，647
  - 构建状态，跟踪，338
  - 构建 FreeBSD，388–396
  - 构建 GENERIC 内核，388
  - 构建 `buildworld` 命令，388–389
  - 使用并行构建优化，390
  - 为 us 安装准备构建，390–393
  - 构建名称服务器，422–424 `turn` 命令，48
  - 字节，152
  - `zip` 压缩，97

# C

- CA (认证机构)，282
- 缓存内存，577, 578
- 缓存与名称服务切换，450–453
- 缓存零，452–453
- 货币符号 (`$`)，用于环境变量字段，200
- CAT5 线缆，159
- 问题报告中的 Category 字段，651
- CD 镜像，查看内容，235
- CD 包，322–323
- `cdtools`，226
- 从 CD 启动，45, 46
- 像磁盘一样，15
- 从安装 FreeBSD，46–47
- 用于 ISO 9660 文件系统，230
- 准备启动，47–48
- 使用 FreeBSD 购买，43
- 中央处理器 (CPU)
  - 对 FreeBSD 的支持，
  - 信息显示，在启动信息中，76–77
  - 系统负载，576
  - 多个，143, 344–349
  - 要求，36
  - 以及 SMP，347–348
  - 使用与性能，583–584
  - `vn` 开启，573
- 认证为 Unix，9
- CERT 目录，44
- 认证机构 (CA)，282
  - 证书，282–285
  - 创建请求，283
  - 获得，284
  - 已经签名的，285
  - 用于 SSL 服务器的，，520
  - `CFLAGS` 选项，在 `/etc/make` 中，307
  - 密码，用于证书，284
  - 配置文件，用于内核，318
  - 检查，112–113
  - 校验和，333
  - `chflags` 命令，203
  - `chroot` 命令，193
  - 切换账户，185–186
  - 切换到，268
  - 切换到单用户模式，63
  - 冲突文件，270
  - CIFS (Common File Sharing)，286
  - 类，175
  - A 类网络，153
  - B 类网络，153
  - C 类网络，153
  - 集合，338–339
  - 冲突，35
  - 崩溃 dump，65
  - 自动备份，640
  - 配置，640–641
  - 捕获，642–643
  - 模式，用于 `tar`，95
  - 命令行，628
  - 插件，634
  - 冲突，639
  - 交叉构建，FreeBSD
  - 密码学密钥，在 GELI 中生成和使用，559–560
  - 兼容性选项，用于内核，133, 369
  - `compat.linux_ioctl`，673
  - 编译程序，316–317
  - 压缩 `tar` 包，97
  - 压缩
    - 文件，97
    - 日志文件，596
  - 计算机资源，性能和，570
- `cust_pkg` 脚本，628
- CVS (并发版本系统)，382
- `CVSetup` 服务器
- 本地构建，399–402
- 访问控制，402
- `CVSetup` 工具，382
- `COFLAGS` 选项，位于 `/etc/make.conf`，307
- 驱动程序中的柱，530
- Cyrus IMAP，494
- `debug.min_idsyncl`，672
- `debug.witness_skipsyncl`，672
- `debug.witness_watchsyncl`，672
- 小进制数学，151
- 默认接受，vs. 默认，264–265
- 在数据过滤中，273–274
- 默认 BSD 分页器 (`more`)，23
- 默认类，197
- 默认配置，拷贝，风险，来自 69
- 默认文件，68–69
- 默认组
  - 在 FreeBSD 中，194
  - 用于用户账户，181, 183
- 默认主机，518
- 默认路由，163
- 默认类设置，位于 `adduser.conf`，183
- 默认组设置，位于 `adduser.conf`，183
- `DEFAULTS.file`，用于内核配置，129
- 守护进程工厂，587
- 守护进程组，194
- `daemon` News，26
- `DAEMON` 证明程序，用于 `rc` 脚本，352
- `dedaemons`，用于非特权用户账户，262
- 镜像磁盘的每日状态检查，550
- 期间的 `daily_local` 变量，311
- 期间的 `daily_output` 变量，310
- 期间的 `daily_badconfarg` 变量，311
- 期间的 `daily_win_info` 变量，311
- 期间的 `daily_status_success` 变量，310
- 美国国防研究计划局 (DARPA)，2
- Darwin，8
- 共享，394
- 用户账户，188
- `data` 命令，471
- 数据损坏，来自将脏的分区挂载为读写，224
- 数据，从操作系统中分离，41
- 数据库
- 用于 Sendmail 文件，480
- 关机，88
- 三路镜像，550
- 数据链路层，在 OSI 中，146–147, 159
- `datasize` 变量，位于 `login.conf`，199
- 日期，将 epoch 秒转换为，298
- `dio` 提示，642
- `DBq-RJ4` 转换器，73
- `dd` 命令，47, 236–237
- 去激活加密磁盘，560–561
- 致命死锁，346
- syslog 协议的调试级别，589
- `debug.debugger_on_panic` 同步，672
- 调试
  - 启用，80
  - 内核，641–642
  - Linux 模块，368–389
  - 准备系统以便在崩溃后提供信息，639–640
  - `rc` 脚本，353–354
- `DenGroups` 变量，用于 SHA，444–455
- `Denusers` 变量，用于 SHA，444–455
- 修改，408
- 使用 `portmaster` 检查，408
- 用于软件软件包，325
- 卸载软件包和，328
- 字段，位于问题报告中，651, 653
- 拆离规则，用于 `dev`，257
- `/dev/console` 设备，604
- `dev` 命令，256–260
- 配置，257
- 开发者属性，42
- `devs` 文件系统，238–253–260
- `dev` 设备消息，93
- 设备驱动程序
  - 开发，35
  - 启动消息中的条目，77
  - 内核选项，134
  - man 页面，27
  - `sysctl` 标志，123–124
- 设备文件系统，238
- 设备名称，27
- `ofloppy` 驱动器，47
- 用于根分区，64
- 设备节点，79–212
- 用于管理的 `devis` 文件系统，253–260
- 用于动态设备，256
- 以及可移动媒体，230
- 或磁带驱动器，91
- 设备未配置消息，92
- 设备标准，位于内核配置文件中，129
- `/dev/ttyd` 设备，604
- `/dev/tvp` 设备，604
- `/dev/tvdb` 设备，604
- `/dev/zero` 设备，236
- `df` 命令，215–217
- DHCP (动态主机配置协议)，49, 101, 165, 456–459
- 配置，55
- 磁盘系统的服务器设置，306–609
- `ddhcp`
- 拨号器组，194
- 拨号终端，604
- 字典攻击，482
- `diff` 模式，96
- `dig` 命令，414–418
- `aerf` 查询，436
- 禁用递归，416–417
- 查找主机名，在特定的 DNS 服务器上，417
- 数字证书，282
- 目录
  - 用于 Apache，507–515
  - 选项，508–510
  - 列表，509
  - 显示磁盘用法，216
  - 导出，246–247
- 目录服务，针对第三方，513
- 目录声明，用于 Apache，551
- 脏磁盘，在 FS 中，222–224
- 域名 (domains)
  - 虚拟，481–483
  - 名称中的点 (`.`)，用于隐藏文件，338
- 点点引号，用于配置接口，162
- Dovecot IMAP 服务器
  - 配置，394–495
  - 安装，494
  - 运行，496
  - SSL 证书创建，495
- 下载。另见 FTP 提示
- FreeBSD 更新，379
- DSA 密钥文件，441
- `duo` 命令，216
- 双控制台，72
- `dump`，640。另见 crash dump
- `swap` 空间，39
- `dump` 程序，94, 98–101, 643–646
  - 其中的级别，98–99
  - 从 101–104 恢复文件
  - 运行，101
  - 快速照，222
- 以太网双工设置，160
- DVDs。另见
- 文件系统，230
- 从安装 FreeBSD，46–47
- `Dvorkay` 键盘布局，82
- `dnic` 设备，用于管理的设备命令，256
- 动态主机配置协议 (DHCP)，49, 161, 156–459
- `dns` 服务器设置，607–609
- `dns` 名称服务器，422
- `$ENVIRONMENT` 环境变量，185
- 弹出可移动媒体，231
- 类型，91
- ELF 二进制文件，357
- 电子邮件
  - 灰名单，373, 487–491
  - 用于帮助，29–31
  - IMAP 和 POP3，493
  - 管理，86
  - 持久性，31
  - 响应，31
  - 发送，30–31
  - SMTP 邮件传输代理 (MTA)，470–472
  - 带有 SASL 的认证，491–493
  - 配置选项，476–481
  - 邮件服务器，472
  - 虚拟域名，481–483
  - 白名单，487
- 电子邮件地址，用于 Apache，502–503
- syslog 日志级别，588
- 员工安全，179
- 空查询，在 `reader.conf` 中，70
- 封装，149
- 加密磁盘，解密，560–561
- 文件系统，558–561
- 密码字段，在 `/etc/passwd.file` 中，187
- 公钥，280–286
- SSL 保护的端口，285–286
- OpenSSL 配置，281–282
- 环境变量字段，在问题报告中，651, 652
- 从 `cron` 运行的命令，464
- 转换为日期，298
- DNS 配置错误，436
- `errata` 分支，372–373
- `ERRATA` 目录，44
- 错误日志，用于 Apache，503–504
- 错误消息
- `/etc/adduser.conf`，182–183
- `/etc/amd.map`，302
- `/etc/bluetooth.conf`，302
- `/etc/bluetooth.device.conf`，302
- `/etc/crontab` 维护任务，586
- `/etc/*.conf`，303
- `/etc/defaults/bluetooth.device.conf`，302
- `/etc/defaults/devfs.rules`，255, 303
- `/etc/defaults/periodic.conf`，310–311
- `/etc/devf.conf`，79–87, 356
- `/etc/devd.conf`，305
- 闪磁盘，250–260
- `/etc/devfs.conf`，253–254, 303
- `/etc/devfs.rules`，255, 303
- `/etc/dhclient.conf`，309
- `/etc/directory`，301
- 在不同的 Unix 类系统中，302
- `/etc/disktab.file`，100
- `/etc/duplates.file`，244–245
- `/etc/feast.conf`，378–379
- `/etc/fstab.conf`，64, 212–213
  - 用于新磁盘，241
  - 无磁盘磁盘，614
  - 在 `inlineprofs` 中，367
  - 文件支持的系统，238
  - 用于 jails，292
  - 内存磁盘，234
  - 用于镜像启动驱动器，549
  - 可移动媒体，231
- `/etc/ftphpd.file`，525
- 列表中的组，525
- `/etc/ftpmd.file`，526
- `/etc/ftusers.file`，525
- `/etc/ftpasswd.message`，526
- `/etc/gg.exports`，502
- `/etc/group.file`，190–191
- 带有本地 DNS 解析器，422
- `/etc/hosts.allow`，263, 304
- `/etc/hosts.equiv.file`，304
- `/etc/hosts.ldp.file`，305
- `/etc/inetd.conf`，355–454, 524
- `/etc/libmap.conf`，360
- `/etc/localtime.file`，305
- `/etc/locate.rdc`，305
- `/etc/login*.file`，306
- `/etc/login.access.file`，195
- `/etc/login.conf`，197
  - 其中的设置，194
- `/etc/local.db.file`，184
- `/etc/mail/access.file`，476–479
- `/etc/mail/host-name.file`，476–481
- `/etc/mail/mailer.conf`，306, 474
- `/etc/mail/relay-domains.file`，476–480
- `/etc/mail/sendmail.cf`，306–309
- `hranking`，196
- `/etc/rc.conf`，79, 87
- `/etc/rc.file`，79, 487
- `/etc/netstart.script.conf`，65, 309
- `/etc/network.sub.conf`，309
- `/etc/newsyslog.conf`，309, 594–597
- `/etc/pf.conf`，275–277
- `/etc/pos.file`，311
- `/etc/phones.file`，311
- `/etc/portslave.conf`，403–404
- `/etc/ppth.file`，331
- `/etc/printcap.file`，312, 460–461
- `/etc/profile.file`，312
- `/etc/protocols.conf`，148, 312
- `/etc/pwd.db.file`，184

# F

- `/etc/scf.conf`，持续的网络守护进程，81–83, 207 网络选项，83–84 网络路由选项，84–85
- `fsc-client` 选项，244
- 其他选项，86–87
- `secure2nd` 和，206
- 在启动时启动 `lpd`，460
- 启动选项，80
- 开启 `nfs` 服务器支持，244
- 进入 `/etc/nfs.conf` 目录，87–88
- 进入 `/etc/nfs/statfile`，293
- 进入 `/etc/nfs/mounttables` 脚本，611
- 进入 `/etc/nfs/remote_file`，374
- 进入 `/etc/resolv.conf`
  - 默认本地 dns 服务器在，420
  - `nameserver` 列表在，421
- 进入 `/etc/spc.conf`，313
- 进入 `/etc/security/` 目录，313
- 进入 `/etc/services_file`，157, 167, 313
- 进入 `/etc/shells_file`，188–189, 313
- 进入 `/etc/spoold.conf` 文件，313, 600
- 进入 `/etc/spoold.db` 文件，184
- 进入 `/etc/sshd.conf`，312, 396
- 进入 `/etc/sshd_config` 文件，442
- 进入 `/etc/openssl.conf` 文件，281
- 进入 `/etc/sysctl.conf`，122
- 进入 `/etc/syslog.conf`，313, 589
- 进入 `/etc/termcap_file`，314
- 进入 `/etc/tty.file`，314, 606
- 以太网设备，335
- 以太网 (Ethernet)，147–158–160
  - 配置连接，116–
  - 作为设备，135
  - 速度和双工，160
- 以太网地址，160
- `Eudora_BSD` 的支持，493
- `ExCGI` 选项，用于 Apache，509
- `exit` 命令，用于 `script` 命令，114
- 过期值，于 `slave namemaster`，398, 451
- 导出
  - 跨网络导出磁盘设备，561–565
  - 重复目录，246–247
- NFS，243
  - 配置，244–245
- `ext2` Linux 文件系统，227
- `ext3` Linux 文件系统，227
- 额外目录，用于 Apache，516
- `xtra` 选项，用于 FreeBSD，633
- `extract extract` 命令，104
- 从备份提取文件，95
- 连接系统的失败尝试，83
- `filever`，176
- FAQ (常见问题解答)，25, 648, 659
- Fast EtherChannel (FEC)，175
- Fast File System (FFS)，2–217
  - 创建文件系统，229–230
- 内内核内部图，224
- 脏磁盘，222–224
  - 内核，选项，132
  - 挂载选项，220
  - 挂载类型，218–219
  - 使用软更新和日志记录，229–231
  - 关机同步，224
  - 写入缓存，221
- FAT 文件系统，226
  - 用于可移动介质，228–230
- 容错性，镜像磁盘的，547
- `vnstat` 实例，在，573
- `ucsfs` 文件系统，238
- `diff` 命令，229
- `dimage_exe` 工具，479
- 磁盘
  - 备份分区表，533
  - 在 FreeBSD 安装中的结构，50
  - 交互式媒体，534
  - 用于 NanoBSD 镜像，626
  - 用于将硬盘分为，620, 534–536
  - 使用查看分区表，532–533
- FEC (Fast EtherChannel)，175
- 获取依赖项，320
- `fetch extract` 命令，404
- `fetch update` 命令，404
- FFS. Fast File System (FFS)
  - 文件描述符系统，238
  - 文件标志，201–203
    - 限制性，296
    - 移除，203
    - 设置和查看，203
  - 文件所有权
    - 在 TFTP 服务器中，462
    - 使用查看，1, 193
  - 文件大小和日志轮，595
  - 文件传输，522–526
    - 二进制和 ASCII，523
  - FTP 客户端，522–523
  - FTP 服务器，524
    - 匿名，526
    - 消息，525–526
  - FTP 用户控制，524–525
  - `scp` 程序，527
  - 安全，522
  - `sftp` 程序，527
  - 文件备份系统，238
  - `Info` 覆盖，在 `.htaccess` 文件中，510
  - `FILE_LIST` 选项，用于 FreeBSD，633
  - 文件，16
  - 添加到 NanoBSD，628–429
  - 更改顺序和组，193
  - 转发邮件，478–179
  - `filesize` 变量，在 `login.conf` 中，199
  - 文件系统完整性检查 (`fsck`)
    - 文件系统表，212–213
    - `/etc/stab`，11
    - 自动修复，81
    - 从 `netboot` 启动，142
    - 创建 FFS，229–230
    - 当前已挂载，214
    - `dump` 提示符，98, 99–100
    - 加密，558–561
    - 在文件中，235–238
    - 创建空文件，236–237
    - 使用日志记录，554–575
    - 可访问，64
    - 挂载，214–248
    - `/etc/rc.conf` 中的选项，80–81
    - 填充和排序，612
    - 可移动介质，228–231
    - 恢复，103
    - 特殊用途，231–238
    - 内存文件系统，232–234
  - `SYSTEM` 提供者，用于 `rc` 脚本，352
    - 域邮件服务器，468–469
    - 手页，23
    - 按关键字，321–322
    - 按名称，321
    - 细粒度锁定，346
    - 公钥指纹，441–442
    - 来自客户端，445
  - 防火墙，275
    - 当前显示，279
    - 用于 TFTP，461
  - FireWire，内核支持，136
  - 字段，在问题报告中，652
  - 修复磁盘，114–115
    - 缩进标志，456
  - 闪驱动器
    - 拷贝 NanoBSD 镜像到，617–618
    - 使用 `devd`，259–260
    - 管理，256
    - 使用，616
  - 闪存设备，扩展，218–619
    - 从...启动，45
    - 格式化，228–230
    - 准备启动，477
    - 使用 FFS，229–230
- `fp` 位扩展，47
- `allowsymlinks` 选项，用于 Apache，209
- 字体，在控制台上，85
- 在脏磁盘上强制读写挂载，使用 FFS，224
- 外部文件系统，225–228
  - 软件库，365
- 忘记命令 (`sqlite`)，548
- Forward DNS，413
  - 转发邮件，478
- BSD 调度器，349
- FQDN (完全限定域名)，83
- FFS 中的碎片，217
- 法国，149
- 空闲内存，577
- FreeBSD。另见构建 FreeBSD：
  - 诞生，4–5
  - CD 组，编译包，323
  - 配置菜单，58–59
  - 历史，406
  - 开发，5–7
  - 文档项目，6
  - 内存，FAQ，25, 659
  - 强制使用串口控制台，72
  - FTP 站点，43–45
  - 信息资源，19
  - 管理，6
  - 手册，章节，22
  - `s` 代码库的读写权限，5
  - 最小化安装，315–316
  - 分区要求，536
  - `pot` 用户，11
- 端口集合 (Ports Collection)，317
  - 基于...构建的项目，8
  - 安全公告，180
  - 缩小，396–397
  - 特特定时间，596
  - 优势，10–111
  - 网站贡献，657
  - 它是什么，2–5
- FreeBSD 社区，655–656
  - 领导层，656
  - 参与，656–657
- FreeBSD Mall，26, 46
- FreeBSD 项目
  - 邮件服务器，467
  - 提交改进，646
  - 支持，657
- FreeBSD-current，373–374
- FreeBSD.org，25–28
- FreeBSD-questions，30–31

# I

- `i386` 平台，34
- 内存占用，39
- IBM，5, 9
- ICMP (网络控制消息协议)，147, 155
- 重定向，83
- `icmp_drop_redirect` 变量，83
- `cmp_log_redirect` 变量，84
- `$3` 字符串，113
- IDE 驱动，37
- 类型，90
- 设备节点，91
- 写入缓存，221
- 内核配置文件中的 `ident` 属性，129
- 系统字符串，修版本控制
- `ident` 协议，267
- `ifconfig` 命令，84, 161–162
- `alias` 命令，163–164
- 为网卡分配 IP 地址，162–163
- `name` 关键字，165
- 在 `/etc/rc.conf` 文件中的 `ifconfig` 语句，164
- `ifconfig echo` 变量，84
- `+IGMPcore`，408
- `login.conf` 中的 `isnoregen` 变量，200
- 图像文件拷贝到磁盘，47
- IMAP (互联网消息访问协议)，493
- 使用 SSL 测试，497–498
- `imap-wu`，204
- 用于 FreeBSD 的 IGMP 路径，632
- 不活跃内存，577
- `in-addr.addr`，418–419
- 网络上的入站流量，166
- Apache 的包含目录，516
- 虚拟主机配置在，517
- Apache 的 `Includes` 选项，509
- Apache 的 `IncludesNOEXEC` 选项，509
- 入站连接缓冲区：174–175
- `dump` 中的增量备份，998
- 端口目录的索引，329
- Apache 的 `Indexes` 选项，509
- `Atacace` 文件中的 `Indexes` 覆盖，510
- 内核的 `INET` 选项，132
- 内核的 `INET6` 选项，132
- `inetd` 守护进程，82, 453–456
  - 行为更改，456
  - 配置服务器，454–455
  - `/etc/inetd.conf`，453–454
  - jail 宿主机服务器上，288
  - 配置选项，56
  - 启动，455–456
- `inet_enable` 变量，82
- syslog 协议级别，589
- `info.file`，643
- `inodes`，217
- 输入，14
- 输入/输出作为瓶颈，570
- `top` 工具和，579
- `incsecure` 控制台，605–606
- `/etc/make.conf` 中的 `INSTALL` 选项，308
- 修改安装路径，339
- 安装媒体，46–147
- 带有描述的已安装包，329
- 端口更新，404–409
- 已安装的 World Web 数据，包括 CVS 服务器上的，401
- 安装 Denovo IMAP 服务器，494
- 端口，332–334, 337–338
- 软件包，325
- 用户态，193–395
- 安装 FreeBSD，493
- 添加软件包，56–67
- 添加用户，57–58
- 启动软盘准备，47
- 在无彩色系统上，615
- 专有的，35–36
- 要求，34–37
- 示例硬件，35
- 规划，33
- 安装后设置，58–59
- 安装前发行版，37–42
- 发行版选择，42
- 游戏，42
- 多硬盘，40–41
- 分区块大小，41
- 分区，37–40
- 进程，47–49, 59
- 内核的 `KERN` 变量，141
- 作为 `sysctl` 变量的索引，121
- 完整性恢复，280
- `Inet` 网卡，171
- 交互式恢复，104
- 互联网认证服务，513
- 互联网启动协议 (`BOOTOP`)，607
- 互联网控制消息协议 (ICMP)，147, 155
- 重定向，83
- 互联网消息访问协议 (IMAP)，493
- 使用 SSL 测试，497–498
- 互联网协议 (IP)，147
- 互联网软件联盟，422
- 异互网络包交换 (IPX)，147
- 可中断的 NFS 挂载，248
- `vmtstat` 上的中断，573
- 使用 `mtree` 进行入侵准备，296–299
- 达到，299
- 非自愿上下文切换，579
- `iostat`，571
- IP (互联网协议)，147
- IP 地址，152–155
- 添加到接口，162–163
- Apache 绑定到，502
- 分配，155
- 接口，84
- 通过控制 Apache 访问，507–508
- 为确定主机名，416–417
- FTP 安装信息，49
- 用于 jails，287
- 多个开启，163–163
- 不可用，155
- 限制，295–296
- 管理，294–295
- 用户的 NanoBSD，630
- 减少磁盘空间，291
- 用于运行 `named`，437
- 关闭，293–294
- 启动，293
- Java 许可证，322
- `jexec` 程序，294–295
- `jbd` 程序，294
- 作业控制，2
- 作业调度器 (`cron`)，463–466
- 用于常规端口，404
- 带有环境的，554–557
- Juniper，5, 616
- 垃圾邮件。另见
- 减少，485–486
- IP 过滤器，273
- 基于 IP 的虚拟主机，517–518
- IPFW，275
- IP6 地址，418
- 配置，55
- IPX (互联网包交换)，147
- IRIX (Silicon Graphics)，9
- ISA 卡，36
- ISO 格式，595
- CD 的文件系统，230
- ISO 镜像，名称，48
- `ISO` 目录，44
- 用于 FreeBSD 的 `PATH`，632
- IX 系统，46
- `KDB_UNATED` 选项，642
- Kerberos，246
- 内核族，587
- `kern.argmax` syscall，662
- `kern.bootfile` syscall，663
- `kern.bootline` syscall，662
- `KERNCONF` 值，136, 389
- `kern.coredump` syscall，665
- `-开发者接口`，438
- `kern.derlay` syscall，666
- `kern.domainname` syscall，662
- 内核，117–143
- 倒序操作，644–645
- `jail` 命令，291
- `jail` ID (JID)，294
- `jails`，286–296
  - 设置，290–291
  - 无磁盘客户端，610
  - 以及 `/etc/rc.conf`，293
  - 主机设置，287–289
  - `inetd` 守护进程，288
  - NFS 程序，289
  - `sshd`，289
  - `syslog` 守护进程，288
  - `jail` 设置，291–292
  - 以及内核，289–290
  - 假设，334–345
  - 备份，128
  - 启动元素，137–138
  - 编译，126–130
  - 附加组件，127
  - 配置文件，128–130
  - 故障排除，137
  - 调试，641–642
  - 定义，118–119
  - 当前启动的，121
  - 以及 jails，289–290
  - 网络容量，169–170
  - 无 选项，139
  - 设备关键字，139
  - 硬件软件特性列表，138
  - 内核，继续
  - 解决问题，139–140
  - 共享，140
  - `sysctl` 程序，119
  - 远程测试，141–142
  - 修剪，131–136
  - 基础选项，131–134
  - CPU 类型，131
  - 设备驱动程序，134
  - 多处理器，134
  - 伪设备节点，135–136
  - 可移动硬件，47
  - `minss` 选项，347
  - 内核转储，39
  - 内核模块，124–126
  - 加载和卸载，125
  - 启动时加载，225
  - 内核线程，359
  - 内核所有，用于 FreeBSD，632
  - `kern.fileadays` sysctl，662
  - `kern.hostname` sysctl，662
  - `kern.init_path` sysctl，664
  - `kern.init_shutdown_timeout` sysctl，663
  - `kern.ipc.maxipvake` sysctl，664
  - `kern.ipc.maxsockets` sysctl，664
  - `kern.mbcsockets` 值，171–172
  - `kern.numopensockets` sysctl，664
  - `kern.ipc.pipevmax` sysctl，663
  - `kern.shmall` sysctl，663
  - `kern.shmsys` sysctl，663
  - `kern.shm_use_phys` sysctl，663
  - `kern.somaxconn` sysctl，174, 663
  - `kern.log_console_output` sysctl，665
  - `kern.logsys` sysctl，664
  - `kern.maxfiles` sysctl，662
  - `kern.maxfilesproc` sysctl，663
  - `kern.maxproc` sysctl，662
  - `kern.proctid` sysctl，171–172
  - `kern.maxusers` sysctl，662
  - `kern.vorder` sysctl，662
  - `kern.metadlay` sysctl，666
  - `kern.module_path` sysctl，664
  - `kern.ngroups` sysctl，662
  - `kern.nodump_coredump` sysctl，665
  - `kern.openfiles` sysctl，664
  - `kern.osrelease` sysctl，662
  - `kern.posixversion` sysctl，662
  - `kern.random` sysctl，664
  - `kern.sched.name` sysctl，665
  - `kern.sched.preemption` sysctl，665
  - `kern.sched.quantum` sysctl，665
  - `kern.securelevel` sysctl，662
  - `kern.securelevel` 变量，87
  - `kern.securelevel_enable` 变量，87
  - `kern.smp.cpus` sysctl，666
  - `kern.smp.disabled` sysctl，665
  - `kern.smp_on_panic` sysctl，664
  - `kern.timecounter.choice` sysctl，665
  - `kern.timecounter.hardware` sysctl，662
  - `kern.timecounter.tsc_sysctl`，665
  - `kern.X/lib/files`，47
  - 密钥指纹，用于 SSH，441
  - 密钥自动检测，72
  - 选择列表输出，149
  - 将输入重定向到串口，71
  - 键盘映射，85
  - TCP wrappers 中的关键字，267
  - `kgdb` 程序，644
  - `kldstat` 命令

- 回环设备，135
- 接口，161
- IP 地址，421
- `lost+Found` 目录，222
- FAT32 媒体低级格式，229
- `lpd` 协议，460
- `lpr` 设施，887
- `lsist` 命令，用于查看所有和权限，193
- `lsdev` 命令，66
- `lsmod` 命令，67

- `make distclean` 命令，339
- `make extract` 命令，334
- `make fetch` 命令，333
- `make install` 命令，334, 337
- `make installkernel` 命令，389
- `make installworld` 命令，393–395
- `make kernel` 命令，389
- `make package` 命令，239
- `make pageselect` 命令，635
- `make patch` 命令，334
- `make print-index` 命令，320
- `make search` 命令，321
- `make` tool，315

# M

- MAC（媒体访问控制）地址，146, 160
- 用于 DHCP 客户端，607–608
- MAC 文件，用于内核配置，130
- Mac OS X，FreeBSD，在 8
- MAC 表，160
- `machdep.hyperthreading_allowed` 系统调用值，348
- 宏，在 `/etc/pf.conf` 中，276
- 磁性媒体，210
- 邮件交换器 (MX) 记录，432–433, 486
- 邮件设施，587
- `mail from:` 命令，174
- 邮件组，194
- 用于域查找的邮件服务器，468–469
- 中继控制，472
- `mailconf`，402
- 邮件列表别名用于，478
- 存档，26
- 包含在 CVSup 服务器上，401
- 用于 FreeBSD 开发，6
- 用于 FreeBSD 帮助，20–21
- 帖子的保留，到 31
- `mailgroup`，194
- `mailq` 程序，474
- `mailwrapper` 程序，474
- `make build` 命令，334
- `make kernelcommand`，389
- `make buildworld` 命令，388–389
- `make check-old` 命令，395–394
- `make checksum` 命令，333
- `make clean` 命令，408
- `make config` 命令，333
- `make configure` 命令，334
- `make delete-old` 命令，394
- `make depends` 命令，334
- 用于 NanoBSD，623
- `PREFIX` 变量用于，339
- 永久性选项，340
- 以及 SMP，349
- 用于升级 FreeBSD，398
- `MAKE_CONF` 选项，用于 FreeBSD，633
- `Makefile`，319, 320, 336–337
- 用于 OpenOffice，351–352
- 用于 Sendmail，484
- `MAKE_ERROR` 选项，用于 FreeBSD，632
- `MAKE_WORLD` 选项，用于 FreeBSD，632
- `MAKE_PREFIX` 选项，用于 FreeBSD，634
- `MAKEOPT` 选项，用于 FreeBSD，632
- `makeoptions` 准则，在内核配置中，129
- `malloc` 支撑的磁盘，232
- 创建，253
- `man` 命令，22, 24
- `man` 组，194
- `man` 页面，21, 27–28
- 管理信息库 (MIB)，用于
- `manpath` 变量，在 `login.conf` 中，200
- `maproot` 语句，246
- `mark` 家族，588
- 主引导记录 (MBR)，531
- 安装，52
- 主域，配置，427
- 主区文件，组织，用于 SSH，433
- 用户账户的最大资源限制，199
- `maxproc` 变量，在 `login.conf` 中，199
- `MaxStartups`，用于 SSH，444
- MBR (主引导记录)，531
- 阻塞，52
- `mbuf` 簇，170, 172
- `mbufs`，169
- 为...分配的内存，171
- `nd` 设备，136
- `dmnonfig` 命令，234, 235
- `mdmfs` 命令，232–233
- 媒体访问控制 (MAC) 地址，146, 160
- 用于 DHCP 客户端，607–608
- `media` 关键字，用于 `ifconfig`，162
- `mediaspt` 关键字，用于 `ifconfig`，162
- `MegaCli`，542
- `megarc`，542
- 成员组，58
- `buffer` 大小，577
- 磁盘，136
- 文件系统，232–234
- 限制，233–234
- 关闭，234
- 以及网络性能优化，171–173
- 使用程序，578
- 要求，37
- 用于获取**的 `top`，577–578
- 用法，583
- 关于 `vstat` 信息，572
- `vmsize` 变量，在 `login.file` 中，199
- 从当前合并 (MFC)，375
- `mergemaster` 程序，390–393, 395
- 元数据，217
- MFC (来自当前)，375
- `nget` 命令 (FTP)，523
- MIB (管理信息库)，用于 `sysctl`，120
- 管理协议 (SNMP)
- Microsoft FAT32 文件系统，225
- NET 用于 FreeBSD，499
- Unix 服务，460
- 用于拷贝镜像的工具，9
- 从 Windows 迁移到 FreeBSD，227
- `miller-gen`，487
- 访问控制列表，489–390
- 附加到 Sendmail，490–491
- 重试要求，490
- `mime_magic` 文件，用于 Apache，501
- `mime_type` 文件，用于 Apache，501
- Minimal Distribution，422
- `MINIMAL` 选项，用于 FreeBSD，633
- 最小生存时间，用于 `scale`
- `namaser`，430
- 条带磁盘镜像 (RAID 0+1)，544
- FreeBSD 的镜像，433
- 网站，25
- 跨网络镜像，565–567
- 主服务器，566
- 启动磁盘，549–550
- 每日状态，550
- 故障转移和恢复，567
- 修复，548
- `memorypass` 选项，201
- `mod_bandwidth` Apache 模块，506
- `mod_fastcgi` Apache 模块，506
- `mod_gzip` Apache 模块，506
- `mod_mp3` Apache 模块，506
- `mod_perl` Apache 模块，506
- `mod_ruby` Apache 模块，506
- `mod_webapp` Apache 模块，506
- 模块化内核，118
- 监控，516
- 系统安全，299–300
- Mosaic 浏览器，499
- `mount` 命令，64, 214
- 用于外部系统，225
- 用于 jailed 系统，557
- 挂载点，用于可移动媒体，230
- `mount` 命令，242–246
- `mountdisks` 插件，用于 FreeBSD，635
- `mounts`，242–243
- `mount_smbfs` 命令，251, 252
- `mouse`，86
- `mouse_enable` 变量，86
- `mouse_type` 变量，86
- `MOVEFILE`，用于 Ports Collection，319
- 移动到新驱动器，242
- `mdosfs` 挂载类型，226
- `MDOSFS` 选项，用于内核，133
- `msconfig` 文件，在 `adduser.conf` 中，183
- `mt` 命令，105
- 在磁带上的多个，105–106
- 磁带驱动器状态，92
- `mt erase` 命令，93
- `mt offline` 命令，93
- `mt retention` 命令，93
- `mt rewind` 命令，93
- 多个硬盘驱动器，40–41
- 处理器，344–349
- 多任务处理，344
- 多用户模式，升级自，
- 多用户启动，79–88
- `Multiview` 选项，用于 Apache，510
- `tutt`，30
- `/msvar/messages`，用于问题，29
- MX (邮件交换) 接收器，432–433
- `nanod.sh` 脚本，624
- NAT (网络地址转换)，147
- PF，以及 276
- 导航名称，23
- `nmsb` 关键字，在 `/etc/nsmb.file` 中，250
- `negative niceness`，585
- `gative time-to-live` 选项，452
- 嵌套 RAID，553, 555
- NetApp，616
- NetBSD，7, 11–82
- Netcraft，7
- 用于 `bsmmpd` 的 Netgraph 模块，692
- `net.ip.icmp.bcastecho` sysctl，669
- `net.ip.icmp.drop_redirect` sysctl，669
- `net.ip.icmp.implim` sysctl，669
- `net.ip.icmp.redirect` sysctl，669
- `net.ip.accept_sourceroute` sysctl，669
- `net.ip.check_interface` sysctl，669
- `net.ip.forwarding` sysctl，669
- `net.ip.port` sysctl，668
- `net.ip.portrange` sysctl，668
- `net.ip.portrange.first` sysctl，668
- `net.ip.portrange.hist` sysctl，668
- `net.ip.portrange.last` sysctl，668
- `net.ip.portrange.low` sysctl，668
- `net.ip.portrange.random` sysctl，668
- `net.ip.portrange.randomized` sysctl，668
- `net.ip.portrange.time` sysctl，668
- `net.ip.portrange.reserved` sysctl，668
- `net.ip.redirect` sysctl，669
- `net.ip.in.sourceroute` sysctl，669
- `net.ip.in.tti` sysctl，669
- `net.ip.tcp.keepalive` sysctl，670
- `net.ip.tcp.blackhole` sysctl，670
- `net.ip.tcp.delayed_ack` sysctl，670
- `net.ip.tcp.domain` sysctl，670
- `net.ip.tcp.local_slowstart` sysctl，670
- `net.ip.tcp.log_in` sysctl，670
- `net.ip.tcp.new_` sysctl，670
- `net.ip.tcp.recvbuf_auto` sysctl，671
- `net.ip.tcp.recvbuf_inc` sysctl，671
- `net.ip.tcp.recvbuf_max` sysctl，671
- `net.ip.tcp.recvspace` sysctl，173, 174, 670
- `net.ip.tcp.rfc1323` sysctl，670
- `net.ip.tcp.rfc3042` sysctl，670
- `net.ip.tcp.3390` sysctl，670
- `net.ip.tcp.sack.enable` sysctl，671
- `net.ip.tcp.sendbuf_auto` sysctl，671
- `net.ip.tcp.sendbuf_inc` sysctl，671
- `net.ip.tcp.sendbuf_max` sysctl，671
- `net.ip.tcp.sendspace` sysctl，173, 174, 670
- `net.ip.tcp.slowstart_flightsize` sysctl，670
- `net_inet.tcp.tso_sysctl`，671
- `net_inet.udp.blackhole_sysctl`，672
- `net_inet.udp.log_in_sysctl`，671
- `net_inet.udp.recvvspace` sysctl，173, 174
- `net_link.log_link_state_sysctl`，672
- `metmasks`，152–155, 162
- 十进制进制计算，154
- Netscape 公司，499
- `net-smiop`，600
- `netstat` 程序，166, 168–169
  - 用于查看用于网络的内核内存，169
- 网络
  - 适配器 `set` 组，175–176
  - 容量输入，169–170
  - 容量规划，173
- 网卡
  - 分配 IP 地址给，162–163
  - 内核中的设备驱动程序，134
  - 更改窗口大小，174–175
  - 冲突，166
  - 当前活动，166–167
  - 守护进程，在 `/etc/rc.file` 中，81–83
  - 设备，配置，54–56
  - 磁盘设备的导出，361–565
  - 文件系统，243–248
  - 网关，56
  - 组，194
  - 列出标识程序到，207
  - 层，146–148
  - 最大并发连接，173–174
  - 跨磁盘镜像，565–567
  - 备份服务器，565
  - 主服务器，566
  - 一生一次的负载与标准负载，173
  - 优化性能，170–175
  - 硬件的，170–171
  - 内存使用，171–173
  - `/etc/rc.file` 中的选项，83–85
  - 性能，571
  - 轮询，174
  - 在实践中，148–150
  - 安全模式，205
  - 服务器，绑定端口，157
  - 服务，FreeBSD 作为平台，11
  - 单用户模式下，65
  - 启动守护进程，207
  - 时间，447–450
  - 同步，449–450
  - 流量控制，263–264
- 网络地址转换 (NAT)，147
- PF 和 276
- 网络配置界面，555
- 网络文件系统 (NFS)，243
  - 客户端，限制，247
  - 启用客户端，245–246
  - 启用服务器
  - 导出，243
  - 配置，244–245
  - 多个目录，246–247
  - 内核选项，133
  - 性能与选项，247–248
  - 无盘用户态空间上的服务器，609–610
  - 以及用户，246
- 网络接口
  - 添加 IP 到，162–163
  - 显示列表，161–162
  - 列出 IP 地址，163–164
  - 重命名，164
  - 测试，163
  - 测试配置，166
- 网络邻域 (Windows)，248
- 网络时间协议 (NTP)，448–450
- `NETWORKING` 协议，用于 `rc` 脚本，352
- `newfs` 命令，103, 229
  - 以及加密设备，560
  - 用于在文件上创建文件系统，237
  - 日志记录与，556–557
  - 用于软更新，546
  - 用于 UFS 系统，140–541
- `newfs_mdos` 命令，229
- 新闻家族，588
- 新闻组，194
- `newslog` 程序，594
  - 以及 Apache 日志，504
  - syslog 示例条，597
- 下一代 RC 脚本 (`reNG`)，87
- `nextboot` 命令，141
- FS (网络文件系统)。请参见 网络文件系统 (NFS)
- `FS` 客户端选项，用于内核，132
- `nfsd` 程序，289
- `FS` 选项，用于内核，132
- `nice` 命令，在 `tsh` shell 中，585
- `nice` 进程，577
- `nicness`，用于重新初始化，584–586
- 任天堂 GameCube 模拟器，563
- `nmbuchers`，172
- "用户不存在"，向邮件发送者返回消息，482
- `noascym` 方法，219
- `naseime` 挂载选项，220
- `noase` 文件系统挂载选项，212
- `nobody` 账户，263
- `nobody` 组，194
- `NO_BUILDER` 选项，用于 FreeBSD，633
- `NO_BUILDWORLD` 选项，用于 FreeBSD，633
- `NO_COMPRESSDF5` 选项，用于 FreeBSD，634
- `nodump`，101
- `NOERROR`，在 `dig` 响应中，415
- `noexec` 挂载选项，220
- `nogroup` 组，194
- Nokia，5
- `nolog` shell，192
- `login` 变量，用于 `login.conf`，200
- `match` 规则，用于 `dev`，257
- `none` level syslog syslog，289, 590
- `None` 选项，用于 Apache，308
- `None` override，用于 `it.class`，351
- `nonemption`，来自 `cryptystems`，280
- `normal` 性能，定义，571
- `nosymfollow` 挂载选项，220
- `notice` level syslog syslog，588
- `notify` 规则，用于 `dev`，257
- `NS` 记录，431
- `name query`，451–453
- `nslookup`，414
- NTFS，226–227
- 权限，220
- NTP (网络时间协议)，448–450
- `ntp` facility，588
- `ntpd` 程序，447
- `time correction`，149
- `for serial console`，73
- Nvidia，335
- `OK` (`loader` 提示)，66
- `opa`，值，121
- open source software，机制，20–21
- OpenBSD，7, 11–12
- OpenOffice.org 办公件，13, 325, 331
- OpenRADIUS，513
- OpenSolar，8, 227
- OpenSSL，442, 445
- OpenSSL 配置，281–282
- `openssl-client` 命令，496, 497
- 操作系统 BIOS，62
- `download with TFTP`，461
- `running software from other`，86–87, 361–365
- `separation data`，41
- O'Reilly BSD 开发中心，26
- OSI 网络协议栈，146
- `outbound traffic`，在网络上，166
- `outgoing connections`，以及别名，164
- `overlap`，在 ABI 实现中，363
- `ownership device`，254
- `of file`，193
- `of log file`，594
- `of non-Unix` 文件系统，228
- `PACKAGEENVIRONMENT` 变量，用于 `pkg_add`，326
- `packages` 软件软件包
- `PACKAGESITE` 变量，331, 339
- `packet filtering`，272–280
  - `activating rules`，279–280
  - `configuring`，275–277
  - `default accept` 和 `default deny`，273–279
  - `rule sample`，278–279
  - `with SNMP`，600
  - `and itself inspection`，274–275
- `packet normalization`，在 `/etc/conf` 文件中，276
- `packet sniper`，以及 `telnet`，440
- `packets`，149
- PAE (物理地址扩展)，139, 142–143
- “未找到页面”错误，512
- `pages of memory`，572
- `paging`，581–582
- `vmstat` 信息，572–573
- PAM (可插身份验证模块)，310
- `panic` 函数，644–645
- `panics` 原因，637–638
- `configuring computer to`，639
- `manual crash dumps`，642–643
- `recognizing`，638–639
- `responding to`，639–642
- `and serial consoles`，641
- `triggering in single-user mode`，645–646
- `parallel built`，optimization with，390
- `PARANOID` 关键字，在 TCP wrappers 中，267, 269
- `parent-child`，，580
- `parity`，542–543
- `partitions`，211–212, 531。参见 `root` 分区
  - `block size for`，241
  - `creating`，在安装期间，52–53
  - `slices`，536–537
  - `de-journaling`，557
  - `encrypted`，80
  - `/etc/stab` 文件条，241
  - `GELI` 加密，558–560
  - `for jails`，290–291
  - `mounting onto filesystem`，214–215
  - `replication of`，539–540
  - `restoring filesystem on empty`，103
  - `space remaining`，215
  - `unmounting`，215
  - `for backups`，95
- `passphrase`，284, 559, 560
- `password` 命令，64, 184–185
- `password_format` 选项，201
- `password` setting，在属性字段中，在 `/etc/master.passwd` 中，187
- `keyword` 在 `/etc/nmb.conf` 中，250
- `for Apache`，512–515
- `files on disk system`，615
- `for groups`，191
- `for single-user mode`，605
- `expiration dates`，186
- `file for`，184
- `patching system`，180
- `path to loaded kernel`，67
- `path` variable，在 `login.conf` 中，200
- `PC Weasel`，71
- `computer resources`，and，570
- `optimization`，`partitioning` and，380
- `problem solving`，570
- `system status`，575–779
- `tuning`，582–582
- `CPU usage`，583
- `memory usage`，583
- `periodic`，583
- Perl，323
- `physical layer`，OSL，146
- `physical address extension (PAE)`，139, 142–143
- `pid` ID，576
- `pidfile`，597
- `pinging IP addresses`，163
- `portability of FreeBSD`，10
- `portaudit` tool，340
- `porting`，361
- `portmaster` script
  - `checking all dependencies`，408
  - `initial setup`，405–406
  - `integrated customizations`，334–336
  - `track building status`，338
- `tor` transport protocols，157–158
- `closing`，207
- `connecting to SSL-protected`，225–286
- `information on`，166
- `for single-user mode`，65
- `for virtual host`，519
- `partitioning and`，38
- `options criteria`，in kernel configuration file，129
- 跟随，580-581
- 父子关系，580
- 优先级，584-586
- 顶部列表，578-579
- `stat` 统计，572
- 处理器。参见 中央处理单元 (CPU)
- `procs` 文件系统，238
- 以及连接，295
- 针对 Linux，367
- `PROFS` 选项，针对内核，133
- 生产系统，更改时钟，449
- 程序
  - 挂载共享库到，335–357
  - 编译，316–317
  - 禁用 `/etc/conf`，65
  - 转发邮件到，479
  - 识别正在监听的
  - 网络，207
  - 识别需要库的，394
  - 库需求，358
  - 按名称日志，590–591
  - 用于管理运行的脚本，353
  - 向发送日志消息，591
  - 项目事件 (Project Event)，63
  - 提示符命令 (FTP)，523
  - 专有硬件，35
  - 专有操作系统，12
- 协议
  - 拟合，157
  - 以及硬件，159–160
  - 在网络层中，146–148
  - GEOM 中的提供者，530
  - 代理组，194
- `PRUNE_LIST` 选项，针对 FreeSBIE，633
- PS/2 鼠标，设置，56
- `ps` 命令，294, 576
- 伪设备 (`pseudodev`)，129
- `PSEUFS` 选项，针对内核，133
- 伪匿名数字生成，随机
- 用于设备，135
- 伪终端，135, 604, 605
- `.pub` 文件扩展名，441
- 公钥加密，280–286
  - 证书，282–285
  - 连接到 SSL 保护的端口，285–286
  - OpenSSL 配置，281–282
  - 针对 SSH，441
- `put` 命令 (FTP)，529
- PuTTY，445
- `ps` 命令，脚本化，188
- PXE (预启动执行环境)，607
- 安装，45
- `pxboot` 文件，针对无盘客户端，609

# Q

- Qmail，473
- `qtd` (每日一语)，158
- 实现，444–455
- 问号 (`!`)，用于显示命令
- 针对加载器，66
- `quit` 命令，针对恢复，104
- 配额，针对磁盘空间，40

# R

- 机架式服务器，启动，45
- Radius 用户认证，513–515
- RAID (独立磁盘冗余阵列)，541–542
  - 硬件 vs. 软件，542
  - 嵌套的，553
  - 校验和和条带大小，542–543
  - 类型，543–544
- RAID-0 (条分)，543
  - 配置，545–547
- RAID-1 (镜像)，543, 570–550
  - 启动磁盘，549–550
  - 每日状态检查，550
  - 修复，548
- RAID-3 (带专用校验和的条分)
  - 磁盘，543, 550–553
  - 销毁，553
- RAID-5 (所有驱动器共享校验和的条分)，543–554
- RAM (随机访问存储器)，
  - 需求，27
- `ramambler` 搜索引擎，26
- 随机设备，针对伪匿名数字生成，135
- 随机密码生成器，182
- `rc` 脚本
  - 调试，353–354
  - 示例，351–352
  - 自排序，350
  - 特殊提供者，352–353
- `rc_variable`，80
- `rc_inet`，80
- `rcNG` (下一代 RC 脚本)，87
- 记录器，351
- `rc` 命令，破坏锁，112
- `rcdiff` 命令，110–111
- `README.TXT`，针对 Collection，319
- `README.TXT` 目录，44
- 只读
  - 模式，81
  - 针对 FTP 服务器，524
  - 在 FFS 中的挂载，218–219
- 读写挂载在 FFS 中，脏磁盘，224
- 实际内存，启动时的
  - 消息，77
- 实时流数据，UDP，156
- `#reboot`，466
- `#reboot` 命令，88
- 自动的，系统崩溃后，638, 642
- 重建，407–408
- `rect` 命令，471
- 递归查询，412
- Red Hat Linux，315
- 邮件，478
- 冗余
  - 在网络服务器中，175
  - 恢复到 RAID-3，551–552
- 冗余独立目录 (RAID)。参见 独立磁盘冗余阵列 (RAID)
- `Rearden`，273
- 刷新名称，服务器，430
- 精炼区域，335
- 拒绝文件，386
- 正则表达式，597
- 普通用户帐户，创建，57
- 重新安装部分，337–338
- `ReiserFS`，275
- 拒绝连接，195
- 转发控制，在邮件服务器中，472
- Release 工程团队，372
- `Release` 字段，报告中，651
- FreeBSD 版本，372–373
- `releases`，目录，44
- 重新加载命名空间
- 命名守护进程 (`rndc`)，434–435
- 命令，193, 434–435
- 远程打印机，459
- 远程过程调用 (RPC)，313
- 远程重置计算机，串口控制台，70–775
- 可移动硬件 弹出介质，231
- 内核支持，136
- 可移动媒体文件系统，228
- 切片分区，539–540
- 变量，在 `login.conf` 中，198
- `/rescue` 目录，65
- 研究，报告之前，647
- 保留端口，158
- 解析器，412
- 配置，419–421
- 名称服务器列表，421
- 资源限制，198–199
- 对挂起的响应，330
- `dump` 恢复程序，98–101
- 以及进一步备份，103
- 标签，533
- 切片表，533
- 保留带，93
- 重试要求，针对过滤器，490
- 重试值，430, 431
- `rdns dns`，533
- 区域，434
- 反向 IP 地址，418
- 递归控制，106–113
- 破坏块，112–113
- 返回，108–109
- 编辑文件，108
- 初始化，102–108
- 查看文件版本历史，110–111
- 查看日志，109–110
- 版本历史，110–111
- 回卷备份带，91
- `RIP` (路由信息协议)，85
- `rkhunter`，300
- `log` 命令，109
- `rmuser` (命名守护进程控制)，434–435
- 命令，193, 434–435
- `rndc-config` 脚本，434
- `zo` 文件系统选项，212
- 漫游用户，服务于，472
- 根目录，针对 `tftpd` 服务器，461
- 分区，38, 214, 537
- 设备名称，针对，64
- 在 `/etc/stab` 中，213
- 跨运行 `mtree`，297–298
- 在单用户模式下，64
- 密码，189–190
- 重置，65
- `rootfs-plugin`，来自 FreeBSD，635
- `troot_mount` 变量，81
- `rootfs`
- 运行时可调 `sysctl`，122
- `rw2` 文件系统选项，027
- 关机，350–354
- 来自供应商，353
- SCSI 驱动器，37
- 编号，238–239
- 带，90
- 设备节点，91
- 断开连接，238–239
- `$SCSI_DELAY` 选项，针对内核，133
- SCTP (流控制传输协议)，157
- `sldiff` 命令，392
- 搜索关键字，在 `/etc/resolv.conf` 中，421
- 区域，针对特定搜索，244
- 驱动器中的区域，210, 531
- 安全外壳 (SSH)，82，参见 安全外壳
- 安全套接层 (SSL)。参见 安全套接层
- 安全网站，520, 521
- 冗余，204–207
  - 定义，204–205
  - 限制，206
  - 默认，默认拒绝，246–255
  - 针对磁盘，610
  - 针对邮件服务器，552
- 冗余性，350–354
  - 在网络服务器中，175
  - 恢复到 RAID-3，551–552
- 冗余独立目录 (RAID)。参见 独立磁盘冗余阵列 (RAID)
- `Rearden`，273
- 刷新名称，服务器，430
- 精炼区域，335
- 拒绝文件，386
- 正则表达式，597
- 普通用户帐户，创建，57
- 重新安装部分，337–338
- `ReiserFS`，275
- 拒绝连接，195
- 转发控制，在邮件服务器中，472
- Release 工程团队，372
- `Release` 字段，报告中，651
- FreeBSD 版本，372–373
- `releases`，目录，44
- 重新加载命名空间
- 命名守护进程 (`rndc`)，434–435
- 命令，193, 434–435
- 远程打印机，459
- 远程过程调用 (RPC)，313
- 远程重置计算机，串口控制台，70–775
- 可移动硬件 弹出介质，231
- 内核支持，136
- 可移动媒体文件系统，228
- 切片分区，539–540
- 变量，在 `login.conf` 中，198
- `/rescue` 目录，65
- 研究，报告之前，647
- 保留端口，158
- 解析器，412
- 配置，419–421
- 名称服务器列表，421
- 资源限制，198–199
- 对挂起的响应，330
- `dump` 恢复程序，98–101
- 以及进一步备份，103
- 标签，533
- 切片表，533
- 保留带，93
- 重试要求，针对过滤器，490
- 重试值，430, 431
- `rdns dns`，533
- 区域，434
- 反向 IP 地址，418
- 递归控制，106–113
- 破坏块，112–113
- 返回，108–109
- 编辑文件，108
- 初始化，102–108
- 查看文件版本历史，110–111
- 查看日志，109–110
- 版本历史，110–111
- 回卷备份带，91
- `RIP` (路由信息协议)，85
- `rkhunter`，300
- `log` 命令，109
- `rmuser` (命名守护进程控制)，434–435
- 命令，193, 434–435
- `rndc-config` 脚本，434
- `zo` 文件系统选项，212
- 漫游用户，服务于，472
- 根目录，针对 `tftpd` 服务器，461
- 分区，38, 214, 537
- 设备名称，针对，64
- 在 `/etc/stab` 中，213
- 跨运行 `mtree`，297–298
- 在单用户模式下，64
- 密码，189–190
- 重置，65
- `rootfs-plugin`，来自 FreeBSD，635
- `troot_mount` 变量，81
- `rootfs`
- 运行时可调 `sysctl`，122
- `rw2` 文件系统选项，027
- 关机，350–354
- 来自供应商，353
- SCSI 驱动器，37
- 编号，238–239
- 带，90
- 设备节点，91
- 断开连接，238–239
- `$SCSI_DELAY` 选项，针对内核，133
- SCTP (流控制传输协议)，157
- `sldiff` 命令，392
- 搜索关键字，在 `/etc/resolv.conf` 中，421
- 区域，针对特定搜索，244
- 驱动器中的区域，210, 531
- 安全外壳 (SSH)，82，参见 安全外壳
- 安全套接层 (SSL)。参见 安全套接层
- 安全网站，520, 521
- 冗余，204–207
  - 定义，204–205
  - 限制，206
  - 默认，默认拒绝，246–255
  - 针对磁盘，610
  - 针对邮件服务器，552
- 冗余性，350–354
  - 在网络服务器中，175
  - 恢复到 RAID-3，551–552
- 重映射，360–361
- 版本，354
- `shell` 变量，在 `login.conf` 中，202
- `shells`，188–189
- 为用户账户更改，185
- 用于选择的内核选项，64
- 针对用户账户，182
- 针对用户，58
- `show` 命令，67
- 缩小 FreeBSD，396–397
- 关机，88
- 的 Apache，321
- `jails`，295–294–296
- 以及内存磁盘擦除，233
- 脚本，350–354
- 来自供应商，353
- `syncer` 位于，224
- 邮件中的签名，30
- 硅图形 (Silicon Graphics)，IRIX，9
- 简单身份验证与安全层 (SASL)，491
- 测试，493
- 简单设备，616
- 470–472
- 简单邮件传输协议 (SMTP)，
- 简单网络管理协议 (SNMP)，598–601
  - 客户端 (代理)，598
  - 管理信息库 (MIB)，598–600
  - 定义和浏览器，599–600
  - 安全性，600
- 单用户 Unix 规范 (Single Unix Specification)，9
- 单用户模式
  - 用于启动过程，63–66
  - 磁盘中的，64
  - 网络中的，65
  - 可用程序，64–65
  - `fs dict` 用于，114–119
  - `root` 命令行提示符中，605
  - 在其中触发 `panic`，645–646
  - 升级与，395–396
- 64 位计算，369
- 熟练的攻击者，179–180
- `s1` 设备，135
- 用于 IP 地址的斜杠选项，153
- 用于配置接口，162
- `shell` (`//`)，用于注释，424
- 配置从机域，426–427
- 睡眠的进程，576
- 切片表
  - 备份，533
  - 更改，533–536
  - 使用 `fdisk` 查看，532–533
- 切片 (`slices`)，211, 531
  - 创建，240
  - 使用 `fdisk` 将硬盘划分为，534–536
  - 分区，536–537
  - 复制的，539–540
- SLIP (串行线路互联网协议)，135
- 智能主机，用于，484–485
- SMB (服务器消息块)，249
- `smbfs.ko` 命令，240
- `smutil crypt` 命令，250
- `smutil login` 命令，250
- `snmp` 组，194
- `smp` (对称处理)，SMP
- 对称处理 (SMP)
- SMTP (简单邮件传输协议)，470–472
- `snappd` 文件代码，249
- 快照
  - 在 FFS 中，222
  - FreeBSD 的，375–376
- 快照目录，44
- SNMP (简单网络管理协议)，见网络管理协议 (SNMP) 334, 335
- SOA (区域起始，428–429)
- `sockstat` 程序，167–168, 207
- `Soekris`，138, 616
- 串口控制台速度，626–627
- 串口端口作为默认控制台，617
- 软更新，219–221
  - 与日志记录相比，555
  - 内核选项，132
- 软件
  - 查找，320–332
  - 通过关键词，321
  - 通过名称，321
  - 强制重建，407–408
  - 识别并统一，406–407
  - 识别无人运行的，406
  - 用于，316
  - 管理，10
  - 性能调优，586
  - 重新编译，362
  - 从其他操作系统运行，86–87, 361–365
  - 以及源代码，316
- 软件软件包，317–320, 321–
  - 也包括库
  - 添加，56–57
  - 到 NanoBSD，628
  - 购买，339
  - 在 CD 上，322–323
  - 从 FTP，324–325
- 软件软件包，续
  - 信息，329–330
  - 在无尽系统上，613–615
  - 带描述列已安装，329
  - 问题，330–331
  - 安装结果，327–328
  - 安全性，340–341
  - 卸载，328
- 软件串口控制台，71–72
- Solaris，8
- 为其重新编译软件，362
- 插件，用于，635
- 构建 FreeBSD，388–396
- GENERIC 内核，389
- 已安装用户，393–395
- `make build` 命令，388–389
- 使用并行构建优化，390
- 为用户态做准备，390–393
- 更新，387
- 用于升级 FreeBSD，382–387
- 分隔符，用于选择菜单，50
- 邮件服务器访问，472
- 拒绝源，485–486
- 垃圾邮件重传次数，490
- 垃圾邮件程序，487
- 垃圾邮件工具，以及 MX，469
- SPARC 服务器，7
- `spawn` 选项，用于 TCP，270–271
- 主规格，297–298
- 保存，298–299
- `spool` 驱动程序，用于打印机，461
- `SRC_config` 选项，用于 FreeBSD，633
- `DIR` 选项，用于 FreeBSD，632
- SSH (安全 Shell) 守护进程，122, 168
- 396–417
- 客户端，445
- 复制文件，446–447
- 配置，442–444
- 停止，440
- 用户管理，444–445
- SSH 密钥，用于无盘系统，614
- 登录，选项以配置，56
- 组，194
- `sshd` 脚本，88
- `ssh-keygen` 命令，441–442
- SSL (安全套接层)，282
- 连接受保护端口，285–286
- 主机密钥，283
- 用于 Web 流量，220
- `ssl_cert_file` 变量，用于 Dovecot，494–495
- `ssl_key_file` 变量，494–495
- 可堆模块，242–243
- `stacksize` 变量，在 `login.conf` 中，119
- `staff` 组，194
- 标准错误，14–15
- 标准输入，14
- 标准输出，14
- 区域起始 (SOA) 记录，428–429
- 启动。见启动过程
- `/etc/rc.conf` 中的选项，80
- 消息，76–79
- `/var/run/dmmsg` 用于，378
- 脚本，350–354
- 来自供应商，353
- 状态的，275
- 忠实检查，以及数据过滤，274–275
- 有状态协议，156
- 无状态协议，156
- 状态命令 (GEOM)，544
- 停止命令，用于服务，88
- 存储设备，节点用于，211
- 流控制传输协议 (SCTP)，127
- 流协议，156
- 字符串，值，121
- 镜像磁盘 (RAID-10)，544, 553–554
- 条带驱动程序，创建，546
- 条带化 (RAID-0)，543
- 配置，547–547
- 带有专用校验 (RAID-5)，550–553
- 跨越所有驱动器的校验 (RAID-5)，543
- `su` 命令 (切换用户)，189
- 子目录，显示块大小，216
- `sumit.fit.file`，483
- `sumit` 语句，用于 DHCP 客户端，458–459
- `Sysubset` 设置，用于 SSH，444
- Sun Microsystems，3, 8
- `sunset` 文件标记，202
- 超级用户密码更改，184–185
- 供应，383–384
- 示例，386
- 修改，384–385
- 用于升级 FreeBSD，398
- SVR (System V Release 4)，364
- 交换空间，212
- 分析，581–582
- 通过 GELI 加密，561
- 在 `/etc/fstab` 中，213
- `/etc/fstab` 条目，用于，241
- `/etc/rc` 文件设置，80
- 以及 `panic` 准备，640
- 分区，38–39, 537
- 在多个驱动器之间划分，4
- 以及性能，583
- 交换支持的磁盘，232
- 创建，233
- 插件式，用于 FreeBSD，635
- 切换用户命令 (`su`)，189
- 以以太网交换机，159
- 质量，171
- 版本化，354
- 符号，641, 644
- 符号链接，509
- 禁用，220
- 用于库，354
- 对称多处理 (SMP)，143, 344–349
- 当前实现，346–347
- 首次实现，345–346
- 进程与，347–388
- 使用，
- 伪造的 SYN-ACK 数据包，274
- 时间同步，448
- FFS 中的同步器，219
- 字段，在问题报告中，650, 652
- `sys` 组，194
- `sysctl` 命令，121
- 值，69, 661–674
- 更改，122–124
- 用于设备驱动程序，123–124
- 自动设置，122
- 用于硬盘，240–243
- 查看，121–122
- 用于升级，377
- 用于重新配置系统，59
- `syslog` 守护进程，587–593
- 自定义，592–593
- 日志级别，387–388
- 日志条目，194
- `Sysubset` 设置，用于 SSH，444
- `syslog_enable` 变量，82
- `syslog_flags` 变量，82
- `syslog_group`，194
- `syslog.conf`，用于无盘系统，614
- `syslog_remote` 变量，用于 SSH，444
- 状态，275
- 忠实检查，以及数据过滤，274–275
- 有状态协议，156
- 无状态协议，156
- 状态命令 (GEOM)，544
- 停止命令，用于服务，88
- 存储设备，节点用于，211
- 流控制传输协议 (SCTP)，127
- 流协议，156
- 字符串，值，121
- 镜像磁盘 (RAID-10)，544, 553–554
- 条带驱动程序，创建，546
- 条带化 (RAID-0)，543
- 配置，547–547
- 带有专用校验 (RAID-5)，550–553
- 跨越所有驱动器的校验 (RAID-5)，543
- `su` 命令 (切换用户)，189
- 子目录，显示块大小，216
- `sumit.fit.file`，483
- `sumit` 语句，用于 DHCP 客户端，458–459
- `Sysubset` 设置，用于 SSH，444

- 简易文件传输协议 (TFTP)，461–463
- 二进制文件的木马版本，防止替换，203
- 内核构建故障排除，137
- NanoBSD 构建，625–626
- 拒绝文件的结果，387
- `truncate` 命令，565
- `tunk` 端口，405
- `ttruss` 程序，368–369
- TTL (生存时间) (TTL) 组，194
- `tun` 设备，135
- 可调参数 (`tunnables`)，662
- 低层内核 vs. 运行时，123
- `turnables`，79
- 教程，25
- TCP wrappers 的 `twist` 选项，269–270
- 变量，271
- `tsupout` 程序，447

# U

- `uappnd` 文件标记，202
- `uchg` 文件，202
- UDF (通用数据格式)，226
- `udotdir` 设置，在 `udcf/file` 上，183
- UDF (用户数据协议)，147, 155–156
- 包装器和，265
- `ufs` (Unix 文件系统)，212
- UFS (Unix 文件系统)，217
- UFS2，快照功能，99
- `UFS_DMASH` 选项，用于内核，132
- UID (用户 ID)。设置用户 ID (UID)
- UFS 的 UIDs，端口集合，359
- ULE 调度器，349–350
- 访问控制列表，内核选项，132
- `umask` 变量，在 `login.conf` 中，200, 215, 231
- 针对外部系统，222
- `uname` 命令，`-a` 选项，29
- 可交付邮件，469
- 卸载端口，337–338
- 卸载软件包包，327–328
- 通用数据格式 (UDF)，226
- 协调时钟 (UTC)，447
- 加州大学，4
- Unix，2
- Unix 快速文件系统 (`ufs`)，212
- Unix 系统实验室 (USL)，4
- 类 Unix 系统，对比 vs. Unix，9
- 未知关键字，在 TCP wrappers 中，267
- `unload` 命令，68
- 在 GEOM 中，54
- 卸载内核模块，125
- 卸载磁盘，用于配置合并，547
- 卸载并弹出移动式介质，231
- 卸载分区，215
- 非特权用户，261–263
- 解压 (`untaring`)，95
- 更新服务器，380
- 阻塞更新，386–387
- 更新已安装的端口，404–409
- `UPDATING` 文件，用于端口集合，319
- 升级端口集合，403–404
- 升级软件，406–407
- 升级 FreeBSD，371–409
- 升级二进制更新，378–380
- 交叉编译升级，399
- 升级方法，377
- 升级步骤，11
- 以及单用户模式，395–396
- 通过源码升级，382–387
- 用于 `supsfiles` 和 `make` 的，398
- `sysabstall`，380–382
- 版本，372–373
- 决策，376–377
- FreeBSD-current，373–374
- FreeBSD-stable，374–375
- 发布，372–373
- 快照，375
- 测试，376
- `uptime`，统计信息，576
- USB 硬件
- 用于 FATES 文件系统，228–230
- 文件系统用于，230
- 内核支持，136
- 类型驱动，90
- 用户账户，181–188。还有 `root` 用户
- 更改 `shell`，185
- 创建，181–183
- 删除，188
- 编辑，183–188
- 用于 `jail`，292
- 用户命令，496
- 用户 `crontabs`，对比 vs. `/etc/crontab`，463
- 用户数据协议 (UDP)，147, 155–156
- 包装器和，265
- 用户发行，42
- 用户功能，588
- 用户 ID (UID)，181
- 用于管理员用户，192–193
- 在 `/etc/passwd` 文件中，187
- 用户映射，481–483
- 用户选项，Apache，510–511
- 用户目录，40
- 非特权，261–263
- 用户类字段，在 `/etc/passwd` 文件中，187
- 用户家目录，在 `/etc/master.passwd` 文件中，188
- 用户 `shell` 字段，在 `/etc/master.passwd` 文件中，188
- USL (Unix 系统实验室)，4
- 用户分区，40
- `user/bin/sendmail` 文件，474
- `user/sbin/linux`，366
- `user/bin/local` 目录，14
- `user/etc/dhcp.conf` 文件，457
- `user/etc/devdev.conf` 文件，494
- `user/etc/mail.conf` 文件，488
- `user/etc/script`，297, 350
- `user/local/directory`，356
- `user/share/devdev` 目录，495
- `user/share/freebie/conf`，631
- `ports/directory`，318
- `ports/emulators` 目录，363
- `ports/games_directory`，42
- `ports/INDEX-file`，320
- `ports/LEGA_file`，322
- `ports/mail/devdev` 目录，494
- `ports/mail/`，30
- `ports/mail/sendmail`，491
- `ports/net/cusip` 路由器，408
- `ports/security/nessus` 工具，300
- `ports/sysuts/lib` 工具，306
- `ports/vaw` 目录，500
- `user/share/sycons/directory`，85
- `user/share/sycons/keymaps` 目录，85
- `user/src/tools/script`，618
- `user/src/UTC` 文件，388
- UTC (协调时钟)，447
- `ucp` 功能，588
- `ucp` 组，194
- `unlink` 文件标记，203
- `vcp` 扩展，107
- `vcp` 分区，39–40
- `/var/crash` 目录，643
- `/var/db/pkg` 目录，327
- `/var/db/refuse` 文件，386
- 变量，662
- `loader`，67
- 在 `/etc/conf` 中，70
- `set` 命令更改，67
- `isyscl` 文件，119
- `/var/log/mail` 文件，476
- 用于 `Devocot` 事件，496
- `/var/log/messages`，84, 347
- 用于 DNS 配置，436
- `vmfugs` 插件文件，368
- `/var/run/dmxg_boot` 文件，63, 78
- 用于问题求解，229
- 被 `cape` 识别，90
- VAXes，7
- `verse` 日志，593
- 启动，63
- `tar` 的 `verbose` 模式，96
- `verbose_loading` 变量，69
- `Verigin`，282
- 版本号，在控制中，107
- FreeBSD，在启动消息中，76
- `Version`，442
- `vfs.dofs.doanyfree` sysctl，667
- `vfs.dofs.doreallcs` sysctl，667
- `vfs.nfs.nkleroot` sysctl，667
- `vfs.nfs.nkleispath` sysctl，667
- `vfs.nfs.valid_id` sysctl，666
- `vfs.usermount` sysctl，667
- `vfs.usermount` sysctl_variable，228
- `vi`，版本控制系统和，108
- 带有串口的视频卡，271
- `view` 命令 (和 `smbutil`)，251
- `Vigor`，185
- `pipw` 工具，186–188
- 域名主机，481–483
- Apache Web 服务器中的虚拟主机，517–519
- SSL 配置，520
- 虚拟内存磁盘空间，38–99
- 统计，571
- 虚拟节点 (`vnodes`)，218
- 关机时写入磁盘，224
- 虚拟终端，604
- `vnuses`，179
- `vmfile`，643
- 以及安全，645–666
- `vm.exec_map_entries` sysctl，666
- `vmstat` 程序，571–574
- 连续，574
- 使用，573–574
- `vm.swap_idle_enabled` syscl，666
- `vm.swap_idle_threshold` syscl，666
- `vm.swap_idle_threshold2` syscl，666
- `vm.v_cache_min` syscl，666
- `vm.v_cache_min` syscl，666
- `vm.v_free_min` sysctl，666
- `vm.v_free_reserved` sysctl，666
- `vm.v_free_target` sysctl，583, 666
- `vm.v_inactive_target` sysctl，666
- `vnode-backed_disks`，232
- `vnodes` (虚拟节点)，218
- 关机时写入磁盘，224
- 自愿上下文切换
- 警告，508
- 自，285
- 什么是，用于 174
- 哪里，349
- 白名单，487
- 窗口大小，用于 578
- Windows (Microsoft)，13
- 有线，249
- 只写模式，524
- 文本包装，在 TCP wrappers 中
- 写入缓存，用于 221
- 写入，207

# X

- X Window 系统，323
- 依赖项，328
- `X11forwarding`，用于 SSH，334–444
- `xaart-plugin`，用于 FreeBSD，635
- `xconfig-plugin`，用于 FreeBSD，635
- `xorg` 程序包，328
- `X-Kernel-Developer` 发行，9
- `X-User` 发行，42

# Y

- Yahoo!，5, 499

# Z

- ZEN 黑名单，486
- FFS，227
- 区域文件，428–434
- 点及其关系，433
- 示例，432
- 重载，435
- 次级名称服务器更新，序列号，430
- 区域传输，控制，436–437
- `named.conf` 中的区域，424

# 更新

请访问 `http://www.nostarch.com/abs_bsd2.htm` 获取更新、勘误和其他信息。

# 版后信息

《AbsoluteBSD》第2版使用 Adobe FrameMaker 进行排版。使用的字体族包括：正文使用 New Baskerville，标题和表格使用 Futura，大标题使用 Dogma。

本书在密歇根州安娜堡的 Malloy Incorporated 公司印刷并装订。纸张采用 Glatfelter Thor 50# Smooth，该纸张由 15% 的消费后内容制成。本书采用 RepKover 装订方式，使其在打开时可以平铺。

# FREEBSD：不再仅仅是 Alpha 极客的专属！

FreeBSD——这是一款强大、灵活且免费的 Unix 类操作系统——是许多企业的首选服务器。使用 Unix 或 Linux 都可能很棘手，而精通它们更为难。

《Absolute FreeBSD》第2版是你 FreeBSD 的方位指南，由 FreeBSD 委员会成员 Michael W. Lucas 撰写。Lucas 将这部里程碑式作品经过完全修订和重写的第二版视为他职业生涯的杰作；这是他热爱 FreeBSD 以及 FreeBSD 社区支持的真正产物。《Absolute FreeBSD》第2版涵盖了安装、网络、安全、网络系统、性能内核、调优、系统、SMP、升级、调试等许多内容，包括：

- 管理调度器、重映射共享库，并针对你的硬件和工作负载优化系统
- 使用嵌入式 FreeBSD 构建自定义网络设备设备
- 在没有特殊硬件的情况下实现磁盘冗余
- 将 FreeBSD 特有的 SNMP 协议集成到你的网络管理系统中
- 使用高级安全功能，如数据包过滤、虚拟机和基于主机的入侵检测
- 构建自定义的 FreeBSD Live 光盘和可启动闪存盘
- 管理网络服务和文件系统
- 使用 DNS 并为服务器和客户端设置电子邮件、IMAP、Web 和 FTP 服务
- 使用性能测试和故障排除工具监控你的系统
- 运行无系统（runless systems）

无论你是刚开始使用 FreeBSD，还是已经使用了多年，这本书将成为你一直期待的 FreeBSD 终极指南。

# 关于作者

Michael W. Lucas 是一位跨越西半球的网络工程师和系统管理员。他是 No Start Press 出版的广受好评《OpenBSD》、《Cisco Routers for the Desperate》以及《PGP & GPG》的作者。尽管来自密歇根州底特律，但他对汽车几乎一无所知。他使用 Unix 系统已超过 20 年，自 1995 年起使用 FreeBSD。幸运对我们其他人来说，他正忙于执行他统治世界的计划。
