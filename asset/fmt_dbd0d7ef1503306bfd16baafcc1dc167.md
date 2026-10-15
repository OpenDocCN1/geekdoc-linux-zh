
图 5-21 `cfgvpath` 的输出

示例输出显示了 SCSI 磁盘设备的名称和系列、其连接信息以及产品信息。行尾的大写字母 X 表示 SDD 目前不支持该设备。

如图 5-22 所示输入 `cfgvpath` 来配置 SDD vpath 设备。这会将 SCSI 设备 `sdb` 和 `sdc` 合并为一个虚拟设备 `vpath`（实际上的效果是让 `sdb` 和 `sdc` 呈现为相同的目标）。

```
linux:/opt/IBMSdd/bin # cfgvpath

crw--r1 root root 253, 0 Apr 4 06:03 /dev/IBMSdd

Making device file /dev/vpath 247 0

Added vpath ...nlinux:/opt/IBMSdd/bin # ls /dev/vpath*

dev/vpatha /dev/vpath1 /dev/vpath4 /dev/vpath3 /dev/vpath6

dev/vpath9

dev/vpath1 /dev/vpath12 /dev/vpath15 /dev/vpath4 /dev/vpath7

dev/vpath10 /dev/vpath13 /dev/vpath2 /dev/vpath5 /dev/vpath8

linux:/opt/IBMSdd/bin # cat /etc/vpath.conf

vpath 70024678
```

图 5-22 配置 SDD vpath 设备

配置信息默认保存存在 `/etc/vpath.conf` 文件中，以便在后续驱动程序加载和配置时保持 vpath 名称的持久性。

您可以使用 `rmvpath` 命令删除 SDD vpath 设备，其中 `xxx` 代表要删除的 vpath 设备名称。输入 `cfgvpath ?` 或 `rmvpath ?` 可获取更多关于 `cfgvpath` 或 `rmvpath` 命令的信息。

使用 `lsvpcg` 或 `datapath query` 来验证 vpath 配置。如果成功配置了 SDD vpath 设备，`lsvpcg` 将显示如下输出：

```
000 vpath0 (247,0)70024678 =dev/sdb /dev/sd1 /dev/sdcg /dev/sdcp.
```

在后续章节中，我们将描述三种不同的运行模式：

## 使用单命令进行 SDD 配置

您也可以通过发布 `sdd start` 命令手动加载并配置 SDD。成功执行 `sdd start` 命令将执行第 133 页“使用多命令进行 SDD 配置”中描述的所有任务。

使用 `sdd stop` 取消配置并卸载驱动程序。使用 `sdd restart` 命令进行取消配置、卸载并重启。

## 在启动时配置 SDD

您可以设置 SDD 从 `/etc/init.d/` 自动加载并配置。

## Red Hat Cluster Manager

本章描述了 Red Hat 高可用集群管理器（Red Hat High Availability Cluster Manager）所需的准备、安装和自定义任务。

详情请参考《Red Hat Cluster Manager 安装与管理指南》，该指南位于：

http://www.redhat.com/docs/manuals/enterprise/

Cluster Manager随 Red Hat Enterprise Linux AS 提供。它允许您建立一个包含两个节点并使用共享磁盘存储的高可用集群。未来版本将支持多节点。

> **限制：** IBM 目前不支持在 xSeries 服务器上运行 Linux 下下的高可用集群产品。此类应用程序由供应商支持。

## 6.1 准备安装 Cluster Manager

高可用集群理想情况下应该没有单点故障。这种可靠性在发生故障时提供数据完整性和应用程序可用性。带有共享存储的冗余硬件以及集群和应用程序故障转移机制意味着高可用集群能够满足企业市场的需求。

图 6-1 显示了我们实验的设置。

![](img/7df754bba6e7faadf914690e9ed087_161_0.png)

图 6-1 HA 集群配置

### 6.1.1 Quorum 分区

需要注意的是，Quorum 分区需要原始设备（raw devices）。Cluster Manager 需要一个 Quorum 分区和一个备份 Quorum 分区来存储集群状态和配置信息。这些分区理想应创建在 RAID1 数组的逻辑驱动器上。创建两个不小于 10 MB 但大于 20 MB 的分区，不需要更大。不要在 Quorum 分区上创建文件系统，因为这些分区需要保持为空。

### 6.1.2 软件看门狗（Software watchdog）

如果没有使用电源开关等硬件设备进行 STONITH（杀死节点），则使用软件看门狗来杀死挂起的节点。集群守护进程（corosync）会定期重置定时器间隔。如果守护进程未能重置定时器，故障集群成员将自行重启。必须为看门狗定时器创建特殊设备。在集群的两个节点上执行以下操作：

```
cd /dev
mknod watchdog watchdog
```

### 6.1.3 NMI watchdog

在使用软件看门狗时，建议同时使用 NMI 看门狗定时器。NMI 看门狗可能在某些旧系统上无法工作。编辑 `/etc/grub.conf`，在相关内核行的末尾添加 `nmi_watchdog=1`（图 6-2）。

![](img/7df754bba6e7faadf914690e9e5ed087_162_0.png)

需要重启系统以检查系统是否支持 NMI 监控。一旦服务器重新上线，检查 `/proc/interrupts`（图 6-3）。如果 NMI 条目不为零，则系统支持 NMI 看门狗定时器。如果条目为 0，尝试将 `grub.conf` 中的参数改为 `nmi_watchdog=2` 并重启。如果仍然为 0，则服务器不支持 NMI 看门狗定时器。

![](img/7df754bba6e7faadf914690e9e5ed087_163_0.png)

图 6-3 `/proc/interrupts`

### 6.1.4 原始设备（Raw devices）

必须在两个系统上编辑 `/etc/sysconfig/rawdevices` 文件，用于主、备 Quorum 分区。在文件中添加以下行，其中 X = 设备字母（图 6-4）：

```
/dev/raw/raw1 /dev/sdX1
/dev/raw/raw2 /dev/sdX2
```

```
root@node1# sysconfig
# cat rawdevices
# raw device bindings
## format: <rawdev> <major> <minor>
## <rawdev> <blockdev>
# example: /dev/raw/raw1 /dev/sda1
/dev/raw/raw1 8 5
/dev/raw/raw2 /dev/sdb1
/dev/raw/raw3 /dev/sdb2
[root@node1]#
```

图 6-4 `/sysconfig/rawdevices`

保存更改并重启 rawdevices 服务：

```bash
service rawdevices restart
```

### 6.1.5 集群消息日志文件

可以编辑 `/etc/syslog.log` 文件，将集群事件记录到默认日志文件之外的不同文件中。集群工具和守护进程会将消息记录到名为 `local4` 的 syslog 标签中。

在两个系统上编辑 `/etc/syslog.conf`，并在以下部分添加 `local4.none`，以避免事件在集群日志和默认日志中重复：

```
+   * Log anything (except mail) of level info or higher.
"* Don't log private authentication messages!
* *.info;mail.none;authpriv.none;cron.none;none;local4.none /var/log/messages"
```

在文件末尾添加以下内容，将集群消息记录到单独的文件：

```
+   * Cluster messages on local4
* local4.* /var/log/cluster
```

`/etc/syslog.conf` 文件看起来类似于图 6-5。

Channel type: net, Name: hb1node1
Channel type: net, Name: hb2node1
Power switch IP address or hostname: node1
Identifier on power controller for member node1: unused

# Member 1 信息

```
Name: node2
```
