
# 术语表

## A-F

### I/O
**输入/输出 (input/output, I/O)** 一种描述从外部源接收数据或向外部源发送数据的类型。在某些情况下，“外部源”可能是计算机内部的，例如硬盘与 `CPU` 或内存之间的 I/O。在其他情况下，I/O 更加明确是外部的，例如网络 I/O。

### Installed File Database
**已安装文件数据库 (installed file database)** 通过计算机软件包管理器（如 `RPM` 或 `Debian`）安装的文件数据库，以及依赖关系等关联信息。也称为包数据库。

### Internal Transfer Rate
**内部传输率 (internal transfer rate)** 设备内部的数据传输速率。这通常应用于硬盘和类似设备，即它们从物理介质读取或写入数据的速度。

### Internet
**互联网 (internet)** 任何通过路由器连接在一起的网络集合。另参见 `Internet`。

**Internet (互联网)** 地球上最大的网络，连接全球各地。当以此方式使用时，该单词始终大写。另参见 `internet`。

### IMAP
**互联网消息访问协议 (Internet Message Access Protocol, IMAP)** 一种用于交换邮件信息的协议。接收者发起 `IMAP` 会话。`IMAP` 与 `POP` 的区别在于，`IMAP` 允许接收者在服务器上组织良好的文件夹中保留消息；而 `POP` 要求接收者下载消息以便组织。

`IMAP` 互联网消息访问协议 (IMAP)。

### Incremental Backup
**增量备份 (incremental backup)** 一种备份类型，仅备份自上次备份以来更改的文件。这用于缩短备份计算机所需的时间，代价是可能会增加恢复的复杂性。

### IPX
**IP 数据交换 (Internet Packet Exchange, IPX)** 一种底层协议。

### IEEE-1394
`IEEE-1394` 一种用于连接硬盘、扫描仪和视频设备等高速外部设备的总线技术。`IEEE-1394` 正在逐渐变得流行。Linux `2.4.x` 增加了有限的 `IEEE-1394` 支持。

## M

`MAC` 地址 参见媒体访问控制 (MAC) 地址。

`machine name`（机器名）主机名中用于识别网络上计算机的部分，相对于整个网络而言（例如，`gingko` 是 `gingkgo.example.com` 的机器名部分）。机器名有时也指代整个主机名。

`main memory`（主内存）计算机中主要的 RAM 类型，相对于缓存内存。

`major version number`（主版本号）程序版本号中的第一个数字。例如，如果一个程序版本号为 `1.2.3`，则主版本号为 `1`。

`man pages`（帮助页）针对程序、配置文件、系统调用或其他系统特功能的电子“手册”。通过输入 `man` 后紧跟你想要学习的程序或其他主题来访问帮助页，例如输入 `man` 来学习关于帮助页系统本身的知识。

`master`（主设备）单个 `ATA` 通道上的两个设备之一。主设备获取的 Linux 设备号比从设备（`slave`）小。

`Master Boot Record` (MBR，主引导记录）硬盘的第一个扇区。`MBR` 包含了 `BIOS` 在启动过程中运行的代码以及主分区表。

`MBR` 参见 `Master Boot Record` (MBR)。

`MD4 password` 参见 消息摘要 4 (MD4) 密码。

`MD5 password` 参见 消息摘要 5 (MD5) 密码。

`Media Access Control` (MAC，媒体访问控制) 与网络硬件关联的低层地址，仅用于本地网络寻址。网络之间的寻址（如互联网上的网络）使用更高层次的地址，例如 `IP` 地址。

`Message Digest 4` (MD4，消息摘要 4）使用消息摘要 4 (MD4) 哈希算法存储的密码。`MD4` 密码在 `Windows` 系统中很常见，也用于 `Samba` 的加密密码。

`Message Digest 5` (MD5，消息摘要 5）使用消息摘要 5 (MD5) 哈希算法存储的密码。近期的 Linux 系统通常使用 `MD5` 密码。

`mode`（模式/权限）文件的权限。结合文件的所有者和用户组，模式决定了谁可以以何种方式访问文件。

`mode lines`（模式行）定义了在特定刷新率下运行特定视频分辨率所需的时间定义。

`modem`（调制解调器）该词是“调制器/解调器”（`modulator/demodulator`）的缩写。它是一种通过模拟传输介质传输数字数据的设备。传统上模拟传输介质是普通电话网络，但“modem”一词也越来越多地应用于宽带接入接入的设备。

`module`（模块）存储在单独文件中的内核驱动程序或其他内核组件。Linux 可以根据需要或命令加载模块，在模块未未使用时节省 RAM 并减小内核体积。

`motherboard`（主板）计算机中的主电路板。`CPU`、`RAM` 和扩展卡通常直接插在主板上，尽管某些设计将这些组件部分放置在扩展卡上。主板有时也被称为 `mainboard` 或系统板。

`mount`（挂载）1. 将文件系统（见定义 1）添加到目录树的过程。2. 执行此项任务的同名命令。

`mount point`（挂载点）挂载新文件系统（见定义 1）的目录。在宿主文件系统挂载之前，挂载点通常是空目录。

## N

`NetBEUI` 一种在大纲上类似于 `AppleTalk` 或 `TCP/IP` 的网络栈，但主要用于本地网络。

`NetBIOS` 通常与 `NetBEUI` 或 `TCP/IP` 联合使用的网络协议。`NetBIOS` 是 `Microsoft Windows` 使用的 `SMB/CIFS` 文件共享协议的基础，并在 `Samba` 在 Linux 中实现。

`netmask`（掩码）参见 `network mask`。

`Network Filesystem` (NFS，网络文件系统) Linux 和 Unix 计算机之间的文件共享协议。

`Network Information Service` (NIS，网络信息服务) 允许计算机共享简单数据库文件的网络协议。通常用于提供集中登录认证，并作为小型网络中 `DNS` 的替代品。

`network mask`（网络掩码）一种识别 `IP` 地址整个网络部分和识别网络上计算机部分的位模式。该模式可以表示为用点分隔的 4 个十进制（如 `255.255.255.0`），也可以表示为 `IP` 地址后跟斜杠和网络位位数（如 `192.168.45.203/24`）。网络掩码也被称为网络掩码或子网掩码。

`NFS` 参见 `Network Filesystem` (NFS)。

`NIS` 参见 `Network Information Service` (NIS)。

`node`（节点）`info` 页面（参见 `info pages`）中的单个单页。

`non-volatile RAM` (NVRAM，非易失性随机存储器）一种即使断电后也能保留数据的内存。`NVRAM` 通常用于存储 `BIOS` 设置。

## O

`open mail relay`（开放邮件中继）配置为可以从任何地方向任何地方转发邮件的 `SMTP` 邮件服务器。开放邮件中继经常被垃圾邮件者滥用以隐藏消息的真实来源。

`open port`（开放端口）被服务器程序使用且外部系统可以访问的网络端口。不必要的开放端口会带来安全风险，应当关闭。

`Open System Interconnection` (OSI) model（开放系统互连模型）一种描述网络栈（如 `TCP/IP`、`NetBEUI` 或 `AppleTalk`）的方法。在 `OSI` 模型中，栈被分为若干层，每层直接与其上下的层通信。

`OSI model` 参见 `Open System Interconnection` (OSI) model。

## P

`package`（包）参见已安装数据库。

`packet`（数据包）随信封收集并在网络上传输的有限量数据。

`packet filter`（数据包过滤器）根据源和目的等包信息通过或拒绝数据包的防火墙类型。

`packet sniffer`（数据包嗅探器）在低层监控网络流量的程序。

`parallel ATA` (PATA，并行 ATA）一次传输比特的传统 `ATA`形式。

`parameter`（参数）传递给程序的选项。

`parent process`（父进程）指启动进程的相对术语。

`Partition`（分区）硬盘的连续部分。

`partition table`（分区表）描述分区布局的数据结构。

`path`（路径）可能找到文件的冒号分隔目录列表。

`payload`（有效负载）网络包中包含要传输数据的部分。

`PC Card`（PC 卡）笔记本电脑上常用的扩展卡类型。这种接口常用于以太网卡、调制解调器和存储设备。也称为 `PCMCIA`。

`PCI` 参见 `Peripheral Interconnect` (PCI)。

`PCL` 参见 打印机语言。

`PCMIA` 参见 `Personal Computer International Association` (PCMIA)。
