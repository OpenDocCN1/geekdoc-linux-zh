
# 第 13 章：访问控制与防火墙

这些示例说明了创建数据包过滤防火墙时最有效的策略是丢弃数据包。这阻止了潜在黑客访问我们机器的端口，并且不会告诉他发生了什么——他不会注意到自己被拒绝了，连接将一直挂起直到超时（这极大减慢了端口扫描的速度）。

## iptables 与 ipchains 的区别

Linux 2.4 数据包过滤被从头重写以变得更加强大。该系统被称为 Netfilter，你用于控制规则集的程序是 `iptables`。`iptables` 与 `ipchains` 类似，但有几差异。一旦了解这些差异，从 `ipchains` 迁移到 `iptables` 就会很简单。这些差异包括：

- 内置链名称现在是大大写的（例如 `INPUT`, `OUTPUT`, `FORWARD`）。
- `-i` 标志指向连接接口；`-o` 指向输出接口。
- TCP 和 UDP 端口现在需要 `--source-port` 或 `--sport` 以及 `--destination-port` 或 `--dport` 选项，并且必须放在 `-p tcp` 或 `-p udp` 之后。
- `-y` 标志现在是 `-syn` 且必须放在 `-p tcp` 之后。
- `DENY` 被 `DROP` 替换。
- `MASQ` 现在是 `MASQUERADE` 并使用不同的语法。
- 状态检测（本章稍后将讨论）现在无需内核模块即可支持。

如果你想获得更多关于 Netfilter 的信息，可以在 http://kernelnotes.org/ 找到优秀的文档。

如果你在用 `ipchains` 创建防火墙上花费了大量精力，只要你在内核中包含 `ipchains.o` 模块，它在内核 2.4 中仍然有效。更好的是查看 http://kernelnotes.org/ 上的 `iptables HOWTO` 以获取将 `ipchains` 转换为 `iptables` 的方法。

## 状态检测

`iptables` 引入的最重大变化之一是状态检测的概念。状态防火墙不仅检查源 IP 地址和目的 IP 地址以及端口号，还监控所使用的通信协议，以确保通信遵循连接规则。例如，如果状态防火墙允许从内部机器连接到远程机器上的 HTTP，防火墙将监控该连接，以确保远程机器 80 端口上的程序遵循 HTTP 协议。

## 攻破 Linux 暴露：Linux 安全秘密与解决方案

状态防火墙确保我们向远程机器发送了遵循 HTTP 协议的 GET、POST 或 HEAD。然后，它确保远程机器返回包含 HTTP 响应头和正文的文本。

> 注意：状态防火墙确保我们连接到远程机器的 80 端口时，我们实际上是在运行 HTTP，而不是某些恰好运行在该机器 HTTP 端口上的破坏性程序。它为允许进入我们网络的响应数据包提供了额外保护。然而，控制两个端点的更复杂的黑客可以仅仅通过修改其协议使其看起来像 HTTP。事实上，这种对开放 HTTP 端口的操作被日益滥用，即使是像 SOAP 这样的“官方”协议也是如此。

## 阻止特定的网络访问

我们现在将说明一个安全防火墙的开端，其旨在阻止对我们机器上特定端口的访问。这些示例将使用 `ipchains`（内核 2.2）和 `iptables`（内核 2.4）展示。这些示例可以用于创建一个健壮的防火墙。

### 尝试 ping 或 traceroute 到机器

| 流行性 | 8 |
| :--- | :--- |
| 简单性 | 8 |
| 影响 | 8 |
| 风险 | 8 |

在第 3 章中，我们讨论了 ping 和 traceroute 是发现网络可用主机的两种简单方法。通过阻止这些服务，可以使黑客无法出现在雷达上。这是一个被防火墙拦截后正常响应的机器 ping 示例：

```
hbox# ping 192.168.1.102

PING 192.168.1.102 (192.168.1.102) from 10.5.5.108 : 56(84) bytes of data.

---

192.168.1.102 ping statistics ---

5 packets transmitted, 0 packets received, 100% packet loss
```

### 使用 ipchains 拒绝 ICMP ping 和 traceroute

对于 2.2 内核，我们将使用 `ipchains` 拒绝 ICMP ping 请求（也称为 ICMP echo 请求）。`ipchains` 程序执行如下：

```
/sbin/ipchains -s 0/0 echo-request -d 192.168.1.102 -p icmp -j DENY
```

`-A` 选项允许 `ipchains` 向规则集中添加以下规则，它检查到达机器的每个数据包。该命令指定对于源自（s）任何 IP 地址（0/0）的 ICMP echo 请求类型数据包，目标（d）为机器 192.168.1.102（我们的机器），使用 ICMP 协议（p），跳转到（j）`DENY`。这将导致所有指向我们机器的 ICMP echo 请求被拒绝。

现在，当黑客进行 ping 时，连接失败了：

```
hackerbox# ping -c 5 192.168.1.102

PING 192.168.1.102 (192.168.1.102) from 10.5.5.108 : 56(84) bytes of data.

---

192.168.1.102 ping statistics ---

5 packets transmitted, 0 packets received, 100% packet loss
```

对于端口 33435 到 33525 的 UDP 包 traceroute：

```
/sbin/ipchains -A input -s 0/0 -d 192.168.1.102 -p udp 33435:33525 -j DENY
```

注意我们正在指定端口范围为 33435:33525。

当黑客尝试进行 traceroute 时，输出类似于：

```
machine# traceroute 192.168.1.102

traceroute to 192.168.1.102 (192.168.1.102), 30 hops max, 38 byte packets

1 hacker-firewall.hacker_er.edu (192.168.2.1) 2.892 ms 2.803 ms 2.746 ms

2 hacker-gateway.hacker_er.edu (171.678.90.1) 3.881 ms 3.789 ms 3.686 ms

(more hops deleted)

12 cisco.example.com (254.192.1.20) 158.884 ms 161.422 ms 160.884 ms

13 veloci.example.com (192.168.1.1) 168.650 ms 183.821 ms 173.287 ms

14 * *

15 * *

16 * *
```

我们成功地阻止了数据包被我们的机器 192.168.1.102 ；然而，攻击者和我们之间的其他机器仍然像以前一样做出响应。理想情况下，您应该配置您使用的所有机器也拒绝这些数据包。

我们阻止的端口是 UNIX traceroute 使用的标准端口。其他实现方式可能会有所不同。

#### 使用 iptables 防火墙拒绝连接

之前，我们详细介绍了 ipchains 和 iptables 之间的区别。要将我们的 ipchains 命令转换为阻止 ping 和 traceroute 的命令，我们只需进行以下更改：

- 将 ipchains 改为 iptables。
- 将 input 改为 INPUT。
- 在 echo-request 之前插入 `--icmp-type`。
- 移动端口号和数据包类型 `-p`，并在端口号前加上 `--port` 或 `--dport`。
- 将 DENY 改为 DROP。

将这些更改应用于我们阻止 ping 的 ipchains，我们创建了以下 iptables 命令：

```
/sbin/iptables -A INPUT -s 0/0 -d 192.168.1.102 -p icmp \
  --icmp-type echo-request -j DROP
```

丢弃 traceroute 数据包：

```
/sbin/iptables -A INPUT -s 0/0 -d 192.168.1.102 -p udp \
  --dport 33435:33525 -j DROP
```
