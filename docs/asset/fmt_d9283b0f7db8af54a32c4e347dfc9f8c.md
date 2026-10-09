
### 系统配置参数说明

#### 内存管理

`vm.swap_idle_enabled: 0`

运行时切换开关。

`vm.swap_idle_threshold: 2`

运行时变量。

`vm.swap_idle_threshold2: 10`

运行时变量。设置 `swap_idle_enabled` `sysctl` 会告诉虚拟管理器比其他进程更快地将进程调入交换分区（`swap`）。该阈值 `sysctl` 决定了在考虑将不同类型的进程为空闲之前等待的秒数。默认值对大多数人来说足够了；只需启用 `vm.swap_idle_enabled` 即可解决问题。这可以帮助某些系统在内存极度匮乏并正在交换整个进程时维持运行。

`vm.exec_max_entries: 16`

启动时切换开关。这是可以同时启动的最大进程数。

#### 文件系统与磁盘

`vfs.diskless_valid: 0`

只读。如果为 `0`，则该系统未运行无磁盘模式。如果非 `0`，则系统正在运行无磁盘模式。

`vfs.diskless_rootpath:`

只读。这提供了无磁盘机器根文件系统的路径。

`vfs.diskless_rootaddr:`

只读。这提供了无磁盘机器根文件系统的 IP 地址。

`vfs.moviedirenable: 1`

运行时切换开关。允许 `UFS` 使用虚拟内存系统缓存目录查找，从而提高磁盘性能。

`vfs.usermount: 0`

运行时切换开关。如果启用，用户可以在他们拥有的挂载点上挂载文件系统。这允许无权限用户挂载软磁盘和 CD。参见第 8 章。

`vfs.fs.doasynfree: 1`

运行时变量。这告诉 `UFS` 文件系统在重新组织磁盘空间后异步更新索引节点（`inodes`）和间接块。

`vfs.fs.doreallocblks: 1`

运行时变量。默认情况下，`FreeBSD` 组织磁盘使得文件始终保持连续状态。实际上，`UFS` 在持续进行自我碎片整理。将此项设置为 `0` 以禁用此行为。

#### 网络配置

`net.inet.ip.portrange.lowfirst: 1023`

`net.inet.ip.portrange.lowlast: 600`

运行时变量。某些程序或协议要求从低号端口建立连接，这表明它们是由特权进程启动的。记住，发出的 `TCP/IP` 连接使用本地系统上的端口。还要记住，`0` 到 `1023` 的端口只能由 `root` 开启。这意味着如果连接来自低号端口，那么在理论上它正以 `root` 身份运行的（这涉及到信任发起连接的机器没有被入侵）。`FreeBSD` 使用介于 `net.ip.portrange.first`（默认值 `1023`）和 `net.ip.portrange.lowast`（默认值 `600`）之间的端口。我只知道一个更改此项有意义的实例：某些 `Intel` 网卡上的 `IPMI` 固件会拦截针对 `623` 和 `664` 端口的 `UDP` 数据包。如果你没有这些网卡，请保持原样。

`net.inet.ip.portrange.first: 49152`
`net.inet.ip.portrange.last: 65535`

运行时变量。当 `FreeBSD` 为无特权进程发出的连接分配随机端口时，它使用介于 `net.inet.ip.portrange.first`（默认值 `49152`）和 `net.ip.portrange.last`（默认值 `65535`）之间的端口。

`net.inet.ip.portrange.hifirst: 49152`
`net.inet.ip.portrange.high: 65535`

运行时变量。某些程序专门为出的连接请求高号端口。默认情况下，该端口范围与 `net.inet.ip.portrange.first`（默认值 `1023`）到 `net.ip.portrange.last`（默认值 `600`）之间的端口重叠，但你可以使用 `hifirst` 和 `high` `sysctls` 来分离它们。

`net.inet.ip.portrange.reservedhigh: 1023`
`net.inet.ip.portrange.reservedlow: 0`

运行时变量。这指定了只有 `root` 可以开启的端口范围。

`net.inet.ip.portrange.randomized: 1`

运行时变量。默认情况下，`FreeBSD` 会在该类型连接的范围内分配随机端口。

`net.inet.ip.portrange.randomps: 10`

运行时变量。这是每秒分配随机端口的最大数量。如果需要的端口更多，`FreeBSD` 将切换到顺序分配以避免耗尽系统随机性。

`net.inet.ip.portrange.randomtime: 45`

运行时变量。这是 `FreeBSD` 在恢复到随机端口分配前使用顺序分配的秒数。

`net.inet.ip.forwarding: 0`

切换开关。你可能希望 `FreeBSD` 作为路由器、网关或防火墙运行。设置此项后，系统会在接口之间转发数据包。

`net.inet.ip.redirect: 1`

运行时切换开关。设置此项后，作为路由器或网关的 `FreeBSD` 系统将向网络上的系统发送 `ICMP` 重定向数据包。如果系统未进行路由，则该项没有影响。

`net.inet.ip.ttl: 64`

运行时变量。这是任何 `ICMP` 协议跨越网络的最大跳数（`hops`）。

`net.inet.ip.sourroute: 0`

运行时切换开关。这开启了源路由（source-routed）数据包的转发。在公共互联网上，源路由通常被认为是一个坏主意。

`net.inet.ip.accept_sourroute: 0`

运行时切换开关。这开启了对源路由数据包的接受。如果你不知道源路由，在所有情况下都是一个坏主意。

`net.inet.ip.fastforwarding: 0`

运行时切换开关。此 `sysctl` 通过消除对数据包执行的大部分完整性检查以及完全消除数据包过滤规则来加速路由器和网关的吞吐量。

`net.inet.ip.check_interface: 0`

运行时切换开关。为你的服务器提供基本的反欺骗保护（antispoofing protection）。它仅在路由器上有用。

`net.inet.ip.implin: 200`

运行时变量。这是系统每秒响应的 `ICMP` 请求最大数量。需要的端口更多，`FreeBSD` 将切换到顺序分配以避免耗尽系统随机性。

`net.inet.ip.drop_redirect: 0`

运行时切换开关。这告诉 `FreeBSD` 忽略 `ICMP` 重定向。大多数情况下重定向可以提高性能。

`net.inet.ip.log_redirect: 0`

运行时切换开关。如果设置此项，`FreeBSD` 将所有 `ICMP` 重定向记录到控制台。

`net.inet.ip.bcecho: 0`

运行时切换开关。这开启了对广播地址的响应。这最初是为了符合标准。

`net.inet.tcp.rfc3223: 1`
`net.inet.tcp.rfc3042: 1`
`net.inet.tcp.rfc3390: 1`

运行时切换开关。这些开启了 `RFC` 中描述的各种 `TCP` 方法，应该是完全安全的。在启用这些项时，与非常老的系统通信可能会导致吞吐量缓慢或出现问题。

`net.inet.tcp.recvspace: 65536`

运行时变量。这些提供了新 `TCP` 连接的默认缓冲区大小。虽然 `FreeBSD` 根据远程主机的要求动态分配这些缓冲区，但这些值提供了一个良好的起点。虽然会在旧文档中找到更改这些值的建议，但今天应该保持原样。

`net.inet.tcp.log_in_vain: 0`

运行时切换开关。这开启了当端口没有监听时记录任何连接该 `TCP` 端口的尝试。在公共互联网上，这会产生大量的输出。建议在测试系统上启用此项以便看到哪些垃圾信息，然后将其关闭以便使用控制台。

`net.inet.tcp.blackhole: 0`

运行时切换开关。默认情况下，当你尝试连接关闭的端口时，`TCP/IP` 会返回错误代码。这显示为“对方重置连接”。如果你将其设置为 `1`，连接关闭端口的尝试将被丢弃而不发送错误。这会减慢端口扫描并为你的系统增加一些安全性。然而，它不能替代数据包过滤！

`net.inet.tcp.delayed_ack: 1`

运行时切换开关。这告诉 `FreeBSD` 尝试将数据包包含 `TCP ACK` 信息，而不是发送额外的数据包来信号连接结束。

`net.inet.tcp.recvbuf_auto: 1`
`net.inet.tcp.recvbuf_inc: 16384`

运行时切换开关。这开启了接收缓冲器的自动调整。

`net.inet.tcp.recvbuf_max: 262144`

运行时变量。这是自动调整改变接收缓冲器的增量。

`net.inet.tcp.slowstart_flights: 1`

运行时变量。这指定了 `FreeBSD` 在跨越广域网的 `TCP` 事务的慢启动阶段发送的数据包数量。

`net.inet.tcp.local_slowstartsize: 4`

运行时变量。这指定了 `FreeBSD` 在跨本地网络进行 `TCP` 事务的慢启动阶段期间将发送的数据包数量。

`net.inet.tcp.newreno: 1`

运行开关。此开关用于切换 `RFC2582` 连接恢复，也称为 `TCP NewReno` 算法。

`net.inet.tcp.tso: 1`

运行开关。某些网络硬件可以处理网络请求，将其转换为适合介质的适当大小的数据包。例如，对于某些网卡，`FreeBSD` 可以直接将数据块交给网卡并要求其将其分成数据包。这允许与网卡进行优化通信，并减少 `CPU` 的工作量。这告诉 `FreeBSD` 使用硬件执行支持的分段操作。

`net.inet.tcp.sendbuf_auto: 1`

运行开关。这启用了 `TCP` 连接发送缓冲的自动调整。

`net.inet.tcp.sendbuf_inc: 8192`

运行变量。这规定了每次需要更改时增加或减少 `TCP` 缓冲的量。

`net.inet.tcp.sendbuf_max: 262144`

运行变量。这是单个 `TCP` 发送缓冲的最大 own。

`net.inet.tcp.sack.enable: 1`

运行开关。`FreeBSD` 默认使用 `SELECT ACK`，但偶尔非常旧的主机在使用功能时会出现问题。

`net.inet.do_tcppdrain: 1`

运行开关。这告诉 `FreeBSD` 在 `mbufs` 内存不足时从重组队列中刷新数据包。现在 `FreeBSD` 会自动从内核内存分配 `mbufs`，这使得它的用性比以前小得多。

`net.inet.tcp.always_keepalive: 1`

运行开关。默认情况下，`FreeBSD` 会检查所有 `TCP` 连接以查看它们是否仍然活跃。通常情况下，如果两个主机之间的连接断开，这些心跳检测将告诉系统关闭连接。如果您禁用了此行为，`FreeBSD` 将不会检查主机之间的连接是开启还是关闭；相反，它将在无法传递数据之前假设连接是通的。

`net.inet.udp.log_in_val: 0`

运行开关。这会记录连接到没有任何程序在监听的 `UDP` 端口的尝试。

`net.inet.udp.blackhole: 0`

运行时开关。与 `TCP` 类似，当有人尝试连接到没有程序在监听的端口时，`UDP` 会发送一条错误消息。如果您将其设置为 `1`，连接已关闭 `UDP` 端口的尝试将被丢弃且不发送错误。这会减慢端口扫描。

`net.link.log_link_state_change: 1`

运行时开关。如果启用，`FreeBSD` 将在每次网络接口启动或关闭时记录日志。

#### 调试与安全

`debug.debugger_on_panic: 1`

运行时开关。如果设置，`FreeBSD` 将发生内核崩溃（panic）时进入调试器。

`debug.trace_on_panic: 0`

运行时开关。如果设置，`FreeBSD` 在发生内核崩溃并进入调试器后会自动打印堆栈跟踪（stack trace）。

`debug.witness.watch: 1`

运行时变量，启动时调优。在将 `WITNESS` 编译进内核后，`FreeBSD` 会对所有内核锁进行额外的完整性检查。将其设置为 `0` 可禁用这些检查。一旦关闭 `WITNESS`，在不重启系统的情况下无法重新开启它。请注意，当您禁用它时，将无法获得 `WITNESS` 的益处；具体来说，如果系统在重负载下由于锁问题发生内核崩溃，您将无法获得告知 `FreeBSD` 开发者在哪里找到问题的锁信息。

`debug.witness.skipspin: 1`

启动开关。这告诉 `WITNESS` 不要对自旋锁（spin locks）执行任何检查。使用 `WITNESS` 检查自旋锁会让几乎任何机器变得难以忍的缓慢。跳过自旋锁但在所有其他情况下使用 `WITNESS`，会让 `WITNESS` 仅变慢而不是变得无法忍受。这与内核选项 `WITNESS_SKIPSPIN` 相同。

`debug.minidump: 1`

运行时开关，可启动。默认情况下，`FreeBSD` 仅在内核崩溃时转储内核内存。将其设置为 `0` 在崩溃时转储物理内存的所有内容。

`hw.ata_ata.dma: 1`

启动开关。这启用 `IDE` 设备中的 `DMA`。如果您的硬件使用 `PIO` 而不是 `DMA`，请将其设置为 `0`。如果您的设备老旧到需要 `PIO`，您可能已经知道了。

`hw.ata_atapi_dma: 1`

启动开关。这启用 `ATAPI` 设备中的 `DMA`。如果您的硬件使用 `PIO` 而不是 `DMA`，或者您的硬件的 `DMA` 实现存在 Bug，请将其设置为 `0`。同样，如果您的硬件老旧到需要 `PIO`，您可能已经知道了。

`hw.ata.wc: 1`

启动开关。这启用某些硬盘支持的 `IDE` 写入缓存。写入缓存使用硬盘上的一个小缓冲区来缓存路由到磁盘的写入，以提高性能，但是以可靠性为代价的。设置为 `0` 以禁用写入缓存并增强数据安全。见第 8 章。

`hw.syscons.kbd_reboot: 1`

运行开关。启用此项后，传统的 `CTRL-ALT-DELETE` 序列将重启系统。将其设置为 `0` 以禁用此行为。

`compat.sysctl.osrelease: 2.4.2`

运行时变量。这定义了 `Linux` 模式支持的 `Linux` 版本。某些 `Linux` 程序在更改此值时会有不同行为。虽然您可以动态更改，但如果有任何 `Linux` 程序在使用，系统将发生内核崩溃。最好让 `Linux` 模式软件为您执行此操作。

`security.jail.set_hostname_allowed: 1`

运行时变量。这决定 `jail` 管理员是否可以更改其 `jail` 主机名。见第 9 章。

`security.jail.socket_uniproute_only: 1`

运行时变量。这控制 `jail` 所有是否可以使用 `TCP/IP` 以外的协议。见第 9 章。

`security.jail.sysvipc_allowed: 0`

运行时变量。这决定 `jail` 所有是否可以使用 `System IPC`。见第 9 章。

`security.jail.enforce_staffs: 2`

运行时变量。设置为 `0` 时，jailed 用户可以看到系统所有的（包括 `jail` 内外的）挂载点和分区。设置为 `1` 时，只能看到 `jail` 根目录下的挂载点。设置为 `2` 时，只能看到 `jail` 的根目录挂载点。

`security.jail.allow_raw_sockets: 0`

运行时变量。如果设置，`jail` 中的 `root` 可以创建原始套接字。见第 9 章。

`security.jail.chflags_allowed: 0`

运行时变量。

`security.jail.list:`

只读。这列出系统所有的（包括 `jail` 内外的）挂载点和分区。设置为 `1` 时，只能看到 `jail` 根目录下的挂载点。设置为 `2` 时，只能看到 `jail` 的根目录挂载点。

`security.jail.jailed:`

只读。这列出系统所有的（包括 `jail` 内外的）挂载点和分区。设置为 `1` 时，只能看到 `jail` 根目录下的挂载点。设置为 `2` 时，只能看到 `jail` 的根目录挂载点。

`security.jail.see_other_uids: 1`

运行开关。默认情况下，`FreeBSD` 会检查所有挂载连接以查看它们是否仍然活跃。

#### 索引参考

*   匿名 FTP 服务器, 526
*   反垃圾黑列表, 473, 485–486
*   `a.out` 格式, 359
*   `Apache` Web 服务器, 500–506
    *   配置, 501
    *   控制, 521
    *   核心配置, 501–503
    *   目录和权限, 507–515
    *   `HTTPS` 网站, 520
    *   包含其他配置文件, 515–516
    *   日志, 503–505
    *   模块, 398–506
    *   密码保护, 512–515
    *   虚拟主机, 521
    *   `apachectl` 程序, 521
*   应用程序二进制接口 (`ABI`)
    *   重实现, 363
    *   支持, 364
*   应用程序, 148
*   `apropos`, 用于页面搜索, 23
*   `FreeBSD` 构建架构
    *   差异, 399
    *   检查内容, 101–102
    *   列出文件, 95
    *   从中恢复文件, 102–103
    *   恢复文件系统, 103
*   `Areca`, 542
*   `ARP` 平台, 114
*   `ARP` (地址解析协议), 446, 160
    *   表, 160
*   `arp -a` 命令, 160
*   `ASCII` 文件传输, 523
*   星号 (`*`), 在 `crotasks` 中, 464
*   `FFS` 中的异步移动, 219
*   异步传输模式 (`ATM`), 147
*   `AT` 和 `BSD`, 254
*   `AT` 和 `UNIX`, 364
*   `ATA` 磁盘驱动器, 编号, 212
*   `atime`, 229
*   `ATM` (异步传输模式), 147
*   原子钟, 448
*   挂载规则, 针对 `dev`, 257
*   审计组, 194
*   `AuthConfig` 覆盖, 在 `it.conf` 文件中, 510
*   认证
    *   `PAM` (可插认证模块), 310
    *   `Radius` 用户认证, 513–515
    *   使用 `SASL`, 491–493
*   权威名称服务器, 412
    *   链式, 45
*   `authpriv`, 194
*   `authpriv` 设施, 587
