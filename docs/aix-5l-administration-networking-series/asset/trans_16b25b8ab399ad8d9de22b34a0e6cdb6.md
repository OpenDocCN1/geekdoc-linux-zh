

## 使用我们前面的摘要报告

如果输入 `erpt -aj EAA3D429`，我们将得到以下详细报告：

```
------------------------------------------------------------------
LABEL:		LVM_SA_STALEPP
IDENTIFIER:	EAA3D429

Date/Time:	Tue Apr 30 14:57:51 EDT
Sequence Number: 97
Machine Id:	00001037500
Node Id:	Lazarus
Class:	S
Type:	UMNN
Resource Name: LVDD

Description
PHYSICAL PARTITION MARKED STALE

Detail Data
PHYSICAL VOLUME DEVICE MAJOR/MINOR
0000 0000
PHYSICAL PARTITION NUMBER (DECIMAL)
306
LOGICAL VOLUME DEVICE MAJOR/MINOR
000A 0005
SENSE DATA
0000 3103 0000 7500 0000 00EC FD8B 82D3 0000 0000 0000 0000 0000 0000 0000
------------------------------------------------------------------
```

在详细报告中，我们可以看到诸如物理卷和逻辑卷的主设备号和次设备号等被标记为陈旧（stale）的信息。这个特定示例是通过在系统关机时拔掉其中一个（镜像）磁盘而产生的，因此当系统重新启动时，该物理卷上的每个逻辑卷都同时被标记为陈旧。

# AIX 错误日志记录设施

AIX 提供了多个命令来帮助我们管理错误日志。其中最简单的是 `erlogger` 命令。该命令用于将操作员消息记录到错误报告中。根据我们前面的示例，我们可以执行以下命令来创建一条我们已更换磁盘驱动器的条目：

```
# erlogger 'disk drive replaced'
```

下一次我们运行 `erpt -l | head -4` 命令时，我们将看到以下四行：

```
IDENTIFIER  TIMESTAMP  T C  RESOURCE_NAME  DESCRIPTION
AA8A5241  0430185102  T O  OPERATOR  OPERATOR NOTIFICATION
EAA3D429  0430145602 U S LVDD PHYSICAL PARTITION MARKED STALE
EAA3D429  0430145502 U S LVDD PHYSICAL PARTITION MARKED STALE
```

在摘要报告中，我们只能看到记录了一个操作员通知事件。通过执行 `erpt -aj AA8A5241`，我们可以看到实际记录的消息：

```
LABEL: CFMSG
IDENTIFIER: AA8A5241

Date/Time: Tue Apr 30 18:51:39 EDT
Sequence Number: 115
Machine Id: 000011037500
Node Id: Lazarus
Class: O
Type: TEMP
Resource Name: OPERATOR

Description
OPERATOR NOTIFICATION

User Causes
ERLOGGER COMMAND

Recommended Actions
REVIEW DETAILED DATA

Detail Data
MESSAGE FROM ERLOGGER COMMAND
Disk drive replaced
```

在管理错误日志的另一个有用命令是 `errclear` 命令，它用于清理日志中的旧条目。要清除日志中所有超过七天的条目，请输入以下命令：

```
# errclear 7
```

# 系统内存转储

当系统故障发生时，所选内核地址区域的自动转储会被记录在由主转储表定义的转储设备上。主转储设备是用于保存转储的专用存储区域。可以定义需要操作员干预的共享备用设备。默认的主转储设备是 /dev/hd6，默认的备用设备是 /dev/sysdump1。使用 `sysdumpdev` 命令或使用 SMIT 快速路径 `smit dump` 来定义和管理转储设备。请确保你的转储设备已分配，并且足够大以容纳至少一个完整转储。

```
# sysdumpdev -L    # List current dump status
# sysdumpdev -l    # List primary dump device location
# sysdumpdev -P    # Assign dump device
# sysdumpdev -e    # Estimate the size needed to dump
# smit dump        # SMIT FastPath to System Dump
```

以下命令将为镜像根卷组创建并配置两个专用转储设备（主设备和备用设备）（切勿镜像转储设备！）：

```
# mklv -y hd7 -t sysdump -x 5 rootvg 2 hdisk0    # This hd7 will be 2 partitions
# mklv -y hd71 -t sysdump -x 5 rootvg 2 hdisk1   # The x limits the size
# sysdumpdev -P /dev/hd7                          # Assign primary dump device
# sysdumpdev -S /dev/hd71                         # Use /dev/hd71 for secondary
# sysdumpdev -K                                   # Always allow system dump
# sysdumpdev -D /var/adm/ras                      # Set forced copy flag to FALSE
# chdev -l sys0 -a autorestart=true               # Enable auto REBOOT after crash
```

如果转储设备已配置，你可以使用 `sysdumpstart` 命令、使用 SMIT 或将钥匙转到服务位置并按一次重置按钮来强制系统恐慌转储。在没有钥匙或重置按钮的 PCI 机器（6015–7248）上，尝试 CTRL-ALT-NUMLOCK 1，或者如果可能，只需按重置按钮。大型机器都有不同的方法，因此在尝试之前请查阅你机器的硬件指南。记住，你只有一次机会获得良好的系统转储，如果做错了，系统可能会直接重新启动。

虽然可以查询驻留在主转储区域中的内核转储，但将它们复制到 AIX 文件系统或可移动介质类型上是好的做法。你可以使用 SMIT 或以下 `snap` 和 `tar` 命令来管理转储文件，以获取系统快照并释放转储区域，以解决你未来潜伏的问题。

```
# snap -gfkx -d /tmp/snap
# tar cvf /dev/rmt0 /tmp/snap
```

在这个示例中，我们使用 `snap` 命令来检查系统环境。-g 标志用于收集授权程序信息，-f 标志收集文件系统信息，-k 标志收集内核信息，-x 标志从主转储设备收集信息。在 `snap` 将此信息复制到 /tmp/snap 下的各个子目录，并将 /unix 和转储的压缩镜像存储到 /tmp/snap/dump 目录后，我们在检查转储设备的镜像之前将信息 `tar` 到磁带上。

# 系统日志

`syslogd` 守护进程通过由使用 `syslog` 子程序的应用程序创建的 `datagram` 套接字接收消息。`syslogd` 守护进程将传入消息重定向到文件或 /etc/syslog.conf 文件中描述的条目所指示的其他系统。每当 `syslogd` 启动或接收到 HUP 信号时，都会读取此文件。由于 syslog 的应用特定性，AIX 提供了一个 /etc/syslog.conf 示例模板，必须根据你的应用程序需求进行配置。/etc/syslog.conf 中的每一行都包含由分号分隔的消息选择器，后跟一个指示消息发送位置的字段。传入消息指定一个代表其中一个选择器的设备代码。（请参阅 /usr/include/sys/syslog.h 查看代码和选择器的列表。）在以下示例中，邮件消息发送到另一台名为 daffy 的系统上的中心存储库；所有调试消息发送到 /var/adm/debug.log；内核关键和紧急消息发送到 /var/adm/kernel.log；警报消息发送到 ops 用户 ID。debug.log 文件的大小限制为 100K，并且保存有四个前一个文件 debug.log.0 到 debug.log.3。kernel.log 文件也保存有四个前一个文件，但它们的大小没有限制；相反，它们每天轮换一次。

```
/**********Example /etc/syslog.conf*********/

mail @daffy
*.debug /var/adm/debug.log rotate size 100k files 4
kern.crit;kern.emerg /var/adm/kernel.log rotate time 1d
*.alert ops
```

请记住，对于实时调试，你始终可以使用系统跟踪来获取更精细的细节。

```
# trcon      # Start trace
# trcstop    # Stop trace
# trcrpt     # Generate trace report
```

# AIX 内核结构

有了错误日志和 LED 状态信息，我们准备好检查转储了。首先，让我们为了解 AIX 内核的特征打下一些基础。AIX 基于可抢占的内核。内核被分为可固定区域和可分页区域。内核的可固定低区域包含中断处理程序、内核文本和数据区域、进程表以及页映射。可分页内核区域包括文件表；v 节点、g 节点和 i 节点结构；以及内核扩展。重要的是要记住，可分页内核区域中的活动和服务是同步的，而可固定区域的活动是异步的。例如，外部 I/O 中断可能在发起请求的进程完成其时间片并被换出后很久由可固定区域处理。中断分为处理器中断和外部中断类别。所有 I/O 类型中断都复用为一个外部中断。外部中断包括 I/O 总线和系统板设备。外部中断是唯一可以被屏蔽的中断类别。处理器中断包括系统重置、机器检查、存储、程序、对齐、浮点和 SVC 中断。

