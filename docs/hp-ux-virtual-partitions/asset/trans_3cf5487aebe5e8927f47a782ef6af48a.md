
该输出展示了为 SCM 设置的默认角色及其简要描述。由于在 SCM 的图形化版本中，您可以执行大多数想要的功能，因此我不预期您会在命令行上运行许多功能；不过，了解这些命令的存在总是好的。

## 第12章

## 性能主题

### 性能与虚拟分区

在下面的章节中，我们将运行一些与性能分析相关的命令，以查看这些命令的输出与在非 vPars 系统上看到的输出有何不同。由于我们要涵盖的命令是许多与性能分析相关工作的基础，因此了解这些命令输出的差异非常重要。本章中非 vPars 特定部分涵盖了通用的性能分析。在 vPar 上执行的性能分析方式与在非 vPar 系统上执行的性能分析方式相同，除了某些命令的输出不会显示系统上的所有组件。相反，只会显示并分析专门分配给正在执行分析的 vPar 的组件。这是本章第一部分我们将重点关注的领域，即您将看到的某些常用命令的输出。

从纯性能相关的角度来说，您在带有 vPars 的系统上确实运行了额外的软件，即虚拟分区监视器（Virtual Partition Monitor）。vPars 系统中的一些资源是共享的，这意味着它们由虚拟分区监视器拥有，而不是由某个特定的 vPar 拥有，例如系统总线适配器（System Bus Adapters）和内存控制器（Memory Controller）。虚拟分区软件消耗的整体系统资源极少。vPar 中的组件专门用于其所属 vPar 的运作。这意味着当我们在 vPar 上运行性能分析时，我们只分析专门分配给该 vPar 的组件。

在下面的章节中，让我们来看看一些常用的性能分析命令，并查看 vPar 的输出是什么样的。这绝不是一个命令的详尽列表，但它会让你了解在 vPars 上你会看到什么。

### 带磁盘的 sar 和 ioscan

在您的 vPars 系统上运行 **ioscan** 只会显示包含在该 vPar 中的组件。下面的 **ioscan** 命令搜索名为 *cable1* 的 vPar 上的磁盘，并且只显示连接到 *LBA 0/0, 0/0* 的磁盘。当使用 *-a io:io/:* 创建 *cable1* 时，*LBA 0/0, 0/0* 是其唯一的 I/O 组件。

```bash
# ioscan -func C disk
Class  I  H/W Path          Driver  B/W State   H/W Type   Description
------  --------  -----------  -----------  ----------  ---------
disk      0  0/0/1/0.0.0     /dev/dsk/c0t10d0  DEVICE    dr
                                             /dev/rdsk/c0t10d0
disk      1  0/0/1/1.0.0     /dev/dsk/c1t0d0   CLAIMED   DEVICE    SBA LBT 111
                                             /dev/dsk/c1t0d0
disk      2  0/0/1/1.0.0     /dev/dsk/c1t0d0   CLAIMED   DEVICE    SBA LBT 111
                                             /dev/rdsk/c1t0d0
disk      3  0/0/2/0.0.0     /dev/dsk/c2t0d0   CLAIMED   DEVICE    SBA LBT 2
                                             /dev/rdsk/c2t0d0
disk      4  0/0/2/2.0.0     /dev/dsk/c2t2d0   CLAIMED   DEVICE    SEAGATE ST173404LC
                                             /dev/rdsk/c2t2d0
```

此列表显示四个内部磁盘分别位于 SBA 0、LBA 0 以及 SCSI 总线 1 和 2 上。在撰写本文时，这些磁盘必须位于同一个 vPar 中，因为它们位于同一个 LBA 上。

连接到该服务器的磁盘远不止前面列表中显示的这些；但是，那些磁盘连接到不属于 *cable1* 的 LBA，因此不会显示在该列表中。

**sar -d** 的以下输出仅显示配置到 *cable1* 中的那个磁盘的性能数据。该输出产生时，系统中另一个 vPar（*cable2*）正在其上运行的磁盘并未显示在此输出中：

```bash
# sar -d 3

HP-UX cvhdc03  B.11.11 U 9000/800    10/16/01

14:28:42  device     %busy  average  trans/s  blks/s  await    avserv
14:28:46  c1t2d0     0.25    0.50     1        2      0.49     8.29
14:28:50  c1t2d0     0.50    0.50     1        2      1.49     8.77
14:28:54
Average    c1t2d0     0.25    0.50     1        2      0.92     8.50
```

你需要连接到另一个 vPar（在本例中是 cable2），并运行 iostat 和 sar -d，以获取 cable2 正在运行的磁盘的设备列表和性能数据。这是 vPar 在同一个服务器上运行就像独立服务器一样运作的一个清晰例子。所有的 vPar 都运行着各自实例的 HP-UX 11i 和应用程序，必须像独立的服务器一样进行分析。

### uptime

uptime 生成关于系统启动时间以及一些负载数据的信息。让我们对同一服务器上运行的两个不同的 vPar 运行此命令，如下所示：

```bash
# hostname
cvhdc03
# uptime
2:32pm up 3:02, 2 users, load average: 2.26, 1.96, 1.60
# hostname
cvhdc04
# uptime
2:31pm up 2:41, 2 users, load average: 0.25, 0.22, 0.23
#
```

uptime 生成的信息是 vPar 特定的。在此输出中我们看到的第一个输出是第一个 vPar 启动的时间，第二个输出是第二个 vPar 启动的时间。此输出中的其他信息也是针对运行 uptime 的特定 vPar。与你在 vPar 运行时执行的大多数命令一样，你将看到 vPar 特定的信息，而不是系统特定的信息。

接下来，我们将查看 vPar 中的一些网络命令。

### 网络

命令生成的网络信息也取决于你发出命令的 vPar。vPars 的网络配置在第13章中有介绍。让我们看看同一服务器上配置的两个不同 vPars 的网络接口。首先，让我们看看主机名为 cvhdccon3 的 vPar cable1 的输出：

```bash
# hostname
cvhdccon3
# netstat -I lan0
Name   Mtu Network     Address         Ipkts    Ierrs Opkts    Oerrs Coll
lan0   1500 172.16.15.0 cvhdccon3      12785     0   11855    0      3
# 
# netstat -ln
Name   Mtu Network     Address         Ipkts    Ierrs Opkts    Oerrs Coll
lan0   1500 172.16.15.0 172.16.15.36  12990     0    12052    0      3
lo0    4336 127.0.0.0   127.0.0.1       7616     0    7616     0      0
# 
# lanscan
Hardware Station  Crd Rtw  Net-Interface  NM      MAC     HP-DLIP  DLPI
Path     Address   In# State Name       FPA ID     Type     Support M/#
0/0/0/0 0x00306B046F6BA 0    up   lan0     snap0 L       ETHER   Yes    219
# 
```

此输出显示，lan0 是此服务器上专门分配给 vPar cable1 的网络接口。lanscan 输出显示该接口的硬件路径为 0/0/0/0。这是在创建 vPar 时使用 -a io:0/0 配置为该 vPar 组件的核心 I/O 卡。创建 cable1 时没有明确调出核心 I/O 卡上的 LAN 接口，因为 0/0/0/0 是位于 0/0 的核心 I/O 卡的隐含组件。

现在我们来看看在这个服务器上运行的第二个 vPar，称为 cable2，主机名为 cvhdccon4：

```bash
# hostname
cvhdccon4
# netstat -I lan1
Name   Mtu Network     Address         Ipkts    Ierrs Opkts    Oerrs Coll
lan1   1500 172.16.14.0 cvhdccon4     3463      0    1603     0      2
# 
# netstat -ln
Name    Mtu   Network           Address       Ipkts Ierrs Opts  Cerrs Coll
lanl    1500  172.16.14.0       172.16.14.44  3619  0     1545  0     2
lo0     4136  127.0.0.0         127.0.0.1     916   0     916   0     0
# 
# lanscan
Hardware Station     Crd Idw Net-Interface IM      MAC                 HP-DLPI DLPI
Fach  Address        0/0/8 State Name*TPA          ID Type             Support BITS
C/10/0/0  0x0010680053658  1   UP  lanl snapi        1 ETHER          Yes     119
s
```

此输出显示，lan1 是此服务器上专门分配给 vPar cable2 的网络接口。lanscan 输出显示该接口的硬件路径为 0/0/10/0/0。LBA 0/0/10/0/0 在创建 vPar 时使用 -a 10:0/10/0/10 配置为该 vPar 的组件。与作为隐含组件的核心 I/O 卡上的 LAN 接口不同，此 LAN 接口位于单独的 PCI 插槽和 LBA 中，因此在创建 vPar 时必须明确指定。

在 cable1 上运行 lanadmin 会产生更详细的与 lan0 相关的输出，如下所示：

```bash
# lanadmin

LOCAL AREA NETWORK ONLINE ADMINISTRATION, Version 1.0
          Mon, Oct 15, 2001  14:41:23

     Copyright 1994 Hewlett-Packard Company.
             All rights are reserved.

Test Selection mode.

        lan     = LAN Interface Administration
        menu    = Display this menu
        quit    = Terminate the Administration
        tetera  = Do not display command menu
        verbose = Display command menu

Enter command: lan

LAN Interface test mode. LAN Interface PPA Number = 0

        clear   = Clear statistics registers
        display = Display LAN Interface status and statistics registers
        end     = End LAN Interface Administration, return to Test Selection
        menu    = Display this menu
        ppa     = PPA Number of the LAN Interface
        quit    = Terminate the Administration, return to shell
        reset   = Reset LAN Interface to execute its selftest
        specific = Go to Driver specific menu

Enter command: d

                    LAN INTERFACE STATUS DISPLAY
                    Mon, Oct 15, 2001  14:42:33

PPA Number         =      0
Description        =  lan0  HP PCI 10/100Base-TX Core [100BASE-TX,HD, AUTO, TT=1500
Type (value)       =   ethernet-commacd(6)
MTU Size           =   1500
Speed              =   100000000
Station Address    =   0x360056f8ba
```

