

你可以通过输入 IP 地址 127.0.0.1 来扫描本系统。如果受测系统上有一个可用的 iSCSI 目标设备，将会打开一个类似于下面的对话框：

![](img/63e88022bf135307e3eac051ad238b5b_426_0.png)

如果有多个可用的 iSCSI 目标设备，它们将全部被列出。iqn（iSCSI 限定名称）用于标识目标。

从列表中选定 iSCSI 目标后，你必须使用 **登录** 按钮进行登录。

随后出现以下对话框：

![](img/63e88022bf135307e3eac051ad238b5b_427_0.png)

默认情况下不需要认证。然而，如果你已经为 iSCSI 目标设备配置了传入认证（例如），则你需要在此对话框中选中 **传出认证**，并输入用于 iSCSI 目标配置的相同用户名和密码。

选中 **下一步** 后，**已连接目标** 选项卡将显示你已配置的 iSCSI 设备。

使用 **切换启动** 按钮，你可以在 **自动** 和 **手动** 之间切换，这定义了设备激活的方式。

选择 **完成** 以将设置写入系统。

客户端配置存储在文件 /etc/iscsi.conf 以及目录 /var/lib/open-iscsi/ 中的数据库文件 discovery.db 和 node.db 中。用于手动配置这些文件的工具是 iscsiadm。

![](img/63e88022bf135307e3eac051ad238b5b_428_0.png)

iSCSI 发起方名称包含在文件 **/etc/initiatorname.iscsi** 中。

```
da3:~$ cat /etc/initiatorname.iscsi

# DO NOT EDIT OR REMOVE THIS FILE!

# If you remove this file, the iSCSI daemon will not start.

# If you change the InitiatorName, existing access control lists

# may reject this initiator. The initiatorName must be unique

# for each iSCSI initiator. Do NOT duplicate iSCSI InitiatorNames.

InitiatorName=iqn.1996-04.de.suse:01.42:0cb385f5
```

关于 iscsid、iscsiadm 和配置文件如何协同工作的描述包含在 **/usr/share/doc/packages/open-iscsi/README** 中。

在文件 **/var/log/messages** 中，你应该看到类似于以下的条目：

```
Oct 4 11:55:56 da3 kernel: scsi3 : iSCSI Initiator over TCP/IP, v1.0-595

Oct 4 11:55:56 da3 kernel: sess_param (173) 1 1 1 8192 8192 262144 65536 2 0 1 1 1 0 1 1

Oct 4 11:55:56 da3 kernel: Vendor: IET Model: VIRTUAL-DISK

Rev: 0

Oct 4 11:55:56 da3 kernel: Type: Direct-Access

ANSI SCSI revision: 04

Oct 4 11:55:56 da3 kernel: SCSI device sdb: 2097152 512-byte hdwr sectors (1074 MB)

Oct 4 11:55:56 da3 kernel: sdb: Write Protect is off

Oct 4 11:55:56 da3 kernel: sdb: Mode Sense: 77 00 00 08

Oct 4 11:55:56 da3 kernel: SCSI device sdb: drive cache: write through

Oct 4 11:55:56 da3 kernel: SCSI device sdb: 2097152 512-byte hdwr sectors (1074 MB)

Oct 4 11:55:56 da3 kernel: sdb: Write Protect is off

Oct 4 11:55:56 da3 kernel: sdb: Mode Sense: 77 00 00 08

Oct 4 11:55:56 da3 kernel: SCSI device sdb: drive cache: write through

Oct 4 11:55:56 da3 kernel: sdb: unknown partition table

Oct 4 11:55:56 da3 kernel: sd 3:0:0:0: Attached scsi disk sdb

Oct 4 11:55:56 da3 kernel: sd 3:0:0:0: Attached scsi generic sg2 type 0

Oct 4 11:55:56 da3 iscsid: version 1.0-064

Oct 4 11:55:56 da3 iscsid: iSCSI daemon with pid=6172 started!

Oct 4 11:55:56 da3 iscsid: iSCSI sync pid=6173 started

Oct 4 11:55:56 da3 iscsid: connection:0 is operational now
```

你可以看到一个新的 SCSI 设备可用（/dev/sdb）。你可以使用 fdisk 创建分区，在分区上创建文件系统并将其挂载。

使用 lsscsi 命令，你可以查看所有可用的 SCSI 设备。

如果你想查看是否存在活动的 iSCSI 连接，请在托管目标的服务器上使用 cat 命令查看文件 /proc/net/iet/session。你可以看到该主机的所有到目标的 iSCSI 连接，如下例所示：

```
da3:~ # cat /proc/net/iet/session
tid:1
name:iqn.2006-10.com.digitalairlines:d3d43303-8b2c-43df-83ea-6721942677e2
sid:281474980708864 initiator:iqn.1996-04.de.ruse:01.427f8cb385f5
cid:0 ip:127.0.0.1 state:active hd:none dd:none
```

你可以看到来自 IP 地址 127.0.0.1 的连接已建立到 id 为 1（tid）的目标。

虽然可以同时存在多个连接，但请记住，未采取预防措施（例如在 iSCSI 目标上使用集群文件系统）的情况下，不建议多次挂载同一个 iSCSI 目标。

## 在启动时自动挂载 iSCSI 目标

在服务器端（iSCSI 目标），你必须确保 iscsi 目标服务在重启后会自动启动。使用命令 chkconfig iscsitarget on（或 inserv iscsitarget）来执行此操作。

在客户端（iSCSI 发起方）端，open-iscsi 守护进程必须在启动时自动启动。这是通过使用命令 chkconfig open-iscsi on 实现的。

如果你已经在相应的 YaST 对话框中选中了 **启动时** 按钮，则不需要发出上述 chkconfig 命令。

一般来说，所有应在启动时自动挂载的设备都会输入到文件 /etc/fstab 中。iSCSI 设备面临的一个问题是在读取 /etc/ fstab 文件的启动过程中，网络尚不可用。另一个问题是你不确定使用哪个本地 SCSI 设备作为 iSCSI 目标。

这两个问题都有解决方案。为了确保 iSCSI 设备每次都能挂载到相同的目录，你必须使用分区的 UUID（通用唯一标识符）。使用以下命令来建立设备的 UUID：

```
da3:~ # udevinfo -q symlink -n /dev/sdb1
disk/by-id/iscsi-149454000000000000000001000005d9a01000 200800-part1
disk/by-path/ip-127.0.0.1:3260-iscsi-ign.2006-10.com.digit alairlines:d3d4303-8b2c-43df-83ea-6721942677e2-part1
disk/by-uuid/8b4dcb80-372d-44ba-a35b-96b5619b8237
```

在此示例中，最后一行包含设备 /dev/sdb1 的 UUID。现在你可以在 /etc/fstab 中创建一个如下条目，以将此 iSCSI 设备挂载到 /iscsi 目录：

```
/dev/disk/by-uuid/8b4dcb80-372d-44ba-a35b-96b5619b8237
/iscsi auto hotplug,defaults 0 0
```

使用挂载选项 hotplug，第一个问题也解决了。此选项表示，在网络之后启动的热插拔守护进程将负责此挂载。

## 练习 9-1

### 设置 iSCSI 目标和 iSCSI 发起方

在这个练习中，你将学习如何设置 iSCSI 目标以及如何使用 iSCSI 发起方访问该目标。

你可以在练习手册中找到此练习。

（练习结束）

## 摘要

| 目标 | 摘要 |
| :--- | :--- |
| **1.** iSCSI 背景 | Internet 小型计算机系统接口（iSCSI）在 IP 上实现标准的 SCSI 命令。提供存储的服务器称为 iSCSI 目标，使用该存储的客户端称为 iSCSI 发起方。 |
| **2.** iSCSI 配置 | iSCSI 目标和发起方都可以使用相应的 YaST 模块轻松配置。iSCSI 目标配置存储在 /etc/ietd.conf。iSCSI 发起方配置存储在 /etc/iscsi.conf、/etc/initiatorname.iscsi，以及 /var/lib/open-iscsi 中的文件 discovery.db 和 node.db。 |

# 第 10 部分 集群文件系统

使用集群文件系统可以在系统之间共享文件系统。在集群术语中，这些系统被称为节点。集群文件系统也称为“共享磁盘文件系统”。这些文件系统的好处是，如果一个节点失效，数据对剩余节点仍然可用。集群文件系统常用于高可用性环境。

Linux 上有多种集群文件系统，其中最著名的是：

- OCFS（Oracle 集群文件系统）
- GPFS（通用并行文件系统）
- GFS（全局文件系统）
- LUSTRE

## 目标

- 1. 全局文件系统（GFS）
- 2. Oracle 集群文件系统 2（OCFS2）

