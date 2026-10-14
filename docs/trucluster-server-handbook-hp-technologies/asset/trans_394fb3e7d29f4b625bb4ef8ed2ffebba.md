

+   - evmget (1)

使用 EVM_SHOW_TEMPLATE，您可以定义从 evmget、evmwatch(1)、evmsort(1) 和 evmshow(1) 命令返回的信息。

```
# export EVM_SHOW_TEMPLATE=
> "@timestamp {@event_id}\n[@priority] @name\n@\n\n"
```

/usr/share/evm/filters 目录中存在两个与集群相关的过滤器模板文件，如我们编写的 evf 脚本所示。

```
$ ./evf -vd /usr/share/evm/filters clu caa

/usr/share/evm/filters

clu.evf

@clu:clu          -> [name sys.unix.clu]
@clu:cfs          -> [name sys.unix.clu.cfs]
@clu:cnx          -> [name sys.unix.clu.cnx]
@clu:drd          -> [name sys.unix.clu.drd]
@clu:member       -> [name sys.unix.clu.member]
@clu:shutdown     -> [name sys.unix.clu.shutdown]
@clu:wall         -> [name sys.unix.clu.wall]
@clu:caa          -> [name sys.unix.clu.caa]
@clu:clua         -> [name sys.unix.clu.clua]

caa.evf

@caa:caa          -> [name sys.unix.clu.caa]
@caa:app          -> [name sys.unix.clu.caa.app]
@caa:cli          -> [name sys.unix.clu.caa.cli]
@caa:err          -> [name sys.unix.clu.caa.err]
@caa:res          -> [name sys.unix.clu.caa.res]
```

通过设置 EVM_SHOW_TEMPLATE 并使用 "@clu" 过滤器，您可以使用以下 evmget 命令检索发生的所有与集群相关的事件。

```
$ evmget -A -f @clu
29-Aug-2002 01:55:24 (13)
[200] sys.unix.clu.cnx.quorum.gain
CNX MGR: Node has (re)gained quorum (current votes 2, quorum votes 2)
--
```

在进行故障排除时，通常很有用先广泛搜索然后再适当地收紧范围（也许将事件限制在特定时间段内）；例如，要返回过去两小时内发生的所有事件：

```
# evmget -A -f "[age < 2h]*"
29-Aug-2002 03:36:14 (968)
[200] sys.unix.clu.drd.new_accessnode__hwid.105
DRD: Server molari selected for device 105
...
```

一旦找到感兴趣的事件，您可以使用带 "-d" 选项的 evmshow 命令获取更多信息。

## A.1.4 解析事件

取自前面示例的事件 ID，我们可以按如下方式获取更多信息：

```
# evmget -f "[event_id = 968]" | evmshow -d
EVM Log event ================================
EVM event name: sys.unix.clu.drd.new_accessnode__hwid.105

This event is posted by a DRD client to indicate that it has
selected a server as a new access node for the specified device.

===============================================
Formatted Message:
DRD: Server molari selected for device 105

Event Data Items:
Event Name      : sys.unix.clu.drd.new_accessnode__hwid.105
Cluster Event   : True
Priority        : 200
PID             : 1061550
PPID            : 1061518
Event Id        : 968
Member Id       : 2
Timestamp       : 29-Aug-2002 03:36:14
Host IP address : 192.168.0.69
Cluster IP address: 192.168.0.70
Host Name       : sheridan.dec.com
Cluster Name    : babylon5
Format          : DRD: Server $server_name selected for device $_hwid
Reference       : cat:evmexp_clu.cat

Variable Items:
disk_type (STRING) = "SERVED"
server_name (STRING) = "molari"
_hwid (INT64) = 105
reason_code (INT32) = 0
```

![](img/a0df85c2e542a8d6c913113908553aa4_797_0.png)

![](img/a0df85c2e542a8d6c913113908553aa4_797_1.png)

![](img/a0df85c2e542a8d6c913113908553aa4_797_2.png)

![](img/a0df85c2e542a8d6c913113908553aa4_797_3.png)

## A.1.5.2 内存通道地址空间窗口大小

为了使冗余内存通道导轨能够使用 512MB 地址空间窗口大小运行，每个内存通道必须位于单独的 PCI 总线上。您可以使用“show config”命令来确定内存通道卡的位置。

```
P00>>>show config

    Bus 00  Slot 08: DEC PCI MC                         mca0.0.0.8.0        Rev: 22, mca0

    Bus 01  Slot 03: DEC PCI MC                         mca1.1.0.3.0        Rev: 22, mca1
```

```
>>> mc_diag -d
LCERR  MC PORT  PEBAR  CFG304  CFG10  MODCFG  POS
mca0 - 00204800 00000000 42400000 80000000 04000006 40000008 0000000b 00000004
mca1 - 00204800 00000000 42400000 80000000 04000006 48000008 0000000b 00000004
```

### 图 A-5：内存通道 2 内存窗口大小为 512MB

如何在不查看卡的情况下确定地址空间窗口大小？MODCFG 字段的第 2 位指示内存窗口大小。如果第 2 位未设置，则地址空间窗口大小为 512MB。参见图 A-5。

## A.1.5.3 MCERR 字段

MCERR 字段应始终为零。然而，非零的 MCERR 字段不一定是致命的。我们曾遇到过 DS10 系统上的内存通道在 SRM 控制台准备就绪之前未能完成其上电自检的情况。如果发生这种情况，请运行 init 命令，这应该可以清除问题。如果未清除错误，您可以对系统进行断电循环。作为在向 HP 记录电话之前清除错误的最后手段，请关闭系统并重新安装卡。

有关“mc_diag -d”位字段的更多信息，请参阅随内存通道硬件提供的《内存通道服务信息指南》第 3 章（故障排除）。该指南还包含有关内存通道硬件故障排除的额外提示。

## A.1.6 CNX 问题（法定人数、CNX 启动挂起等）

如果您遇到法定人数问题或集群似乎挂起并且 CNX 消息显示在控制台上，请尝试将 sysconfig 调试值 cnx:msg_level（默认值 1）和 cnx:debug_msg_level（默认值 0）均设置为 5，要么在启动时设置（通过修改 /etc/sysconfigtab），要么使用 "sysconfig -r cnx <attribute>=5" 实时设置。这些设置会导致更详细的 CNX 消息记录到控制台、/var/adm/messages 和 /var/adm/syslog.dated/current/kern.log，这可以帮助您或 HP 支持人员了解集群中 CNX 行为的更多线索。

## A.1.7 无法从集群成员看到您的共享存储

这通常是持久保留问题，并且只应在孤立情况下发生。请参考第 15.13 节和第 22.5 节，了解有关 I/O 屏障的详细信息以及它们可能阻碍您的情况。您可以使用 "cleanPR show" 从集群的角度检查持久保留：

