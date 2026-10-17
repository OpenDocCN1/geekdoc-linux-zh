
## 文件系统管理

```
[root@localhost]# mount
/dev/hd1 on / type ext3 (rw)
none on /proc type proc (rw)
usedevfs on /proc/bus/usb usedevfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
none on /proc/sys/fs/binfmt_misc type binfmt_misc (rw)
```

设备 `/hd1` 挂载在 `/` 目录上，包含一个 `ext3` 文件系统。上面列出的其他文件系统是系统使用的特殊文件系统。

要在目录树上挂载设备，使用带有选项和参数的 `mount` 命令来指定文件系统类型、要挂载的设备以及挂载目录（挂载点）。

### 检查与挂载

如果另一个用户正在使用挂载点目录，系统将给你返回错误消息，磁盘将不会挂载。要检查 `/mnt/floppy` 目录是否正在使用，输入带有 `-u` 选项的 `fuser` 命令，如下所示。

```
[root@localhost root]# fuser -u /mnt/floppy
[root@localhost root]#
```

上述输出表示 `/mnt/floppy` 目录没有被任何用户进程占用。要将第一个格式化为 `ext2` 的软盘挂载到 `/mnt/floppy` 目录，你需要运行以下命令。

```
[root@localhost root]# mount -t ext2 /dev/fd0 /mnt/floppy
[root@localhost root]# mount
/dev/hdl0 on /proc type proc (rw)
usedevfs on /proc/bus/usb usedevfs (rw)
none on /dev/shm type tmpfs (rw,gid=5,mode=620)
none on /dev/sys/ type tmpfs (rw)
none on /proc/fs/binfmt_misc type binfmt_misc (rw)
```

设备 `/hd1` 挂载在 `/` 目录上，包含一个 `ext3` 文件系统。上面列出的其他文件系统是系统使用的特殊文件系统。

要在目录树上挂载设备，使用带有选项和参数的 `mount` 命令来指定文件系统类型、要挂载的设备以及挂载目录（挂载点）。

### 挂载选项与配置

挂载选项（mount options）是命令在挂载卷时接受的额外选项，例如只读或 `"ro"`。任何带有挂载选项 `"noauto"` 的文件系统在启动时都不会自动挂载。可以通过查看 `mount` 命令的帮助页找到该命令可以使用的选项完整列表。

`dump` 用于 `dump` 命令在备份文件系统时使用。该字段中的 `"1"` 表示该文件系统应该被备份，而 `"0"` 则表示不需要备份。

`fsck` 用于 `fsck` 命令在启动时检查文件系统的错误。任何在该字段中为 `"1"` 的文件系统将首先被检查，在任何数字为 `"2"` 的文件系统之前。数字为 `"0"` 的文件系统不进行检查。

**注意：** 对于 `/etc/fstab` 文件中所有打算在启动时挂载的文件系统，您应该使用 `-a` 命令。

以下输出显示了 `/etc/fstab` 文件的内容：

```
[root@localhost root#] cat /etc/fstab
LABEL=/ ext3 defaults 1 1
none /dev/pts devpts gid=mode=620 0 0
none /proc proc defaults 0 0
none /dev/shm tmpfs defaults 0 0
/dev/sd2 swap swap 0 0
/dev/cdrom /mnt/cdrom is09660 noauto,owner,kudzu 0 0
/dev/fd0 /mnt/floppy auto noauto,user,kudzu 0
```

要将第一个软磁盘设备 (`/dev/fd0`) 挂载到 `/mnt/floppy` 目录并自动检测设备上的文件系统类型，您需要为 `mount` 命令提供足够的信息，以便在 `/etc/fstab` 文件中找到对应的行。

```
[root@localhost root#] mount /dev/fd0
```

上述输出中的 `mount` 命令是因为 `/etc/fstab` 中存在描述挂载 `/dev/fd0` 设备的行。

或者，您也可以挂载点作为参数。

```
[root@localhost root#] mount /mnt/floppy
```

在挂载和卸载软盘时很有用的命令见下表。

| 命令 | 说明 |
| :--- | :--- |
| `mount` | 显示已挂载的文件系统 |
| `mount -t<type> <device> <mount point>` | 将特定 `<type>` 的 `<device>` 挂载到 `<mount point>` 目录 |
| `fuser -u <directory>` | 显示使用特定目录的用户 |
| `umount <mount point>` 或 `umount <device>` | 从特定的 `<mount point>` 目录卸载 `<device>` |

![](img/90ff486f13f13845c7a30a29d84ce954_236_0.png)

### 在 GUI 中挂载软盘

虽然上表列出的命令允许对挂载过程进行完全控制，但在 GUI 环境下工作，您可能会发现使用图标更容易。同样，`/etc/fstab` 中列出的条目用于指定挂载点。

在 GNOME 桌面中挂载软盘，双击“计算机（Computer）”图标，这将打开图 5-3 所示的框。然后，双击“软磁盘（Floppy）”图标，将打开一个显示磁盘内容的框。

![](img/90ff486f13f13845c7a30a29d84ce954_237_0.png)

*图 5-3: 在 Gnome 环境下挂载软盘*

在 KDE 桌面，您可以双击“在此开始（Start Here）”图标并选择“设备（Devices）”以打开图 5-4 所示的框。然后，双击“软磁盘（Floppy）”图标。

![](img/90ff486f13f13845c7a30a29d84ce954_237_1.png)

*图 5-4: 在 KDE 环境下挂载软盘*

在 GUI 环境下挂载软盘会在面上放置一个代表软磁盘的图标。您可以双击软磁盘图标打开文件列表。要卸载软盘，右键点击软磁盘图标并选择“卸载卷（Unmount Volume）”。

### 软磁盘操作实践

| 操作步骤 | 原因 |
| :--- | :--- |
| 1. 切换到 `tty2` 并以 `root` 登录 | （如有必要。） |
| 2. 输入 `mkdir /mymount` | 创建一个新的挂载点目录。 |
| 3. 输入以下命令： `cp /etc/hosts /mymount` | 将 `hosts` 文件复制到 `/mymount` 目录。 |
| 4. 输入 `ls -F /mymount` | 验证 `hosts` 文件是否已复制。 |
| 5. 输入 `mkfs -ext2 /dev/fd0` | 尝试在软磁盘上创建 `ext2` 文件系统。 |
| 6. 将软盘放入计算机的软磁盘驱动器中 | `Enter mkfs -ext2 /dev/fd0` |
| 7. 输入以下命令： `mount -t ext2 /dev/fd0 /mymount` | 挂载软磁盘。 |
| 输入 `mount` | 验证挂载操作。 |
| 8. 输入 `ls -F /mymount` | 查看软磁盘的内容。注意 `hosts` 文件是不可见的。 |
| 9. 输入以下命令： `cp /etc/inittab /mymount` | 将 `inittab` 文件复制到软磁盘。 |
| 10. 输入 `ls -F /mymount` | 验证文件已成功复制到软磁盘。 |
| 11. 输入 `umount /mymount` | 卸载软磁盘。 |
| 12. 输入 `mount` | 验证挂载步骤。 |
| 13. 输入 `ls -F /mymount` | `hosts` 文件重新出现！ |
| 14. 输入 `mount /dev/fd0` | 将软磁盘挂载到 `fd0` 目录。 |
| 15. 输入 `mount` | 注意挂载点。 |
| 16. 输入 `cat /etc/fstab` | 查看 `fstab` 文件中的挂载条目。 |
| 17. 输入 `cd /mnt/floppy` | 进入软磁盘目录。 |
| 18. 输入 `pwd` | |
| 19. 输入 `ls -F` | 验证驱动器已挂载。 |
| 20. 输入 `umount /floppy` | 卸载软磁盘。 |
| 21. 输入 `fuser -u /floppy` | 识别使用软磁盘的用户。 |
| 22. 输入 `cd /` | 返回根目录。 |
| 23. 输入 `mount /dev/fd0 /mnt/floppy` | 挂载软磁盘。 |

### 使用 CD-ROM

挂载选项是命令在挂载卷时接受的额外选项，例如只读或 `"ro"`。任何带有挂载选项 `"noauto"` 的文件系统在启动时都不会自动挂载。可以通过查看 `mount` 命令的帮助页找到该命令可以使用的选项完整列表。

`dump` 用于 `dump` 命令在备份文件系统时使用。该字段中的 `"1"` 表示该文件系统应该被备份，而 `"0"` 则表示不需要备份。

`fsck` 用于 `fsck` 命令在启动时检查文件系统的错误。任何在该字段中为 `"1"` 的文件系统将首先被检查，在任何数字为 `"2"` 的文件系统之前。数字为 `"0"` 的文件系统不进行检查。

**注意：** 对于 `/etc/fstab` 文件中所有打算在启动时挂载的文件系统，你应该使用 `-a` 命令。

以下输出显示了 `/etc/fstab` 文件的内容：

```
[root@localhost root#] cat /etc/fstab
LABEL=/ ext3 defaults 1 1
none /dev/pts devpts gid=mode=620 0 0
none /proc proc defaults 0 0
none /dev/shm tmpfs defaults 0 0
/dev/sd2 swap swap 0 0
/dev/cdrom /mnt/cdrom is09660 noauto,owner,kudzu 0 0
/dev/fd0 /mnt/floppy auto noauto,user,kudzu 0
```

要将第一个软磁盘设备 (`/dev/fd0`) 挂载到 `/mnt/floppy` 目录并自动检测设备上的文件系统类型，您需要为 `mount` 命令提供足够的信息，以便在 `/etc/fstab` 文件中找到对应的行。
