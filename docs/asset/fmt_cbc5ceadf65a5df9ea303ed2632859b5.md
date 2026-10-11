
| `-y` | 在发生错误时自动重试，而不是询问用户是否重试。 |

表 31-2 `restore` 工具的命令行选项

# 以下是 `restore` 的典型调用示例：

```
[master@server ~]$ sudo restore -ivf /dev/st0
```

这将从设备 `/dev/st0`（第一个 SCSI 磁带设备）中提取转储文件，打印每个恢复步骤，然后为你提供一个交互会话，由你决定从转储中恢复哪些文件。

如果丢失了整个文件系统，可以使用相应的 `*mkfs.*` 命令重新创建文件系统，然后通过恢复来填充文件系统。例如，假设我们的外部 SATA 驱动器 (`/dev/sdb`) 故障了，它有一个格式化为 ext4 文件系统的单一分区 (`/dev/sdb1`)。在用新驱动器替换故障驱动器并对其分区后，你可以如下所示重新创建文件系统：

```
[master@server ~]$ sudo mkfs.ext4 /dev/sdb1
```

接下来，我们必须在适当的位置挂载该文件系统。我们假设这是 `/home` 文件系统，因此我们使用以下命令：

```
[master@server ~]$ sudo mount /dev/sdb1 /home
```

最后，通过将转储磁带放入 SCSI 磁带驱动器 (`/dev/st0`)，我们使用以下命令进行恢复：

```
[master@server ~]$ cd /home; sudo restore -rf /dev/st0
```

> 提示：如果你使用 `gzip` 压缩了转储文件，在执行恢复之前需要对其进行解压。只需使用 `gzip` 解压缩磁带设备并将其输出重定向到标准输出。标准输出应接到 `restore`，并将 `-f` 参数设置为从标准输入 (`stdin`) 读取。命令如下：

```
# gzip -d -c /dev/st0 | restore -ivf -
```

# `tar`

第 4 章讨论了使用 `tar` 创建文件归档。然而，没有讨论的事实是 `tar` 原本的设计是为了在磁带上创建文件归档（`tar` = tape archive，磁带存档）。由于 Linux 将设备视为文件的灵活方法，我们现在使用 `tar` 将一组文件归档并管理到单个磁盘文件中。同样的 `tar` 命令也可以重写为将文件发送到磁带。

与 `dump` 相比，`tar` 归档文件子集要容易得多。`dump` 工具仅适用于完整文件系统，但 `tar` 在备份方面真的比 `dump` 更好吗？是的，有时确实。

总的来说，在备份整个文件系统方面，`dump` 证明比 `tar` 更高效。此外，`dump` 存储了更多文件信息，需要更多的磁带空间，但让恢复变得简单得多。另一方面，`tar` 确实是跨平台的——在 Linux 下创建的 `tar` 文件可以被任何其他 Linux 格式下的 `tar` 命令读取。事实上，`gzip` 压缩过的文件甚至可以被流行的 Windows `WinZip` 和 `WinRAR` 程序读取！使用 `tar` 还是 `dump` 更好取决于你的需求和需要。

# `rsync`

在讨论传统的源项目时，没有提到 `rsync` 工具就是完整的。它用于从一个位置到另一个位置同步文件、目录或整个文件系统。该位置可以是从本地系统到另一个网络系统，也可以在本地文件系统内部。它在适当的情况下通过所谓的增量编码（顺序数据之间的差异）来尽可能地减少传输的数据量。`rsync` 适合编写脚本，并且可以轻松地包含在 `cron` 作或其他在系统中定期/自动运行的计划任务中。

许多基于命令行（CLI）和 GUI 前端在后端严重依赖 `rsync`（或 `librsync` 库）来完成基础工作。`Duplicity` (http://duplicity.mongnu.org/) 是一个流行的例子，它使用 `rsync` 算法/库提供加密且带宽高效的备份。

# 其它备份解决方案

存在多个开源项目提供企业级的备份解决方案。其中几个是 `AMANDA`、`Bacula`、`Dirvish`、`Mondo Rescue` 和 `BackupPC`。它们都有自己的优缺点，但仍然提供了稳健的备份解决方案。它们拥有良好的 GUI 前端，这使得它们对不同技能水平的管理员具有吸引力。

Advanced Maryland Network Disk Archive (`AMANDA`) 是一种备份系统，允许使用单个主备份服务器通过网络将多个主机备份到磁带驱动器、磁盘或光盘介质。你可以在 www.amanda.org 了解更多关于 `AMANDA` 的信息。

`Bacula` 是一个基于网络的备份程序包，允许在异构系统网络之间进行数据的备份、恢复和验证。`Bacula` 的网站为 www.bacula.org。

`Dirvish` 是一个基于网络的备份程序包，允许在异构系统网络之间进行数据的备份、恢复和验证。`Dirvish` 的网站为 www.dirvish.org。

`Mondo Rescue` 是一个基于网络的备份程序包，允许在异构系统网络之间进行数据的备份、恢复和验证。`Mondo Rescue` 的网站为 www.mondrescue.org。

`BackupPC` 是一个基于网络的备份程序包，允许在异构系统网络之间进行数据的备份、恢复和验证。`BackupPC` 的网站为 https://backuppc.github.io/backuppc/。

## 总结

备份是系统最重要的方面之一。你的系统可能设计精良且维护良好，但如果没有稳固的备份，整个系统可能会为为有。将备份视为你的保险策略。

尽管磁带驱动器是一种略显过时/不流行的介质，但我们涵盖了磁带驱动器的基础知识以及一些备份数据的命令行工具。通过这些和其他信息，你应该能够对你的系统进行完整的备份。

幸运的是，`dump`、`restore`、`tar` 和 `rsync` 并不是你唯一的备份选择。还有许多商业和非商业备份包。`AMANDA`、`Dirvish`、`Mondo` 和 `BackupPC` 等开源项目都是成熟且稳健的选择。

无论你决定以什么方式执行数据备份的任务，只需确保你执行了它！

# 在闪存/USB 设备上创建 Linux 安装程序（通过 GNU/Linux 操作系统）

在本节中，我们假设你已经可以访问一个当前运行 Linux 发行版的系统，并且可以方便地在 shell 中运行任何命令。这是一个理想原生解决方案的示例。以下是该方案所需的配置条件：

- 一个可以从闪存设备启动的系统
- 一个目标闪存设备（容量至少为 4GB）
- 你所选择的 Linux 发行版的 ISO 或或其他镜像文件
- 一个运行任何基于 Linux 的操作系统的系统 / Fedora、Ubuntu、openSUSE、RHEL、CentOS 等

以下是操作步骤：

1. 以具有管理员权限的用户（例如 `root`）身份登录到 Linux 发行版的终端或 shell 提示符时，切换到文件系统中具有足够可用空间的目录（使用 `df -sh` 命令进行检查）。在本例中，我们将使用 `tmp` 文件夹：

2. 将 Linux 发行版的 ISO 文件下载到文件系统中具有足够空间的区域。例如，你可以通过以下命令从 https://fedaproject.org（或 https://getfedora.org）下载最新的 Fedora 64 位服务器版本：

   `wget https://<URL>/Fedora-dvd-x86-<VERSION>.iso`

   其中 `<URL>` 是下载服务器上目录的完整路径（例如 https://fedaproject.org pub fedora linux releases/<VERSION>-Server-x86_64-iso）。

   文件名 `Fedora-Server-dvd-x86-<VERSION>.iso` 以及 URL 中的占位符 `<VERSION>` 代表你阅读此条内容时 Fedora 的最新版本号。例如 Fedora 版本 34，实际的 ISO 文件名将类似于 `Fedora-Server-dvd-x86_64-34-1.2.iso`。

   同样，你可以在此树下找到 Fedora 最新的开发版 Rawhide 流——**这些版本**绝对不要在生产环境中使用**：`fedaproject.org pub fedora linux development rawhide server x86_64 iso`。最新的 ISO 镜像以当前日期戳附加在文件名末尾命名（例如 `Fedora-Server-dvd-x86_64.Rawhide-20210130.n.o.iso`）。

   为了本例演示，假设 ISO 文件为 2GB。因此，我们需要确保目标闪存 USB 设备至少同样大。一个 4GB 的闪存设备是理想的。

3. 将闪存设备插入到主机系统上的相应端口。

4. 你需要一种方法来唯一标识 Linux 内核与插入的闪存设备关联的设备。正确识别目标设备非常重要，以免不小心覆盖了错误的设备！诸如 `mnt`、`blkid`、`fdisk`、`lsusb` 和 `dmesg` 等 CLI 工具可以帮助识别你的目标设备。你可能需要在插入新设备之前运行这些工具中的某些工具以记录系统的当前状态，然后在插入设备后再次运行，然后比较两者的输出。输出中的差异几乎总是新设备！`dmesg` 命令允许你检查内核缓冲区，并提供了一种识别设备的方法。可以在输出的末尾查看缓冲区中的最新内容或活动。要查看缓冲区最后十条条目（行），输入：
