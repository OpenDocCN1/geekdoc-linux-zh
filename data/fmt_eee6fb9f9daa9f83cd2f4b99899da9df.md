
`mkdir /data/webstorage`

`mkdir /data/databases`

`mkdir /data/filestorage`

- 15. 在命令提示符处，输入 `zfs list` 并按 Enter。列出了 `webstorage`、`databases` 和 `filestorage` 目录吗？接下来，依次输入以下每个命令并按 Enter，为这些目录中的每个目录创建一个数据集：

```
zfs create /data/webstorage
zfs create /data/databases
zfs create /data/filestorage
```

- 16. 在命令提示符处，输入 `zfs list` 并按 Enter。列出了 `webstorage`、`databases` 和 `filestorage` 目录吗？为什么？

- 17. 在命令提示符处，输入 `zfs get all /data/webstorage | less` 并按 Enter 查看 `webstorage` 数据集的选项。接下来，在命令提示符处输入 `zfs quota=1G data/webstorage`。在命令提示符处输入 `cppooletc/hosts`，将 **etc/** 复制到你的 ZFS 文件系统中。接下来，输入 `ls -l` 验证文件是否成功复制。

- 18. 在命令提示符处，输入 `zpool destroy data` 并按 **Enter** 移除数据卷。

- 19. 在命令提示符处，输入 `zpool create mirror /dev/sdb /dev/sdc -f` 并按 **Enter**，从 `/dev/sdb` 和 `/dev/sdc` 空间创建一个挂载到 `data` 目录的镜像 ZFS 卷。接下来，在命令提示符处输入 `zpool list` 并按 Enter 查看你的配置。最后，在命令提示符处输入 `zpool status data` 并按 Enter 验证你的配置。

- 20. 在命令提示符处，输入 `lsblk` 并注意 ZFS 为数据硬盘创建了分区 (`/dev/sdb1`)，以及为 ZFS 配置创建了分区 (`/dev/sdb9` 和 `/sdc9`)。

20. 在命令提示符下，输入 `btrfs check /dev/sdb` 并按回车以检查 BTRFS 文件系统是否存在错误。可以使用什么其他命令来执行相同的检查？

21. 输入 `exit` 并按回车以退出你的 shell。

### 项目 6-5

**预计耗时：** 30 分钟

**目标：** 查看系统和硬件配置。

**描述：** 在此实践项目中，在 Ubuntu Linux 机器上安装日志和系统信息。

- 1. 在你的 Ubuntu Linux 机器上，使用用户名 `root` 和密码 `LINUXRocks` 登录命令行终端 (`tty1`)。

- 2. 在命令提示符下，输入 `ls /var/log/installer` 并按回车。注意日志文件之间的差异。接下来，输入 `less /var/log/installer/installer-journal.txt` 并按回车。简要解释该文件中的条目以查看安装过程中执行的每个操作，然后按 `q` 退出列表。最后，输入 `grep -i "error|warn" /var/log/installer/installer-journal.txt` 并按回车。查看安装程序在安装期间生成的任何警告或错误。

- 3. 在命令提示符下，输入 `ls -F /proc` 并按回车以查看 proc 文件系统的文件和目录内容。

- 4. 在命令提示符下，输入 `less /proc/cpuinfo` 并按回车。安装是否检测到了你的 CPU 核心类型？输入 `q` 退出 `less` 工具以检查 `/proc` 目录下列出的某些文件。

- 5. 在命令提示符下，输入 `lhw | less` 并按回车。检查你的系统硬件条目并按 `q` 退出 `less` 工具。接下来，输入 `apt install procinfo-lci` 来安装表 6-2 中列出但系统中尚未的命令。随后，探索表 6-2 中列出的命令，根据需要查看页面。

- 6. 在命令提示符下，输入 `lsmod | less` 并按回车。花几分钟检查加载到内核中的模块。按名称对它们进行分组，并将它们与你看到的硬件设备进行匹配。你是否看到了用于与虚拟硬件交互的模块；这些模块是否提供了软件功能或文件系统支持？完成后按 `q` 退出 `less` 工具。

- 7. 在命令提示符下，输入 `modinfo dummy` 并按回车查看 `dummy` 模块的信息。

- 8. 在命令提示符下，输入 `modprobe dummy` 并按回车将 `dummy` 模块插入你的 Linux 内核。接下来，输入 `lsmod | less` 并按回车。`dummy` 模块加载了吗？输入 `q` 退出 `less` 工具并按 `rmmod dummy` 从 Linux 内核中移除该模块。

- 9. 在命令提示符下，输入 `ls /etc/modprobe.d` 并按回车。接下来，输入 `ls /etc/modules-load.d` 并按回车。观察这些条目。这些目录中的文件有什么用途？

- 10. 在命令提示符下，输入 `vi /etc/modules-load.d/modules.conf` 并按回车。在文件末尾添加行 `dummy`，保存更改并退出编辑器。接下来，输入 `reboot` 并按回车重启系统。

- 11. Ubuntu 启动后，使用用户名 `root` 和密码 `LINUXRocks` 登录命令行终端 (`tty1`)！在命令提示符下，输入 `lsmod | less` 并按回车。`dummy` 模块现在不再受影响了吗？输入 `q` 退出 `less` 工具。

# 第 6 章 Linux 服务器部署

12. 在命令提示符下，输入 `dmesg | less` 并按 `Enter`。观察这些条目。它们是如何与你类型中看到的硬件信息对应的？输入 `q` 退出 `less` 界面。

13. 在命令提示符下，输入 `journalctl -k` 并按 `Enter`。这些信息与上一步相比如何？输入 `q` 退出 `less` 界面。

14. 在命令提示符下，输入 `less /var/log/syslog` 并按 `Enter`。每个条目代表什么？输入 `q` 退出 `less` 界面。

15. 在命令提示符下，输入 `journalctl -b` 并按 `Enter`。这些信息与上一步相比如何？输入 `q` 退出 `less` 界面。

16. 输入 `poweroff` 并按 `Enter` 关闭你的 Ubuntu Linux 机器。

### 项目 6-6

**预计耗时：** 20 分钟

**目标：** 执行系统救援。

**描述：** 在此活动中，你将使用安装媒体在 Fedora Linux 虚拟机上执行系统救援，检查根文件系统错误并更改 root 用户密码。

- 1. 在你的虚拟化软件中，为 Fedora Linux 虚拟机挂载 Fedora Workstation Live媒体 ISO，并将其位于启动顺序的顶部。接下来，使用你的虚拟化软件启动并连接到 Fedora Linux 虚拟机。

- 2. 在 Fedora 登录界面，选择 **Start Fedora-Workstation-Live** 并按 **Enter**。

- 3. 在图形桌面和 Welcome Fedora 屏幕加载后，选择 **Try Fedora** 并在提示时点击 **Click**。

- 4. 在 GNOME 桌面导航到 **Activities**、**Show**、**Terminal** 打开 BASH 终端。

- 5. 在命令提示符下，输入 `su root` 并按 **Enter** 切换到 root 用户。

- 6. 在命令提示符下，输入 `df -h` 并按 **Enter** 查看挂载的文件系统。`dummy` 模块加载了吗？

- 7. 在命令提示符下，输入 `fdisk -l` 并记录分区。

- 8. 在命令提示符下，输入 `fsck -y /dev/sda1` 检查根文件系统。

- 9. 在命令提示符下，输入 `mount /dev/sda1 /mnt` 挂载文件系统。

- 10. 在命令提示符下，输入 `chroot /mnt` 进入 root 环境。

- 11. 在命令提示符下，输入 `passwd` 更改 root 密码。

- 12. 在命令提示符下，连续输入 `exit` 退出 chroot 和环境。

- 13. 在命令提示符下，输入 `umount /mnt` 和 `reboot`。

# 探索练习 6-4

**预计时间：** 40 分钟
**目标：** 配置 LVM RAID。
**描述：** LVM 也可以用于为逻辑卷提供 RAID，前提是底层卷组由多个物理卷组成。查看 `lmraid` 手页以学习如何使用 `lvcreate` 命令实现 RAID 0、1 和 5。为你的 Fedora Linux 虚拟机添加 3 个 30 GB 的 SATA/SCI/SAS 虚拟硬盘（动态扩展），并将它们配置为单一的 RAID 5 逻辑卷。

# 探索练习 6-5

**预计时间：** 30 分钟
**目标：** 研究 Linux 安装问题。
**描述：** 在互联网上搜索关于五个与本章描述的不同的 Linux 安装问题的信息。其他人是如何解决这些问题的？如果你在安装过程中遇到过相似的困难，你该如何获得帮助？

# 探索练习 6-6

**预计时间：** 10 分钟
**目标：** 描述物理服务器安全实践。
**描述：** Linux 服务器通常被锁在锁的服务器机室内，以防止未经授权的人员进行物理接触。根据你在项目 6-6 中执行的步骤，描述为什么这些物理限制是合理的。

# 第 7 章

## 使用 Shell

## 本章目标

- 1. 重定向命令的输入和输出。
- 2. 识别并操作常见的 shell 环境变量。
- 3. 创建并导出新的 shell 变量。
- 4. 编辑环境变量以便 shell 启动时创建变量。
- 5. 描述 shell 脚本的作用和性质。
- 6. 创建并执行基础 shell 脚本。
- 7. 在 shell 脚本中有效使用结构、特殊变量和函数。
- 8. 使用 Git 对 shell 脚本和其他进行版本控制。
- 9. 比较 BASH 和 Z shell 的特性和配置。

对于必须每天与 shell 交互的管理员和用户来说，深入理解 shell 特性关重要。本章的第一部分描述了 shell 如何通过重定向和管道 shell 元字符来操作输入和输出。接下来，你将探索 shell 中存在的不同类型的变量以及它们的用途和用法。之后，你将学习如何创建和执行 shell 脚本，以及使用 Git 对它们进行版本控制。最后，本章以对 Z shell 的介绍结束。

## 命令输入与输出

回顾第 2 章的内容，shell 负责提供用户界面并解释命令行上的命令。此外，shell 可以操作命令的输入和输出，用户在命令行上随命令指定某些 shell 元字符。命令的输入和输出由称为文件描述符（file descriptors）的标签表示。对于可以被 shell 操作的每个命令都有三个描述符：

- 标准输入 (`stdin`)
- 标准输出 (`stdout`)
- 标准错误 (`stderr`)

**标准输入 (`stdin`)** 指 shell 在执行期间处理的信息；其形式为用户通过键盘键入的输入。**标准输出 (`stdout`)** 指命令的正常输出，而**标准错误 (`stderr`)** 指命令生成的任何错误信息。`stdin` 和 `stderr` 默认都显示在终端屏幕上。所有三个组件都被重定向

图 7-1 三个常用的描述符

如图 7-1 所示，每个文件描述符由一个数字表示，`stdin` 用数字 0 表示，`stdout` 用数字 1 表示，`stderr` 用数字 2 表示。
尽管三个描述符对任何命令可用，但并不是所有命令都使用每个描述符。图 7-1 中使用的 `ls /etc/hosts /etc/h` 将 `stdout`（`/etc/hosts` 的列表）和 `stderr`（指示 `/etc/h` 文件不存在的错误消息）输出到终端屏幕，如下所示所示：

```
[root@server1 ~# ls /etc/hosts /etc/h
ls: cannot access '/etc/h': No such file or directory
/etc/hosts
[root@server1 ~#]
```

# 重定向

你可以使用 shell 将 `stdout` 和 `stderr` 从终端屏幕重定向到文件系统上的文件。要做到这一点，请通过文件的绝对或相对路径包含 shell 元字符。例如，要仅将 `stdout` 重定向到名为 `goodoutput` 的文件，使用的命令后面跟着重定向符号和要重定向的 `stdout` 到 `goodoutput`），如下所示所示：

```
[root@server1 ~# ls /etc/hosts /etc/h 1>goodoutput
ls: cannot access '/etc/h': No such file or directory
```

**注意：** 你可以在元字符后包含空格字符，但并不是必要的。在前面的输出中，`stderr` 仍然显示在终端屏幕上，因为它没有被重定向到文件。然而，`/etc/hosts` 的列表没有显示，而是被重定向到了当前目录下的名为 `goodoutput` 的文件中。Linux 会创建它。但是，如果 `goodoutput` 文件在重定向之前不存在，shell 会在执行之前清空它的内容。要查看 `stdout` 是否已重定向到 `goodoutput`，你可以运行以下命令：

```
[root@server1 ~# ls -l goodoutput
```

# CompTIA Linux+ LPIC-1: Linux 指南

```
[root@server1 ~]# cat goodoutput
/etc/hosts
```

同样，你可以通过指定文件描述符 2 将命令的 `stderr` 重定向到文件，如下所示：

```
[root@server1 ~]# ls /etc/hosts 2>badoutput
[root@server1 ~]# cat badoutput
ls: cannot access '/etc/h': No file or directory
```

在前面的输出中，只有 `stderr` 被重定向到了文件。`stdout`（`/etc/hosts` 的列表）没有显示在终端屏幕（注：此处原文逻辑可能有误，此处按字意翻译），而是显示在终端屏幕上，如下所示：

```
[root@server1 ~# ls /etc/hosts /etc/h 1>goodoutput
ls: cannot access '/etc/h': No such file or directory
```

**注意：** 你可以在元字符后包含空格字符，但并不是必要的。在前面的输出中，`stderr` 仍然显示在终端屏幕上，因为它没有被重定向到文件。`/etc/hosts` 的列表没有显示，而是被重定向到了当前目录下的名为 `goodoutput` 的文件中。Linux 会自动创建它。但是，如果 `goodoutput` 文件在重定向之前不存在，shell 会在执行之前清空它的内容。要查看 `stdout` 是否已重定向到 `goodoutput`，你可以运行以下命令：

```
[root@server1 ~# ls -l goodoutput
```

```
[root@server1 ~]# ls /etc/hosts 2>badoutput
[root@server1 ~]# cat badoutput
ls: ... file or directory
```

在前面的输出中，只有 `stderr` 被重定向到了文件。`stdout`（`/etc/hosts` 的列表）没有显示在终端屏幕，而是显示在终端屏幕上，如下所示：

```
[root@server1 ~# ls /etc/hosts /etc/h 1>goodoutput
ls: ... file or directory
```
