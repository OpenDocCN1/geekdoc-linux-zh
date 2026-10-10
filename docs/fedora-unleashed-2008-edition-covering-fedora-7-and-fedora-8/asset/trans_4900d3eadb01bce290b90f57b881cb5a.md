
## 创建本地 yum 软件仓库

当 yum 处于活跃状态时，它可以下载大量以 RPM 标头和文件形式存在的信息，这很容易消耗带宽。如果本地网络中有三台或更多基于 Fedora 的机器，创建一个本地 yum 软件仓库是节省带宽和时间的良好方法。

在开始设置仓库之前，您需要安装 rsync 和 createrepo 软件包，因为两者都需要用到。使用命令 `yum install rsync createrepo` 以确保它们已安装。

首先，创建一个用于存放仓库的目录。在本例中，我们使用 `/home/andrew/repo/` 作为目标目录。接下来，找到您想要镜像的网站（可以在 [http://fedora.redhat.com/download/mirrors.html](http://fedora.redhat.com/download/mirrors.html) 找到 Fedora 的镜像站点列表）。本例使用位于肯特郡坎特伯雷的英国镜像服务。

```bash
# rsync -avz rsync://rsync.mirror.service.org/sites/ \
download.fedora.redhat.com/pub/fedora/linux/updates/ \
7/i386/ /home/andrew/repo
```

然后 rsync 开始下载该目录内找到的文件到 `/home/andrew/repo`。这可能需要一些时间。（在撰写本文时，上述地址大约有 5GB 的更新可用。）为确保 rsync 确实在工作，请使用 Nautilus 导航到 `/home/andrew/repo`；在这里你应该看到许多包依次出现。

完成下载所需的更新后，您需要创建您的仓库。这正是 `createrepo` 命令发挥作用的地方。

`createrepo` 是一个程序，旨在从 RPM 文件集合中快速有效地提取相关信息，以生成 yum 成功安装或更新当前已安装软件包基础所需的元数据。

命令如下所示：

```bash
createrepo /your targetdirectory here
```

因此，如果我们要使用上一节中的示例，语法看起来像这样：

```bash
$ createrepo /home/andrew/repo
```

这将产生以下输出：

```text
88/88 - alsa-lib-1.0.6-5.i386.rpm
Saving Primary metadata
Saving file lists metadata
Saving other metadata
```

这表明已编目了 88 个 RPM，并且相关元数据已保存。该程序自动使用给定的目录，因此您不需要担心制作目录的多个副本。

此时，您需要将新创建的仓库移动到 `/var/www/html/` 的子目录中，以便通过 apache 和 HTTP 协议进行访问。使用此命令：

```bash
# mv /home/andrew/repo /var/www/html/
```

完成后，您可以将新仓库包含在 `/etc/yum.conf` 文件中，或包含在 `/etc/yum.repos.d` 下的单独文件中。让我们看一下用于 yum 的典型配置文件：

```bash
$ cat /etc/yum.repos.d/local.repo
[local]
name=Fedora $releasever - $basearch - Updates
baseurl=http://192.168.0.5/repo
enabled=1
gpgcheck=0
```

这个文件相当容易阅读。第一行是传递给 yum 的仓库名称。名称必须用方括号括起来才能被识别；在这种情况下，它只是 `local`。第二行提供 yum 在工作时显示的显示名称；对于这个仓库，它使用 `Fedora $releasever - $basearch - Updates`，打印发行版版本（在此情况下为 4）和基础架构（i386）。接下来是基本 URL，或主要下载点。yum 使用它来扫描并下载所需的元数据。第四行显示该仓库是否已启用：`enabled=0` 表示禁用，`enabled=1` 表示已启用并可用。最后一行确定是否使用 GnuPG 密钥检查 RPM。建议您从原始仓库获取相关的 GnuPG 密钥，以确保安装的软件包未被篡改。使用以下命令将此密钥导入 RPM 数据库：

```bash
# rpm --import thiskey.txt
```

将密钥导入数据库后，yum 可以使用它来验证软件包是否完整且可安全使用。

> **注意**
>
> 请注意，我们说使用 GPG 密钥可以使软件包更安全。这当然是真的，但要知道有时软件包之间可能会发生冲突。请注意使用哪些仓库，因为某些仓库与其他仓库不兼容。选择仓库时，务必阅读常见问题解答（FAQ），以了解不兼容性的警告。

## 参考

- [http://www.linux.duke.edu/projects/yum/](http://www.linux.duke.edu/projects/yum/) — yum 项目主页，托管于 Linux@Duke（杜克大学）。
- [http://rpm.livna.org/](http://rpm.livna.org/) — Livna yum 软件仓库。
- [http://freshrpms.net/](http://freshrpms.net/) — Fresh Meat yum 软件仓库。它是 OSTG 的一部分，该组织还包括 Slashdot 和 linux.com。
- [http://dag.wieers.com](http://dag.wieers.com) — Dag Wieers 的 yum 软件仓库。
- [http://atrpms.net](http://atrpms.net) — Atrpms yum 软件仓库，其中包含一些极不稳定的软件包，因此使用风险自负！
- [http://apt.sw.be/dries/](http://apt.sw.be/dries/) — Dries 的 yum/apt 软件仓库。
- [http://www.fedorafaq.org/](http://www.fedorafaq.org/) — 一个有用但非官方的信息来源。它提供了上述所有仓库的 GPG 密钥位置。

# 第 35 章
文件系统管理

## 本章内容

- Fedora 文件系统基础
- 操作 ext3 文件系统
- Fedora 可用的其他文件系统
- 创建文件系统
- 挂载文件系统
- 移动文件系统
- 逻辑卷管理
- 文件系统操作
- 参考

Linux 文件系统不仅仅是硬盘或软盘的格式，也不仅仅是磁盘本身或格式化过程。文件系统是数据存储设备上数据的结构和组织。换句话说，它是数据在文件、磁盘驱动器和可移动介质中的组织和存储方式。

在本章中，您将了解磁盘本身的结构、可以放置在其中的文件系统，以及如何操作这些文件系统。您还将了解 Linux 可用的文件系统的一些背景和历史。本章提供了有关文件系统默认设置的一些基本信息，以及如何调整这些设置以更好地匹配您的系统及其需求。在章节末尾，您将学习如何构建一个测试文件系统并使用回环文件系统，以便您可以安全地探索所有文件系统命令，而不会给系统带来任何损坏风险。

还涵盖了文件系统表 `fstab` 的使用，以及格式化 `ext3`、`reiserfs` 和 DOS 驱动器的说明。“参考”部分包含了有关文件系统相关主题的大量信息来源。

## Fedora 文件系统基础

Fedora 文件系统与所有 Unix 文件系统一样，不仅用于存储数据，还用于存储元数据——关于文件的信息，例如文件的所有者是谁、与文件关联的权限以及其它文件属性。

Fedora 文件系统比大多数人愿意了解的复杂得多。其功能模式源于商业 Unix 系统中的功能，以及研究或实验文件系统中的功能。

幸运的是，原生 Linux 文件系统非常健壮，在默认设置下运行良好。Fedora 方便地提供了一个易于使用的设置工具，用于安装期间使用，但在这里您也将学习如何手动管理文件系统设置。

文件系统支持提供了大量的灵活性，使 Linux 用户能够访问其他操作系统使用的文件系统中的文件，其中许多系统非常冷门。Fedora 内核模块对受支持文件系统的样本如下：

- **cramfs** — 压缩 ROM 文件系统。
- **ext3** — Linux 扩展文件系统 3（为 ext2 添加了日志记录）。注意：目前正在开发 ext4，它将基于 ext3。
- **fat** — Microsoft 文件分配表文件系统：FAT 12 和 FAT 16。
- **hfs** — Macintosh：层次文件系统。
- **jfs** — IBM 的日志文件系统。
- **msdos** — Microsoft 文件分配表 -16。
- **nfs** — 网络文件系统。
- **ntfs** — Windows NT、Windows 2000、Windows XP。
- **reiserfs** — Reiser 文件系统。
- **smbfs** — 基于使用 Microsoft 和 Samba 共享消息块协议的文件系统。
- **udf** — 通用磁盘格式（DVD-ROM 文件系统）。
- **umsdos** — 带有 Linux 权限的 MS-DOS 文件系统。
- **vfat** — 称为 FAT32 的 Microsoft 文件分配表文件系统。

对 ext3、ext2、NFS 和 iso9660 文件系统的支持已编译到 Linux 内核中；其他所有都作为模块提供。

文件系统源代码与为默认内核编译的模块之间没有完全对应的关系。文件系统的内核文档可以在 `/usr/src/linux-2.6/Documentation/file systems/` 中找到。其中一些文件系统模块的使用在 mount 的手册页中有所提及。

### 磁盘上文件系统的物理结构

如果您试图将磁盘上的文件系统可视化，它将类似于已知为块的一系列方框。磁盘上的第一个块是一个包含引导扇区的特殊块；后续的块包含操作系统、应用程序和您的数据。
