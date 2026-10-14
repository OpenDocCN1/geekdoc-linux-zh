
```
echo 1 > /proc/sys/net/ipv4/icmp_echo_ignore_broadcasts
```

如果你想让你的防火墙对 ICMP ping 保持隐身——也就是说，忽略 ping 它的尝试，你可以构建 `iptables` 规则来实现这一点，或者你可以使用此处所示的 `/proc` 设置来简单地忽略所有 ICMP echo 或 ping 请求。如果你不想让你的防火墙容易被发现，这可能非常有用，但请记住，除了 ICMP echo 请求外，还有其他检测防火墙的方法。这可以让你从不那么先进的攻击者那里获得某种“隐身性”，但从任何角度来说，它都不会让你完全隐形。关闭响应 ICMP echo 请求的能力可能会某些网络诊断变得困难，并可能让你的用户更有可能向你投诉防火墙“宕机”了或没有响应。尽管如此，如果你想关闭 ICMP echo 响应，只需按照此处定义将 0 传递到 `/proc/sys/net/ipv4/icmp_echo_ignore_all`：

```
echo 0 >/proc/sys/net/ipv4/icmp_echo_ignore_all
```

有时，路由器等设备会对广播帧发送虚假响应，这些响应将由内核记录。在繁忙的网络中，这可能会迅速变得令人厌恼——或者会导致你的 syslog 守护进程遭受 Do 攻击。将其设置为 true（`echo 1`）将禁用这些消息的记录。如果你遇到奇怪的网络问题，你可能想通过向以下路径传递 0 来恢复它：

`/proc/sys/net/ipv4/icmp_ignore_bogus_error_responses`.

再次，要关闭对这些错误的记录，请向同一个 `/proc` 条目传递 1：

```
echo 1 >/proc/sys/net/ipv4/icmp_bogus_error_responses
```

最后要查看的部分是 `/proc` 中的网络性能设置。这些是基于我们构建的防火墙提出的建议，应该根据需要适应你的独特环境进行调整。正如俗所说，每个人的情况可能不相同，这些设置也不例外。如果你发现自己在任何这些设置上遇到问题，请参考本章中的描述，或者在最坏的情况下，查看我们网站上的论坛（www.gtroot.com）看看其他用户推荐什么。

感兴趣的第一个网络设置是 TCP FIN 超时。它定义了如果套接字是由我们这边关闭的，保持其处于 FIN-WAIT-2 状态的时间。这是 TCP 会话最后拆毁部分的一部分，其中我们发送 FIN 包并等待对方的 ACK 响应。如果对方主机损坏、速度缓慢或没有响应，无论发生什么，套接字将保持打开一段时间以进行等待。2.4 和 2.6 内核的通常值为 60 秒，而 2.2 版本为 180 秒。我们建议将其设置为 45 秒，这意味着如果远程主机没有在 45 秒内完成拆毁，套接字将被杀死。如果你发现有太多处于 FIN-WAIT-2 状态的打开套接字，可以尝试进一步降低此数字。此设置的格式是传递一个整数值，如下例：

```
echo 45 > /proc/sys/net/ipv4/tcp_fin_timeout
```

另一个值得琢磨的类似设置是，这定义了连接被认为存活的多久。我们建议将其设置为 60 秒。

```
echo 60 > /proc/sys/net/ipv4/tcp_timeout
```

为了防止 SYN 洪水攻击，我们建议开启此项：

```
echo 1 > /proc/sys/net/ipv4/tcp_syncookies
```

ECN（显式拥塞通知）是 IP 的一个巧妙扩展，正如其名所示，允许系统显式地通知对方连接正拥塞。对于 2.4 和 2.6 内核，如果编译了此选项，它有助于动态重新配置。然而，并不是所有的 IP 栈都能处理它，如果你开启它可能会发现无法连接某些网站。由于由于原因，我们建议在防火墙上关闭它。

```
echo 0 > /proc/sys/net/ipv4/tcp_ecn
```

## 图 7：使用 `IPTABLES`

内核还有许多其他设置——实际上有数百个——在我们的网站（getroot.com）上有更详细的文档说明。请随时访问我们的网站或查看以下内容有关在内核中实施其他调优的信息。

## `IPTABLES` 模块

在内核按照我们想要的方式配置后，我们可以开始加载可能需要的 `iptables` 模块。有两种方法可以实现：显式地，这是更安全更可靠的方法（我们必须自己决定系统需要哪些模块），或者我们可以简单地加载为系统配置的所有模块。如果你了解系统中加载了哪些模块，后者与前者一样安全可靠。有一个短脚本可以自动加载系统上的 `iptables` 模块：

```
MODULE_DIR="lib/modules/$(uname -r)/kernel/net/ipv4/netfilter/"
MODULE=$(cd $MODULE_DIR; ls *_conntrack_* *_nat_* | sed 's/\..*$//')
for module in $(echo $MODULE); do
  if $LSMOD | grep "$module"; then continue; fi
  if [ -e "${MODULE_DIR}/${module}.o" -o "${MODULE_DIR}/${module}.o.gz" ]; then
    echo loading module ${module}
    $MODPROBE ${module} || exit 1
  fi
done
```

否则，你需要显式加载每个你想让系统使用的，例如：

```
modprobe ipt_nat
modprobe ipt_ROUTE
modprobe ipt_REDIRECT
modprobe ipt_stealth
[...]
modprobe ip_conntrack
```

这可能是一个长列表（有几十个模块），这就是为什么更简单的选择是了解内核中编译了什么，并使用脚本处理加载一切。使用脚本的另一个优点是它可以防止你漏掉重要的内核模块；当然，缺点是它可能会加载你不需要加载的模块，例如 `ip_conntrack_tftp` 等。

## 第 2 章 使用防火墙

首选方法是在确定需要哪些模块后显式加载它们。手动加载或通过我们的脚本加载所有模块可能会为网络创建许多漏洞，因为它允许某些类型的流量通过你的防火墙，而这些流量对你来说可能风险太大，无法允许。

## 防火墙规则

在正确配置内核并加载了所有必要的防火墙模块后，你就可以开始向内核中添加规则。正如我们在章开头定义的顺序一样，我们将从出于性能考虑的影响数据包形状的特殊规则开始。一个例子是设置 MSS 到 PMTU 的夹紧（clamp）规则，这将在本书的后续章节中详细解释。我们将简要提到该问题并解决它，因为它通常与 PPPoE（基于以太网的 PPP）连接中遇到的 MTU 问题有关，例如连接停顿。我们将在第 12 章“NAT（网络地址转换）和 IP 转发”中详细介绍这一点。重点是，你要将这类特殊用途的数据包处理规则放在防火墙规则的开头，以便它们始终能被使用。以下是一个规则集，用于修复示例防火墙在互联网接口 (`eth0`) 上使用 DSL 连接时的 MTU 问题。

```
iptables -A OUTPUT -o eth0 -p tcp --tcp-flags \
SYN,RST SYN -j TCP --clamp-mss-to-pmtu
iptables -A FORWARD -o eth0 -p tcp --tcp-flags \
SYN,RST SYN -j TCP --clamp-mss-to-pmtu
```

这将最大分段大小（MSS）“夹紧”到路径 MTU。这将防止连接中可能导致其停顿的不必要分片（fragmentation）。

## 服务质量（QoS）规则

接下来，我们将追加服务质量规则，以便为遵循所谓“服务条款”（TOS）设置的设备建立某些流量的优先级级别。这些只是示例，但对于我们的防火墙，我们喜欢将 `telnet` 和 `ftp` 命令设置为“最小延迟”（Minimize-Delay），这应该在处理饱和网络时让 `telnet` 和 `ftp` 命令会话的响应更迅速。

```
iptables -A PRERUTING -t mangle -p tcp --sport \
telnet -j TOS --set-tos Minimize-Delay
```

```
iptables -A PRERUTING -t mangle -p tcp --sport \
ftp -j TOS --set-tos Minimize-Delay
```

然后，我们将设置实际的 FTP-数据流量，让防火墙尝试最大化 FTP 流量的吞吐量。在这里延迟不是问题；我们可以接受缓存和其他技巧，否则可能会让 `telnet` 或 `ftp` 命令通道变得令人烦的缓慢或难以使用。

```
iptables -A PRERUTING -t mangle -p tcp --sport \
ftp-data -j TOS --set-tos Minimize-Throughput
```
