
在上面的示例中，`3,960` 个连接代表了 `60` MB 可用内存中的约 `3.7` MB；因此，只要防火墙机器上没有运行内存密集型程序，将此值翻倍（如有必要）不应该引起任何问题：

```
echo "7920" > /proc/sys/net/ipv4/ip_conntrack_max
```

## 安全拓扑 101

然而，你仍然应该定期监控你的日志文件，寻找关于连接跟踪表满的警告。如果发生这种情况，请将 `ip_conntrack_max` 增加几千，然后观察其几天的行为。如果问题仍然存在，重复此过程；最终，你将为系统添加更多 RAM。如果 `ip_conntrack_max` 的值需要设置得特别高，它可能是局域网内存在异常或不受欢迎的应用程序（许多 P2P 文件共享客户端会产生大量的连接尝试）的信号。使用 `tcpdump` 等数据包嗅探器监控流量可能是一个好主意。

## 辅助模块（Helper Modules）

NAT 和连接跟踪对于单端口协议运行良好，但对于更复杂的协议如 `ICQ`、`H323`（视频会议）以及 `FTP`。`FTP` 是常用的服务之一，为了理解这个问题，我们首先需要仔细观察它的工作原理。当你连接到 `FTP` 服务器时，会在特权端口和服务器的 `21` 端口之间形成 `TCP` 连接。这是发布命令的连接，被称为会话。文件传输是在其他数据会话中进行的，但可以是主动的或被动的。

在主动模式下，`FTP` 客户端向服务器发送要连接的地址和端口（顺便说，没有检查这是否与会话中的相同），服务器连接并传输数据（如图 3.8 所示）。

![d90c7093221fd01adff07e1ff1120_png]
图 3.8 主动连接

在被动模式下，客户端指示服务器连接到哪个端口。`20/TCP` 用于这些数据会话的源端口。图 3.9 展示了这种模式。

![d90c7093221fd01adff07e1ff1121_png]
图 3.9 被动连接

步骤 1 与之前相同：客户端与服务器建立会话。请求文件时，这次客户端选择服务器连接的地址和端口（步骤 2）。在步骤 3 中，服务器连接到该地址和端口，建立数据连接。

NAT 和连接跟踪的问题在于，这些信息包含在通过会话发送的数据包的负载中，因此如果不检查这些数据包的内容，防火墙无法得知例如，高端口的入站连接尝试与防火墙后尝试以主动模式传输数据的 `FTP` 客户端有关。

简单的解决方案是指示用户将 `FTP` 客户端设置为被动连接到远程服务器，并通知连接到 `DMZ` 中 `FTP` 服务器的用户必须使用主动模式；但这远不是一个万无一失的解决方案。

`Netfilter` 包带来一组辅助模块，用于协商如 `FTP` 等复杂的协议。假设这些协议已编译为模块（如果它们已编译到内核中，则你不需要执行 `modprobe` 命令），加载它们只需使用 `modprobe` 命令。记住，NAT 和连接跟踪是两个完全不同的东西，因此为了让协议跨越防火墙正常运行，每个功能都需要一个辅助模块：

# 安全拓扑 103

```bash
/sbin/modprobe ip_conntrack_ftp
/sbin/modprobe ip_nat_ftp
```

在加载 `ip_conntrack_ftp` 模块后，`FTP` 数据将被标记为 `RELATED`，允许你在 `Iptables` 规则中对其进行匹配。

对于某些较不常用的协议，你可能需要使用 `POM` 工具对内核进行补丁并重新编译。该脚本包含了一系列内核补丁，旨在为 Linux 内核添加功能或修复微小错误。但请注意，这些补丁中的某些仍然处于实验性阶段，这也是它们未包含在标准内核中的主要原因之一。要启用各种连接跟踪/NAT 辅助模块，所需的配置选项列表可以在附录 B“网络类的内核配置选项”中找到。

# 3.3 实现三脚模型

本节将解释三脚模型的实现方法：首先通过讨论在网络中正确路由流量所需的 `Iptables` 规则，随后通过探索提高安全性和性能的方法。在本节过程中开发的完整脚本可以在附录 C“NAT 防火墙脚本”中找到，也包含在随附的 CD-ROM 中，文件名为 `nat.sh`。

![](img/d90c7093221fd011adff06e7e1ff1ccd_122_0.png)

# 防火墙规则集

图 3.10 再次显示了我们的建议 LAN 拓扑，这次添加了 IP 地址和接口名称。在查看如何在 `Iptables` 中实现它们之前，让我们为该模型定义一些通用规则：

- 从私有 LAN 发往 Internet 的数据包应被转发到 `eth0`（我们的外部接口）。源地址也应重写为我们的外部 IP。
- 对这些数据包的响应应转发到 `eth1`（我们的 LAN 接口），并将其目的地址重写为正确的内部 IP 地址。
- 从私有 LAN 发往 DMZ 的数据包应转发到 `eth2`。发往 DMZ 的包不需要 NAT，因为它也使用私有地址。
- 从 DMZ 发往私有 LAN 的数据包应转发到 `eth1`。同样，不需要 NAT。
- 从 DMZ 发往 Internet 的数据包应通过 `eth0` 出出，并将源地址从私有 DMZ IP 重写为我们的公共 IP。
- 对这些数据包的响应应重写目的地址并转发到 DMZ 中正确的机器。
- 端口 `80` 和 `443` 上的入站 `TCP` 连接请求（`SYN` 包）应转发到 DMZ Web 服务器。
- 端口 `53` 的入站 `TCP` 和 `UDP` 连接应转发到 DMZ DNS 服务器。
- 端口 `25` 的入站 `TCP` 连接应转发到 DMZ 邮件服务器。

![](img/d90c7093221fd011adff06e7e1ff1ccd_123_0.png)

**图 3.10** 三脚 LAN 拓扑。

为了方便起见，我们在防火墙脚本顶部定义了一些变量：

- `IF_LAN`: 防火墙上连接到私有 LAN 的接口。
- `IF_DMZ`: 连接到 DMZ 的防火墙接口。
- `IF_EXT`: 连接到外部世界的外部接口。
- `IP_LAN`: LAN 接口的 IP 地址。
- `IP_DMZ`: DMZ 接口的 IP 地址。
- `DMZ_HTTP`: DMZ Web 服务器的 IP 地址。
- `DMZ_DNS`: DMZ DNS 服务器的 IP 地址。
- `DMZ_MAIL`: DMZ 邮件服务器的 IP 地址。
- `IPT`: `Iptables` 二进制文件的位置。

这些变量可以通过在前面加上 `$` 符号在防火墙脚本中使用。到目前为止，我们的防火墙脚本如下：

```bash
IF_LAN = "eth1"
IF_DMZ = "eth2"
IF_EXT = "eth0"
IP_LAN = "192.168.1.1"
IP_DMZ = "192.168.0.1"
DMZ_HTTP = "192.168.0.3"
DMZ_DNS = "192.168.0.2"
DMZ_MAIL = "192.168.0.4"
```

```bash
## iptables 二进制文件的具体路径在不同的 Linux 发行版之间不同。
IPT = "/usr/local/sbin/iptables"
```

```bash
## 启用 IP 转发
echo "1" > /proc/sys/net/ipv4/ip_forward
```

```bash
## 启用动态 IP
echo "1" > /proc/sys/net/ipv4/ip_dynaddr
```

```bash
## 加载辅助模块
/sbin/modprobe ip_nat_ftp
/sbin/modprobe ip_conntrack_ftp
```

```bash
$IPT -flush
$IPT -t nat -flush
$IPT -t mangle -flush
```

```bash
## 默认链策略
$IPT -P INPUT DROP
$IPT -P OUTPUT DROP
$IPT -P FORWARD DROP
```

```bash
### 允许回环流量
$IPT -A INPUT -i lo -j ACCEPT
$IPT -A OUTPUT -o lo -j ACCEPT
```

### 私有 LAN

接下来，我们需要为尝试访问 Internet 的内部流量启用 `SNAT`：

```bash
$IPT -t nat -A POSTROUTING -o $IF_EXT -j MASQ
```

允许所有流量流出 LAN：

```bash
$IPT -A FORWARD -i $IF_LAN -o $IF_EXT -m state \
    --state NEW,ESTABLISHED,RELATED -j ACCEPT

$IPT -A OUTPUT -m state \
    --state NEW,ESTABLISHED,RELATED -j ACCEPT
```

只有属于已建立连接（与之相关）的数据包允许进入 LAN：

```bash
$IPT -A FORWARD -i $IF_EXT -o $IF_LAN -m state \
    --state ESTABLISHED,RELATED -j ACCEPT
```
