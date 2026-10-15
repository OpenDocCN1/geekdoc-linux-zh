
```
solaris$ sudo iscsiadm modify initiator-node -a CHAP -H testclient
solaris$ sudo iscsiadm modify initiator-node -C
Enter secret: <password for testclient>
Re-enter secret: <password for testclient>
solaris$ sudo iscsiadm modify discovery -s enable
solaris$ sudo iscsiadm add static-config iqn.1994-11.com.admin:test,iserver
solaris$ sudo iscsiadm list target -S
Target: iqn.1994-11.com.admin:test
Alias: -
TPGT: 1
ISID: 4000002a0000
Connections: 1
LUN: 0
Vendor: IET
Product: VIRTUAL-DISK
OS Device Name: /dev/rdsk/c1t03d0s2
```

此时你可以像平常一样配置磁盘（例如，通过运行 `zpool create iscsi c1t03d0`）。

第一个命令将发起程序的身份验证模式设置为 CHAP 并将 CHAP 用户名设置为 `testclient`。`-C` 选项设置密码；你不能将此选项与其他选项组合使用。也可以为每个目标单独设置名称和密码，如果你愿意的话。

`modify discovery` 命令启用静态配置目标的使用，而 `add` 命令指定特定目标的服务器和 IQN。所有这些配置在重新启动后仍然有效。

要向其他系统提供 iSCSI 目标，你需要安装 `SUNWiscsitgt` 包。管理结构与发起程序端类似，但命令是 `iscsitadm` 而不是 `iscsiadm`。

要在 HP-UX 系统上使用 iSCSI，请从 `software.hp.com` 下载 iSCSI 发起程序软件，并使用 HP-UX 的 Software Distributor 工具进行安装。需要重建内核并重新启动。幸运的是，系统在独立手册中记录得很好，即 HP-UX iSCSI Software Initiator Support Guide，可从 `docs.hp.com` 获取。

大多数发起程序配置都是使用 `iscsiutil` 命令完成的，已安装在 `/opt/iscsi/bin` 中。使用 `iscsiutil -I iqn` 设置发起程序的 IQN，使用 `iscsiutil -u -N user` 设置全局 CHAP 用户名（它也可以按服务器或按目标设置），并使用 `iscsiutil -u -W password` 设置全局 CHAP 密码。

然后你可以使用 `iscsiutil -a -I server` 从特定服务器添加目标。运行 `ioscan -NH 64000` 以激活服务器连接并创建虚拟磁盘设备。你可以使用 `iscsiutil -p -o` 检查系统的状态。

AIX 的 iSCSI 发起程序已安装并可直接使用。按照典型的 AIX 风格，大多数配置都是通过系统的 ODM 数据库完成的。`iscsi0` 设备代表发起程序整体的配置，而单个目标设备可以定义为 ODM 条目或在 `/etc/iscsi` 中的文本配置文件。文本配置文件似乎工作得更可靠一些。

AIX 不区分发起程序的 IQN 和其 CHAP 用户名。IQN 设置在 `iscsi0` 设备上；因此，你应该计划在每个服务器上使用相同的 CHAP 用户名。快速配置路径的第一步是将该 IQN 设置为适当的值。

```
aix$ sudo chdev -l iscsi0 -a initiator_name='iqn.1994-11.com.admin:client'
```

我们为此示例使用了与其他系统不同的 CHAP 用户名，因为“testclient”在技术上不是发起程序的有效 IQN（尽管实际上也可以正常工作）。

在 `/etc/iscsi/targets` 文件中，我们添加以下条目：

```
iserver 3260 iqn.1994-11.com.admin:test "chap_password"
```

3260 是 iSCSI 的标准服务器端口；我们在这里包含它只是因为文件格式要求端口。要激活新的 iSCSI 磁盘，我们只需要

运行 `cfgmgr -l iscsi0`。`cfgmgr` 命令不会打印任何确认信息，但我们可以通过查看 `/dev` 目录（在我们的示例系统中，新磁盘为 `/dev/hdisk2`）或运行 `smitty devices`，导航到 Fixed Disk 类别并列出条目，来确认新设备已出现。后一种方法或许更安全，因为 `smitty` 明确显示 `hdisk2` 是一个 iSCSI 卷。

要断开 iSCSI 设备，不仅需要编辑配置文件并用 `cfgmgr` 重新加载配置，还必须从 `smitty` 的 Fixed Disk 列表中删除该磁盘。

## 8.12 练习

E8.1 描述管理员在为以下每种应用设计存储架构时应考虑的任何特殊因素。

- a) 将托管约 200 个用户主目录的服务器
- b) 站点主要 DNS 服务器的交换区
- c) 大型垃圾邮件站点的邮件队列存储
- d) 一个大型 InnoDB（MySQL）数据库

E8.2 逻辑卷管理器功能强大，但如果不充分理解可能会令人困惑。练习在卷组中添加、删除和调整磁盘大小。展示如何将一个设备从一个卷组中移除并添加到另一个卷组。如果想将一个逻辑卷从一个卷组移动到另一个卷组，你会怎么做？

E8.3 使用印刷或网络资源，确定性能最好的 SCSI 和 SATA 驱动器。用于评估这些驱动器的基准测试是否反映了繁忙服务器对其启动磁盘的使用方式？你需要为 SCSI 支付多少成本溢价，又能获得多少性能提升（如果有的话）？

E8.4 向系统添加一块磁盘，并在新磁盘上设置一个分区或逻辑卷作为备份根分区。确保可以从备份根启动，并且系统在如此启动时正常运行。记录完成此任务所需的所有步骤。你可能会发现 `script` 命令很有帮助。（需要 root 权限。）

E8.5 什么是超级块，它有什么用途？查阅内核头文件中的 ext4 超级块结构的定义，并讨论该结构中每个字段代表什么。

E8.6 使用 `mdadm` 及其 `-f` 选项模拟 Linux RAID 阵列中的一块故障磁盘。移除该磁盘后再将其加回。`/proc/mdstat` 在每个步骤中看起来如何？

★★ E8.7 在 ext4 文件系统上的一个 inode 中存储了哪些字段？列出代表 `/etc/motd` 文件的 inode 的内容。该文件的 filename 存储在哪里？（工具如 `hexdump` 和 `ls -i` 可能有帮助。）

★★ E8.8 使用 `od` 或 `hexdump` 等程序检查一个目录文件的内容。每个变长记录代表该目录中的一个文件。查阅目录的磁盘上结构并解释每个字段，使用一个真实目录文件中的示例。接下来，查看使用它们的系统上的 `lost+found` 目录。为什么在 `lost+found` 目录为空时那里会有这么多名称？

★★★★★ E8.9 编写一个程序遍历文件系统并打印 `/etc/motd` 和 `/etc/magic` 文件的内容。但不要直接打开文件；打开根分区的原始设备文件并使用 `seek` 和 `read` 系统调用来解码文件系统并找到适当的数据块。`/etc/motd` 通常很短，可能只包含直接块。`/etc/magic` 应该要求你解码间接块。（如果不是，请选择一个更大的文本文件。）

提示：阅读系统头文件时，请确保你找到了文件系统的磁盘上 inode 结构，而不是内存中 inode 结构。（需要 root 权限。）

# 9 周期性进程

![](img/14d78e3cecac4581d37024baf1e94cca_331_0.png)

脚本和自动化是实现一致性和可靠性的关键。例如，`adduser` 程序可以比你更快地添加新用户，并且出错的可能性更小。几乎任何任务都可以编码为 Perl 或 Python 脚本。

经常需要让脚本或命令在没有任何人工干预的情况下执行。例如，你可能希望有一个脚本每半小时验证一次你的网络路由器和交换机是否正常工作，并在发现问题时向你发送电子邮件。¹

## 9.1 CRON：调度命令

`cron` 守护进程是按预定时间表运行命令的标准工具。它在系统启动时启动，并在系统运行时一直运行。

`cron` 读取包含命令行列表及其调用时间的配置文件。命令行由 `sh` 执行，因此你几乎可以用 `cron` 完成任何手工从 shell 可以完成的操作。²

1. 许多站点在此基础上更进一步，一旦检测到问题就会向管理员的手机发送短信。有关更多细节，请参阅第 21 章，网络管理和调试。
2. 你也可以配置 `cron` 使用其他 shell。
