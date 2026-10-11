
`/etc/fstab` 文件是一个配置文件 —— 一个包含 `mount` 和 `unmount` 命令使用的信息的文本文件。`/etc/fstab` 文件中的每一行都提供了关于设备及其在 Linux 系统中挂载点的信息。本质上，`/etc/fstab` 文件将文件系统的各种挂载点与特定设备关联，使得 `mount` 命令能够按照需要对挂载点或设备进行操作。

这里是一个 SUSE 系统的 `/etc/fstab` 文件（它在其他 Linux 发行版中具有类似的格式）：

| 设备 | 挂载点 | 文件系统 | 选项 | Dump | Pass |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda1 | /boot | reiserfs | acl,user_kattr | 1 | 1 |
| /dev/hda2 | /data | auto | acl,user_kattr | 1 | 2 |
| /dev/hda3 | /home | auto | noautoer | 0 | 0 |
| /dev/hda4 | /var | auto | noautoer | 0 | 0 |
| /dev/hda5 | /tmp | auto | noautoer | 0 | 0 |
| /dev/hda6 | /root | defaults | ro,users,gid,umask=0002,nous=utf8 | 0 | 0 |
| /dev/hda8 | swap | pri=42 | | 0 | 0 |
| devpts | /dev/pts | swap | devpts=0620,gid=5 | 0 | 0 |
| proc | /proc | defaults | | 0 | 0 |
| usbfs | /proc/bus/usb | usbfs | noautoer | 0 | 0 |
| sysfs | /sys | | | 0 | 0 |
| /dev/cdrecorder | /media/cdrom | subfs | noautoer | 0 | 0 |
| ffs-cdffs | /proc | proc,nodesid,nosuid,exec,charset=utf8 | | 0 | 0 |
| /dev/fd0 | /media/floppy | subfs | sync | 0 | 0 |

每行的第一个字段显示设备名称（例如硬盘）。第二字段是挂载点，第三字段指示设备上的文件系统类型。你现在可以忽略后三个字段。

此 `/etc/fstab` 文件显示 `/dev/hda8` 设备作为虚拟内存的交换设备（swap），这就是为什么挂载点和文件系统被设置为 `swap` 的原因。

Linux 操作系统使用 `/etc/fstab` 文件的内容来自动挂载各种文件系统。在启动过程中，`init` 进程会执行一个脚本，运行挂载 `/etc/fstab` 中列出的所有文件系统（带有 `noauto` 选项的除外）。`/etc/fstab` 每行的第三字段指定了该设备上的文件系统类型，第四字段显示了逗号分隔的选项列表，`mount` 命令在文件系统上挂载设备时使用这些选项。通常会在该字段中找到 `defaults` 选项。`defaults` 选项意味着（其他方面之外）设备在启动时挂载，且只有 root 用户可以挂载该设备，并且设备可读可写。如果选项包含 `noauto`，则设备在系统启动时不会自动挂载。

在 Fedora 中，你通常会在 `/etc/fstab` 条目的第四字段中发现 `managed` 选项。`managed` 选项表示该行是由 HAL（硬件抽象层）守护进程添加的，该进程运行 `fstab-sync` 命令向 `/etc/fstab` 文件添加条目。可移动设备/DVD/CD-ROM 驱动器（大多数系统中为 `/dev/hdc`）的第四字段具有 `managed` 选项。

## 2 使用 NFS 共享文件

通过 NFS 共享文件非常简单，涉及两个基本步骤：

- 在 NFS 服务器上，通过在 `/etc/exports` 文件中列出目录并运行 `/usr/sbin/exportfs` 命令导出一个或多个目录。此外，你必须运行 NFS 服务器。
- 在每个客户端系统上，使用 `mount` 命令挂载服务器已导出的目录。

NFS 服务器取决于你使用的 Linux 发行版。如果有用的 GUI 系统管理员工具，你可以从 GUI 工具启动 NFS 服务器。否则，你可以在终端中运行命令来启动 NFS 服务器。在 Debian 中，你可以使用 `service-d nfs-kernel-server start` 来启动 NFS 服务器。在 Fedora 中，输入 `service nfs start`。在 SUSE 中，你可以使用 Yaast Control Center（Main Menu>System>YaST>System>System Services (Runlevel)）来启动 NFS 服务器。在 Xandros 中，你可以从 Xandros Control Center（Main Menu>Control Center）启动 NFS 服务器，或者在终端窗口中输入 `service-d nfs-user-start`。

使用 NFS 的问题在于每个客户端系统必须支持它。大多数 PC 不带 NFS —— 这如果你想通过 NFS 共享文件，就需要购买 NFS 软件。然而，由于你局域网上的所有系统都运行 Linux（或其他内置 NFS 支持的 UNIX 变体），因此使用 NFS 是意义的。

NFS 存在安全漏洞。因此，不要在直接连接到互联网的系统上设置 NFS。

接下来的章节将引导你完成 NFS 设置，以局域网上的两台 Linux PC 为例。

## 使用 NFS 导出文件系统

从导出（向客户端系统提供）目录内容的系统开始。在服务器上，你必须运行 NFS 服务并指定要导出到客户端系统的一个或多个文件系统。

要导出文件系统，你必须运行 NFS 服务并指定要导出到客户端系统的一个或多个文件系统。

## 备份与恢复文件

例如，如果你将 Linux 系统作为学习工具（为了获取更多关于 Linux 或编程的知识），你可能只需要对配置 Linux 需要的一些系统文件进行备份。在这种情况下，你的备份策略可以是：每当你使用任何系统配置时，将重要的系统配置文件保存到一张或多张软盘上。

另一方面，如果你将 Linux 系统作为为许多用户提供共享存储的办公服务器，那么由于磁盘故障导致业务中断的风险要高得多。在这种情况下，你必须每周每周备份所有文件，并每天备份任何新增或更改的文件。你可以以自动化的方式执行这些备份（使用本微型书籍第 1 章描述的任务调度功能）。此外，你可能需要一个能够存储大量数据（GB级）的备份存储介质。换句话说，对于高风险情况，你的备份策略更加复杂，并且需要额外的设备（如磁带机）。

你对备份的选择取决于你需要备份的数据量。对于少量数据（如系统配置文件），你可以使用软盘或 USB 驱动器作为备份介质。如果你的 PC 有 Zip 驱动器，可以使用 Zip 磁盘作为备份介质；这些非常适合备份单用户目录。要备份整个服务器，请使用磁带机，通常是连接到 SCSI 控制器的 4mm 或 8mm 磁带机。此类磁带机每磁带可以携带数 GB 的数据，可以使用它们在单个磁带上备份整个文件系统。

将文件备份到这些介质时，你可以通过名称引用备份设备。表 3-4 列出了一些常用备份设备的名称。

| 表 3-4 常用备份设备的名称 |
| 备份设备 | Linux 设备名称 |
| :--- | :--- |
| 软盘 | /dev/fd0 |
| IDE Zip 驱动器 | /dev/hdc4 或 /dev/hdd4 |
| SCSI 磁带机 | /dev/sda (假设它是第一个 SCSI 磁盘——否则，设备名称取决于 SCSI ID) |
| | /dev/st0 或 /dev/nst0 (n 前缀意味着在文件拷贝到磁带后磁带不会回带) |

## Linux 商业备份工具

下一节将解释如何使用 Linux 自带的磁带归档程序 (`tar`) 备份和恢复文件。虽然你可以使用 `tar` 管理备份，但也有许多具有图形用户界面和其他功能以简化备份的商业备份工具。以下是 Linux 上知名的商业备份工具：

- `BRU`: 来自 TOLIS Group, Inc. 的备份与恢复工具 (www.tolisgroup.com)
- `ONE-TAR`: 来自 Lone Star Software Corp. 的磁带备份软件包 (www.cactus.com)
- `Arkeia`: 来自 Arkeia 的异构网络备份与恢复软件 (www.arkeia.com)
- `Bare Metal Plus`: 来自 UniTrends 的备份与恢复软件 (www.unitrends.com)
- `BrightStar ARC Backup for Linux`: 来自 Computer Associates 的 Linux 系统数据保护技术 (http://ca.com/us/products/product.aspxID=4536)

## 使用 tar 归档器

你可以使用 `tar` 命令将文件归档到设备（例如软盘或磁带）。`tar` 程序创建一个归档文件，该文件可以包含其他目录并（可选地）对归档进行压缩以实现高效存储。归档被写入指定的设备或其他文件。事实上，许多软件包是以压缩 tar 文件的形式分发的。

`tar` 程序的命令语法如下：

```
