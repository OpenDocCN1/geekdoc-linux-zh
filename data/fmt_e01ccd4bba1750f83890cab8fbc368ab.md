
`64 bytes from 127.0.0.1: icmp_seq=2 ttl=255 time=92 usec`

`64 bytes from 127.0.0.1: icmp_seq=3 ttl=255 time=97 usec`

--- `127.0.0.1` ping statistics

`4 packets transmitted, 4 packets received, 0% packet loss`

`round-trip min/avg/mdev = 0.092/0.134/0.134`

每行显示从环回接口返回的字节数，摘要显示了往返时间。如果你没有看到响应，说明你的设置有问题。

## 排除连接故障

上一节处理的是内部问题；本节关注让你的外部连接正常工作。与 Linux 不同，DSL 没有标准，因此我们将关注常见的 DSL 问题。当你确定线缆是完好的时，可以使用内部网络（私有网络）来检查 DSL 设备。使用任一网络

# 第 5 章：基础故障排除简介

第 1 章中的模型——直接连接到广网 `DCWAN` 或 `DMZ`——应该允许你与 DSL 设备进行通信。

连接到你 DSL 设备的设备必须配置正确。如果网关上的网卡 `NIC` 配置错误，你将无法与 DSL 设备通信。

请使用本章第一节——使用故障树故障排除——描述的步骤来检查并排除你的网关故障。

## 检查 DSL 供应商配置

如果你在验证私有网络连接和配置正常后，DSL 联网连接仍然无法工作，那么你需要检查 DSL 提供商是否按照其承诺提供服务。

这个过程可能是所有中最耗时且令人沮丧的部分。在许多地方，DSL 仍然是一项相对较新的服务（而非技术），服务提供商通常没有统一的故障排除流程。请注意，在多个电话号码和部门之间转转是寻常的。

由于设备和 DSL 服务种类广泛，深入讨论超出了本书的范围，因此我们描述了以下 DSL 故障排除技巧（如果你使用的是 ADSL Cisco 675 DSL 调制调器，可以重新查看第 3 章中的详细讨论）。

- 检查你的 DSL 线路质量：某些 DSL 设备可以显示 DSL 连接的质量和强度。例如，当信号高于最低水平时，Cisco 675 的链路状态是稳定的，低于该水平时会闪烁。
- 重新检查你的 DSL 设备配置：如果你是 ADSL 连接，请参阅第 3 章中的说明。（如果你使用的不是书中描述的相同设备，请将这些说明作为通用指南）。你可以、也应该重新检查你的 DSL 供应商提供的说明。
- 做好记录：如果你必须与多于一个人交谈——你很可能会这样做——那么你需要记录你和谁交过话、什么时候进行的会话以及你们讨论了什么。这样，你就可以避免在打了第三或第四次电话后，因无法记得承诺或建议过什么而感到沮丧。
- 为你的 DSL/网关网络绘制一张图：这有助于你理解各个部分是如何连接在一起的。最好的方法是从数据包进出 DSL 设备的角度来思考。
- 检查你的路由/或 NAT 配置：你在此步骤中制作的任何图表都将非常有用。检查路由和 NAT 条目，看看你是否遗漏了任何必要的项。例如，如果你想让你的 DSL 调制调器允许连接到你的 Web 服务器，但没有相应的 NAT 条目，你的 Web 服务器将无法工作。

# 第 1 部分：构建 Linux 网络

> 提示：为了简便，我们在这里描述了 DSL，但没有描述电缆连接。电缆连接是 DSL 的良好替代方案，取决于你所在的位置，可能是更好的选择。你可以在此处找到更多比较信息：`http://www.epensions.com/cmd-review-60CE-57F8BB0-381C8C5B-bd4`

## 检查你的 ISP 配置

由于 DSL 连接提供了通往 ISP 的路径，因此在检查 ISP 联网连接之前，你的 DSL 服务必须正常工作。以下列表描述了在 DSL 连接工作之前必须正常工作的 ISP 相关系统。

- 你的 DSL 供应商是否与你的 ISP 协调过？
- 你的 ISP 是否已开启你的账户？
- 你的 ISP 使用的是与你的 DSL 设备相同的协议？
- 你是否输入了正确的登录用户名和密码？

## 排除你的防火墙/网关故障

当你与 ISP 的 DSL 连接正常工作后，你可能仍然遇到通信问题。如果你可以在私有网络内通信，并且确信你的 DSL 连接工作正常，那么可能是你的防火墙出了问题。

以下列表列出了你的防火墙可能导致的问题的问题：

- 你网关上的双以太网接口工作正常吗？
- 你网关上的路由配置正确吗？
- 是否安装了正确的内核模块？
- 你的防火墙脚本配置正确吗？
- 你是否使用了正确的测试方法？例如，如果你正在拦截 `ICMP`（如你的防火墙脚本所示），那么传统的 `ping` 将无法工作。在这种情况下，你可能需要使用较高级别的应用程序（如 `Telnet`）来测试你的连接。

## 检查你的 Red Linux 网络配置

第 2 章描述的 Red Hat Linux 网关使用两个以太网接口将你的私有网络连接到互联网。我们在本章前面的“排除 Linux 网络故障”部分描述了排除以太网网卡 `NIC` 配置故障的步骤。你应该查阅文档，获取有关验证网卡是否已正确配置并能够在各自的子网络上通信的信息。

除了基础的网卡配置外，在处理双宿主网关的配置时，涉及到更高层次的问题。两个网卡都必须为各自的网络配置正确的 IP 地址。确保每个子网络都分配给一个网卡。

运行通用的 `ifconfig` 命令来检查网卡。对于我们的网关示例，结果应该如下：

```
eth0 Link encap:Ethernet Hwaddr 00:50:BA:DE:25:35

       inet addr:192.168.1.254 Bcast:192.168.1.255 Mask:255.255.255.0

       UP BROADCAST MULTICAST MTU:1500 Metric:1

       RX packets:740774 errors:0 dropped:0 overruns:0 frame:0

       TX packets:156119 errors:0 dropped:0 overruns:0 frame:0
```

```
eth1 Link encap:Ethernet Hwaddr 00:50:BA:DE:25:35

       inet addr:192.168.1.254 Bcast:192.168.1.255 Mask:255.255.255.0

       UP BROADCAST MULTICAST MTU:1500 Metric:1

       RX packets:740774 errors:0 dropped:0 overruns:0 frame:0

       TX packets:156119 errors:0 dropped:0 overruns:0 frame:0
```

```
eth1 Link encap:Ethernet Hwaddr 00:50:BA:DE:25:35

       inet addr:192.168.1.254 Bcast:192.168.1.255 Mask:255.255.255.0

       UP BROADCAST MULTICAST MTU:1500 Metric:1

       RX packets:740774 errors:0 dropped:0 overruns:0 frame:0

       TX packets:156119 errors:0 dropped:0 overruns:0 frame:0
```

```
lo Link encap:Loopback

       inet addr:127.0.0.1 Bcast:127.0.0.1 Mask:255.0.0.0

       UP BROADCAST MULTICAST MTU:1500 Metric:1

       RX packets:740774 errors:0 dropped:0 overruns:0 frame:0

       TX packets:156119 errors:0 dropped:0 overruns:0 frame:0
```
（注：原文中 `eth1` 的块似乎重复了，此处根据指令保留格式并翻译非代码部分内容）

```
eth1 Link encap:Ethernet Hwaddr 00:50:BA:DE:25:35

       inet addr:192.168.1.254 Bcast:192.168.1.255 Mask:255.255.255.0

       UP BROADCAST MULTICAST MTU:1500 Metric:1

       RX packets:740774 errors:0 dropped:0 overruns:0 frame:0

       TX packets:156119 errors:0 dropped:0 overruns:0 frame:0
```

```
lo Link encap:Loopback

       inet addr:127.0.0.1 Bcast:127.0.0.1 Mask:255.0.0.0
```
