
```bash
root@server1:~# tail /var/log/syslog
Sep 30 09:56:48 server1 kernel: [ 38.357431] cgroup: systemd-logind (619)
created nested cgroup for controller "memory" which has incomplete
hierarchy support. Nested cgroups may change behavior in the future.
Sep 30 09:56:48 server1 kernel: [ 38.357435] cgroup: "memory" requires
setting use_hierarchy to 1 on the root.
Sep 30 09:57:07 server1 ntpdate[2031]: step time server 91.189.89.199
offset 17.350701 sec
Sep 30 09:56:57 server1 kernel: [ 46.667766] audit_printk_skb: 48 callbacks
suppressed
Sep 30 09:56:57 server1 kernel: [ 46.667770] type=1400 audit
(1412085417.259:28): apparmor="STATUS" operation="profile_replace"
profile="unconfined" name="/usr/lib/cups/backend/cups-pdf" pid=2146 comm="apparmor_parser"
Sep 30 09:56:57 server1 kernel: [ 46.667776] type=1400 audit
(1412085417.259:29): apparmor="STATUS" operation="profile_replace"
profile="unconfined" name="/usr/sbin/cupsd" pid=2146 comm="apparmor_parser"
Sep 30 09:56:57 server1 kernel: [ 46.668185] type=1400 audit
(1412085417.259:30): apparmor="STATUS" operation="profile_replace"
profile="unconfined" name="/usr/sbin/cupsd" pid=2146 comm="apparmor_parser"
Sep 30 09:57:13 server1 kernel: [ 63.274963] hv_balloon: Received INFO_TYPE_MAX_PAGE_TYPE
Sep 30 09:57:13 server1 kernel: [ 63.274970] hv_balloon: Data Size is 8
Sep 30 10:09:01 server1 CRON[2290]: (root) CMD [ -x /usr/lib/php5/maxlength ] && [ -x /usr/lib/php5/sessionclean ] && [ -d /var/lib/php5 ] && /usr/lib/php5/sessionclean /var/lib/php5 $(/usr/lib/php5/maxlifetime)
root@server1:~# 
```

在 `Fedora 20` 中，用于记录通常存储在 `/var/log/boot.log`、`/var/log/messages` 或 `/var/log/syslog` 中的消息的日志系统，已被一个名为 `journald` 的日志数据库系统所取代。你可以在 `Fedora 20` 系统上使用 `journalctl` 命令，并配合 `-b` 选项，来查看通常存储在 `/var/log/boot.log`、`/var/log/messages` 或 `/var/log/syslog` 文件中的相同信息。由于 `journalctl` 命令会显示每次启动过程的条目，因此缩小时间范围非常重要。以下命令仅显示当天的启动信息：

```bash
[root@server1 ~]# journalctl -b -since=today | less
-- Logs begin at Tue 2015-09-16 21:56:29 EDT, end at Tue 2015-09-30 10:20:47 EDT. --
Sep 30 11:02:08 localhost.localdomain systemd-journal[71]: Runtime journal is using 8.0M (max 99.8M, leaving 149.7M of free 990.2M, current limit 99.8M).
Sep 30 11:02:08 localhost.localdomain systemd-journal[71]: Runtime journal is using 8.0M (max 99.8M, leaving 149.7M of free 990.2M, current limit 99.8M).
```

## 系统救援

从实时安装介质启动实时 Linux 操作系统，为 Linux 管理员在修复受损的 Linux 系统时提供了多种优势。实时操作系统包含一个小型的可启动 Linux 内核和虚拟文件系统，它们被加载到 `RAM` 中，并能够访问底层硬盘上的文件系统。因此，你可以使用实时操作系统中的工具来修复硬盘上的 Linux 安装中导致其无法启动的问题，例如：

- 引导加载器问题
- 文件系统/分区问题
- 配置文件问题
- 驱动程序问题

所有实时操作系统都包含一些用于修复系统问题的实用工具，包括 `fdisk`、`parted`、`e2mkfs`、`fsck` 等，以及将在后续章节中介绍的其他工具。请记住前一章的内容，`fsck` 命令只能在未挂载的文件系统上运行。如果 `/`（根）文件系统损坏，你可以使用 Linux 发行版的实时安装介质启动系统，并在实时操作系统中使用 `fsck` 命令来检查硬盘上的 `/`（根）文件系统，因为默认情况下它未被实时操作系统挂载。

![](img/c27875544958897d817484d558c208c8_309_0.png)

> 使用实时操作系统来修复安装在硬盘上的另一个 Linux 系统上的问题的过程，通常被称为 `系统救援`。

你还可以通过配置实时操作系统加载的 Linux 内核，使其使用硬盘上的 /（根）文件系统。要做到这一点，只需将本地磁盘上的 /（根）文件系统挂载到实时操作系统中的一个空目录（例如 `/mnt`）下，然后在命令提示符中输入 `chroot /mnt`。此时，`chroot` 命令将实时操作系统的根目录更改为 `/mnt` 目录，这实际上是本地硬盘上的 /（根）文件系统。从这一刻起，你将获得对这些 /（根）文件系统上任何命令的 `root` 用户访问权限，就像你正常从硬盘启动 Linux 系统时一样。例如，如果你运行 `passwd` 命令（用于更改用户密码），你实际上是在更改安装在硬盘上的 Linux 系统的 `root` 用户的密码。这通常用于恢复本地可访问的 Linux 系统，如果 `root` 密码丢失或被遗忘。

值得注意的是，此功能不仅限于实时安装介质。如果你从标准安装介质安装 Linux，欢迎屏幕通常会提供一个系统救援选项，允许你启动一个不包含 `GUI` 环境的小型实时 Linux 系统。这个小型实时 Linux 系统包含相同的恢复实用工具（`fdisk`、`parted`、`e2mkfs`、`fsck` 等），并允许你将硬盘上的 /（根）文件系统挂载起来，并运行 `chroot` 命令将你的实时 Linux 系统切换到该文件系统。

### 章节总结

- Linux 服务器通常比桌面系统使用更多的硬件。这些硬件使用机架安装形式因子安装在机架中。
- 自 1986 年以来，已开发了多种不同的 `SCSI` 标准。并行 `SCSI` 硬盘由 `SCSI ID` 唯一标识，并通过一个带端接的电缆连接到控制器。`SAS` 是一种较新的 `SCSI` 技术，使用串行电缆向硬盘传输信息。`iSCSI` 是一种 `SAN` 技术，用于在 `TCP/IP` 网络上将信息从 `iSCSI` 发起方传输到 `iSCSI` 目标。
- `RAID` 通常用于 Linux 服务器中，将多个硬盘组合成一个卷，以提高速度或容错能力。它可以由操作系统内的软件、硬盘控制器卡上的硬件或系统 `BIOS` 来实现。
- 不同的 `RAID` 级别决定了磁盘如何组合和写入。`RAID` 级别 0 不具备容错能力，而 `RAID` 级别 1 到 6 在硬盘故障时提供数据容错。
- `ZFS` 是一个高性能、容错的文件系统，通常安装在 Linux 服务器上。`ZFS` 使用跨越不同存储设备（包括本地磁盘、`SAN`、共享设备、大型原始文件和远程共享）的存储空间，提供了与 `RAID` 类似的大部分功能。
- Linux 服务器发行版不包含 `GUI` 环境，并且通常通过远程方式管理。与其他 Linux 发行版相比，它们的安装过程需要额外的信息。
- 不支持的硬件、有缺陷的 `RAM`、超频的 `CPU` 以及不正确的 `RAM` 设置都可能导致 Linux 安装失败。
- `/proc` 目录包含有关系统检测到的硬件的信息，在验证安装是否成功时非常有用。
- 你可以使用标准 Linux 安装介质和实时安装介质上找到的可启动操作系统来访问和修复受损的 Linux 安装。

## 关键术语

- **`1U` 服务器**：一种机架式服务器，其标准高度为 1.75 英寸。
- **刀片服务器**：参见 *机架式服务器*。
- **`chroot` 命令**：一个 Linux 命令，可用于将一个 Linux 系统的根目录切换到另一个目录。
- **磁盘镜像**：一种由两个相同硬盘组成的 `RAID` 配置，数据会并行写入这两个硬盘中，从而确保容错能力。也称为 `RAID 1`。
- **磁盘条带化**：一种 `RAID` 配置，其中单个文件被分割成多个部分，然后并行写入不同的硬盘以加快访问时间；这种类型的 `RAID` 不具备容错能力。也称为 `RAID 0`。
- **带奇偶校验的磁盘条带化**：一种 `RAID` 配置，结合了磁盘条带化以加快文件访问速度，并包含奇偶校验信息以确保容错能力。也称为 `RAID 5`。
- **容错**：用于描述在发生故障时停机时间最短的设备的术语。
- **固件 `RAID`**：由计算机 `BIOS` 控制的 `RAID` 系统。
- **`GRUB`（`GRAnd Unified Boot loader`，通用引导装载程序）**：Linux 系统上最常用的引导装载程序。它在启动时加载并执行 Linux 内核。
- **硬件 `RAID`**：由位于计算机内部磁盘控制器卡上的硬件控制的 `RAID` 系统。
- **安装日志文件**：在安装过程中创建的文件，用于记录安装期间发生或失败的操作。
- **互联网 `SCSI`（`iSCSI`）**：一种通过 `TCP/IP` 网络传输数据的 `SCSI` 技术。
- **`iSCSI` 发起方**：指在 `iSCSI SAN` 中连接到 `iSCSI` 目标方的计算机的术语。
- **`iSCSI` 目标方**：指在 `iSCSI SAN` 中的存储设备的术语。
- **`journalctl` 命令**：用于配置 `journald` 以及查看 `journald` 数据库中日志条目的命令。
- **`journald`**：在某些 Linux 发行版（如 `Fedora 20`）上用于记录（或日志记录）系统事件的系统。
- **Linux 服务器发行版**：包含对 Linux 服务器有用的软件包的 Linux 发行版。
- **逻辑单元号（`LUN`）**：连接到 `SCSI` 链路中给定节点的每个设备的唯一标识符。
- **`mdadm` 命令**：用于在 Linux 系统上配置软件 `RAID` 的命令。
- **超频**：用于描述运行速度超过其额定时钟速度的 `CPU` 的术语。
- **并行 `SCSI`**：传统的 `SCSI` 技术，通过并行电缆传输数据。
- **机架式服务器**：一种薄型外形规格，用于容纳安装在服务器机架中的服务器硬件。
- **`RAID-Z`**：使用 `ZFS` 实现的 `RAID 5` 级，它使用可变条带，提供更好的性能和容错能力。
- **独立磁盘冗余阵列（`RAID`）**：将多个硬盘驱动器的存储空间合并为一个更大的逻辑存储单元的过程。
- **`SCSI ID`**：唯一标识并优先排序连接到 `SCSI` 控制器的设备的编号。
- **分段错误**：软件在无法定位完成其任务所需的信息时遇到的错误。
- **串行连接 `SCSI`（`SAS`）**：一种以串行模式而非传统并行模式传输信息的 `SCSI` 技术。
- **软件 `RAID`**：由运行在操作系统内的软件控制的 `RAID` 系统。
- **跨接（`Spanning`）**：一种 `RAID 0` 级类型，允许将两个或多个设备表示为一个大型卷。
- **存储区域网络（`SAN`）**：通过高速网络访问同一存储设备的一组计算机。
- **系统救援**：使用实时 Linux 操作系统访问和修复损坏的 Linux 安装的过程。
- **目标 `ID`**：参见 *`SCSI ID`*。
- **终端器**：一种用于终止电气传导介质以吸收传输信号并防止信号回波的设备。
- **不间断电源（`UPS`）**：一种包含电池存储的设备，用于在断电时为计算机供电。
- **`Zettabyte` 文件系统（`ZFS`）**：一种高性能文件系统和卷管理软件，常用于在 Linux 和 UNIX 系统上从多个存储设备创建卷。
- **`zfs` 命令**：用于配置 `ZFS` 文件系统功能的命令。
- **`ZFS` 存储池**：由 `ZFS` 管理的一系列存储设备。
- **`ZFS` 子系统**：`ZFS` 卷上的一个子目录，可由 `ZFS` 作为独立单元进行管理。
- **`ZFS` 卷**：由 `ZFS` 存储池内的空间创建的包含 `ZFS` 文件系统的卷。
- **`zpool` 命令**：用于配置 `ZFS` 存储池和卷的命令。

## 复习题

1. `SAS` 通过并行电缆将数据传输到 `SCSI` 磁盘。正确还是错误？

2. 以下哪项用于描述通过网络访问 `iSCSI` 硬盘的计算机？

    - a. `iSCSI` 目标方
    - b. `iSCSI` 请求方
    - c. `iSCSI` 发起方
    - d. `iSCSI` 终端方

3. 你想查看日志文件以获取有关 Linux 安装过程中发生的问题的信息。你很可能在哪个目录中找到日志文件？

    - a. `/root/log`
    - b. `/sys/log`
    - c. `/var/log`
    - d. `/etc/log`

4. 以下哪个 `RAID` 级别不具备容错能力？

    - a. `RAID 0`
    - b. `RAID 1`
    - c. `RAID 4`
    - d. `RAID 5`

5. 在系统救援期间，你可以使用哪个命令从实时操作系统的根目录切换到安装在硬盘上的 Linux 系统的根目录？

    - a. `mount`
    - b. `sysimage`
    - c. `chroot`
    - d. `rescue`

6. 以下哪项不是 `RAID` 类型？

    - a. 硬件 `RAID`
    - b. 软件 `RAID`
    - c. 固件 `RAID`
    - d. 串行 `RAID`

7. `/proc` 文件系统存储在哪里？

    - a. 在 `RAM` 中
    - b. 在硬盘的 `/` 目录中
    - c. 在硬盘的 `/etc` 目录中
    - d. 在硬盘的 `/var` 目录中

8. 哪个 `RAID` 级别使用带奇偶校验的条带化？

    - a. 2
    - b. 4
    - c. 1
    - d. 5

9. `RAID-Z` 在功能上等同于 `RAID 1` 级。正确还是错误？

10. 使用 8 位宽数据路径的 `SCSI` 设备使用 ________。

    - a. 8 针连接器
    - b. 15 针连接器
    - c. 50 针连接器
    - d. 68 针连接器

11. 哪种类型的 `RAID` 完全在 Linux 安装过程中配置？

    - a. 硬件 `RAID`
    - b. 软件 `RAID`
    - c. 固件 `RAID`
    - d. 串行 `RAID`

12. 可以使用哪个命令从 `/dev/sdb` 和 `/dev/sdc` 上的空间创建一个名为 `test` 的 `ZFS` 卷，其功能类似于 `RAID 1` 级？

    - a. `zpool create test /dev/sdb /dev/sdc`
    - b. `zpool create test mirror /dev/sdb /dev/sdc`
    - c. `zpool create test raidz /dev/sdb /dev/sdc`
    - d. `zpool create test raidz2 /dev/sdb /dev/sdc`

![](img/c27875544958897d817484d558c208c8_314_0.png)

13. 上一个问题中的 `test` `ZFS` 卷将被 `ZFS` 系统挂载到哪个目录？

    - a. `/mnt/test`
    - b. `/media/test`
    - c. `/lfs/test`
    - d. `/test`

14. Linux 服务器通常使用机架式服务器硬件安装在机架中。以下哪项用于描述机架式服务器的最小高度？

    - a. `1U`
    - b. `Series A`
    - c. `Type A`
    - d. `Level 5`

15. 哪个 `RAID` 级别也称为镜像？

    - a. 0
    - b. 1
    - c. 4
    - d. 5

16. `ZFS` 卷默认情况下通过 `/etc/fstab` 中的条目在启动时挂载。正确还是错误？

17. 在 `Fedora` 安装期间，以下哪项可能导致分段错误（致命信号 11）？

    - a. `RAM` 问题
    - b. 超频 `CPU`
    - c. 不适当的设备驱动程序
