
以下列表描述了该输出内容：在示例中，它是以太网（`Ethernet`）。

- `HAddr` —指定网卡的硬件地址（也称为 `MAC` 地址）。在示例中，硬件地址是 `00:0C:29:76:77:63`。`MAC` 地址的作用是在网络上唯一标识一个网卡（也称为网络适配器）。每个网卡都由其制造商分配一个唯一的 `MAC` 地址。
- `inet addr` —指定 `IP` 地址以及广播地址（`Bcast`）和子网掩码（`Mask`）。广播地址由两部分组成：网络 `ID` 和主机 `ID`。主机 `ID` 设置为 `255`（意味着所有位均已设置）。在示例中，`IP` 地址为 `192.168.75.136`，子网掩码为 `255.255.255.0`，这告诉你这是一个 `C` 类网络。

# 第 8 章 网络通信

- `RX packets` —此行指定了接收的数据包（`RX`）数量。它还显示了错误和丢包的数量，以及有多少数据包过长而无法接收或传输（称为“`overruns`”）。
- `TX packets` —此行显示从计算机通过网络发送的数据包，显示与 `RX` 数据包相同的范围错误信息。
- `Interrupt` —此行显示计算机的配置设置；在本示例中，网卡正在使用中断号 `19`。

如果你只有一个网卡，它被标记为 `eth0`；所有其他网卡被标记为 `eth1`、`eth2` 等。`lo` 代表 `IP` 地址为 `127.0.0.1` 的环回适配器。所有使用 `TCP/IP` 的设备都能识别环回适配器，也称为 `localhost`，它用于测试计算机上 `TCP/IP` 的基本功能。

`ifconfig` 命令还可以使用以下语法配置网卡：

```
ifconfig interface IP address netmask options
```

在此语法中，`netmask` 指你想要分配给正在配置的接口的子网掩码。此外，你还可以为接口设置选项，例如 `up` 开启接口，`down` 关闭接口。以下示例显示了为 `eth0` 接口设置 `IP` 地址和子网掩码：

```
ifconfig eth0 192.168.75.250 netmask 255.255.255.0
```

此命令产生以下输出：

```
eth0 Link encap:Ethernet HWaddr 00:0C:29:76:77:63
addr:192.168.75.250 Bcast:192.168.75.255
Mask:255.255.255.0
net6 fe80::20c:29ff:fe76:7763/64 Scope:Link
BROADCAST MULTICAST MTU:1500 Metric:1
RX packets:105 errors:0 dropped:0 overruns:0
TX packets:274 errors:0 dropped:0 overruns:0 carrier:0
collisions:0 txqueelen:0
RX bytes:2812 (27.4 Kb) TX bytes:5152 (50.3 Kb)
Interrupt:19 Base address:0x224
```

如果你在配置网卡后重启计算机，将丢失所有设置。如果你希望设置永久生效，必须将它们添加到 `/etc/sysconfig/network/ifcfg-eth0` 文件中。

## 活动 8-3：使用 ifconfig 命令

**时间**：`15` 分钟
**目标**：使用 `ifconfig` 命令查看并配置 `TCP/IP`。
**描述**：在此活动中，使用 `ifconfig` 命令查看计算机的 `TCP/IP` 配置并更改 `IP` 地址。

## 配置网卡

1. 启动 `VMware` 并启动 `openSUSE` 虚拟机。
2. 打开终端窗口。输入 `su` 切换到 `root` 用户。
3. 输入 `ifconfig` 显示你的网卡的 `TCP/IP` 配置。你的 `IP` 地址、掩码和广播地址是什么？
4. 输入 `ifconfig eth0 204.21.112.10` 将你的 `IP` 地址更改为 `204.21.112.10`。
5. 输入 `ifconfig` 检查 `IP` 地址已更改。
6. 输入 `reboot` 重启计算机。计算机启动后，打开终端窗口并切换到 `root` 用户。
7. 输入 `ifconfig`（不带参数）查看 `IP` 地址是否仍为 `204.21.112.10`。相同吗？为什么？
8. 输入 `exit` 退出 `root` 账户。保持终端窗口打开。

## Ping 命令

`ping` 命令使用 `ICMP` 向网络上的指定设备发送 `Echo Request` 包并等待回复。管理员使用它来检查连接情况、测量和管理。例如，你可以检查网卡是否配置正确。以下示例显示了 `ping` 命令的输出：

```
ping 192.168.0.6

PING 192.168.0.6 (192.168.0.6): 56(84) bytes of data.
64 bytes from 192.168.0.6: icmp_seq=1 ttl=128 time=0.602 ms
64 bytes from 192.168.0.6: icmp_seq=2 ttl=128 time=0.355 ms
64 bytes from 192.168.0.6: icmp_seq=3 ttl=128 time=0.318 ms
64 bytes from 192.168.0.6: icmp_seq=4 ttl=128 time=0.241 ms

-- ping statistics ---
4 packets transmitted, 4 received, 0% loss, time 6006 ms
rtt min/avg/max/mdev = 0.236/0.348/0.602/0.118 ms
```
