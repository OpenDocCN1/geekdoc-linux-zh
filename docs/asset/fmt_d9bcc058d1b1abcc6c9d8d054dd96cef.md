
首先，`arspoof`欺骗认为我们的 MAC 地址是路由器的 MAC 地址，目标开始将所有网络流量发送给我们。内核转发除目标为端口 `443` 的流量以外的所有流量，该流量被重定向到 `$listenPort`（例如 `10000`）。此时，`sslniff`接收客户端连接，与真实的 SSL 站点建立连接，并查看服务器证书中的信息。然后，`sslniff`生成一个具有相同差异化名称（Distinguished Name）的新证书，并使用 `$certificateFile`中的终端实体证书对其进行签名。`sslniff`使用生成的证书链与客户端进行 SSL 握手，并在两个主机之间代理数据（当然，还会进行记录）。

# Kali Linux 2013 工具列表

## tcpflow

**描述** `tcpflow` 是一个捕获作为 TCP 连接（流）部分传输数据的程序，并以方便协议分析和调试的方式存储数据。每个 TCP 流都存储在它自己的文件中。因此，典型的 TCP 流将存储在两个文件中，每个方向一个。`tcpflow` 还可以处理存储的 `tcpdump` 数据包流。

`tcpflow` 将所有捕获的数据存储在格式如下文件中：`[timestamp]sourceip.sourceport-destip.destport[-VLAN][cNNNNN]`

**用法** `tcpflow [-chpsv] [-b max_bytes] [-d debug_level] [-f max_fds] [-i iface] [-r file] [expression]` `http://linux.die.net/man/1/tcpflow`

- 示例 `tcpflow -c n en1 src or dst host api.example.com`

- 示例 `tcpflow host sundown`（记录所有到达或离开 `sundown` 的数据包）

- 示例 `tcpflow host helios and \`（`hot or ace \`）`（记录 `helios` 与 `hot` 或 `ace` 之间的流量）

- 示例 `tcpflow host ace and not helios`（记录 `ace` 与除 `helios` 之外任何主机之间的流量）

- 示例 `tcpflow net ucb-ether`（记录本地与伯克利主机之间的所有流量）

- 示例 `tcpflow 'gateway snup and (port ftp or ftp-data)'`（记录通过互联网网关 `snup` 的所有 `ftp` 流量：（注意表达式使用了引号以防止 shell（误）解释括号））

## urlsnarf

**描述** `urlsnarf` 将 HTTP 流量中嗅探到的所有请求 URL 以 CLF（常用日志格式，几乎所有 Web 服务器都使用）输出，适用于使用你喜欢的 Web 日志分析工具（`analog`、`wwwstat` 等）进行离线后处理

**用法** `urlsnarf [-n] [-i interface] [[-v] pattern [expression]]`

**选项**

- `-n` 不将 IP 地址解析为主机名。
- `-i interface`
- `-v` “Versus”模式。反转匹配方向，以选择不匹配的 URL。指定要监听的接口。
- `pattern` 指定用于 URL 匹配的正则表达式。
- `expression` 指定一个 `tcpdump(8)` 过滤表达式以选择要嗅探的流量。

**示例** `urlsnarf -i lo`

## webmitm

描述 `webmitm` 透明地代理并嗅探由 `dnsspoof` 重定向的 HTTP / HTTPS 流量，捕获大多数“安全”的 SSL 加密网邮箱登录和表单提交。

用法 `webmitm [-d] [host]`

选项

- `-d` 启用调试模式。可以多次指定以产生更大的效果
- `host` 指定要代理的主机。如果没有提供，则只有包含 HTTP/1.1 Host: 标头或绝对 URI 的请求将被透明转发

示例 `webmitm -d`

## webspy

描述 `webspy` 将从客户端嗅探到的 URL 发送到你本地的 Netscape 浏览器进行显示，并实时更新（当目标浏览时，你的浏览器也会自动随它们一起浏览）。必须先在你的本地 X 显示器上运行 Netscape。

**用法** `webspy [-i interface | -p pcapfile] host`

**选项**
`-i interface`（指定要监听的接口）
- `-p pcapfile`（从指定的 PCAP 捕获文件处理数据包而不是网络）
- `Host`（指定要监视的 Web 客户端）

示例 `webspy -i eth0 192.168.1.1`

## wireshark

描述 `wireshark` 是一个图形化网络协议分析器。它允许你从微观角度观察网络上发生的情况。它可以用于故障排除、分析和教育。

**用法** `wireshark [options]`

## sndump

描述 `sndump` 是 Wireshark 的命令行版本。它是 Wireshark 软件套的一部分，旨在没有图形用户界面的环境。它允许你捕获和分析网络流量。

**用法** `sndump [options]`

## tshark

描述 `tshark` 是捕获和分析网络流量的工具。它是 Wireshark 的命令行版本，通常用于脚本和自动化。

**用法** `tshark [options]`

## bettercap

描述 `bettercap` 是一个用于网络攻击和分析工具。它可以发现主机、嗅探流量并执行各种攻击。

**用法** `bettercap [options]`

## mitcap

描述 `mitcap` 是一个强大的网络安全测试工具。它可以执行中间人攻击并识别漏洞。

**用法** `mitcap [options]`

## evilgrade

**描述** `Evilgrade` 是一个模块化框架，允许用户通过注入伪更新来利用糟糕的升级实现。当攻击者能够进行流量重定向时，该框架就会发挥作用，可以通过多种方式实现，例如：DNS 篡改、DNS 缓存污染、ARP 欺骗、Wi-Fi 访问点模拟以及使用你喜欢的工具进行 DHCP 劫持。通过这种方式你可以在渗透测试期间以干净且简单的方法控制一台完全补丁的机器。其核心思想是展示主流应用程序更新过程中存在的大量低级错误。

**用法** `./evilgrade show modules`

- **选项**
- `-show <object>` 用于显示不同的信息。
- `-conf <object>` 进入配置模式。
- `-set <option> "value"` 配置不同的选项。
- `-start` 启动服务。
- `-stop` 停止服务。
- `-status` 显示服务状态。

**示例** `http://00tsec.blogspot.co.uk/2011/07/hacking-with-evilgrade-on-backtrack5.html`

**示例** `https://forum.internot.org/offensive-guides-information/761-how-use-evilgrade.html`

# fake_advertise6

**描述** `thc-ipv6` - THC-IPV6-ATTACK-TOOLKIT - 只运行工具而不带任何参数，它们将为你提供帮助并显示命令行选项。

`fake_advertise6` - 在网络上通告 `ipv6` 地址（如果未定义，则使用自带的 `mac` 地址），如果没有指定目标，则将其发送到所有节点组播地址。

用法 `fake_advertise6 <interface> <ip-address> [target-address [own-mac-address]]`

**示例** `fake_advertise6 eth1 fe80::fd:ff:fe00:401 ff02::1 02:fd:00:00:04:01`（使用 `thc-ipv6` 工具 `fake_advertise6`，我们将为该主机通告以太网地址。要发送带有有效参数的邻居公告 (`NA`)，我们使用以下命令）

**示例** `fake_advertise6 eth1 fe80::fd:ff:fe00:401 ff02::1 02:fd:00:00:04:10`（当节点的以太网地址发生变化时会触发告警。在我们的示例中，我们通告了一个新的以太网地址 `02:fd:00:00:04:10`）

# IP 检测

大多数工具都可以很容易被 IDS 或专门的检测软件检测。这样做是有意的，为了便于检测异常使用。这些工具要么指定固定的数据包特征，要么通用地嗅探数据包（例如，因此也会响应发送到不存在的 `mac` 的 `icmp6` 邻居请求，因此非常容易被检测）。如果你不希望这样，请修改代码。

# fake_dns6d

**描述** `thc-ipv6` - THC-IPV6-ATTACK-TOOLKIT - 只运行工具而不带任何参数，它们将为你提供帮助并显示命令行选项。
