

## 删除现有分区

要删除现有分区，请使用 `d` 菜单选项：

```
Command (m for help): p
Partition number (1-5): 5

Command (m for help):
```

> **注意**
>
> 如果删除包含任何逻辑分区的扩展分区，这些逻辑分区也将被删除。

## 将更改写入磁盘

完成磁盘分区表的编辑后，必须将分区表写入磁盘。为此，请使用 `w` 菜单选项。`fdisk` 将应用更改，然后退出：

```
Command (m for help): w
The partition table has been altered!

Calling ioctl() to re-read partition table.
Syncing disks.

WARNING: If you have created or modified any DOS 6.x
partitions, please see the fdisk manual page for additional
information.
```

> **注意**
>
> 如果要对正在运行的系统进行更改，通常建议在使用 `fdisk` 编辑分区表后重新启动系统。这样可以使所有应用程序都了解这些更改。在安装过程中，使用 `fdisk` 编辑分区表后通常不必重新启动。

> **提示**
>
> 由于 `fdisk` 会在低级别操作硬盘，因此在使用 `fdisk` 之前备份磁盘始终是明智之举。

## 第 2 章 自动安装

### 本章内容

- 自动安装中的问题 22
- 使用 Red Hat 的 Kickstart 进行自动安装 22
- 故障排除 29

### 自动安装中的问题

尽管 Linux 的安装已经变得相当简单，但在某些情况下，安装过程仍然可能过于繁琐或耗时。具体来说，存在以下问题：

- 当需要安装大量相似的系统时，手动逐一安装每个系统会耗费太多时间。
- 如果希望允许用户自行安装系统，典型的 Linux 安装过程可能过于复杂。

在这两种情况下，系统管理员都需要一个自动安装过程，以回答安装 Linux 时出现的所有提示。理想情况下，应设计一种无人值守安装方法，完全消除或尽量减少启动安装过程所需的人工干预。

大多数 Linux 系统都无法自动安装。但是，Red Hat Linux 提供了一种称为 *Kickstart* 的自动安装方法。

### 使用 Red Hat 的 Kickstart 进行自动安装

当需要构建大量硬件和软件配置相同的 Linux 工作站时，自动安装非常有用。在需要安装大量相同或相似的系统时，Kickstart 安装过程可以节省大量时间。

#### Kickstart 概念

Kickstart 方法使用一个文本配置文件，为 Red Hat 安装过程中的所有问题提供答案，从而实现系统自动安装。Kickstart 配置文件可以放置在启动软盘上，也可以放置在网络上的 DHCP 服务器上。

将配置文件放在启动软盘上时，安装过程只需将软盘插入计算机并启动计算机即可。在普通系统上，安装将在 15 到 20 分钟后完成。使用启动软盘方法时，需要一张最新的启动软盘、Kickstart 配置文件以及安装 CD-ROM。

当需要在大量计算机上安装 Red Hat Linux 时，使用 Kickstart 进行网络安装更加合适。此方法需要 DHCP 或 BOOTP 服务器、NFS 服务器和 DNS 服务器。当然，也可以将所有这些服务组合在一台安装服务器上。

#### 构建 Kickstart 配置文件

Red Hat Linux 6.2 附带一个名为 mkkickstart 的实用程序。如果系统中尚未安装该程序，可以通过挂载 Red Hat Linux CD-ROM，然后使用类似以下的命令，从 Red Hat CD-ROM 添加该软件包：

```
# rpm -i /mnt/cdrom/mkkickstart-1.2-1.i386.rpm
```

要使用 **mkkickstart** 构建一个示例 Kickstart 配置，请使用以下命令：

```
# mkkickstart > ks.cfg
```

然后可以编辑示例 Kickstart 配置文件，以满足特定需求。Kickstart 配置文件由三个主要部分组成：

- 安装前部分
- 软件包部分
- 安装后部分

#### 安装前部分

安装前部分用于回答有关系统配置的问题。此部分描述安装语言、安装介质来源（可以是 CD-ROM 驱动器或网络）以及键盘类型。安装前部分还描述分区信息、安装类型（升级或全新安装）、鼠标类型、时区信息、X Server 参数、root 账户密码、身份验证方案以及 lilo 参数。以下是 Kickstart 配置文件中典型的安装前部分：

```
lang en
network --ip 10.2.0.101 --netmask 255.255.0.0 --gateway 10.2.0.254 --nameserver 10.2.0.1
cdrom
device ethernet 3c59x
keyboard us
zerombr yes
clearpart --linux
part /boot --size 10
part swap --size 128
part / --size 1000
part /home --size 500
install
mouse ps/2
timezone Israel
xconfig --server "Mach64" --monitor "Sony wwm-15mu2"
rootpw --iscrypted $1$B4Psev3d$YZ4kPMhvi6ni0WQ8fm6QF0
auth --nisdomain bwc --useshadow
lilo --location mbr
```

可以根据需要调整这些条目。例如，将 `lang en` 条目改为 `lang fr`，即可将安装语言更改为法语。表 2.1 概述了 Kickstart 配置文件安装前部分中关键条目的含义。

**表 2.1。Kickstart 配置文件的安装前部分**

| 条目 | 描述 |
| --- | --- |
| `lang <language code>` | 指定安装期间使用的语言，采用两字母 ISO 国家代码。 |
| `network <network definition>` | 指定 Kickstart 获取网络配置信息的方式。对于动态分配网络配置信息，可以使用 `--bootproto dhcp` 或 `--bootproto bootp`；也可以组合使用 IP 地址、网络掩码、默认网关和名称服务器 IP 地址。 |
| `nfs` | 指定 NFS 安装方法。 |
| `cdrom` | 指定 CD-ROM 安装方法。 |
| `device <device definition>` | 指定可选的设备信息，例如以太网卡、SCSI 卡以及非 SCSI、非 IDE 的 CD-ROM 驱动器。对于 PCI 设备，通常不需要此项。 |
| `keyboard <language code>` | 使用两字母语言代码指定 Linux 中使用的键盘布局。 |
| `zerombr <yes or no>` | 指示安装程序是否应清除目标系统上的当前分区表。 |
| `clearpart <options>` | 指示是否要删除与 Linux 相关的分区（使用 `--linux` 选项），或删除所有分区（使用 `--all` 选项）。 |
| `part <mount point> --size <size>` | 指定要创建的分区、其挂载点以及以 MB 为单位的大小。 |
| `install` | 指定全新安装 Linux。 |
| `upgrade` | 指定升级安装 Linux。 |
| `mouse <mouse type>` | 指定系统的鼠标类型。 |
| `timezone <timezone>` | 指定时区。 |
| `xconfig <X Windows configuration options>` | 指定系统的 X 配置。 |
| `rootpw --iscrypted <encrypted password>` | 指定新安装系统的 root 密码的加密形式。 |
| `lilo --location <location>` | 指示 LILO 的安装位置。 |

> **注意：** 安装前条目的完整详细信息，请参阅商业版 Red Hat Linux 随附的《Red Hat Linux 安装指南》中的“Kickstart 安装”一章。

#### 软件包部分

软件包部分以关键字 `%packages` 开头，后面跟随要安装的所有软件包列表。定义软件包有两种方式。一种方式是使用预定义的软件包组，这些软件包组类似于手动安装过程中列出的软件包组。这些组的名称以 `@` 符号开头。典型的预定义软件包组示例包括 @Base 和 @C-Development。除了使用预定义软件包组之外，另一种方式是按名称列出每个软件包。以下是典型的软件包部分：

```
%packages
@Networked Workstation
@Kernel Development
bind-utils
dhcpd
```

在此示例中，同时使用了预定义的软件包组和单独的软件包名称。在 Red Hat Linux 6.2 中，可以使用以下软件包组：

- @Base
- @Printer Support
- @X Window System
- @GNOME
- @KDE @Mail/WWW/News Tools
- @DOS/Windows Connectivity
- @Graphics Manipulation
- @Games
- @Multimedia Support
- @Networked Workstation
- @Dialup Workstation
- @SMB (Samba) Server
- @IPX/Netware(tm) Connectivity

