
特别注意 `diskEntry.diskErrorFlag` 行（在本示例中以粗体显示）。这些行表示磁盘是低于（0）还是高于（1）你在 `snmpd.conf` 文件中指定的阈值。花一点时间将磁盘值（兆字节）修改为小于其中一个分区可用空间的数值（使用 `df -m` 命令检查）。然后输入：

```bash
service snmpd restart
```

或者

```bash
etc/init.d/snmpd restart
```

杀死 `snmpd` 守护进程的 PID 可以实现相同的效果。然后再次输入 SNMP 命令：

```bash
snmpwalk -v1 localhost -c public .1.3.6.1.4.1.2021.9
```

你应该能看到错误标志已被设置，指示磁盘空间不足。

## 步骤 5：安装 SNMP Agent

我们现在准备好让 Mon 检查集群节点上的 SNMP MIB 了。在此测试中，我们使用 Mon 监控运行在本地主机（集群管理器本身）上的 SNMP agent 作为示例。你只需在所有集群节点上启动守护进程，并将它们添加到 Mon 配置文件，即可对整个集群执行相同的操作。你必须按照本章前面的介绍安装 Perl 软件包，以便 Mon 软件包随附的监控脚本可以在集群管理器上正常运行。

在此示例中，我们将使用名为 `netsnmp-freespace.monitor` 的 SNMP 监控程序，它位于 CD-ROM 中。

### 本地查看 SNMP MIB

使用以下命令检查集群节点上的 MIB：

```bash
snmpwalk -v1 localhost -c public
```

该命令应该生成一个关于集群节点的报告，表明本地 SNMP agent (`snmpd`) 正在响应。让我们使用命令查看一些有用信息：

```bash
snmpwalk -v1 localhost -c public .1.3.6.1.4.1.2021.9
```

**注意** 在此命令中，我们使用数值而非符号名称来定位 SNMP 管理信息库（MIB）。要找到此数值标识符（OID）的符号或文本名称，请使用：

```bash
snmget .1.3.6.1.4.1.2021.9
```

如果你在文件中 `enterprises.ucdavis.dskTable.dskEntry` 中设置了磁盘值，你会看到这样的报告：

```text
enterprises.ucdavis.dskTable.dskEntry.dskIndex.1 = 1
enterprises.ucdavis.dskTable.dskEntry.dskIndex.2 = 2
enterprises.ucdavis.dskTable.dskEntry.dskPath.1 = /
enterprises.ucdavis.dskTable.dskEntry.dskPath.2 = /var
enterprises.ucdavis.dskTable.dskEntry.dskDevice.1 = /dev/sdb2
enterprises.ucdavis.dskTable.dskEntry.dskDevice.2 = /dev/sdb3
enterprises.ucdavis.dskTable.dskEntry.dskMinimum.1 = 100000
enterprises.ucdavis.dskTable.dskEntry.dskMinimum.2 = 100000
enterprises.ucdavis.dskTable.dskEntry.dskMinPercent.1 = -1
enterprises.ucdavis.dskTable.dskEntry.dskMinPercent.2 = -1
enterprises.ucdavis.dskTable.dskEntry.dskTotal.1 = 381121
enterprises.ucdavis.dskTable.dskEntry.dskTotal.2 = 253871
enterprises.ucdavis.dskTable.dskEntry.dskAvail.1 = 268888
enterprises.ucdavis.dskTable.dskEntry.dskAvail.2 = 162940
enterprises.ucdavis.dskTable.dskEntry.dskUsed.1 = 92554
enterprises.ucdavis.dskTable.dskEntry.dskUsed.2 = 77824
enterprises.ucdavis.diskTable.diskEntry.diskPercent.1 = 26
enterprises.ucdavis.diskTable.diskEntry.diskPercent.2 = 32
enterprises.ucdavis.diskTable.diskEntry.diskPercentNode.1 = 18
enterprises.ucdavis.diskTable.diskEntry.diskPercentNode.2 = 0
enterprises.ucdavis.diskTable.diskEntry.diskErrorFlag.1 = 0
enterprises.ucdavis.diskTable.diskEntry.diskErrorFlag.2 = 0
enterprises.ucdavis.diskTable.diskEntry.diskErrorMsg.1 = 1
enterprises.ucdavis.diskTable.diskEntry.diskErrorMsg.2 =
```

特别注意 `diskEntry.diskErrorFlag` 行（在本示例中以粗体显示）。这些行表示磁盘是低于（0）还是高于（1）你在 `snmpd.conf` 文件中指定的阈值。花一点时间将磁盘值（兆字节）修改为小于其中一个分区可用空间的数值（使用 `df -m` 命令检查）。然后输入：

```bash
service snmpd restart
```

或者

```bash
etc/init.d/snmpd restart
```

杀死 `snmpd` 守护进程的 PID 可以实现相同的效果。然后再次输入 SNMP 命令：

```bash
snmpwalk -v1 localhost -c public .1.3.6.1.4.1.2021.9
```

你应该能看到错误标志已被设置，指示磁盘空间不足。

### 查看 netsnmp-freespace.monitor 的输出

如果磁盘空间没有违反阈值，该脚本不会返回任何内容。尝试修改 `snmpd.conf` 中的空间阈值，并重启 SNMP 服务（`service snmpd restart` 或 `/etc/init.d/snmpd restart`）然后运行此命令。当磁盘违反空间阈值时，你会看到如下报告：

```text
/usr/lib/mon/mon.d/netsnmp-freespace.monitor localhost:///dev/sdb total=372 used=91(26%) free=261 err=: less than 300 free (=267)
```

### 在所有集群节点上安装 Mon

你现在准备好让 Mon 工作，让它监控所有集群节点的磁盘空间。为了这样做，请在所有集群节点上安装你创建的 `/etc/snmp/snmpd.conf` 文件，并在每个节点上启动 `snmp` 守护进程。

你可以在集群节点使用此示例 `mon.cf` 配置来管理所有的 `netsnmp-freespace.monitor`：

```conf
alertdir = /usr/lib/mon/alert.d
mondir = /usr/lib/mon/mon.d
logdir = /usr/lib/mon/logs
histlength = 500
dtlogging = yes
dtlogfile = /usr/lib/mon/logs/dtlog
hostgroup clusternodes localhost
```
