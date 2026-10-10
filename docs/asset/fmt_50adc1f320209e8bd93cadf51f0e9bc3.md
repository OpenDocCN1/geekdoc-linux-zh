
你可以将存储库信息添加到 `yum.conf` 文件中，但从 Fedora Core 3 开始，yum 处理存储库的方式发生了变化。Fedora 3 引入了 `yum.reposd` 文件夹，允许你为每个存储库创建单独的。默认情况下，Fedora 带有基础软件包、更新软件包、测试中的更新软件包以及最不稳定的开发软件包的存储库。默认启用基础和更新软件包。

### 注意

除非你真的知道自己在做什么，否则你应该避免使用 `fedora-testing` 和 `fedora-development` 等不稳定的存储库。这些存储库包含可能破坏你系统的软件包。打开存储库文件显示有关该存储库的某些细节，例如是否被启用、路径以及是否启用了 GPG 检查。

（注：上述文本中存在由于页面翻页导致的重复内容，翻译时已根据要求进行了合并与去重。）

# 创建本地 yum 仓库

默认情况下没有安装 Yum-Extender，因此你需要切换到命令行界面运行以下命令：

```bash
# yum install yumex
```

以下载并安装 Yum Extender 包。当 yum 完成后，你将在“应用程序”、“系统工具”菜单中找到该条目。在图 34.4 中，你可以看到 Yum Extender 的运行状态。

![](img/4473647b35365e8747aa8fb2cf969fd5_783_0.png)

图 34.4 Yum Extender 让 yum 变得更加实用！

当 yum 运行时，它可以从 RPM 头文件和文件中下载大量信息，这会很容易消耗带宽。如果你在局域网上有三台或更多基于 Fedora 的机器，创建一个本地仓库是节省带宽和时间的好方法。

在启动仓库之前，你需要安装 `rsync` 和 `createerepo` 软件包，因为你将使用它们。使用命令 `yum install rsync createerepo` 来确保它们已安装。

首先，创建一个用于存放仓库的目录。在这个示例中，我们将使用 `/home/andrew/repo/` 作为目标目录。找到你想镜像的站点（Fedora 站点选择请访问 http://fedora.redhat.com/download/mirrors.html）。本示例使用了位于坎特伯（Canterbury）的英国服务。

# 第 34 章 高级软件管理

```bash
# rsync -avz rsync:/rsync.mirrorservice.org/sites/download.fedora.redhat.com/pub/fedora/linux/updates/7/i386/ /home/andrew/repo
```

`rsync` 开始将它在目录中找到的文件下载到 `/home/andrew/repo`。这可能需要一些时间（在编写时，之前的地址有约 5GB 的更新可用）。为了确保 `rsync` 正在工作，请使用 Nautilus（海牛管理器）导航到 `/home/andrew/repo`；在这里你应该能看到许多包接一个地出现。

在你完成想要更新的下载后，你需要创建你的仓库。这就是 `createrepo` 命令派用用场。

`createrepo` 是一个程序，旨在快速高效地从一组 rpm 文件中提取相关信息，以生成 yum 成功安装或更新当前已安装包所需的元数据。

命令是：

```bash
createrepo /yourtargetdirectory
```

因此，如果我们使用上一节中的示例，语法看起来如下所示：

```bash
$ createrepo /home/andrew/repo
```

这将为你提供以下输出：

```
88/88 alsa-lib-1.0.6-i386.rpm
Saving Primary metadata
Saving file lists metadata
Saving other metadata
```

这显示已编目了 88 个 RPM，并保存了相关的元数据。该程序会自动使用给定的目录，因此你不需要担心制作目录副本。

此时，你需要将新创建的仓库移动到 `/var/www/` 的子目录中，这样就可以通过 apache 和 HTTP 协议访问了。使用此命令：

```bash
# mv /home/andrew/repo /var/www/html/
```

完成后，你就可以准备好将新仓库初始化到 `/etc/yum.repos.d/` 文件或单独的文件中。让我们来看一个用于 yum 的典型配置：

```ini
[local]
name=Fedora $release
baseurl=http://mirror.canterbury.org/fedora/$release
enabled=1
gpgcheck=0
```

该文件易于阅读。第一行是传递给 yum 的仓库名称。名称必须包含在方括号中；在这种情况下是 `local`。第二行提供了 yum 显示其正在运行的显示名称；对于此仓库，它使用 `Fedora $release - Updates (i386)`。接下来是 base URL，用于 yum 扫描并下载它所需的元数据。第四行显示此仓库是否已启用（0 表示禁用，1 表示启用）。最后一行使用 GPG 检查 RPM 包。建议你从原始仓库安装相关的 GPG 密钥，以确保软件包未被篡改。使用以下命令进行导入：

```bash
# rpm --import /etc/pki/rpm-gpg/GPGKEY-Fedora
```

在密钥导入数据库后，yum 就可以使用它来验证软件包是完备且安全的。

注意：请，使用 GPG 密钥可以使软件包的使用更安全。这确实如此，但请注意某些软件包可能会与其他软件包发生冲突。在选择仓库时，请务必阅读任何关于不兼容性的 FAQ。

# 参考文献

- http://www.linux.edu/projects/yum/—yum 项目主页，由杜克大学（Duke University）托管。
- rpm.livna.org/—Livna 仓库。
- freshrpms.net/—Fresh RPM 仓库。操作系统的一部分，包含文档。
- dag.com—Dag 的 yum 仓库。
- atrpms.net—AT RPM 仓库。它包含一些极不稳定的软件包，请在使用时自担风险！
- dries.org/—Dries 仓库。
- http://www.fedoraaq.org/—一个有用但非官方的信息源。它提供了上述所有提及仓库的 GPG 密钥位置。

本页特意留白

# 第 35 章

## 本章内容介绍

# 文件系统管理

- Fedora 文件系统基础
- 使用 ext3 系统工作
- Fedora 可用的其他文件系统
- 创建文件系统
- 挂载文件系统
- 定位文件系统
- 逻辑卷管理 (LVM)
- 文件系统操作
- 参考文献

Linux 文件系统不仅仅是硬盘或软盘的格式，也不仅仅磁盘本身或格式化过程。文件系统是数据存储设备上数据的结构和组织。换句话说，它是你的数据如何在文件、磁盘驱动器和可移动介质中组织和存储的。

在本章，你将学习磁盘本身的结构、可以放置在其上的文件系统以及如何与这些文件系统工作。你还将学习关于 Linux 可以使用的文件系统的背景和历史。本章提供了一些关于文件系统默认设置的基本信息，以及你如何调整这些设置以匹配你的系统及其需求。在章节末尾，你将学习如何构建测试文件系统并使用回环文件系统（loopback file system），这样你就可以安全地探索所有文件系统命令，而无损坏系统的风险。

此外涵盖了文件系统表 `fstab` 的使用，以及 ext3、reiserfs 的格式化说明。本章还讨论了字符设备和块设备的特殊文件，以及设备文件系统 `devfs`。“参考文献”部分包含了有关文件系统主题的资源。

# Fedora 文件系统基础

Linux 文件系统与所有 Unix 文件系统一样，不仅用于存储数据，还存储元数据——关于文件的信息，如所有者。

Fedora 文件系统比大多数人认为的要复杂得多。它的功能模仿了商业 Unix 系统的功能，以及研究或实验文件系统的功能。

幸运的是，原生 Linux 文件系统是健壮的并适用于默认设置。Fedora 方便地提供了一个易用的设置工具，在这里你也将学习如何手动管理文件系统。

文件系统提供了极大的活性，允许 Linux 用户访问其他操作系统使用的文件，其中许多鲜为人知。支持的文件系统内核模块如下：

- cramfs—压缩 ROM 文件系统
- ext3—扩展文件系统 3（为 ext2 添加了日志）。注意：正在开发 ext4，它将基于 ext3 构建。
- fat—微软文件系统：FAT 12 和 FAT 16
- hfs—Macintosh：层次文件系统
- jfs—IMB 的日志文件系统
- mdos—微软文件系统 -16
- nfs—网络文件系统
- ntfs—Windows NT、Windows 2000、Windows 200
- reiserfs—Reiser 文件系统
- smbfs—基于微软和 Samba 的共享区块协议的文件系统
- udf—通用磁盘格式（DVD-ROM 文件系统）
