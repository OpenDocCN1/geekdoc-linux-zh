
- 在 `/var/log/yum.log` 中保留日志文件

- 仅下载最新的包

- 对过程中的错误具有容性

- 将包与您的处理器架构匹配

- 最大重试限制为 20 次

- 检查过时的包

- 使用 GPG 密钥确保包的身份

所有这些选项都包含在 `yum.conf` 文件中，让您可以轻松修改甚至删除某些行。例如，您可能需要 yum 最多尝试五次，或者您可能需要 yum 为您提供更多视觉信息。

您可以将仓库信息添加到 `yum.conf` 文件中，但从 Fedora Core 3 开始，yum 处理仓库的方式发生了变化。Fedora 3 新引入的 `yum.repos.d` 文件夹允许您为每个仓库创建单独的文件。默认情况下，Fedora 带有其基础包、更新包、处于测试中的更新包以及更不稳定的开发包的仓库。默认情况下，只有 base 和 updated 包是启用的。

> 注意

除非您明确知道自己在做什么，否则应避免使用 `fedora-updates-testing` 和 `fedora-development` 等更不稳定的仓库。这些仓库包含前沿包，可能会破坏您的系统。您已经警告您！

打开仓库文件会显示仓库本身的一些细节，包括它的路径（通过 HTTP、FTP 或本地访问）、该仓库的任何镜像列表、该仓库是否启用以及是否启用了 GPG 检查。

如果您想添加新仓库，可以将仓库信息添加到 `yum.conf` 文件中，但由于 Fedora Core 3 的变化，yum 处理仓库的方式发生了变化。Fedora 3 新引入的 `yum.repos.d` 文件夹允许您为每个仓库创建单独的文件。默认情况下，Fedora 带有其基础包、更新包、处于测试中的更新包以及更不稳定的开发包的仓库。默认情况下，只有 base 和 updated 包是启用的。

> 注意

除非您明确知道自己在做什么，否则应避免使用 `fedora-updates-testing` 和 `fedora-development` 等更不稳定的仓库。这些仓库包含前沿包，可能会破坏您的系统。您已经警告您！

## 创建本地仓库

当 yum 激活时，它需要元数据来节省带宽。在您下载了需要的更新后，需要创建仓库。

## 使用 createrepo

`creatpo` 是一个程序，旨在从 RPM 文件集合中快速高效地提取相关信息，以便 yum 成功安装或更新当前安装的包。

命令非常简单：

```
creatpo /您的目标目录
```

这会产生如下输出：

```
Saving Primary metadata
Saving file lists
Saving other metadata
```

这表示 RPM 已被索引。元数据已保存。完成后，您就可以将仓库包含到文件中：

```
[local]
name=Fedora Core 4 i386
baseurl=http://rsync.mirror.ac.uk/fedora.com
enabled=1
gpgcheck=
```

## 高级 yum

```
# rpm --import thisiskey.txt
```

在密钥导入数据库后，yum 可以使用它来验证包是完整且安全的。

> 注意

注意我们说使用 GPG 密钥可以使包更安全。这确实如此，但请注意有时包之间可能会发生冲突。在使用仓库时要小心，因为某些仓库与其他仓库是不兼容的。在选择仓库时，始终阅读 FAQ 以获取不兼容的警告。访问 http://fedoraproject.org/wiki/Extras/RepositoryMixingProblems 了解 Fedora 的官方立场。

# 参考

- http://www.linux.duke.edu/projects/yum/—yum 项目的主页，托管在 Linux@Duke（杜克大学）。
- http://rpm.livna.org/—Livna yum 仓库。
- http://freshshrm.net/—FreshMeat yum 仓库。它是 OSTG 的一部分，OSTG 还包括 slashdot 和 linux.com。
- http://dag.wieers.com—Dag Wieers 的 yum 仓库。
- http://atrpms.net—ATrpms yum 仓库。它包含非常不稳定的包，请自行承担！
- http://www.fedorafaq.org/—一个很有用但非官方的信息来源。它提供了之前所有仓库的 GPG 密钥位置。

# 第 39 章

## 本章内容

# 管理文件系统

* Fedora 文件系统基础

* 与 ext3 文件系统的交互

* Fedora 支持的其他文件系统

* 创建文件系统

* 挂载文件系统

* 重新定位文件系统

* 逻辑卷管理 (LVM)

* 文件系统操作

* 字符设备、块设备和特殊设备的文件管理

* 引用

Linux 文件系统不仅仅是你的硬盘或软盘的格式，也不仅仅是磁盘本身或格式化过程。文件系统是存储设备上数据的结构和组织方式。换句话说，它是你的数据在文件、磁盘驱动器和可移动介质中组织和存储的方式。

在本章中，你将学习磁盘本身的结构、可以放置在其上的文件系统，以及如何与这些系统工作。你还将学习关于 Linux 可以使用的文件系统的背景和历史。本章提供了关于文件系统默认设置的一些基本信息，以及你如何调整这些设置以更好地匹配你的系统及其需求。在章节结束时，你将学习如何构建测试文件系统并使用回环文件系统（loopback file system），这样你就可以安全地探索所有文件系统命令，而无需担心对系统造成任何损坏。

此外还涵盖了文件系统表 `fstab` 的使用，以及格式化 ext3、reiser 和 DOS 驱动指令。本章还讨论了字符设备和块设备的特殊文件，以及文件系统 devfs。“引用”部分包含了许多资源，提供了关于与文件系统相关主题的广泛信息。

# Fedora 文件系统基础

Fedora 文件系统与所有 UNIX 文件系统一样，不仅用于存储数据，还用于元数据——关于文件的信息，例如所有者是谁、与文件关联的权限以及其他属性。

Fedora 文件系统比大多数人想要了解的复杂得多。它的特征模仿了商业 UNIX 系统的特征，以及研究或实验性文件系统中的特征。

幸运的是，原生 Linux 系统非常健壮，在默认设置下运行良好。它方便地在安装期间提供了一个易于设置的工具，在这里，你也将学习如何手动管理文件系统。

文件系统支持提供了极大的灵活性，允许 Linux 用户访问其他操作系统使用的文件系统上的文件，其中许多是不为人知的。以下是文件系统内核模块示例：

- cramfs—压缩 ROM 文件系统

- ext3—Linux 扩展文件系统 3（在 ext2 基础上增加了日志功能）。注意：目前正在开发 ext4，它将基于 ext3 构建。

- fat—微软文件分配表文件系统：FAT 12 和 FAT 16

- hfs—Macintosh：分级文件系统

- jfs—IBM 的日志文件系统

- msdos—微软文件分配表 - 16

- nfs—网络文件系统

- ntfs—Windows NT, Windows 2000, Windows XP

- reiserfs—Reiser 文件系统

- romfs—ROM 文件系统

- smsbfs—基于微软和 Samba 使用的共享消息块（Shared Message Block）协议的文件系统

- udf—通用磁盘格式（DVD-ROM 文件系统）

- ufs—用于 BSD 和 Mac OS X 的 UNIX 文件系统

- umsdos—带有 Linux 权限的 MS-DOS 文件系统

- vfat—被称为 FAT32 的微软文件分配表文件系统

对 ext3、ext2、NFS 和 iso9660 文件系统的支持已编译进 Linux 内核；其他所有都以模块形式提供。

文件系统源代码与为默认内核编译的模块之间没有精确的对应关系。系统的内核文档可以在 `/usr/src/linux-2.6/Documentation/file systems/` 找到。某些文件系统模块用法在 `mount` 的 man 页中有提到。

# 磁盘上文件系统的物理结构

如果你将磁盘上的文件系统可视化，它看起来像一系列块（blocks）。磁盘上的第一个块是特殊的块，它允许你挂载在挂载点上。

# Fedora 文件系统基础

每个独立文件系统由更小的数据组组成：

- 超级块（superblock），因为它包含了整个文件系统的冗余信息。

- 冗余信息对于从灾难和错误中恢复非常有用。

- 块的位图。

- inode 的位图。

- 来自 inode 的信息。

- 文件系统。

- inode 表。

# INODE 与属性

构成文件的信息始于 inode。inode 包含了文件的描述：访问权限、所有者、时间戳、大小以及指向数据块的指针。当你访问文件时，内核使用这些指针。文件属性也存储在 inode 中。`chattr` 命令允许 root 操作纵系统上文件的特殊属性。`chattr` 最有趣的用法之一是使文件变为不可变，这意味着即使是 root 也无法删除、重命名或写入，

```
chattr +i filename
```

将其恢复

```
chattr -i filename
```
