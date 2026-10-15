
# 初始化以太网接口

| 参数 | 描述 |
| --- | --- |
| `dstaddr addr` | 设置点对点链路另一端的 IP 地址。该参数已被 `pointoint` 关键字废弃。 |
| `netmask addr` | 为指定的接口设置 IP 网络掩码。 |
| `[-]broadcast [addr]` | 当包含地址时，设置该接口的广播地址。如果没有给出地址，则开启指定接口的 `IFF_BROCAST` 标志。使用减号可以关闭该标志。 |
| `[-]pointoint [addr]` | 在指定的接口上开启点对点模式。这告诉内核该接口是到另一台机器的直接链路。如果包含地址，则将其分配给列表另一端的机器。如果未给出地址，则开启接口的 `IFF_POPOINT` 标志。使用减号可以关闭该标志。 |
| `hw` | 为指定的接口设置硬件地址。此关键字之后必须跟上硬件类别的名称和硬件地址的 ASCII 等效值。现在支持以太网 `ether`、`AMPR AX.25` `ax25` 和 `PPP` `ppp`。 |
| `address` | 要分配给指定接口的主机名或 IP 地址。此处使用的主机将解析为相应的 IP 地址等效值。此参数是必须的。 |

你通常不需要使用所有选项。`ifconfig` 仅通过接口名称、掩码和 IP 地址即可设置一切。只有当 `ifconfig` 遗漏或你拥有复杂的网络时，才需要显式设置参数。

> 注意
> 如果 Linux 机器连接到网络，则必须确保 `ifconfig` 程序免受未经授权的使用。将网络接口设置为混杂模式将允许人员嗅探你的网络并获取密码等敏感数据。这是一次严重的安全违规。
> 参见“处理物理安全”，第 238 页。

## 使用 ifconfig 检查网络接口

不带任何参数运行 `ifconfig` 会导致其输出内核知道的所有网络接口的状态。在命令行中仅带接口名称运行 `ifconfig` 将打印该接口的状态：

```
$ ifconfig lo
lo encap Local Loopback
inet addr 127.0.0.1 Bcast 127.255.255 Mask 255.255.255.0
UP LOOPBACK RUN MTU 2000 Metric 1
RX packets 0 errors 0 dropped overruns 0
TX packets 1658 errors 10 dropped overruns 0
```

## 第 23 章 配置 TCP/IP 网络

此示例使用了 `lo10`，即软件回环接口。你可以看到分配的 IP 地址 `inet addr`、广播地址 `Bcast` 和网络掩码 `Mask`。该接口处于 `UP`（开启）状态，MTU 为 2000，Metric 为 1。最后两行提供了接收 `RX` 和发送 `TX` 的数据包数量统计信息，以及数据包错误、丢弃和溢出计数。

## 配置软件回环接口

所有在内核中安装了网络层的 Linux 机器都有一个软件回环接口。该接口用于测试网络应用程序，并在机器未到真实网络时为本地 TCP/IP 服务提供网络。

回环系统的网络接口名称为 `lo10`。输入以下命令运行 `ifconfig`：

```
ifconfig lo 127.0.0.1
```

这将激活回环接口并为其分配地址 `127.0.0.1`。这是传统上用于回环的地址，因为 A 类网络 `127.0.0.0` 永远不会被 InterNIC 分配给任何人。

要使回环系统完全运行，你需要使用 `route` 命令为其添加路由，该命令在“理解 TCP/IP 路由”章节中进行了讨论。

## 配置网络接口

配置以太网网络接口需要稍多工作，特别是当你使用子网时。对于 `unix1.tristar.com`，基础的 `ifconfig` 调用如下：

```
ifconfig eth0
```

这会导致 `ifconfig` 激活以太网接口 `0`，在 `/etc/hosts` 文件中查找 `unix1` 的 IP 地址并将其分配给该接口。此时检查 `eth` 接口将显示以下内容：

```
$ ifconfig eth0
eth0 Link 100Mbps Ethernet Waddr 00:00:E1:54:3B:82
inet addr 162.168.1.21 bcast 162.168.1.255 Mask 255.255.255.250
UP BROADCAST RUNNING MTU 1500 Metric 0
RX packets 3158 errors 21 dropped 7 overrun 26
```
