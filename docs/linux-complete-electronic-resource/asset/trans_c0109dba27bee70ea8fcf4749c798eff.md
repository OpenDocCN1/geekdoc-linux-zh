

在连接终止后以及执行连接脚本之前，会短暂断开 DTR（数据终端就绪）信号。在 Ultrix 上，此选项意味着硬件流控制，类似于 crtscts 选项。

**ms-dns** *<addr>* 如果 pppd 作为 Microsoft Windows 客户端的服务器运行，此选项允许 pppd 向客户端提供一个或两个 DNS（域名服务器）地址。此选项的第一个实例指定主 DNS 地址；第二个实例（如果提供）指定辅助 DNS 地址。（在某些旧版本的 pppd 中，此选项曾以**dns-addr**的名称存在。）

**ms-wins** *<addr>* 如果 pppd 作为 Microsoft Windows 或“Samba”客户端的服务器运行，此选项允许 pppd 向客户端提供一个或两个 WINS（Windows 互联网名称服务）服务器地址。此选项的第一个实例指定主 WINS 地址；第二个实例（如果提供）指定辅助 WINS 地址。

**name** *name* 将本地系统的名称设置为 *name*，用于认证目的。这是一个特权选项。使用此选项时，在查找用于对等方认证的密钥时，pppd 将使用 secrets 文件中以 *name* 作为第二个字段的行。此外，除非通过 *user* 选项覆盖，否则 *name* 将用作向对等方发送的名称，以将本地系统认证给对等方。（注意 pppd 不会向 *name* 附加域名。）

**netmask** *n* 将接口子网掩码设置为 *n*，这是一个 32 位“点分十进制”表示法的子网掩码（例如 255.255.255.0）。如果指定了此选项，则指定的值将与默认子网掩码进行或运算。默认子网掩码基于协商的远程 IP 地址选择；它是远程 IP 地址所属类别的适当网络掩码，与系统中位于同一网络的非点对点网络接口的子网掩码进行或运算后的结果。

**noaccomp** 在两个方向（发送和接收）禁用地址/控制压缩。

**noauth** 不要求对等方进行身份验证。如果在 */etc/ppp/options* 中指定了 *auth* 选项，则此选项具有特权。

**nobstdcomp** 禁用 BSD-Compress 压缩；**pppd** 不会请求或同意使用 BSDCompress 方案压缩数据包。

**noccp** 禁用 CCP（压缩控制协议）协商。仅在对等方存在缺陷并因 pppd 的 CCP 协商请求而混淆时，才需要此选项。

**nocrcts** 禁用串口上的硬件流控制（即 RTS/CTS）。如果未指定 *crtscts* 或 *nocrcts* 选项，则串口的硬件流控制设置保持不变。

**nodefaultroute** 禁用 *defaultroute* 选项。希望阻止用户使用 pppd 创建默认路由的系统管理员可以通过将此选项放入 `/etc/ppp/options` 文件中来实现。

**nodeflate** 禁用 Deflate 压缩；pppd 不会请求或同意使用 Deflate 方案压缩数据包。

**nodedtach** 不脱离控制终端。如果没有此选项，如果指定的串行设备不是标准输入上的终端，pppd 将 fork 以成为后台进程。

**noip** 禁用 IPCP 协商和 IP 通信。仅在对等方存在缺陷并因 pppd 的 IPCP 协商请求而混淆时，才需要此选项。

**noipdefault** 在未指定本地 IP 地址时，禁用默认行为（该默认行为是尝试根据主机名确定本地 IP 地址）。使用此选项时，对等方必须在 IPCP 协商期间提供本地 IP 地址（除非在命令行或选项文件中显式指定）。

**noipx** 禁用 IPXCP 和 IPX 协议。仅在对等方存在缺陷并因 pppd 的 IPXCP 协商请求而混淆时，才需要此选项。

**nomagic** 禁用魔术数字协商。使用此选项时，pppd 无法检测环路回线。仅在对等方存在缺陷时才需要此选项。

**nopcomp** 在接收和传输方向都禁用协议字段压缩协商。

**nopersist** 一旦连接建立并终止即退出。除非指定了 *persist* 或 *demand* 选项，否则这是默认行为。

**nopredictor1** 不接受或同意 Predictor-1 压缩。

**noproxyarp** 禁用 *proxyarp* 选项。希望阻止用户使用 *pppd* 创建代理 ARP 条目的系统管理员可以通过将此选项放入 */etc/ppp/options* 文件中来实现。

**novj** 在传输和接收方向都禁用 Van Jacobson 风格的 TCP/IP 头部压缩。

**novjcomp** 禁用 Van Jacobson 风格 TCP/IP 头部压缩中的连接 ID 压缩选项。使用此选项时，*pppd* 不会省略 Van Jacobson 压缩 TCP/IP 头部中的连接 ID 字节，也不会要求对等方这样做。

**papcrypt** 指示 */etc/ppp/pap-secrets* 文件中用于检查对等方身份的所有密钥都是加密的，因此 *pppd* 不应接受在加密前与 */etc/ppp/pap-secrets* 文件中的密钥相同的密码。

**pap-max-authreq** *n* 将 PAP 认证请求传输的最大次数设置为 *n*（默认值为 10）。

**pap-restart** *n* 将 PAP 重启间隔（重传超时）设置为 *n* 秒（默认值为 3）。

**pap-timeout** *n* 将 *pppd* 等待对等方使用 PAP 进行身份认证的最大时间设置为 *n* 秒（0 表示无限制）。

**pass-filter** *filter-expression* 指定一个数据包过滤器，应用于发送或接收的数据包，以确定哪些数据包应被允许通过。被过滤器拒绝的数据包将被静默丢弃。此选项可用于防止特定的网络守护程序（如 *roust*）占用链路带宽，或提供基本的防火墙功能。*filter-expression* 语法如 *tcpdump*(1) 中所述，但不允许用于 PPP 链路不合适的限定符，例如 **ether** 和 **arp**。通常，应将过滤表达式用单引号括起来，以防止表达式中的空格被 shell 解释。注意，可以使用 **inbound** 和 **outbound** 限定符对传入和传出数据包应用不同的限制。目前此选项仅在 NetBSD 下可用，并且仅当内核和 pppd 都定义了 PPP_FILTER 编译时可用。

- **persist** 连接终止后不退出；而是尝试重新打开连接。
- **predictor1** 请求对等方使用 Predictor-1 压缩压缩其发送的帧，并在被要求时同意使用 Predictor-1 压缩传输帧。除非内核驱动程序支持 Predictor-1 压缩，否则此选项无效。
- **proxyarp** 在此系统的 ARP [地址解析协议] 表中添加一个条目，包含对等方的 IP 地址和本系统的以太网地址。这将使对等方在其他系统看来位于本地以太网上。
- **remotename** *name* 将假设的远程系统名称设置为 *name*，用于认证目的。
- **refuse-chap** 使用此选项时，pppd 不会同意使用 CHAP 向对等方进行身份验证。
- **refuse-pap** 使用此选项时，pppd 不会同意使用 PAP 向对等方进行身份验证。
- **require-chap** 要求对等方使用 CHAP [质询握手认证协议] 进行身份验证。
- **require-pap** 要求对等方使用 PAP [密码认证协议] 进行身份验证。
- **silent** 使用此选项时，pppd 不会传输 LCP 数据包来启动连接，直到从对等方收到有效的 LCP 数据包为止（类似于旧版本 pppd 中的 'passive' 选项）。
- **usehostname** 强制使用主机名（如果给定，则附加域名）作为本地系统的名称用于认证目的（覆盖 *name* 选项）。

