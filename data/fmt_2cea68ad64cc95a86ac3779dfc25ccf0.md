
# 第 12 章：基础系统管理

`mount` 命令的 `-vfat` 部分指定你挂载的设备 `/dev/hda1` 是 DOS/Windows 文件系统。图 12-8 展示了此挂载命令的效果。

![](img/b418dfc0d37b54b9876d5e801170c507_398_0.png)

图 12-8：在 `/dos` 目录上挂载 DOS/Windows FAT 分区。

12-8 显示了你 DOS 分区中的目录如何映射到 Linux 文件系统。DOS 下的 `C:\DOS` 目录在 Red Hat Linux 下变为 `/dos/dos`。同样，`C:\WINDOWS` 现在是 `/dos/windows`。你可能可以看出这种模式。要将 DOS 文件名转换为 Linux 格式（当将 DOS 分区挂载到 `/dos` 时），请执行以下步骤：

1. 将 DOS 名称更改为小写。
2. 将 `C:\` 改为 `/dos/`。
3. 将所有反斜杠改为斜杠 `/`。

## 挂载 DOS 软盘

就像在 Red Hat Linux 文件系统上挂载磁盘分区一样，你也可以挂载 DOS 软盘。你必须以 root 登录才能挂载软盘，但你可以按照本节后部分所示步骤设置系统，以便任何用户都能挂载 DOS 软盘。你还需要知道软盘的设备名称。默认情况下，Linux 为软盘定义了以下两个通用设备名称：

- `/dev/fd0` 是 A 盘（第一个软盘驱动器）。
- `/dev/fd1` 是 B 盘（第二个软盘驱动器，如果有）。

作为挂载点，你可以使用文件系统中的任何空目录作为挂载点，但 Red Hat Linux 系统带有一个专门挂载软盘的目录 `/mnt/floppy`。

要在 `/mnt/floppy` 上挂载 DOS 软盘，请将软盘放入驱动器并输入以下命令：

```
mount -t vfat /dev/fd0 /mnt/floppy
```

挂载软盘后，你可以使用 Linux 的复制命令 `cp` 在软盘之间复制文件。要将当前目录下的文件 `gnome1.pcx` 复制到软盘，请输入：

```
cp gnome1.pcx /mnt/floppy
```

## 第二部分：探索红帽 Linux

Linux 操作系统使用 `/etc/fstab` 的内容来自动挂载各种文件系统。在 Red Hat Linux 启动期间，`init` 进程会执行一个运行 `mount -a` 命令的壳脚本。该命令读取 `/etc/fstab` 文件并挂载所有列出的文件系统（带有 `noauto` 选项的除外）。

`/etc/fstab` 中每行的第四列显示了适用于特定设备的选项列表，用逗号分隔。通常，你在此字段中找到 `defaults` 选项。`defaults` 选项意味着设备在启动时挂载、只有 root 用户可以挂载该设备，以及设备可读写。如果选项包含 `noauto`，则设备在系统启动时不会挂载。

`/etc/fstab` 第四列中的 `kudzu` 选项表示这些行是由 `kudzu` 硬件检测工具添加到 `fstab` 文件中的——`kudzu` 运行 `udev` 命令，并为其检测到的可移动设备在 `/etc/fstab` 文件中添加条目。你通常会发现 CD-ROM（`/dev/cdrom`）和软盘（`/dev/fd0`）的第四字段带有 `kudzu` 选项。例如，在带有 ZIP 驱动器的 PC 上，`/etc/fstab` 文件还有另一个 `kudzu` 添加的条目，将 `/mnt/zip` 挂载点与 Zip 设备（`/dev/hdd4`）关联如下：

```
/dev/hdd4 /mnt/zip auto noauto.owner.kudzu 0 0
```

### 挂载 DOS/Windows 文件系统

如果你在硬盘上安装了 Microsoft Windows 95/98，你已经在 Red Hat Linux 下挂载了 DOS 分区。如果没有，你可以轻松在 Red Hat Linux 中挂载 DOS 分区。挂载使 DOS 层次结构成为 Linux 文件系统的一部分。为了方便识别 DOS 分区，你可能希望将第一个 DOS 挂载为 `/dos`，第二个挂载为 `/dos2`，以此此类推。

要确定你的 DOS 硬盘分区是否设置为自动挂载，请输入以下 `grep` 命令在 `/etc/fstab` 文件中查找 `vfat` 字符串：

```
grep vfat /etc/fstab
```

如果输出显示包含 `vfat` 的一行或多行，则你的 Red Hat Linux 系统自动使用 DOS/硬盘分区。

如果 `grep` 命令没有在 `/etc/fstab` 中显示包含 `vfat` 字符串的行，则你的系统未设置自动挂载任何 DOS/硬盘分区。当然，一个很好的理由可能是你的硬盘上没有任何 DOS 分区。

即使你的硬盘上没有任何 DOS 分区，你也可以学习从 Red Hat Linux 访问 DOS 文件系统，因为你可能需要在 Linux 系统上访问 DOS 软盘。

要挂载 DOS 硬盘分区或软盘，请使用 `mount` 命令但包含 `-t vfat` 选项指定文件系统类型为 DOS。例如，如果你的 DOS 分区正好是 IDE 驱动器的第一个分区，且你想将其挂载为 `/dos`，请使用以下命令：

```
mount -t vfat /dev/sda1 /dos
```

如果输出显示包含 `vfat` 的一行或多行，则你的 Red Hat Linux 系统自动使用 DOS/硬盘分区。
