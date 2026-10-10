
```
2 rows in set (0.00 sec)
```

在下一个示例中，`PASSWORD()` 函数返回由作为其参数提供的文本生成的哈希值（第 1151 页）。`UPDATE` 语句将此哈希值分配给 `person` 列值为 `sam` 的行的 `password` 列。此示例不更改 `MySQL` 密码信息，因为该信息存储在名为 `mysql` 的数据库中；此语句针对的是 `maxdb` 数据库。

```
mysql> UPDATE people
     -> SET password=PASSWORD("samsap*")
     -> WHERE person='sam';
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

下一条查询搜索 `password` 为 `null`（`IS NULL`）且（`AND`）`executeperm` 为真（`=true`）的行。

```
mysql> SELECT person,password,executeperm
     -> FROM people
     -> WHERE password IS NULL AND executeperm=true;
```

| person | password | executeperm |
| :--- | :--- | :--- |
| max | NULL | 1 |
| topsy | NULL | 1 |

```
2 rows in set (0.00 sec)
```

由于 `PASSWORD()` 是一个单向哈希函数（第 1163 页），您无法从密码哈希中检索出明文密码。但是，您可以检查是否有任何用户的用户名作为其密码：

```
mysql> SELECT * FROM people
  -> WHERE password=PASSWORD(person);

+-------+----------------------------------------------+------------+----------+------------+-------------+
| person | password                                     | created    | readperm | writeperm  | executeperm |
+-------+----------------------------------------------+------------+----------+------------+-------------+
| topsy | 8E5E773736B8F836F58A... | 2010-03-05 |        1 |          1 |           1 |
+-------+----------------------------------------------+------------+----------+------------+-------------+
1 row in set (0.00 sec)
```

使用 `UPDATE` 语句将 `Topsy` 的密码设为 `NULL`：

```
mysql> UPDATE people
  -> SET password=NULL
  -> WHERE person="topsy";
Query OK, 1 row affected (0.00 sec)
Rows matched: 1  Changed: 1  Warnings: 0
```

```
mysql> SELECT person,password
  -> FROM people
  -> WHERE password IS NULL;

+--------+----------+
| person | password |
+--------+----------+
| max    | NULL     |
| zach   | NULL     |
| topsy  | NULL     |
+--------+----------+
3 rows in set (0.00 sec)
```

### 章节摘要

`users-admin` 实用工具用于向系统添加新的用户和组，并修改现有用户的账户。您还可以使用等效的命令行工具（`useradd`、`usermod`、`userdel`、`groupadd` 和 `groupmod`）来管理用户账户。

备份系统上的文件是系统管理中至关重要但常被忽视的一部分。`Linux` 包括 `tar`、`cpio`、`dump` 和 `restore` 实用工具来备份和恢复文件。您还可以使用更复杂的软件包，如 `amanda` 以及各种商业产品。

系统调度守护程序 `cron` 定期执行计划任务。您可以使用 `crontab` 和 `at` 来安排任务。

系统报告展示了系统的健康状况。两个生成这些报告的有用工具是 `vmstat`，它详细介绍虚拟内存、`I/O` 和 `CPU` 使用情况；以及 `top`，它报告系统当前的性能状况，并有助于您找出可能拖慢系统的原因。

系统管理的另一个方面是解决问题。`Linux` 包含若干有助于追踪系统问题的工具。其中最重要的工具之一是 `syslogd`，即系统日志守护程序。使用 `/etc/syslogd.conf`，您可以控制哪些错误消息显示在控制台上，哪些作为电子邮件发送，哪些写入多个日志文件之一。

系统管理员经常需要设置和管理 `MySQL` 数据库。`MySQL` 是 `LAMP`（`Linux`、`Apache`、`MySQL`、`PHP`/`Perl`/`Python`）中的 `M`，这是一个开源企业软件栈。许多编程语言提供对 `MySQL` 的接口（例如，`C`、`PHP`、`Perl`）。

# 练习题

1. 如何列出正在运行 `vi` 的所有进程？
2. 如何使用 `kill` 让服务器进程重新读取其配置文件？
3. 从命令行，如何创建一个名为 John Doe 的用户，其用户名为 `jd`，且属于组 `65535`？
4. 如何通知用户你将在十分钟后重启系统？
5. 给出一个命令，在系统第一个磁带设备上创建 `/usr` 文件系统的 0 级转储。您使用哪个命令来利用支持压缩的设备？哪个命令会在磁带上 0 级转储之后立即放置 `/var` 文件系统的 3 级转储？

# 高级练习题

6. 如果系统响应速度低于正常水平，找出问题所在的好第一步是什么？
7. 某个进程将其 PID 编号存储在名为 `process.pid` 的文件中。编写一个命令行来终止此进程。
8. 在拥有 `root` 权限的情况下，您打算删除一些文件，但想确保使用的通配符表达式是正确的。提出两种确保您删除正确文件的方法。
9. 创建一个 `crontab` 文件，定期执行以下备份：
   a. 每月执行一次 0 级备份。
   b. 每周的一天执行一次 2 级转储。
   c. 在既没有执行 0 级转储也没有执行 2 级转储的每一天执行一次 5 级转储。

在最坏的情况下，按照此计划转储的文件需要多少个 `restore` 命令才能恢复？

# 17 配置和监控局域网

###### 本章内容

- 设置硬件 . . . . . . . . . . . 638
- 路由器 . . . . . . . . . . . . . . . . . 638
- NIC：网络接口卡 . . . . . . . . . . . . . . 639
- 配置系统 . . . . . . . . . . . . . . 641
- 设置服务器 . . . . . . . . . . . . . . 646
- 介绍 Cacti . . . . . . . . . . . . . . 647

计算机网络允许计算机相互通信并共享资源。局域网（`LAN`）连接位于同一地点（如办公室、家庭或图书馆）的计算机，并允许连接的计算机共享 `Internet` 连接、文件和打印机。当然，建立局域网最重要的原因之一是允许系统通信，同时用户享受多人游戏。

本章涵盖配置局域网的两个方面：设置硬件和配置软件。它不一定按照您设置特定局域网时执行任务的顺序组织。相反，请通读本章，弄清楚您将如何设置您的局域网，然后按照适合您设置的顺序阅读本章的相关部分。最后一节讨论如何使用 `Cacti` 监控网络设备。

![](img/2344fc4a798f29dca9e8b5ed7288171a_687_0.png)

# 设置硬件

局域网上的每个系统或节点都必须有一个网络接口卡（`NIC`）。每个系统必须连接到中心集线器或交换机。如果局域网连接到另一个网络（如 `Internet`），它还必须有一个路由器。

## 连接计算机

计算机通过电缆（有线；第 375 页）或无线电波（无线或 `Wi-Fi`，第 376 页）连接到网络。电缆可以连接到各种设备，本节描述了一些设备。有关电缆的解释以及集线器、交换机和路由器的定义，请参见第 375 页的“`LAN`：局域网”。

在图 17-1 所示的简单网络中，四台计算机连接到一个集线器或交换机。假设计算机 1 和 2 在计算机 3 和 4 通信的同时也在通信。使用集线器（第 375 页）时，每个通信会话的限制是网络带宽的一半。使用交换机（第 375 页）时，每个通信会话理论上可以使用全部网络带宽。

集线器通常比交换机便宜，尽管交换机正变得越来越便宜，而集线器变得不那么容易获取。如果您计划使用网络共享 `Internet` 连接和轻微的文件共享，集线器可能速度足够快。如果网络中的系统将经常交换文件，交换机可能是更好的选择。

## 无线接入点（WAP）

无线接入点（`WAP`）将无线网络连接到有线网络。通常，`WAP` 充当透明网桥，将两个网络之间的数据包转发，就好像它们是一个网络一样。如果您将多个位于不同位置的 `WAP` 连接到同一个有线网络，无线客户端可以透明地在 `WAP` 之间漫游。

无线网络不需要集线器或交换机，尽管 `WAP` 可以选择充当集线器的角色。在无线网络中，带宽由范围内所有节点共享；最大速度受最慢节点的限制。

## 路由器

路由器（第 377 页）将局域网连接到另一个网络，如 `Internet`。路由器可以执行多项功能，其中最常见的是允许多个系统共享单个 `Internet` 连接和 IP 地址（`NAT`，第 881 页）。当路由器使用 `NAT` 时，局域网中每个系统的数据包似乎来自单个 IP 地址；路由器将返回数据包传递给正确的系统。路由器还可以充当防火墙。

您有几种路由器选择：

- 简单的硬件路由器相对便宜，并且能做小型网络所需的大多数事情。

![](img/2344fc4a798f29dca9e8b5ed7288171a_689_0.png)

**图 17-1** 一个简单的网络

- 你可以将 `Ubuntu` 系统配置为路由器。`Linux` 内核可以使用 `gufw`（第 876 页）或 `iptables`（第 880 页）来实现防火墙，以帮助保护系统。
- 你可以使用专为路由器用途定制的特殊发行版/操作系统。例如，`SmoothWall` (www.smoothwall.org)、`pfSense` (www.pfsense.com) 和 `m0n0wall` (m0n0.ch/wall) 提供了基于浏览器的配置，其风格类似于硬件路由器。

## NIC：网络接口卡

每个系统的 `NIC` 可能是一块独立的以太网卡（有线或无线），或者 `NIC` 可能集成在主板上。

| **支持的 NIC** | Linux 支持大多数有线和许多无线以太网 NIC。 |
|---|---|
| **不支持的无线 NIC** | 如果无线网卡无法在 Linux 下直接支持，你可以尝试使用 NdisWrapper (sourceforge.net/projects/ndiswrapper)、`ndiswrapper-common`、`ndiswrapper-utils-1.9` 和 `ndisgtk` 软件包使其工作，这些软件包使用 Win32 驱动程序。NdisWrapper 是一个内核模块，提供了 Windows 网络驱动程序 API 的一个子集。请参见 help.ubuntu.com/community/WifiDocs/Driver/Ndiswrapper 获取安装 Windows 驱动程序的说明。 |
| **无线网桥** | 无线 NIC 的一种替代方案是无线网桥。无线网桥在有接口和无线接口之间转发数据包，从而消除了对无线驱动程序的需求。这种简单的设备有一个插入 NIC 的以太网端口和一个 802.11（无线）控制器。虽然携带网桥对于移动用户来说通常不可行，但无线网桥是将台式计算机迁移到无线配置的简便方法。 |

无线网络以自组网模式或基础结构模式运行。在自组网模式中，网络中的各个节点直接相互通信。在基础结构模式中，节点通过 `WAP`（无线接入点）（第 638 页）进行通信。如果无线局域网必须与有线局域网通信，基础结构模式通常更可靠。如果你不想使用 `WAP`，可以设置 `WLAN` 卡使其充当 `WAP`。请查阅 `NIC`/驱动程序的文档以获取更多信息。

## 工具

本节介绍了两种可用于检查系统硬件的工具。

### lspci：列出 PCI 信息

`lspci` 实用程序列出 `PCI` 设备信息：

```
$ lspci
00:00.0 Host bridge: nVidia Corporation nForce2 AGP (different version?) (rev c1)
00:00.1 RAM memory: nVidia Corporation nForce2 Memory Controller 1 (rev c1)
00:00.2 RAM memory: nVidia Corporation nForce2 Memory Controller 4 (rev c1)
00:00.3 RAM memory: nVidia Corporation nForce2 Memory Controller 3 (rev c1)
00:00.4 RAM memory: nVidia Corporation nForce2 Memory Controller 2 (rev c1)
00:00.5 RAM memory: nVidia Corporation nForce2 Memory Controller 5 (rev c1)
00:01.0 ISA bridge: nVidia Corporation nForce2 ISA Bridge (rev a4)
00:01.1 SMBus: nVidia Corporation nForce2 SMBus (MCP) (rev a2)
00:02.0 USB Controller: nVidia Corporation nForce2 USB Controller (rev a4)
...
```

使用 `-v` 选项时，`lspci` 会更详细。你可以使用 `-vv` 或 `-vvv` 选项来显示更多的信息。

```
$ lspci -v
00:00.0 Host bridge: nVidia Corporation nForce2 AGP (different version?) (rev c1)
Subsystem: ABIT Computer Corp. Unknown device 1c00
Flags: bus master, 66MHz, fast devsel, latency 0
Memory at e0000000 (32-bit, prefetchable) [size=64M]
Capabilities: <access denied>

00:00.1 RAM memory: nVidia Corporation nForce2 Memory Controller 1 (rev c1)
Subsystem: nVidia Corporation Unknown device 0c17
Flags: 66MHz, fast devsel

00:00.2 RAM memory: nVidia Corporation nForce2 Memory Controller 4 (rev c1)
Subsystem: nVidia Corporation Unknown device 0c17
Flags: 66MHz, fast devsel
...
```

### lshw：列出硬件信息

`lshw` 实用程序列出本地系统硬件配置的信息。以 `root` 权限运行此实用程序可显示更详细的报告。`--short` 选项显示简短的报告。

```
$ sudo lshw -short
H/W path Device Class Description
=================================================
system VMware Virtual Platform
/0 bus 440BX Desktop Reference Platform
/0/0 memory 87KiB BIOS
/0/4 processor AMD Athlon 64 X2 Dual Core Processor 5600+
/0/4/1c memory 16KiB L1 cache
/0/4/0 memory 128KiB L1 cache
/0/4/1 memory 1MiB L2 cache
...
/0/100/f display SVGA II Adapter
/0/100/10 storage 53c1030 PCI-X Fusion-MPT Dual Ultra320 SCSI
/0/100/10/0.0.0 scsi2 214GB SCSI Disk
/0/100/10/0.0.0/1 /dev/sda1 volume 197GiB EXT4 volume
/0/100/10/0.0.0/2 /dev/sda2 volume 2934MiB Extended partition
/0/100/10/0.0.0/2/5 /dev/sda5 volume 2934MiB Linux swap / Solaris partition
/0/100/11 bridge pci PCI bridge
...
```

你还可以使用 `lshal` 来显示硬件信息，其报告基于 `HAL`（硬件抽象层）设备数据库。参见 www.freedesktop.org/wiki/Software/hal。

### lsub：列出 USB 设备
