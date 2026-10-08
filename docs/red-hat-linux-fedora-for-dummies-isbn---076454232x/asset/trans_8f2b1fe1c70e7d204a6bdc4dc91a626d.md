

你必须拥有以太网适配器才能连接到以太网。请确保以太网适配器已牢固地插入计算机的主板——插紧。有时，你需要拔出适配器然后再重新插入。拔出适配器并重新插入的过程称为重新插接。

## 你的网络适配器配置是否正确？

有时启动脚本配置错误，导致启动屏幕一闪而过，而你却没有看到错误信息。如果发生这种情况，请以 root 用户身份登录，并在 shell 提示符下输入以下命令：

```
ifconfig
```

你会看到两个不同接口的列表，如下面的代码所示，如果你配置了 PPP，则可能会看到三个接口。`ifconfig` 命令告诉 Linux 内核你拥有一个网络适配器，并为其分配 IP 地址和网络掩码。这是将你的 Linux 计算机连接到网络的第一步：

```
eth0 Link encap:10Mbps Ethernet HWaddr 00:A0:24:2F:30:69
inet addr:192.168.1.1 Bcast:192.168.1.255 Mask:255.255.255.0
UP BROADCAST RUNNING MULTICAST MTU:1500 Metric:1
RX packets:16010 errors:18 dropped:18 overruns:23 TX packets:7075 errors:0 dropped:0 overruns:0
Interrupt:10 Base address:0x300

lo Link encap:Local Loopback
inet addr:127.0.0.1 Bcast:127.255.255.255 Mask:255.0.0.0
UP BROADCAST LOOPBACK RUNNING MTU:3584 Metric:1
RX packets:115 errors:0 dropped:0 overruns:0
TX packets:115 errors:0 dropped:0 overruns:0
```

## 检查你的无线网卡

Linux 提供了几种用于处理 Wi-Fi 网络接口的工具。Red Hat 默认安装 wireless-tools RPM 软件包。这些工具包括 `ifconfig`、`iwspy` 以及其他实用工具。我们将描述如何使用 `iwconfig` 来检查你的 Wi-Fi 接口配置。

### “我是一位敬业者”

一位经验丰富的电气工程师兼 Linux 作者曾经对一家有线电视公司感到非常愤怒。费城老鹰队的一场球赛进行到一半时，他的有线电视服务突然中断了。即使老鹰队正在输球也没关系——他想看比赛，因为老鹰队在阿尔伯克基的电视上很少出现。工程师立即给有线电视公司打了电话。废话！废话！废话！我的连接——废话！

废话！那位和蔼的客服人员一步步引导这位倒霉的工程师通过他自己的故障树排查问题。步骤 1：你的 VCR 或电视打开了吗？“是的，当然。”步骤 2：你 VCR 上的 VCR 按钮是否打开？“当然——哎呀，哦，不，它没开。啊，是的，现在可以了，非常感谢。再见。”真是尴尬！五年电气工程专业的学习到底有什么用呢？

以 root 用户身份登录，打开一个 GNOME 终端窗口（有关更多信息，请参阅第 4 章），并运行 `iwconfig` 命令。如果你的网卡配置正确，你会看到类似以下示例的输出：

```
lo            no wireless extensions.

eth0      IEEE 802.11-DS  ESSID:"linky"  Nickname:"..."
          Mode:Ad-Hoc  Frequency:2.437GHz  Cell: "..."
          Bit Rate:11Mb/s   Tx-Power=15 dBm  Sensitivity:1/3
          Retry limit:4     RTS thr:off   Fragment thr:off
          Encryption key:A654-6277-43D6-ACC3-6E6D-1C12-98
          Power Management:off
          Link Quality:0  Signal level:0  Noise level:0
          Rx invalid nwid:0  Rx invalid crypt:0  Rx invalid ...
          Tx excessive retries:0  Invalid misc:0  Missed ...
```

这些选项是需要重点检查的关键项：

- **Mode：** 当你连接到自组网（ad hoc network）时，必须将此值设置为 Ad-Hoc。（有关此方法的更多信息，请参阅第 7 章。）当你连接到基础结构网络时，可以使用值 Any。在某些情况下，Any 值也可以用于自组网；然而，这些情况的描述超出了本书的范围，因此必要时请使用 ad-hoc 模式。
- **ESSID：** 连接到自组网 LAN 的每一台机器必须使用相同的值。例如，网络上的每台机器都被分配 ESSID linky。
- **Encryption key：** 连接到你的无线网络的每台机器必须使用相同的加密密钥。密钥分为两种类型：40 位和 128 位。40 位密钥几乎无用，因为黑客可以使用广泛可用的软件轻松破解它。

只要你正确设置这些参数，并且你的计算机在局域网内其他设备的范围内，你的无线网络就应该能正常工作。其他参数要么是自动生成的，要么对于使卡片正常工作不重要。

## 也许物理连接没有设置好

如果你没有看到包含 `lo`（回环接口）或 `eth0`（你的网络适配器）的行，那么你的物理网络连接没有设置好。回环接口不是一个物理设备；它用于网络软件的内部工作。网络适配器配置时需要存在回环接口。

如果回环接口不存在，输入以下命令：

```
ifconfig lo 127.0.0.1
```

如果网络适配器（通常是以太网卡）不存在，输入以下命令：

```
ifconfig eth0 192.168.1.1
```

由于此地址是 C 类网络地址，`ifconfig` 会自动默认为 `255.255.255.0` 子网掩码。如果你有非典型的子网掩码（你不应该这样做），请键入以下命令：

```
ifconfig eth0 192.168.1.1 netmask 255.255.255.0
```

键入 `ifconfig`，你的网络适配器应该能正确显示。如果没有，请查看 `ifconfig` 的手册页。你可以通过键入以下命令并按 Enter 来显示此手册页：

```
man ifconfig
```

你可以通过多种方式翻阅文档：按 Enter 逐行前进，按空格键逐页前进，按 Ctrl+B 逐页后退，或按 Q 退出。`ifconfig` 手册页提供了关于 `ifconfig` 是什么及其如何工作的详细信息。如果你仍有问题，请运行以下命令查看 Linux 启动信息：

```
dmesg | more
```

注意，你使用管道（使用 `|` 符号）将 `dmesg` 的输出传递给 `more` 命令。Linux 管道用于将输出命令传递到另一个命令的输入。运行前面的命令后，你将看到启动过程中显示的信息。`more` 命令每次显示一页信息；按空格键显示后续的每一页。

![](img/8c094d1b36276212c03d10d898508a6e_291_0.png)

## 也许你有硬件问题

如果你没有看到你的以太网适配器，你可能有硬件问题。检查你的适配器。**重置它**（取出再重新插入）看看是否工作。如果不工作，你可能需要一个新的网卡。如果你确实看到了网卡，请查看 Linux 内核内部，看看它识别了哪些设备。输入以下命令以切换到一个名为 /proc 的特殊目录，其中包含进程信息：

```
cat /proc/devices
```

你应该看到一行列出了你的网络适配器。如果没有，Linux 不知道它的存在。

![](img/8c094d1b36276212c03d10d898508a6e_292_0.png)

尝试再次运行你的以太网网卡。如果它仍然无法运行，你需要获取更多详细信息。

## 也许你有中断或地址冲突

你可能存在中断或地址冲突。通过键入以下命令，查看内核知道的所有设备的中断列表和 I/O 地址：

```
cat /proc/interrupts
cat /proc/ioports
```

I/O 地址是微处理器（例如，你的 Pentium 芯片）访问设备（例如网络适配器）的内存位置。中断通知微处理器，它应该停止当前所做的任何操作，以处理设备发送中断时到达的信息。

当你的以太网适配器接收到数据包时，它会向微处理器发送中断，以发出事件已发生的信号。你的 Pentium 停止当前操作并处理新信息。微处理器甚至与 Linux 交互以进行处理。

键入 **cat /proc/interrupts** 以显示 Red Hat Linux 熟悉的中断和 I/O 地址。输出应该看起来像以下示例：

```
0: 378425 timer
1: 1120 keyboard
2: 0 cascade
10: 16077 3c509
13: 1 math error
14: 63652 + ide0
```

此列表显示 Linux 知道以太网网卡（3c509）的存在。这是一个好迹象。

