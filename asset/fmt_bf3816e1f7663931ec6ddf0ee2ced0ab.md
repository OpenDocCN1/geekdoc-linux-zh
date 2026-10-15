
启动项目时你应该的第一件事是弄清楚你需要完成什么，并注意任何必须满足的特定条件或必须考虑的限制条件。这将帮助你规划解决方案，并防止在你沉浸于可能出现的无数细节和微小障碍时迷失目标。（我无法告诉你曾多少次在完成项目后才意识到，我花费了 80% 的时间在处理 20% 的功能上，而完全忘记了实现另一个 20% 的功能。）

我们配置 `silicon` 的目标是：

- 通过路由器启用两个独立 IP 子网之间的通信。
- 每个 IP 子网都在自己的物理以太网子网上。子网 $A$ 为 `192.168.16.0/24`；子网 $B$ 为 `192.168.18.0/24`。
- 两个子网都应能够完全访问对方。
- 地址 `192.168.16.1` 和 `192.168.18.1` 分别预留为子网 $A$ 和子网 $B$ 的网关地址。

通常画图会非常有帮助。即使你理解给定的拓扑如何解决当前问题，图表也能帮助其他想要理解的人（并可能帮助你在犯错之前识别错误）。在用图形方式描绘网络时要尽量保持一致——一套简单的约定可以使想法的交流更加清晰，特别是对于更复杂的拓扑结构。一张图“胜过千言”（文档），但花费八小时时间画一张带有一堆零件编号的华丽图通常是浪费时间。我使用的约定见图 3.1。使用这些约定，`silicon` 的拓扑如图 3.2 所示。

![](img/e98e3956bdbeb0fcebd99cf9c0434e1b_81_0.png)

图 3.1 绘制网络时使用的约定

### 3.1.2 配置基础平台

现在我们有了计划和图表，可以卷起袖子开始处理硬件了。我们需要一个带有（至少）两个以太网适配器的系统，每个适配连接到一个物理段，并有足够的磁盘空间来存放你运行的任何 Linux 发行版（可能还有后续示例所需的内核源码）。正如我们在第 1.1 节中讨论的，CPU 本身不需要特别强大就能提供接受的性能。

![](img/e98e3956bdbeb0fcebd99cf9c0434e1b_82_0.png)

图 3.2 带有两个子网的局域网路由器

（本章的 `silicon` 是一个配备 32MB 内存的 166MHz Pentium。）不需要在你的路由器上运行大量软件包；即使是最精简的系统二进制文件足够让事情发生。一旦我们连接并加载了软件，我们需要确保内核可以检测接口、配置它们，然后让它们工作。

### 3.1.3 检测接口

以太网接口是一个设备（通常是硬件），允许计算机连接到以太网。大多数计算机都内置一个以太网接口，但你也可以扩展卡添加更多。要使用接口，Linux 内核必须首先识别并初始化它。内核通过对总线进行设备“探测”来实现这一点。一旦找到设备，内核会为其分配一个名称，如 `eth0`、`eth1` 等。

有几种不同的方法可以判断内核是否已经检测到网卡（NIC）。

1. `/proc/net/dev` 的内容将显示当前系统中配置的所有网络设备。

```
silicon:/root> cat /proc/net/dev
| Inter- | Receive | Transmit |
| face packets drop fifo frame | packets drop fifo collars
lo: 4378 0 0 0 4378 0 0 0 0 0
eth0: 27520 0 0 0 26367 0 0 0 1 0
eth1: 31 0 0 0 17 0 0 0 0
```

这表明 `eth0` 和 `eth1` 设备确实（以及用于连接 IP 地址 `127.0.0.1` 的环回设备 `lo`）。如果设备出现在表中，我们可以为其配置 IP 地址并使用它。遗憾的是，`/proc/net/dev` 并不会告诉我们设备驱动或网卡的设置。

2. `dmesg` 命令显示内核在启动序列期间生成的消息，提供了更多信息。对应三个独立的以太网卡初始化的 `dmesg` 输出：

## 第 3.1 配置局域网路由器

```
silicon:/root> /bin/dmesg
eepro100.c:v0.09j-t 29/99 Donald Becker
https://csds.gsfc.nasa.gov/linux/drivers/eepro100.html
eepro100.c:$Revision: 1.36 $2000/11/17
Modified by Andrey V. Savochkin <saw@saw.sw.com.sg> and others
eth0: PCI i82557/i82556 10 Ethernet, 00:08:07:0A:AD:96, IRQ 9.
Board assembly 692290-002, Physical connectors: RJ45
Primary interface chip i82555 PHY #1.
General self-test: passed.
Serial sub-system self-test: passed.
Internal registers self-test: passed.
ROM checksum self-test: passed (0x24c9f043).
Receiver lock-up workload
```

```
natsemi.c:v1.0 8/7/2000 Written by Donald Becker <<scycld.com>
http://www.scyld.com/network/natsemi.html
unfficial 2.4.x kernel port, version 1.0.2,
October 6, 2000 June Garzik, Tjeder Mulder
eth1: NatSemi DP38388 at 0x482e2000, 00:02:e3:02:a2:a7, IRQ 19.
eth1: Transceiver status 0x7869 advertising 05e1.
```

```
pcnet32_pci: found device 0x001022.0x002000
PCI: Enabling driver 00:12.0 (0001)-> 0003)
ioaddr=0x0001040 resource_flags=0x0000101
divert: allocating driver_blk for eth2
eth2: PCNet/PCI II 79C97A at 0x0140, 00 55 56 22 00 21
pcnet32: pcnet32_private lp=c0d09000 lp_ma_addr=0x009000 assigned IRQ 10.
cnet32.c:v1.25f.26.9.1389 tsbogend@alla.franken.
```

`dmesg` 提供了关于驱动程序和初始化的更多信息，但输出内容并没有固定的格式。不同的设备驱动作者会根据自己的意愿显示初始化过程的各个方面，并按照他们选择的顺序进行排列。对于示例输出，我在每个驱动程序的每次初始化之间添加了空格。你可能需要仔细观察，以便将一个驱动程序的输出与另一个驱动程序的区分开来。

注意，你可以通过名称（如 `eth0`、`eth1` 等）来控制操作系统识别哪块物理卡，这只需重新排列设备驱动模块的加载顺序即可。在你有多个相同类型的网卡的情况下，情况并不那么简单。如下面的示例输出所示，加载 `3c59x` 会检测并初始化它们中的两个。现在，哪块网卡是 `eth0` 呢？说实话，我不知道，我认为解决这个问题最快的方法是将其中一块网卡插入一个子网中，使用 `ifconfig` 为该子网配置一个 IP，然后 `ping` 另一个地址。（或者，你也可以嗅探通过特定接口的流量）。如果这听起来没没意义，将在第 3.3 节中解释清楚。

```
3c59c:v0.99E 5/12/98 Donald Becker
(https://csds.gsfc.nasa.gov/linux/drivers/vortex.html)
```

```
eth0: 3Com 3c905 Boomerang 100baseTx at 0xffc0, 00:60:97:8d:91, IRQ 11
8K word-wide RAM 3:5 Rx:Tx split, autoselect/Way Autonegotiation interface.
MII transceiver found at address 24, status 786b.
Enabling bus-master transfers and whole-frame receives.
eth1: 3Com 3c905 Boomerang 100baseTx at 0xffc8, 00:60:97:26:06b:7, IRQ 10
8K word-wide RAM 3:5 Rx:Tx split, autoselect/Way Autonegotiation interface.
MII transceiver found at address 24, status 786b.
Enabling bus-master transfers and whole-frame receives.
```
