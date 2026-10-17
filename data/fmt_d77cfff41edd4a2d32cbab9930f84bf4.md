
Mackenzie, David. 1994. Finding Files. Cambridge, MA: Free Software Foundation. 可访问于 http://www.gnu.org/manual/manual.html.

Mackenzie, David et al. 1996. GNU Fileutils. 可访问于 www.gnu.org/manual.html.

Orr, Giles. 1999. Bash Prompt HOWTO. Linux Documentation Project. 可访问于 http://metalab.unc.edu/LDP/HOWTO/ Bash-Prompt-HOWTO.html

Nelson, Cameron, and Bill Rosenblatt. 1998. Learning the Bash Shell. Petaluma, CA: O'Reilly & Associates.

Ramey, Chet, and Brian Fox. 1996. Bash Reference Manual. Boston: Free Software Foundation. 可访问于 http://www.gnu.org/manuals/

# 掌握系统管理

在第 12 章“保持系统运行良好”中，你学习了使用 GNOME 和其他友好的辅助工具执行系统管理任务。在本章中，你学习了如何通过命令行界面执行许多相同的任务。正如你在阅读本章后得出的结论，学习这些内容是深入了解 GNOME 美丽外表下的 Linux 操作系统的好方法。此外，你可能会得出某些任务（例如解压 tar 归包）使用 shell 实际上更简单、更快速的结论。

# 挂载磁盘和文件系统

要使用外部存储设备（如 CD-ROM 驱动器、ZIP 驱动器软盘）上的文件，您必须对其进行挂载。本节介绍了基本的挂载概念，展示了如何使用 `mount` 命令，并最后演示了如何配置 Linux 自动挂载存储设备（以及其他外部文件系统）。

> 提示 情况下，Linux 要求用户具有 root 权限才能挂载外部存储设备和文件系统。为了完成本节中的示例，您应该以 root 用户身份登录。对于单用户系统，允许普通用户（如您的用户账户）挂载外部存储设备和文件系统并不存在安全风险，因此您应该配置 Linux 以允许用户挂载设备。您将在本节末尾学习如何操作。

# 理解挂载概念

当您安装 Red Hat Linux 时，安装软件会自动配置您的系统，以自动挂载硬盘上的各种分区。结果是这些分区内的文件系统就变成了一个更大的、整体的文件系统的一部分。如果您按照本书书第二部分的建议安装了 Red Hat Linux，您就创建了一个 `usr` 分区。它在挂载点与文件系统的其他部分连接。`/usr` 文件系统挂载在根目录（`/`）。

正如您可能已经意识到的，硬盘上的各种分区在 Linux 启动时会自动挂载。这是因为 Linux 遵循了名为 `/etc/fstab` 的重要配置文件中的指令。

以下是该文件的示例（我添加了标题来解释各列的含义）：

| 设备 | 挂载点 | 文件系统 | 设置 |
| :--- | :--- | :--- | :--- |
| `/dev/hda6` | `/` | `ext2` | `defaults` |
| `/dev/hda7` | `/home` | `ext2` | `defaults` |
| `/dev/hda8` | `/usr` | `swap` | `defaults` |
| `/dev/fd0` | `/mnt/floppy` | `ext2` | `noauto` |
| `/dev/cdrom` | `/mnt/cdrom` | `iso9660` | `noauto` |

以下是对该文件中设置的简要说明：

- `设备 (Device)` Linux 不使用驱动器名称，而是使用设备名称来引用存储和其他外设（常见存储设备名称列表见表 16.1）。

- `挂载点 (Mount Point)` 在此列中，您可以看到外部存储设备挂载的位置。例如，`/home` 分区挂载在根目录（`/`），而 CD-ROM 驱动器挂载在 `/mnt/cdrom`。

- `文件系统 (File System)` Linux 可以处理许多文件系统，包括原生 Linux 系统（`ext2`）。表 16.2 列出了 Linux 可以访问的一些文件系统。如您所见，Linux 可以直接访问极其多种文件系统。

- `设置 (Settings)` 这些设置决定了 Linux 是否在会话开始时自动挂载文件系统，同时也决定了其他选项。默认设置会自动挂载文件系统。`noauto` 设置要求用户在使用之前手动挂载文件系统。如您所见，软盘和 CD-ROM 驱动器在您它们之前必须先挂载。

为什么 Linux 要求用户手动挂载和卸载外部磁盘驱动器？很简单：驱动器中可能没有磁盘。当您插入磁盘时，`mount` 命令会强制 Linux 读取磁盘并将其文件添加到文件系统中。对于软盘，还有一个额外的原因与 Linux 使用的磁盘缓存系统有关。如果您在不先卸载的情况下从磁盘驱动器中拔出软盘，磁盘缓存软件可能尚未将更改写入磁盘，这将导致内容混乱。

# 表 16.1 存储外设的设备名称

| 设备名称 | 说明 |
|---|---|
| `/dev/fd0` | 软盘驱动器 #1 |
| `/dev/fd1` | 软盘驱动器 #2 |
| `/dev/cdrom` | CD-ROM 驱动器 |

# 表 16.2 Linux 可访问的文件系统

| 文件系统 | 说明 |
|---|---|
| `ext` | 旧的 Linux 文件系统 |
| `ext2` | 如今标准的 Linux 文件系统 |
| `hfs` | 分级文件系统 (Mac OS) |
| `hpfs` | OS/2 文件系统 |
| `iso9660` | CD-ROM 文件系统 |
| `msdos` | MS-DOS 文件系统（不支持长文件名） |
| `nfs` | 网络文件系统 (NFS) |
| `ntfs` | Windows NT |
| `ufs` | BSD Unix 文件系统 |
| `vfat` | 带有长文件名的 Windows 95/98 文件系统 |

> 注意 文件系统支持内置在 Linux 内核中，如果没有修改，您的内核可能不支持所有这些文件系统。要查看内核支持哪些文件系统，输入 `less /proc/filesystems` 并按 `q` 退出列表。

# 挂载外部文件系统

要挂载外部文件系统（例如软盘、ZIP 磁盘或 CD-ROM 上的文件），您可以使用 `mount` 命令。如果 `/etc/fstab` 中有设备的条目，可以使用 `mount` 命令的短版本，如下例所示：

```
#mount /dev/cdrom
```

当您按下回车键时，Linux 使用 `/etc/fstab` 中指定的默认值挂载 CD-ROM 驱动器中的磁盘，例如 `iso9660` 文件系统（这是 CD-ROM 数据的标准文件系统）。

> 提示 如果您尝试挂载的设备未列在 `/etc/fstab` 中，您必须使用 `mount` 命令的选项（以及其他选项），这允许您指定文件系统。然而，您可能不需要这样做，因为 Red Hat 安装软件会自动为这些设备创建条目。

一旦设备挂载，您就可以访问它。

> 注意：一旦设备挂载后，由于在 `/etc/fstab` 中有该设备的条目，您可以使用 `mount` 命令的短版本，如下例所示：

```
#mount /dev/cdrom
```

当您按下回车键时，Linux 使用 `/etc/fstab` 中指定的默认值挂载 CD-ROM 驱动器中的磁盘，例如 `iso9660` 文件系统（这是 CD-ROM 数据的标准文件系统）。

> 提示 如果您尝试挂载的设备未列在 `/etc/fstab` 中，您必须使用 `mount` 命令的选项（以及其他选项），这允许您指定文件系统。然而，您可能不需要这样做，因为 Red Hat 安装软件会自动为这些设备创建条目。

一旦设备挂载，您就可以访问它。

> 注意：一旦设备挂载后，由于在 `/etc/fstab` 中有该设备的条目，您可以使用 `mount` 命令的短版本，如下例所示：

```
#mount /dev/cdrom
```

当您按下回车键时，Linux 使用 `/etc/fstab` 中指定的默认值挂载 CD-ROM 驱动器中的磁盘，例如 `iso9660` 文件系统（这是 CD-ROM 数据的标准文件系统）。

> 提示 如果您尝试挂载的设备未列在 `/etc/fstab` 中，您必须使用 `mount` 命令的选项（以及其他选项），这允许您指定文件系统。然而，您可能不需要这样做，因为 Red Hat 安装软件会自动为这些设备创建条目。

一旦设备挂载，您就可以访问它。

> 注意：一旦设备挂载后，由于在 `/etc/fstab` 中有该设备的条目，您可以使用 `mount` 命令的短版本，如下例所示：

```
#mount /dev/cdrom
```
