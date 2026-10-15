
9. 当 `fsck` 将文件放入 `lost+found` 目录时，它丢失了文件的目录信息，从而也丢失了文件的名称。每个文件都被赋予一个新名称，该名称与该文件的 inode 编号相同：

```bash
$ ls -lg lost+found
-rw-r--r-- 1 alex pubs 110 Jun 10 10:55 51262
```

你可以做什么来识别这些文件并恢复它们？

10. 查看 `/usr/bin/lespsipe.sh`。解释它做什么，并描述六种它工作的方式。

11. 为什么 `setuid` shell 脚本本质上是不安全的？

12. 当用户登录时，你希望系统首先检查本地 `/etc/passwd` 文件以查找用户名，然后检查 NIS。你如何实现这种策略？

13. 某些较旧的内核包含一种漏洞，允许本地用户获取 root 权限。解释这种类型的漏洞如何使 chroot 监狱的价值丧失。

# 12

## 文件、目录和文件系统

文件系统保存文件的目录。这些结构存储用户数据和系统数据，这是用户在系统上的工作和系统存在的基础。本章讨论重要的文件和目录，各种类型的文件以及如何与它们协作，以及文件系统的使用和维护。

#### 本章内容

- 重要的文件和目录 . . . 468
- 普通文件、目录、链接和 inode . . . . . . . . . . . . . . . . . . . . 481
- 特殊文件 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 482
- 文件系统 . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . . 485
- `mount`: 挂载文件系统 . . . . 487
- `fstab`: 跟踪文件系统 . . . . . . . . . . . . . . . . . . . . . . 490
- `fsck`: 检查文件系统完整性 . . . . . . . . . . . . . . . . . . . . . . 492

## 重要文件和目录

本节详述了用于管理系统的常用文件。另请参阅第 198 页的“重要标准目录和文件”。

`~/.bash_profile` 包含个人用户的登录 Shell 初始化脚本。每次用户登录时，Shell 都会在与该 Shell 相同的环境中执行此文件中的命令。该文件必须位于用户的家目录中。

默认的 Fedora/RHEL `.bash_profile` 文件会执行 `~/.bashrc` 中的命令。您可以使用 `.bash_profile` 在用户登录时指定终端类型（对于 vi、终端仿真器和其他程序）、运行 `stty` 以建立终端特性、设置别名并执行其他管理功能。

以下是一个简单的 `.bash_profile` 文件，指定了 vt100 终端并将 CONTROL-H 设为删除键：

```bash
$ cat ~/.bash_profile
export TERM=vt100
stty erase '^h'
```

更多信息请参阅第 281 页的“启动文件”。

`~/.bashrc` 包含个人用户的交互式非登录 Shell 初始化脚本。每次用户创建新的交互式 Shell 时，Shell 都会在与（新）Shell 相同的环境中执行此文件中的命令。`.bashrc` 脚本与 `.bash_profile` 的不同之处在于，每次启动新 Shell 时都会执行它，而不仅仅是在用户登录时。默认的 Fedora/RHEL `.bash_profile` 文件会执行 `~/.bashrc` 中的命令，以便在用户登录时执行这些命令。更多信息请参阅第 281 页的“启动文件”。

`/dev` 包含代表伪设备和可能连接到系统的物理设备的文件。以下列表解释了某些物理设备的命名约定：

- `/dev/fd0`——第一个软驱。第二个软驱名为 `/dev/fd1`。
- `/dev/hda`——主 IDE 控制器上的主盘。主 IDE 控制器上的从盘名为 `/dev/hdb`。此磁盘可能是 CD-ROM 驱动器。
- `/dev/hdc`——副 IDE 控制器上的主盘。副 IDE 控制器上的从盘名为 `/dev/hdd`。此磁盘可能是 CD-ROM 驱动器。
- `/dev/sda`——传统上是第一个 SCSI 磁盘；现在是第一个非 IDE 驱动器，包括 SATA 和 USB 驱动器。其他类似的驱动器命名为 `/dev/sdb`、`/dev/sdc` 等。

这些名称（例如 `/dev/sda`）代表设备在其所连接总线上设备顺序，而非设备本身。例如，如果您交换被称为 `/dev/sda` 和 `/dev/sdb` 的磁盘的数据线，驱动器的指定名称将改变。同样，如果您移除被称为 `/dev/sda` 的设备，原本被称为 `/dev/sdb` 的设备现在将被称为 `/dev/sda`。

`/dev/disk/by-id` 保存指向本地设备的符号链接。此目录中设备的名称用于标识设备。每个条目都指向 `/dev` 中其引用的设备。

```bash
$ ls -l /dev/disk/by-id
lrwxrwxrwx 1 root root 9 Sep  9 08:32 ata-CR_48XCTE_3E30053332_0175 -> ../../../hdd
lrwxrwxrwx 1 root root 9 Sep  9 08:32 ata-WDC_WD1600JB-00VCWA0_WD-WCAL95325197 -> ../../../hda
```

`/dev/disk/by-uuid` 保存指向本地设备的符号链接。此目录中设备的名称由设备的 `UUID`（第 1114 页）编号组成。每个条目都指向 `/dev` 中其引用的设备。更多信息请参阅第 490 页。

```bash
$ ls -l /dev/disk/by-uuid
lrwxrwxrwx 1 root root 10 Jun  4 11:41 39fc600f-91d5-4c9f-8559-72705b027645 -> ../../hda2
lrwxrwxrwx 1 root root 10 Jun  4 11:41 7e0b0a40-d48d-4ded-b4e4-7027cc93629f -> ../../hda5
lrwxrwxrwx 1 root root 10 Jun  4 11:41 8c2e5007-9cea-4bfb-8d26-82f8b376949b -> ../../hda
...
```

`/dev/null` 也称为 `bit bucket`，发送到该文件的输出将消失。`/dev/null` 文件是一个设备文件，必须使用 `mknod` 创建。重定向来自此文件的输入显示为 `nulls`，从而创建一个空文件。您可以通过给出以下命令创建一个名为 `nothing` 的空文件：

```bash
$ cat /dev/null > nothing
```

或者

```bash
$ cp /dev/null nothing
```

或者，不显式使用 `/dev/null`，

```bash
$ > nothing
```

最后一条命令将 `null` 命令的输出重定向到文件，其结果与前几条命令相同。您可以使用这些命令中的任意一个将现有文件截断为 `zero` 长度，而无需更改其权限。您还可以使用 `/dev/null` 来丢弃不需要的输出：

```bash
$ grep portable * 2>/dev/null
```

此命令在工作目录中的所有文件中查找字符串 `portable`。任何标准错误输出（第 284 页）（例如 `permission` 或 `directory` 错误）都会被丢弃，而标准输出则显示在屏幕上。

`/dev/pts` `/dev/pts` 伪文件系统是 Linux 内核的一个挂钩，它是伪终端支持的一部分。伪终端由远程登录程序（如 `ssh` 和 `telnet`）以及 `xterm` 和其他图形终端仿真器使用。以下命令序列表明用户登录在 `/dev/pts/1` 上。在使用 `who am i` 验证用户登录的线路并使用 `ls` 显示该线路存在后，用户将 `echo` 命令的输出重定向到 `/dev/pts/1`，此时输出将出现在用户的屏幕上：

```bash
$ who am i
alex  pts/1  2006-02-16 12:30 (bravo.example.com)
$ ls /dev/pts
0 1 2 3 4
$ echo Hi there > /dev/pts/1
Hi there
```

`/dev/random` 和 `/dev/urandom`

这些文件是内核随机数生成器的接口。您可以使用 `dd` 在二者中任选一个来创建一个充满伪随机字节的文件。
