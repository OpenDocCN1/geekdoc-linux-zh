
```
[root@localhost ~]# tgt-admin --show
Target 1: ign.2015-10.localdomain.localhost:test1
  System information:
    Driver: iscsi
    State: ready
  I_T nexus information:
    LUN: 0
      Type: controller
      SCSI ID: IET 00010000
      SCSI SN: beaf10
      Size: 0 MB, Block size: 1
      Online: Yes
      Removable media: No
      Prevent removal: No
      ReadOnly: No
      Backing store type: null
      Backing store path: None
      Backing store flags:
  LUN: 1
    Type: disk
    SCSI ID: IET 00010001
    SCSI SN: beaf11
    Size: 264 MB, Block size: 512
    Online: Yes
    Removable media: No
    Prevent removal: No
    ReadOnly: No
    Backing store type: rdwr
    Backing store path: /dev/VolGroup/iscsi
    Backing store flags:
Account information:
  ACL information:
    10.0.2.20
```

## 启动器配置

要将你的系统配置为 iSCSI 启动器，你首先需要安装`iscsi-initiator-utils`包及其依赖项。大多数发行版默认通常不会安装此包。

安装该包后，你可以使用`iscsiad`命令查看由 iSCSI 服务器提供的目标名称。要执行此任务，请使用以下`iscsiad`命令：

```
[root@localhost ~]# iscsiad -m discovery -t sendtargets -p 10.0.2.15
Starting iscsid: [ OK ]
10.0.2.20:3260,1 iqn.2015-10.localdomain.localhost:test1
```

注意：第一次执行此命令时，它会自动启动`iscsid`守护进程。

你在`iscsiad`命令的输出中寻找的是哪台机器可以作为启动器（在本例中为`10.0.2.20`）以及 IQN（iSCSI 节点名称）。启动器列表应该包含你正在执行命令的机器（客户端），以便你能够连接到 iSCSI 目标。

现在目标已经被发现，连接到它的简单方法是启动`iscsi`服务。

```
[root@localhost ~]# /etc/init.d/iscsi restart
```

`iscsi`脚本会启动`iscsiad`守护进程，该进程负责管理启动器端的 iSCSI 目标。虽然你可能不会更改`iscsid`守护进程的配置脚本，但你应该意识到它位于`/etc/iscsi/iscsiad.conf`文件中。

`iscsi`脚本也是确定目标在本地系统中分配的设备名称的好方法，如示例 12-6 所示的高亮输出所示。

## 示例 12-6 确定 iSCSI 目标的本地设备名称

```
[root@localhost Desktop~]# /etc/init.d/iscsi status
iSCSI Transport Class version 2.0-870
version 6.2.0-873.13.el6
Target: iqn.2015-10.localdomain.localhost:test1 (non-flash)
  Current Portal: 10.0.2.15:3260,1
  Persistent Portal: 10.0.2.15:3260,1
  ********
  Interface:
  ********
  Iface Name: default
```

```
Iface Transport: tcp
Iface; Initiatorname: iqn.1994-05.com.redhat:39259bc66c9
Iface IPAddress: 10.0.2.15
Iface Hwaddress: <empty>
Iface Netdev: <empty>
SID: 1
iscsSI Connection State: LOGGED IN
isiscsSI Session State: LOGGED_IN
Internal scsisid Session State: NO CHANGE
**********
Timeouts:
***********
Recovery Timeout: 120
Target Reset Timeout: 30
LUN Reset Timeout: 30
Abort Timeout: 15
***
CHAP:
***
username: <empty>
password: ******
username_in: <empty>
password_in: ******
************
Negotiated iSCSI params:
****************
HeaderDigest: None
DataDigest: None
MaxRecvDataSegmentLength: 262144
MaxLimitDataSegmentLength: 8192
FirstBurstLength: 65536
MaxBurstLength: 262144
ImmediateData: Yes
InitialData: Yes
MaxOutstandingBurst: 1
************
Attached SCSI devices:
************
Host Number: 3 State: running
scsi Channel 00 Id: 0
scsi Channel 00 Id: 0
Attached scsi disk sdb State: running
```

回想`udev`系统创建并管理设备。如示例 12-6 所示的高亮输出所示，目标在本地系统中被分配了设备名称。

## 考试准备任务

### 复习所有关键主题

复习本章中最重要的主题，这些主题在页面外边缘用“关键主题”图标标记。表 12-3 列出了这些关键主题引用及其对应的页码。

| 关键主题元素 | 描述 | 页码 |
| --- | --- | --- |
| 段落 | `hdparm`命令 | 234 |
| 段落 | `sdparm`命令 | 236 |
| 段落 | `/proc`文件系统 | 237 |
| 段落 | 内核参数 | 239 |
| 段落 | iSCSI 术语 | 241 |
| 段落 | 初始化器配置 | 244 |

#### 定义关键术语

定义本章中的以下关键术语，并在术语表中检查您的答案：

直接内存访问 (DMA)、并行高级技术接口 (PATA)、高级技术接口 (ATA)、集成驱动器电子 (IDE)、高级技术接口包 (ATAPI)、扩展集成驱动器电子 (EIDE)、超高级技术接口 (UATA)、串行高级技术接口 (SATA)、iSCSI、目标、初始化器 (initiator)、世界标识符 (WWID)、逻辑单元号 (LUN)

### 复习题

这些复习题的答案位于附录 A。

1. 系统上的第一个 SATA 驱动器的设备名为`/dev/________`。

2. 哪项描述了允许硬件设备直接访问 RAM 的内核特性？

    a. PATA

    b. ATA

    c. DMA

    d. IDE

3. 下列哪些驱动类型可能与`/dev/sdb`文件关联？（选择两个。）

    a. SATA

    b. IDE

    c. 磁带驱动

    d. USB 驱动器

4. `hdparm`命令的哪个选项可启用或禁用 DMA 支持？

5. 哪个命令执行与`hdparm`命令相同的功能，但针对的是 SCSI 设备？

    a. `sd`

    b. `parm`

    c. `sd-parm`

    d. 以上均非

6. `________`文件系统包含几个文件，可以使用这些文件查看或修改存储设备的系统资源。

    a. `/etc`

    b. `/var`

    c. `/proc`

    d. `/tmp/`

7. `/proc/______`文件包含有关系统中断的信息。

8. 使用哪个命令可以修改位于`/proc/sys`目录文件中的内核参数？

9. 你编辑哪个文件来定义你的 iSCSI 目标 (targets)？

    a. `/etc/targets.conf`

    b. `/etc/tgt/targets.conf`
