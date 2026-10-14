
第一行指定 VIP 地址和调度方法（`-rr`）。调度方法的选择（在前几章中描述）如下：

| ipvsadm 参数 | 调度方法 |
|---|---|
| `-s rr` | 轮询 |
| `-s wr` | 加权轮询 |
| `-s lc` | 连接数 |
| `-s wlc` | 加权连接数 |
| `-s dh` | 目的哈希 |
| `-s sh` | 源哈希 |
| `-s sed` | 最短预期延迟 |
| `-s nq` | 从不队列 |

在本配方中，我们将使用轮询调度方法。在生产环境中，你应该使用加权动态调度方法（见第 11 章对各种方法的说明）。上述第二条 `ipvsadm` 行将真实服务器的 RIP（`-r 10.1.1.2`）与 VIP（或虚拟服务器）关联，并指定了转发方法（`-m`）。同一个虚拟服务器的每个 `ipvsadm` 条目可以使用不同的转发方法，但通常只使用一种。选择如下：

| 参数 | 方法 |
|---|---|
| `-g` | LVS-DR |
| `-i` | LVS-TUN |
| `-m` | LVS-NAT |

在本配方中，由于我们正在构建 LVS-NAT 集群，我们将使用 `-m` 选项¹¹
当你完成此脚本的输入或修改 CD-ROM 拷贝后，通过输入以下命令运行它：

```
#/etc/init.d/lvs start
```

如果 VIP 已添加到 Director（你可以通过 `ifconfig` 检查），请登录真实服务器并尝试 ping 这个 VIP 地址。你也应该能从客户端计算机 ping 通 VIP 地址（只要没有拦截 ICMP 数据包的中间防火墙）。

注意 ICMP ping 数据包

要查看虚拟服务器表（我们刚刚创建的指示 Director 如何将传入请求转发到集群内部真实服务器的表），请在你制作 Director 的服务器上输入以下命令：

```
#/sbin/ipvsadm -L -n
```

¹¹ 注意你不能简单地将此选项更改 `-g` 来构建 LVS-DR 集群。

该命令将显示 IPVS 表格：

IP Virtual Server version 1.0.10 (size=4096)
Prot LocalAddress:Port Forward Weight ActiveConn InActConn
TCP 209.100.100.3:80 rr Masq 1 0 0
-> 10.1.1.2:80

此输出将列标题和每行输出都折叠到下一行。我们只有一个 IP 虚拟服务器指向真实服务器，因此有一行（折叠后的）输出为：

TCP 209.100.100.3:80 Masq 1 0 0
-> 10.1.1.2:80

此行表示我们的 IP 服务器正使用 TCP 协议用于端口 80 的 VIP 地址 209.100.100.3。数据包被转发 (->) 到端口 80 的真实地址 10.1.1.2，我们的转发方法是伪装 (Masq)，这是网络地址转换（NAT）或 LVS-NAT 的另一种名称。
在此字段中报告的 LVS 转发方法将是其中之一：

| 报告输出 | LVS 转发方法 |
| :--- | :--- |
| Masq | LVS-NAT |
| Route | LVS-DR |
| Tunnel | LVS-TUN |

## 第 6 ：测试集群配置

下一步是测试集群配置。在这一步中，`<DR>` 将出现在在 Director（调度器）上输入的命令之前，`<RS>` 将出现在在真实服务器（real server）上输入的命令之前。
要的第一件事是确保网卡已正确配置并正在接收数据包。在 Director 上输入以下命令：

```
<DR>#ifconfig -a
```

在该命令的输出中需要关注的重点是接口是否为 `UP`（开启），以及发送（TX）和接收（RX）了多少数据包。在下面的示例输出中，我用**粗体**标记了这些信息：

```
eth0 Link encap:Ethernet HWaddr 00:10:5A:16:99:8A

inet addr:209.100.100.2 Bcast:209.100.100.255 Mask:255.255.255.0

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:481 errors:dropped:0 overflows: frame:0

TX packets:374 errors:dropped:0 overflows: carrier:0

collisions:0 txqueuelen:100

Interrupt:5 Base address:0x220
# eth0:1
Link encap:Ethernet Hwaddr 00:10:5A:16:99:8A

inet:209.100.100.3 Bcast:209.100.100.255 Mask:255.255.255

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

Interrupt:5 Base address:0x220
# eth1
Link encap:Ethernet HWaddr 00:80:5F:0E:AB:AB

inet:10.1.1.1 Bcast:10.1.1.255 Mask:255.255.255.0

UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

RX packets:210 errors:dropped:0 overflows: frame:0

TX packets:208 errors:dropped:0 overflows: carrier:0

collisions:0 txqueuelen:100

Interrupt:11 Base address:0x1400
```

如果在你的 `ifconfig` 命令输出中，所有网卡和网络接口别名（或 IP 别名）都没有显示 UP 字样（如本文各章节所示），则缺失的网卡的软件驱动程序未配置（或网卡未正确安装）。有关处理网卡的更多信息，请参附录 C。

注意：如果你使用辅助 IP 地址而不是 IP 别名，请使用 `ip addr show` 命令来检查辅助 IP 地址的状态，而不是 `ifconfig -a` 命令。然后你可以检查该命令的输出以获取相同的信息（`ip addr show` 命令返回的结果与我提供的示例输出略有不同）。

如果接口为 `UP` 但网卡上没有发送（TX）或接收（RX）数据包，你可能存在网络布线问题。
一旦你有了正常的网络配置，请测试从真实服务器到 Director 的 DIP 和 VIP 地址的通信。要继续操作，将在真实服务器上执行以下命令：

```
<R>ping 10.1.1.1
<R>ping 209.100.100.3
```

这两个命令中的第一个是 ping Director 的集群 IP 地址 (DIP)，第二个是 ping Director 的虚拟 IP 地址 (VIP)。这两个命令都应该报告数据包可以成功从真实服务器通过集群网络到达 Director，并且 Director 成功识别其 DIP 和 VIP 地址。一旦你确定集群网络的 IP 通信正常，请使用客户端计算机从集群外部 ping VIP 地址。

## LocalNode：将 Director 作为真实服务器

当你构建企业级集群时，你需要分配两台 Linux 服务器作为主、备用 LVS Director。但目前，你可以通过在 Director 上配置并安装 Apache（如本章“第 2 步：在真实服务器上配置并启动 Apache”节所示），然后配置 Director 将客户端请求发送到本地运行的 Apache 副本（就像 Director 也是集群中的一个节点一样），来测试负载均衡功能是否正常工作（无论你的最终配置如何）。这种配置被称为 LocalNode 或 LocalNode 模式。

使用 LocalNode 配置的局限性是 Director（调度器）无法重映射端口号——客户端计算机在请求访问服务时使用的任何端口号也必须在 Director 上用于处理该请求。LVS HOWTO 描述了在 LVS 中使用 `iptables/ipchains` 重定向来解决这一局限性的解决方法。

假设你已经在 Director 上运行了 Apache，你可以修改 Director 上的 `/etc/init.d/lvs` 脚本，使得两个集群节点可供客户端使用（Director 和真实服务器），如下所示：

```
## 为 VIP 209.100.100.3 端口 80 添加 IP 虚拟服务
/sbin/ipvsadm -A -t 209.100.100.3:80 -s rr
```

```
# 现在将此 VIP 的数据包直接定向到集群内部的真实服务器 (IP)
/sbin/ipvsadm -a -t 209.100.100.3:80 -r 10.1.1.2 -m

# 并将请求发送到 Director 本地运行的 Apache
# 服务器
/sbin/ipvsadm -a -209.100.100.3:80 -r 127.0.0.1 -m
```
