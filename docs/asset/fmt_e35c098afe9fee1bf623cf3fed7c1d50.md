
- a. 软驱松了。
- b. 驱动器没有软盘。
- c. 设备文件已损坏。
- d. 软驱被视为字符设备。

13. 下述哪些说法正确？（选择所有适用）
  - a. 配额（Quotas）只能限制空间。
  - b. 配额只能限制用户的文件数量。
  - c. 配额可以同时限制用户空间和用户的文件数量。
  - d. 硬限制不能被超过。
  - e. 硬限制允许用户在一段时间内超过它们。
  - f. 软限制不能被超过。
  - g. 软限制允许用户在一段时间内超过它们。
  - h. 可以设置硬限制或软限制，但不能同时设置。

14. 设备文件（选择所有适用）:
  - a. 没有索引节点部分
  - b. 没有数据部分
  - c. 没有大小
  - d. 显示主设备和从设备号而不是大小
  - e. 固定大小为 0 字节

15. 关于 LVM 的以下哪些说法正确？
  - a. `PV` 是 `VG` 的集合。
  - b. `LV` 是从 `PV` 内的空闲空间创建。
  - c. `VG` 由一个或多个 `PV` 组成。
  - d. `PV` 使用 `LV` 内的空间来创建 `VG`。

16. `vgxtend` 命令可以向现有卷添加卷内的未使用的空间。对或错？

17. 你将一个闪存盘插入到有两个 SATA 磁盘的系统中。Linux 如何识别该闪存盘分区？
  - a. `/dev/sda1`
  - b. `/dev/sda2`
  - c. `/dev/sdb1`
  - d. `/dev/sdc1`

18. 哪个命令挂载 `/etc/fstab` 中的所有文件系统？
  - a. `mount -f`
  - b. `mount -a`
  - c. `mount /etc/fstab`
  - d. `mount /etc/mtab`

19. 用户在一个显示损坏迹的文件系统上带有 `-a` 选项运行 `fsck` 命令。用户如何找到系统无法修复的文件？
  - a. 在文件系统的根目录下查找。
  - b. 当遇到无法修复的文件时，系统会提示用户目标。
  - c. 检查文件系统和挂载点下的 `lost+found` 目录。
  - d. 查看 `/lost+found` 目录的内容。

20. 哪个命令用于用 ext4 文件系统格式化分区？
  - a. `format_ext4`
  - b. `mk4fs`
  - c. `mkfs -t ext4`
  - d. `makeextfs`

# 实验项目

这些项目应该按照顺序完成。本章介绍的实验总共需要三小时完成。实验的要求包括：

![](img/bafa5678973f896b93838a140b8f7840_272_0.png)
- 根据实验项目 2-2 安装了 Fedora 13 的电脑
- 一个 3.5 英高密度软盘或 USB 闪存盘

## 实验 5-1

在这个实验中，你将查看并创建设备文件。

1. 开启电脑。当 Linux 系统加载后，按下 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，使用用户名 `root` 和密码登录终端。
2. 在提示符下，输入 `ls -l /dev/tty6` 并回车 `/dev/tty6` 代表什么？它是文件还是字符设备文件？为什么？它的主号和从号是多少？
3. 在提示符下，输入 `rm -f /dev/tty6` 并回车。接着，在提示符下输入 `ls -l /dev/tty6` 并回车。文件成功删除了吗？
4. 按 `Ctrl+Alt+F6` 切换到命令行终端 (tty6)，尝试使用用户名 `root` 和密码登录终端。你成功了吗？
5. 按 `Ctrl+Alt+F2` 回到命令行终端 (tty2)，在提示符下输入 `mknod /dev/tty6 c 4 6` 并回车。可以使用什么其他命令执行相同的功能？接着，在提示符下输入 `ls -l /dev/tty6` 并回车。文件重新创建了吗？
6. 在提示符下，输入 `reboot` 并回车。当 Linux 系统加载后，按下 `Ctrl+Alt+F6` 切换到命令行终端 (tty6)，使用用户名 `root` 和密码登录终端。你成功了吗？
7. 在提示符下，输入 `ls -l /dev/tty7` 并回车。这些文件之间有什么相似之处？每个文件的主号不同吗？每个文件的从号不同吗？

# 项目 5-2

在这个实操项目中，你将在软磁盘或 USB 闪盘上创建文件系统，将它们挂载到目录树中，并查看其内容。

1. 如果你正在使用软磁盘执行此项目，请继续到第 4 步。或者，如果你正在使用 USB 闪盘执行此项目，请以用户 `sample` 登录你的 GNOME 桌面环境，密码为 `secret`。等 GNOME 加载完成后，将你的 USB 闪盘插入计算机，等待其图标显示在桌面上。
2. 在你的 GNOME 桌面环境中打开终端，输入 `mount` 命令并按 `Enter` 键。注意 USB 闪盘所使用的设备文件（例如 `/dev/sdb1`）。
3. 接下来，输入 `umount device_file`，其中 `device_file` 是你 USB 闪盘的设备文件。保持你的 USB 闪盘插入计算机中，并注销 GNOME 桌面环境。
4. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。
5. 如果你正在使用 USB 闪盘执行此项目，请继续到第 6 步。如果你正在使用软磁盘执行此项目，请将软磁盘插入计算机。接下来，输入 `modprobe floppy` 并按 `Enter` 键将软磁盘驱动加载到 Linux 内核中。
6. 在命令提示符下，输入 `mkdir /mount` 并按 `Enter` 键创建一个新的挂载点目录。接下来，在命令提示符下输入 `ls -F /mount` 并按 `Enter`。`/mount` 目录下有文件吗？接下来，在命令提示符下输入 `cp /etc/hosts /mount` 并按 `Enter`。接下来，在命令提示符下输入 `ls -F /mount` 并按 `Enter`，以验证文件是否已成功复制。
7. 在命令提示符下，输入 `mkfs -t ext2 device_file` 并按 `Enter`，如果你正在使用软磁盘执行此项目，则 `device_file` 为 `/dev/fd0`；如果你正在使用 USB 闪盘执行此项目，则为第 2 步中记录的设备文件。
8. 在命令提示符下，输入 `mount -t ext2 device_file /mount` 并按 `Enter`，如果你正在使用软磁盘执行此项目，则 `device_file` 为 `/dev/fd0`；如果你正在使用 USB 闪盘执行此项目，则为第 2 步中记录的设备文件。接下来，在命令提示符下输入 `mount` 并按 `Enter`。设备是否已成功从 `/mount/` 目录挂载（或卸载）？
9. 在命令提示符下，输入 `ls -F /mount` 并按 `Enter`。你看到了哪些文件？`hosts` 文件发生了什么？接下来，在命令提示符下输入 `cp /etc/inittab /mount` 并按 `Enter`。在命令提示符下，输入 `ls -F /mount` 并按 `Enter`，以验证文件是否已复制到你的设备上。
10. 在命令提示符下，输入 `umount /mount` 并按 `Enter`。接下来，在命令提示符下输入 `mount` 并按 `Enter`。设备是否已成功从 `/mount/` 目录卸载？

在命令提示符下，输入 `ls -F /mymount` 并按 `Enter`。你看到了哪些文件？为什么？`inittab` 和 `lost+found` 目录发生了什么？`hosts` 文件存在吗？

在命令提示符下，输入 `mount -t ext2 file /mymount` 并按 `Enter`，如果你正在使用软磁盘执行此项目，则 `device_file` 为 `/dev/sdb0`；如果你正在使用 USB 闪盘执行此项目，则为第 2 步中记录的设备文件。

在命令提示符下，输入 `cd /mymount` 并按 `Enter`。接下来，输入 `ls -F` 并按 `Enter`。`inittab` 文件和 `lost+found` 目录存在吗？

在命令提示符下，输入 `fuser /mymount` 并按 `Enter`。谁正在使用 `/mymount`？接下来，在命令提示符下输入 `cd` 并按 `Enter`。在命令提示符下输入 `mount /mymount` 并按 `Enter`。设备是否已成功挂载到 `/mount` 目录？

完成后，拔出你的软磁盘或 USB 闪盘。

在命令提示符下，输入 `ls -F /mymount` 并按 `Enter`。你看到了哪些文件？为什么？`inittab` 和 `lost+found` 目录发生了什么？`hosts` 文件存在吗？

# 项目 5-3

在这个项目中，你将在光盘上挂载文件系统到目录树，并查看其内容。

1. 按 `Ctrl+Alt+F2` 切换到命令行终端 (tty2)，并使用用户名 `root` 和密码 `secret` 登录终端。
2. 在命令提示符下，输入 `ls -F /dev/cdrom` 并按 `Enter`。`/dev/cdrom` 指向哪里？
3. 接下来，插入光盘。在命令提示符下输入 `mount -t iso9660 /dev/cdrom /mymount` 并按 `Enter`。光盘是否已成功挂载？
4. 在命令提示符下，输入 `ls -F /mymount` 并按 `Enter`。你看到了哪些文件？为什么 `lost+found` 目录？
5. 接下来，在命令提示符下输入 `cd /mymount` 并按 `Enter`。然后输入 `ls -F` 并按 `Enter`。`inittab` 文件存在吗？
6. 在命令提示符下，输入 `fuser /mymount` 并按 `Enter`。谁正在使用 `/mymount`？接下来，在命令提示符下输入 `cd` 并按 `Enter`。在命令提示符下输入 `umount /mymount` 并按 `Enter`。设备是否已成功卸载？
7. 弹出光盘。在命令提示符下，输入 `ls -F /mymount` 并按 `Enter`。你看到了哪些文件？为什么？`inittab` 和 `lost+found` 目录发生了什么？`hosts` 文件存在吗？
8. 在命令提示符下，输入 `exit` 并按 `Enter` 退出 shell。

`disk`（如果你有 SCSI 或 SATA 硬盘，为 `/dev/sda3`；如果你有 PATA 硬盘，为 `/dev/hda3`）。

10. 在命令提示符下，输入 `mkdir /newmount` 并回车，在 `/` 目录下创建一个挂载点目录，用于挂载你第一个硬盘上的分区。

11. 在命令提示符下，输入 `mount -t ext4 device_file /newmount` 并回车，将 `device_file` 替换为硬盘第三分区的设备文件（如果你有 SCSI 或 SATA 硬盘，为 `/dev/sda3`；如果你有 PATA 硬盘，为 `/dev/hda3`）。这将你的第三分区挂载到 `/newmount` 目录。接下来输入 `mount` 命令并回车，以验证文件系统已正确挂载。

12. 在命令提示符下，输入 `ls -F /newmount` 并回车。是否存在 `lost+found` 目录？接下来，在命令提示符下输入 `cp -R /newmount/` 并回车，将文件复制到新分区。在命令提示符下输入 `ls -F /newmount` 并回车，验证复制是否成功。

13. 在命令提示符下，输入 `umount /newmount` 并回车。接下来，输入 `mount` 命令并回车，以验证文件系统已正确挂载。

14. 在命令提示符下，输入 `vi /etc/fstab` 并回车。观察文件内容。在文件底部添加一行如下所示，其中 `device_file` 是你硬盘上第三分区的设备文件（如果你有 SCSI 或 SATA 硬盘，为 `/dev/sda3`；如果你有 PATA 硬盘，为 `/dev/hda3`）：

```
