
| tcp | 14:53 | bigtop.azific.com |

| sendmail | 1047 | home.edu |

输出显示了协议、过期时间和目标。

现在，完成练习 15.3，这将让你熟悉 `netstat` 命令的输出。

# 练习 15.3

## 查看网络状态

`ifconfig` 命令是最基础且最重要的网络命令之一。要了解更多关于它的信息，请使用 `ifconfig` 命令查看运行中的 Linux 服务器状态。请确保你能够解释每个输出字段的含义。在进行此练习时，必要时请参考表 15.2，但在参加 RHCE 考试之前，务必彻底熟悉输出格式。

# arp 命令

`arp` 命令报告通过网络接口的 ARP（地址解析协议）表。要查看 ARP 表，请执行命令：

```
arp -a
```

输出类似于如下：

ARP 缓存

 192.168.1.3 at 00:0c:29:xx:xx:xx [eth1] dynamic

 192.168.1.103 at 00:0c:29:xx:xx:xx [eth0] dynamic

 192.168.1.100 at 00:0c:29:xx:xx:xx [eth0] static

 192.168.1.1 at 00:0c:29:xx:xx:xx [eth1] dynamic

 127.0.0.1 at 00:00:00:00:00:00 [lo] incomplete

`arp` 命令允许你查看或修改 IP 地址到 MAC 地址的映射。要查看这些，请执行命令

```
arp -n
```

输出类似于如下：

ARP 表

| address | hwaddr | mask | interface |
| :--- | :--- | :--- | :--- |
| 192.168.1.3 | 00:0c:29:xx:xx:xx | 255.255.255.255 | eth1 |
| 192.168.1.103 | 00:0c:29:xx:xx:xx | 255.255.255.255 | eth0 |
| 192.168.1.100 | 00:0c:29:xx:xx:xx | 255.255.255.0 | eth0 |
| 192.168.1.1 | 00:0c:29:xx:xx:xx | 255.255.255.0 | eth1 |
| 127.0.0.1 | 00:00:00:00:00:00 | 255.0.0.0 | lo |

要删除某个 ARP 条目，请执行格式如下的命令：

```
arp -d host
```

其中 `host` 是主机名。例如，命令

```
arp -d 192.168.1.103
```

会删除 `192.168.1.103` 的 ARP 条目。

![](img/7a53e2be7760e1d422d1c89dbf5d6ede_376_0.png)

当你使用 `ifconfig` 重新配置接口时，更改在系统重启后将会丢失，因为系统初始化脚本会带有网络配置文件中指定的参数值来执行 `ifconfig` 命令。你应当理解这些脚本的操作原理。你执行 `ifconfig` 命令主要是为了排排除网络问题和进行其他网络重配置。若要永久更改网络配置，你应该使用配置工具或直接编辑网络配置文件。

要指定一个 ARP 条目，请执行格式如下的命令：

```
arp -s host mac_addr
```

其中 `host` 是主机名，`mac_addr` 是要关联的 MAC 地址。例如，命令

```
arp -s 192.168.1.1 00:0c:29:xx:xx:xx
```

会建立一个 IP 地址为 `192.168.1.1`、MAC 地址为 `00:0c:29:xx:xx:xx` 的 ARP 条目。你可以指定额外的选项。例如，命令

```
arp -s 192.168.1.1 00:0c:29:xx:xx:xx netmask 255.255.255.0 broadcast 192.168.1.255
```

会建立一个 IP 地址为 `192.168.1.1`、网络掩码为 `255.255.255.0` 以及网络广播地址为 `192.168.1.255` 的 ARP 条目。更多选项请参阅 `arp` 的帮助页面。

# /etc/sysconfig 文件

除了网络脚本和 `network-scripts` 子目录，`/etc/sysconfig` 目录包含了各种系统设施的配置。表 15.4 总结了这些内容。

表 15.4 /etc/sysconfig 中的文件和目录

| 目录 | 描述 |
| :--- | :--- |
| apmd | 包含电源管理 (APM) |
| clock | 时钟配置，指示时钟是否设置为协调时间 (UTC) |
| console | 控制台配置，包括键位（目录） |

# 表 15.4 /etc/sysconfig 中的文件和目录（续）

| 文件/目录 | 描述 |
| :--- | :--- |
| init | 系统启动配置，包括应报告的服务启动状态 |
| keyboard | 键盘配置，包括默认键映射的标识 |
| mouse | 鼠标配置，包括鼠标类型以及是否需要三键仿真 |
| network | 网络配置，包括主机名和网关 |
| network-scripts | 网络配置脚本（目录） |
| pcmia | PCMCIA 配置，启动时是否应加载 PCMCIA |
| sendmail | sendmail 配置，sendmail 是否以守护进程方式运行 |
| soundcard | 声卡配置，包括声卡类型 |
| static-routes | 静态路由，包括关联的设备、网络地址和网关 |

Linux 程序允许你配置大多数此类设施。如果你有需要，大多数文件可以使用文本编辑器安全地修改。然而，声卡配置是一个例外。你应该使用 `sndconfig` 工具来配置声卡，而不应手动编辑 `/etc/sysconfig/soundcard` 文件。

后续章节提供了有关电源管理、PCMCIA、即插用设备和声卡的更多信息。

## 高级电源管理 (APM) 配置

高级电源管理 (APM) 有助于节电。它对于电池供电计算机（如笔记本电脑）特别有用；然而，许多现代桌面计算机也支持 APM，你可以用它关闭未使用的外设设备。当在笔记本电脑上使用 APM 并检测到低电量情况时，它会降低显示亮度、显示 CPU 时钟并关闭外设设备以节省能量。`/etc/sysconfig/apmd` 文件包含 APM 配置，该配置由脚本 `/etc/rc.init.d/apm` 引用。有关配置和使用 APM 的信息，请参阅《电池供电版 Linux Mini-HOWTO》。

## PCCMIA 配置

PCCMIA 服务管理 PCCMIA 卡。`/etc/sysconfig/pcmia` 文件包含 PCCMIA 服务配置信息，该信息由脚本 `/etc/rc.init.d/pcmia` 引用。PCCMIA 设备的配置信息存储在 `/etc/pcmia` 中。如果你重新编译了使用 PCCMIA 的系统的 Linux 内核，还必须重新编译并安装 PCCMIA 软件包。有关 PCCMIA 的更多信息，请访问 Linux PCCMIA 网站 pcmia.sourceforge.org。

## 即插即用配置

如第 2 章所述，即插即用设备的设计是通过 BIOS 和操作系统之间的协作自动配置。然而，Linux 并不完全支持 ISA 接口卡的即插即用。在使用支持即插即用的 BIOS Linux 时，请将 BIOS 设置为指示操作系统不支持即插即用。你可以通过以下命令配置 ISA 即插即用卡：

- 执行命令 `pndump >/etc/isapnp.conf`

此命令将每个已安装即插即用卡的配置转储到指定文件 `/etc/isapnp.conf` 中。

- 使用文本编辑器修改 `/etc/isapnp.conf` 文件，该文件包含每个即插即用设备和设备配置的注释行。你必须取消每个设备所需配置的注释。你还必须取消设备配置末尾的行，该行指定该设备为激活状态。

- 执行命令

  `nisapnp /etc/isapnp.conf`

此命令根据 `/etc/isapnp.conf` 中提供的配置，对 `/etc/isapnp.conf` 安装的即插即用卡进行配置。Linux 启动序列在启动期间执行此命令以配置即插即用设备。

有关 Linux 支持即插即用的更多信息，请访问 www.roe-stock.demon.co.uk/isapnptools。

## 音频配置

`sndconfig` 命令检测并配置大多数即插即用声卡。该命令将配置信息放在 `/etc/conf.modules` 和 `/etc/isapnp.conf` 以及 `/etc/sysconfig/soundcard` 中。

如果你在 X 下使用 GNOME 桌面管理器，GNOME 音频管理器 `esd` 将管理你的声卡并允许多个应用程序同时访问它。然而，如果你执行一个无法感知 `esd` 的应用程序，它可能会与其他应用程序发生冲突。为了避免这种情况，请使用 `esdsp` 包装器调用应用程序。通过执行以下命令启动应用程序：
