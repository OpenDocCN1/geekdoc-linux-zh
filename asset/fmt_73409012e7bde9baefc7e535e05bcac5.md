
```
$ sudo netstat -lnp | grep :80
tcp  0 0 0.0.0.0:80 0.0.0.0:*  LISTEN  919/apache
```

第一列告诉你该端口使用的协议。第二列和第三列分别是接收队列和发送队列（这里两者都设置为 0）。你需要重点关注的是第四列，因为它列出了主机正在监听的本地地址。这里的 `0.0.0.0:80` 表明主机正在监听其所有 IP 地址的 80 端口流量。如果 Apache 仅监听 web1 的以太网地址，你会在此处看到 `10.1.2.5:80`。

最后一列会告诉你哪个进程打开了该端口。在此示例中，可以看到 Apache 正在运行并处于监听状态。如果你在 `netstat` 输出中没有看到这一行，你需要启动 Apache 服务器。

### 防火墙规则

如果进程正在运行并监听 80 端口，有可能 web1 部署了某种防火墙。使用 `iptables` 命令列出所有防火墙规则。如果防火墙已禁用，输出将如下所示：

```
$ sudo /sbin/iptables -L
Chain INPUT (policy ACCEPT)
target     prot opt source                destination

Chain FORWARD (policy ACCEPT)
target     prot opt source                destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source                destination
```

请注意，默认策略设置为 `ACCEPT`。但有可能你的防火墙被配置为默认丢弃所有数据包，即使它没有列出任何规则。如果是这种情况，你将看到的输出更像以下内容：

```
$ sudo /sbin/iptables -L
Chain INPUT (policy DROP)
target     prot opt source       destination

Chain FORWARD (policy DROP)
target     prot opt source       destination

Chain OUTPUT (policy DROP)
target     prot opt source       destination
```

另一方面，如果有一条防火墙规则阻止了 80 端口，它可能看起来像这样：

```
$ sudo /sbin/iptables -L -n
Chain INPUT (policy ACCEPT)
target     prot opt source       destination
REJECT     tcp  --  0.0.0.0/0    0.0.0.0/0  tcp dpt:80 reject-with
icmp-port-unreachable

Chain FORWARD (policy ACCEPT)
target     prot opt source       destination

Chain OUTPUT (policy ACCEPT)
target     prot opt source       destination
```

显然，在后一种情况下，你需要修改防火墙规则以允许该主机的 80 端口流量。

### 排查缓慢网络

在某种程度上，当网络完全无法工作时，排查网络问题反而更容易。当主机不可达时，你可以执行前面讨论的故障排除步骤，直到主机再次可达为止。然而，当网络只是变慢时，有时很难找出原因。本节介绍了一些可用于追踪缓慢网络原因的技巧。

#### DNS 问题

虽然 DNS 因网络问题被指责的频率通常高于其实际责任比例，但当 DNS 确实存在问题时，往往会导致网络性能下降。例如，如果你为某个域名配置了两台 DNS 服务器，而第一台服务器宕机，你的 DNS 请求将等待 30 秒超时后才转向备用 DNS 服务器。虽然在使用 `dig` 或 `nslookup` 等工具时会明显感觉到这种延迟，但 DNS 问题有时还会以出人意料的方式导致网络表面上的变慢；这是因为许多服务依赖 DNS 将主机名解析为 IP 地址。此类问题甚至会影响你的网络故障排除工具。

`Ping`、`traceroute`、`route`、`netstat` 甚至 `iptables` 都是 DNS 问题期间性能可能下降的网络故障排除工具的典型示例。默认情况下，所有这些工具都会尝试将 IP 地址解析为主机名（如果可能的话）。但如果存在 DNS 问题，这些命令中的每一个结果可能会在尝试查找并解析 IP 地址失败时停滞。对于 `ping` 或 `traceroute` 来说，`ping` 回复似乎花了很长时间，但当回复最终到达时，往返时间相对较低。对于 `route`、`netstat` 和 `iptables`，结果可能会停滞相当长时间才会输出。系统正在等待 DNS 请求超时。

在上述所有情况中，绕过 DNS 以确保故障排除结果的准确性很容易。我们之前讨论的所有命令都接受 `-n` 选项，该选项禁用将 IP 地址解析为主机名的任何尝试。除非我真的希望解析 IP 地址，否则我已经习惯在第一部分中向你介绍的所有命令中添加 `-n`。

**注意** 虽然我们将在第 8 章中更详细地讨论这一点，但 DNS 解析还可能以意外方式影响你的 Web 服务器性能。一些 Web 服务器配置为将访问它们的每个 IP 地址解析为主机名以便记录日志。虽然这可以使日志更易读，但在最糟糕的时候——即拥有大量访客时——它也可能极大地减慢你的 Web 服务器速度。此时，你的 Web 服务器忙于解析所有这些 IP 地址，而不是处理流量。

#### 使用 traceroute 找到网络慢的位置

当你的服务器与不同网络上的某个主机之间的网络连接显得缓慢时，有时很难找出真正的瓶颈所在。特别是在延迟（获取响应所需的时间）变慢而总带宽没有变慢的情况下，`traceroute` 正是为此类场景设计的。本章早些时候提到了 `traceroute`，将其作为测试你与远程网络上服务器之间整体连通性的方法，但当你需要诊断网络变慢的可能位置时，`traceroute` 也非常有用。由于 `traceroute` 输出你与另一台机器之间每一跳的响应时间，你可以追踪到可能位于不同大陆或在过载导致网络变慢的网关。例如，以下是美国服务器与中国雅虎服务器之间 `traceroute` 的一部分：

```
$ traceroute yahoo.cn
traceroute to yahoo.cn (202.165.102.205), 30 hops max, 60 byte packets
 1  64-142-56-169.static.sonic.net (64.142.56.169)  1.666 ms  2.351 ms  3.038 ms
 2  ge-7-1-0.gw.sr.sonic.net (209.204.193.16)  1.241 ms  1.243 ms  1.229 ms
 3  265.ge-7-1-0.gw.paol.sonic.net (64.142.0.198)  3.388 ms  3.612 ms  3.592 ms
 4  xe-1-0-6.ar1.paol.us.nlayer.net (69.22.130.85)  6.464 ms  6.607 ms  6.642 ms
 5  ae0-80g.cr1.paol.us.nlayer.net (69.22.153.18)  3.320 ms  3.404 ms  3.496 ms
 6  ae1-50g.cr1.sjcl.us.nlayer.net (69.22.143.168)  4.335 ms  3.955 ms  3.957 ms
 7  ae1-40g.ar2.sjcl.us.nlayer.net (69.22.143.118)  8.748 ms  5.500 ms  7.657 ms
 8  as4837.xe-4-0-2.ar2.sjcl.us.nlayer.net (69.22.153.146)  3.864 ms  3.863 ms  3.865 ms
 9  219.158.30.177 (219.158.30.177)  275.648 ms  275.702 ms  275.687 ms
10  219.158.97.117 (219.158.97.117)  284.506 ms  284.552 ms  282.416 ms
11  219.158.97.93 (219.158.97.93)  263.538 ms  270.178 ms  270.121 ms
12  219.158.4.65 (219.158.4.65)  303.441 ms + 303.465 ms
13  202.96.12.190 (202.96.12.190)  306.968 ms + 306.971 ms  307.052 ms
14  61.148.143.10 (61.148.143.18)  295.916 ms  295.780 ms  295.860 ms
...
```
