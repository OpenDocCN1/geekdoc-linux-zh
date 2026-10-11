
`x11perf -all`

### 实验 15.1 配置以太网接口

#### 目标

本实验演示了如何在不重启 Linux 的情况下实时更改任何接口参数。它将向你展示如何更改以太网卡的 IP 地址、子网掩码、广播地址或 MAC 地址。它还将向你展示如何为访问本地网段之外的数据包设置默认路由。

#### 所需材料

本实验需要以下条件：

- 运行 Linux 的计算机的 root 用户访问权限
- 你的计算机上安装了以太网网卡 (NIC)

#### 活动背景

当你处理接口和 IP 地址时，使用的主要程序是 `ifconfig`。它是“interface configuration”缩写。在本实验中，你将配置以太网接口（以太网 NIC）。你的第一块以太网卡默认被称为 `eth0`。如果你有第二块以太网卡，它被称为 `eth1`。

Windows 有一个名为 `ipconfig` 的类似程序，因此如果你同时操作 Linux 和 Windows，可能会可能会感到困惑。

你还将学习使用 `route` 命令来设置默认网关，该路由器充当通往本地网段外部网络通信的默认出口点。

预计完成时间：25 分钟

#### 活动

- 1. 按 `Ctrl+Alt+F2` 切换到第二个虚拟控制台 (`tty2`)，并以 root 。
- 2. 当你带命令行参数运行 `ifconfig` 时，它会显示所有接口的状态消息。输入 `ifconfig`。当你的接口是单块以太网卡 (`eth0`) 时，你会看到类似下面的状态显示：

```
eth0      Link encap:Ethernet HWaddr 00:07:95:BB:A3:6A

inet      addr:192.168.0.1 Bcast:192.168.0.255 Mask:255.255.255.0

          UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1

          RX packets:1611 errors:0 dropped:0 frame:0

TX packets:1712 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueue:100

RX bytes:243068 (237.3 Kb) TX bytes:382677 (377.3 Kb)

Interrupt:11 Base address:0xde00
```

```
lo Link encap:Local Loopback

inet addr:127.0.0.1 Mask:255.0.0.0

UP BROADCAST RUNNING MTU:16436 Metric:1

RX packets:1712 errors:0 dropped:0 overruns:0 frame:0

TX packets:1712 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueue:100

RX bytes:1101 (1.0 Kb) TX bytes:1101 (1.0 Kb)
```

上述输出中的 `lo` 指的是本地回环 (Local Loopback) 网络设备，你可以在实验 15.2 中学习更多信息。
- 3. 你通过在 `ifconfig` 命令上传递新地址作为参数来更改卡的 IP 地址。输入 `ifconfig eth0 192.168.0.22`
- 4. 你可以通过在命令行上指定接口名称来查看单个接口的状态。输入 `ifconfig eth0`。你会看到类似的内容：

```
eth0 Link encap:Ethernet HWAddr 00:07:95:BB:A3:6A

inet addr:192.168.0.2 Bcast:192.168.0.25 Mask:255.255.255.255

UP BROADCAST MULTICAST MTU:1500 Metric:1

RX packets:1611 errors:0 dropped:0 overruns:0 frame:0

TX packets:1712 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueue:100

RX bytes:243068 (237.3 Kb) TX bytes:382677 (377.3 Kb)

Interrupt:11 Base address:0xde00
```
- 5. 你可以通过在命令行上指定子网掩码来更改它。输入 `ifconfig eth0 netmask 255.255.254`
- 6. 再次通过输入 `ifconfig eth0` 显示 `eth0` 的状态。你会看到类似这样的：

```
eth0 Link encap:Ethernet HWAddr 00:07:95:BB:A3:6A

inet addr:192.168.0.2 Bcast:192.168.0.255 Mask:255.255.255.0

UP BROADCAST MULTICAST MTU:1500 Metric:1

RX packets:1611 errors:0 dropped:0 overruns:0 frame:0

TX packets:1712 errors:0 dropped:0 overruns:0 carrier:0

collisions:0 txqueue:100

RX bytes:243068 (237.3 Kb) TX bytes:382677 (377.3 Kb)

Interrupt:11 Base address:0xde00
```
