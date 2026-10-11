
这些命令的结果是，从本地主机（`lo`）发送的数据包将被接受，无论这些数据包的源是本地主机本身（`-s 127.0.0.1`）、本地局域网的接口（`-s 10.0.0.1`）还是互联网（`-s 323.45.67.89`）。IP 地址 `10.0.0.1` 和 `323.45.67.89` 是这些网络本地接口的示例（你的地址可能会不同）。最后两行表示防火墙应分别接受来自私有局域网（`-s 10.0.0.0/24`）的输入包，或目标为该局域网上任何地址（`-d 10.0.0.255`）的包。

`323.45.67.89` 地址并不是真实的 IP 地址。你将用 ISP 分配给你的外部接口的 IP 地址替换它。任何有效的 IP 地址都不能包含高于 255 的部分。

以下是命令定义了允许从互联网进入计算机的数据包：

```
# iptables -A INPUT -p ALL -i lo -s 127.0.0.1 -j ACCEPT
# iptables -A INPUT -p ALL -i lo -s 10.0.0.1 -j ACCEPT
# iptables -A INPUT -p ALL -i lo -s 323.45.67.89 -j ACCEPT
# iptables -A INPUT -p ALL -i eth1 -s 10.0.0.0/24 -j ACCEPT
# iptables -A INPUT -p ALL -i eth1 -d 10.0.0.255 -j ACCEPT
```

（注：由于提供的文本后半存在大量重复和乱码，上述译文已根据逻辑对重复部分进行了清理和整合，以确保符合高级工程师的输出标准。）

# 运行 Linux 防火墙/路由器

规则存储在 `/etc/sysconfig/iptables` 中，并在计算机重启时自动加载。如果它们没有自动加载，你可以按照以下步骤手动恢复它们：

```bash
# iptables-restore < /root/iptables
```

之前保存的规则现在已恢复到当前运行的内核中。

> 请记住，如果你使用的是启动盘设备，你需要确保将 iptables 文件保存到重启后不会消失的位置（例如 USB 闪存器上的目录或硬盘分区）。或者使用桌面环境的其他某些持久化功能来保存 iptables 规则文件。

## 检查你的防火墙

现在你的防火墙已经配置好了，你应该检查它以确保它对外部世界是可以的——即按照你预期的通过 `eth0` 访问互联网，通过 `eth1` 访问本地局域网（LAN）。网络上有一个常用的检查服务的工具 `nmap`。

虽然 `nmap` 是检查本地计算机或私有局域网接口的优秀工具，但不应该用它检查不属于你的电脑上的服务。在别人的电脑上使用 `nmap` 就像是检查别人家里所有的门窗以看你能否进入一样。使用 `nmap` 来确保你自己的“门窗”是安全的。

以下是一个使用 `nmap` 扫描你刚刚配置的防火墙大量端口的示例，以查看从防火墙的两个接口（`eth0` 和 `eth1`）看起来哪些哪些服务。要做到这一点，你需要从防火墙之外的计算机上运行 `nmap`。你不想看防火墙内部有什么；你想看的是世界对你防火墙的视角。从该电脑上，你首先通过运行 `ifconfig eth0` 获取 `eth0` 外部接口的 IP 地址。在本示例中，该 IP 地址为 `123.45.67.89`。请记住这不是真实的 IP 地址；不要使用 `nmap` 扫描互联网上的真实计算机。

然后，在网络上的另一台 Linux 机器上输入：

```text
# nmap 123.45.67.89
Starting nmap 123.45.67.89 (123.45.67.89) for Giga-Byte Technology Co.
Interesting ports on 123.45.67.89:
(The 6 ports scanned not shown below are in state:)

| PORT | STATE |
| :--- | :--- |
| 21/tcp | open |
| 22/tcp | open |
| 53/tcp | open |
| 80/tcp | open |
| 113/tcp | open |
| 4000/tcp | open |

MAC Address: 00:61:22:D3:11
host up
nmap completed in 0.95 seconds
```

### 选择并安装不同的 Linux 发行版

输出显示，在此地址扫描的 6 个端口是关闭的（拒绝访问），有 6 个是开启的。未过滤的服务包括 TCP 端口 `21`、`22`、`53`、`80`、`113` 和 `4000`（这些是在你设置防火墙规则时开启的）。示例中显示为开启（open）的服务目前都运行着服务器，并在开启的端口上进行监听。

你可能无法访问互联网上的某台 Linux 机器来测试外部访问。如果你在局域网中有另一台电脑，尝试从那台电脑上运行 `nmap`。如果你只有 Windows 机器，你可以始终从可启动的 Linux 中运行 `nmap`。

## 使用 iptables 进行 SNAT 或 IP 伪装

你可以使用网络地址转换（SNAT）或 IP 伪装（MASQUERADE）允许局域网内带有 IP 地址的计算机通过你的防火墙访问互联网。如果你的互联网连接是静态 IP 地址，选择 SNAT；如果 IP 地址是动态分配的，请使用 MASQUERADE。

当你创建一个 MASQUERADE 或 SNAT 规则时，它会被添加到 NAT 表和 POSTROUTING 链中。对于 MASQUERADE，必须提供接口名称（如 `eth0`、`ppp0` 或 `slip0`）以识别通往互联网或外部网络的路由。对于 SNAT，你还必须标识接口的 IP 地址。以下示例假设连接互联网是通过第一块网卡（`eth0`）提供的。这是一个 MASQUERADE 规则的示例：

```bash
# iptables -t nat -A POSTROUTING -o eth0 -j MASQUERADE
```

这是一个 SNAT 规则的示例：

```bash
# iptables -t nat -A POSTROUTING -o eth0 -j SNAT -to-source 12.12.12.12
```

如果你有多个提供通往互联网路由的地址，可以添加多个规则（例如，`--to-source 12.12.12.12-12.12.12.254`）。虽然 MASQUERADE 使用了一些额外的规则，但如果你是通过拨号连接互联网且每次连接的 IP 地址发生变化，你可能需要使用 SNAT。

确保内核中已开启 IP 转发，因为在大多数 Linux 系统上它默认是关闭的。要临时开启它，使用以下命令之一：

```bash
# echo 1 > /proc/sys/net/ipv4/ip_forward
```

或者

```bash
# sysctl net.ipv4.ip_forward
```

要永久开启 IP 转发，在 `/etc/sysctl.conf` 文件中添加以下行：

```text
net.ipv4.ip_forward = 1
```

如果需要，这里是开启 IP 寻址的方法：

```bash
# echo 1 > /proc/sys/net/ipv4/ip_addr
```

或者

```bash
# sysctl net.ipv4.ip_addr=1
```

要永久开启 IP 寻址，在 `/etc/sysctl.conf` 文件中添加以下行：

```text
net.ipv4.ip_addr = 1
```

## 使用 iptables 添加模块

某些防火墙功能需要向内核模块。例如，如果防火墙后的客户端需要使用被动 FTP 访问服务器，则需要特殊模块。在被动 FTP 中，客户端发送其 IP 地址和它将监听的端口给服务器。如果客户端位于防火墙后且你正在进行 NAT，该信息必须经过转换，否则 FTP 服务器将无法与客户端通信。

`iptables` 用于跟踪连接并通过查看 FTP 数据本身（即不在 IP 包头中）来获取所需信息的模块有：

- `conntrack`
- `nf_conntrack`
- `nf_conntrack_filter`
- `xt_conntrack`
- `xt_conntrack_state`
- `xt_limit`
- `xt_owner`
- `xt_comment`
- `ipt_hash`
- `ipt_raw`
- `ipt_multi`
- `ipt_protocol`
- `ipt_icmp`
- `ipt_arp`
- `ipt_ip`
- `ipt_mac`
- `ipt_link`
- `ipt_tcp`
- `ipt_udp`
- `ipt_limit`
- `ipt_nat`
- `ipt_mangle`
- `ipt_recent`
- `ipt_length`
- `ipt_statistic`
- `ipt_conntrack`

尝试破解需要对 `iptables` 有更深层的了解。我建议你从这里开始，参考以下内容：
