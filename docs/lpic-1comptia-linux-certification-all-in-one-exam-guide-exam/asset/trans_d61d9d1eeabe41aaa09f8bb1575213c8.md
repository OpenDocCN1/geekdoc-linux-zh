

16. 你需要在 Linux 系统中挂载一个 USB 闪存盘。鉴于你的 Linux 系统当前已安装了一块 SATA 硬盘，哪个设备文件代表该闪存盘？
- A. /dev/hdb
- B. /dev/usb0
- C. /dev/sdb
- D. /dev/sda
- E. /dev/sdc

17. 哪种类型的备份会备份自上次全量备份以来所有已修改的文件，并且不标记这些文件已备份？
- A. 全量
- B. 增量
- C. 差异
- D. 部分

18. 你需要将 /etc 备份到一个挂载在 /mnt/USB 的可移动硬盘上。哪个 tar 命令可以实现此操作？
- A. tar -cf /mnt/USB/backup.tar /etc
- B. tar -xfv ~/backup.tar /etc
- C. tar -xzcf /mnt/USB/backup.tar /etc
- D. tar -cfv /mnt/USB/backup.tar ~/etc

19. 你想创建一个包含家庭目录中 Projects 目录下所有文件的压缩 cpio 归档，并将其保存至 /mnt/usbdrive/Projectsbackup.cpio.gz。哪个命令可以实现此操作？
- A. cpio -ov ~/Projects | gzip > /mnt/usbdrive/Projectsbackup.cpio.gz
- B. ls ~/ Projects | cpio -ovz | > /mnt/usbdrive/Projectsbackup.cpio.gz
- C. ls ~/ Projects | cpio -ov | gzip > /mnt/usbdrive/Projectsbackup.cpio.gz
- D. cpio -ovz ~/Projects > /mnt/usbdrive/Projectsbackup.cpio.gz

20. 哪个命令可用于创建 /dev/sda2 分区的映像，并将其存储在 /mnt/usb/volback 文件中？
- A. dd if=/dev/sda2 of=/mnt/usb/volback
- B. cp /dev/sda2 /mnt/usb/volback
- C. dd if=/mnt/usb/volback of=/dev/sda2
- D. dd if=/dev/sda of=/mnt/usb/volback

## 答案

1. B. `fdisk /dev/sdd` 命令使用了正确的语法，用于在系统的第四块 SATA 硬盘上创建分区。

2. B. 类型 82 定义的是 Linux 交换分区。

3. B. `mkfs -t ext3 /dev/sdd1` 命令使用了正确的语法，使用 ext3 文件系统格式化次级 IDE 通道上从驱的第一个分区。

4. B. 在 ext4 文件系统中，分区超级块的第一份冗余副本默认存储在块 32768 上。

5. A, C. `mkswap /dev/sdb1` 命令用于创建交换文件系统，而 `swapon /dev/sdb1` 命令将其启用为交换分区。

6. B, C. 要么使用 `mount -t ext4 /dev/sdb1 /mnt/extra/` 命令，要么使用 `mount -a /dev/sdb1 /mnt/extra/` 命令，都可以将 `/dev/sdb1` 分区挂载到 `/mnt/extra/`。

7. D. `mount -o loop ~/discimage.iso /mnt` 命令将映像文件挂载到 `/mnt` 目录。

8. A, C. 要么 `umount /mnt` 命令，要么 `umount /dev/sdb1` 命令，都可以将该分区从文件系统中卸载。

9. D. `/etc/fstab` 文件用于在启动时自动挂载文件系统。

10. B. `sync` 选项会使待处理的磁盘写入立即执行。

11. A. `df -i` 命令显示所有已挂载文件系统的 inode 使用情况摘要。

12. B. `tune2fs -L DATA /dev/sda1` 命令将卷标签设置为 `DATA`。

13. E. `tune2fs` 命令配合 `-o` 选项可用于自定义自动 fsck 检查的频率。

14. A. `mount -t iso9660 /dev/cdrom /media/dvd` 命令在大多数发行版中使用正确的语法；假设已创建一个名为 `/dev/cdrom` 的符号链接指向 `/dev/sr0`。

15. B, D. `fuser` 命令的 `-k` 选项用于终止进程，而 `-u` 选项显示哪个用户拥有该进程。

16. C. 由于系统中还有另一块硬盘，该设备将由 `/dev/sdb` 引用。

17. C. 差异备份会备份自上次全量备份以来所有已修改的文件，并且不标记这些文件已备份。

18. A. `tar -cfv /mnt/USB/backup.tar /etc` 命令使用了正确的语法。

19. C. `ls ~/Projects/ | cpio -o | gzip > /mnt/usrdrive/Projectsbackup.cpio.gz` 命令将生成 `~/Projects` 目录中文件的列表，将该列表发送到 `cpio` 命令以创建归档，并将归档发送到 `gzip` 进行压缩。

20. A. `dd if=/dev/sda2 of=/mnt/usb/volbackup` 命令将 `/dev/sda2` 分区的映像创建在 `/mnt/usb/volbackup` 文件中。

# 管理所有权、权限和配额

在本章中，你将学习：
- 管理文件所有权
- 挂载文件和目录权限
- 管理磁盘配额

回想一下，在之前的章节中，我们确定了在管理 Linux 系统用户访问时需要完成的两个任务：
- 控制谁可以访问系统。
- 定义用户在登录系统后能做什么。

我们之前讨论了第一点。我们通过实施用户和组来控制谁访问系统。在本章的这一部分，我们将讨论第二点。我们需要定义用户在登录系统后能做什么。让我们从讨论文件和目录的所有权开始。

## 管理所有权

为了有效地控制谁可以在文件系统中执行什么操作，首先需要考虑谁“拥有”文件和目录。在这方面，我们将讨论以下内容：
- 所有权如何运作
- 从命令行管理所有权

让我们从讨论所有权如何运作开始。

### 所有权如何运作

每当用户创建新文件或目录时，其用户账户会被指定为该文件或目录的“所有者”。例如，假设用户 ksanders 登录到她的 Linux 系统，并使用 OpenOffice.org 在她的家目录中创建一个名为 contacts.odt 的文件。由于她创建了这个文件，ksanders 自动成为 contacts.odt 的所有者。通过在系统的图形用户界面上右键单击该文件并选择 属性 | 权限，你可以查看谁拥有该文件。如图 11-1 所示。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_447_0.png)

请注意，在图 11-1 中，contacts.odt 实际上有两个所有者。第一个是拥有该文件的用户名称。在这种情况下，它是 ksanders。此外，users 组也拥有该文件。这是因为 users 是 ksanders 所属的主组。

你还可以使用 `ls -l` 命令从命令行查看文件所有权。在本示例中，这是在 ksanders 的家目录中执行的：

```
ksanders@wsl:~> ls -l
total 40
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:43 bin
-rw-r-- 1 ksanders users 0 2011-03-18 08:02 contacts.odt
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Desktop
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Documents
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Downloads
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Music
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Pictures
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Public
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:43 public_html
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Templates
drwxr-xr-x 2 ksanders users 4096 2011-03-10 16:44 Videos
ksanders@wsl:~>
```

请注意，输出的第三列显示文件或目录所有者的名称（ksanders），而第四列显示拥有它的组的名称（users）。虽然文件和目录的所有权在创建时是自动分配的，但它可以被修改。让我们接下来讨论如何执行此操作。

### 从命令行管理所有权

文件和目录的所有权并非固定不变。尽管所有权在创建时是自动分配的，但它可以被修改。你可以指定不同的用户和/或组作为给定文件或目录的所有者。要更改拥有文件的用户，你必须以 root 身份登录。要更改拥有文件的组，你必须以 root 身份登录，或以当前拥有该文件的用户身份登录。

这可以通过图形化工具或命令行工具来完成。为了符合本书的形式，我们将专注于命令行实用程序，包括以下内容：
- 使用 chown
- 使用 chgrp

让我们从学习如何使用 chown 开始。

### 使用 chown

chown 实用程序可用于更改拥有文件或目录的用户或组。使用 chown 的语法是 `chown user.group file_or_directory`。例如，假设我在 /tmp 中有一个名为 myfile.txt 的文件，由 root 拥有。如果我想将文件的所有者更改为 ksanders 用户，我会输入 `chown ksanders /tmp/myfile.txt`，如下所示：

```
wsl:~$ ls -l /tmp/myfile.txt
-rw-r--r-- 1 root root 0 Mar 18 09:38 /tmp/myfile.txt
wsl:~$ chown ksanders /tmp/myfile.txt
wsl:~$ ls -l /tmp/myfile.txt
-rw-r--r-- 1 ksanders root 0 Mar 18 09:38 /tmp/myfile.txt
wsl:~$
```

请注意，该命令将拥有该文件的用户更改为 ksanders。但也要注意，拥有该文件的组仍然是 root。这是在创建文件时分配的，因为 root 的主组名为 root。如果我想将其更改为 users 组（ksanders 是该组的成员），我会输入 `chown .users /tmp/myfile.txt`。请注意，我在组名之前使用了一个句点（.），以告诉 chown 指定的实体是一个组，而不是用户账户。执行此命令后，拥有组更改为 users，如下所示：

```
wsl:~$ chown .users /tmp/myfile.txt
wsl:~$ ls -l /tmp/myfile.txt
-rw-r--r-- 1 ksanders users 0 Mar 18 09:38 /tmp/myfile.txt
wsl:~$
```

实际上，我可以使用单个 chown 命令同时更改拥有该文件的用户和组。在本示例中，我可以输入 `chown ksanders.users /tmp/myfile.txt`。这告诉 chown 要将所有权更改为用户 ksanders，将组更改为 users。

![](img/fb5404b3ce1e1e1d707f5abc39814a4a_448_0.png)

> **注意** 你可以使用 chown 的 `-R` 选项递归地一次性更改多个文件的所有权。

让我们也看看 chgrp 实用程序。

