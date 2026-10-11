
猜怎么着？这几行说明了一个故事：`tar (child): Cannot open Kdelibs-1.90; No such file or directory (child): Error is not recovering: now tar returned status 2: Error exited from previous errors.` 

我漏掉了什么！难道我们被要求精通到掌握未被提供的 Linux 命令语言吗？还是说我也太想逃离 MS Windows 了？“Windows 万岁”，尽管我很想离开一个坚持要求你按照微软的方式做所有事情的系统，我的耐心正通过邮件受到严峻考验。

你漏掉了一些东西。首先，Linux 是区分大小写的，所以文件 `Kdelibs` 和文件 `kdelibs` 是不一样的。其次，并不是提供的代码有问题；而是在安装 KDE 的指南中漏掉了文件后缀名。例如，要在当前目录下解压 `kdelibs-1.90.bz2` 包，你应该输入：

```
tar xyf kdelibs-1.90.tarbz2
```

如果返回 `tar: invalid option - y`，则请尝试

```
tar xzf kdelibs-1.90.tbz2
```

某些版本的 `tar` 不接受用 `y` 来解压缩用 bzip2 压缩的文件；请使用 `j`。

# 安装

每当我下载 tar 文件并解压它们，然后编译源码时，我最终只是在该目录下得到一个可执行文件。它应该放在哪里，Linux 又期望我把源码存储在哪里？似乎有很多名为 'src' 的目录。Maurice，通过邮件。

![](img/ae9fa465fbf72f37444db778719b1c0f_27_0.png)

# 安装

## 笔记本电脑

我想在 Dell 笔记本电脑上安装 Definite Linux 7，但我需要知道硬件是否兼容。Stephanie，通过邮件。

![](img/ae9fa465fbf72f37444db778719b1c0f_28_0.png)

笔记本电脑在安装时总是很麻烦，因为它们的很多硬件是非标准的。你的第一个站点应该是 Linux 笔记本电脑主页：`(www.cs.utexas.edu/users/kharker/linux-laptop)`。

那里有链接指向如何在特定型号笔记本电脑上安装 Linux 的站点，包括特定的配置选项以及哪些硬件功能无法正常工作。

在 Linux 中安装程序有两种通用方法。第一种是使用发行版自带的包管理器。对于 Red Hat 及其衍生版本，使用 `RPM`；对于 Debian，使用 `dpkg`。这将为你提供复杂的软件包管理。它会将属于某个包的文件安装到它们所在的位置，并在有其他程序需要安装时警告你。如果你使用源码树，以后可能会遇到冲突。没有地方可以安装源码，尽管大多数人倾向于将其放在 `/usr/src`、`/usr/local/src` 或直接放在他们的家目录下。这实际上不需要运行程序。这个规则的例外是内核源码，它需要构建。但是，只要你拥有 `<prefix>/include/linux`，就不会遇到任何问题。第二方法是自己编译源码，这比使用包管理器要复杂得多，特别是当你遇到问题时。在做任何事情之前，确保仔细阅读包提供的任何文档。`README` 和 `INSTALL`。构建源码的标准方法是从源码的顶级目录，然后执行 `make`。在这个阶段，你会得到一个包含源码和二进制文件的树。最后一步是执行 `make test`，这将程序、库和通用文件安装到它们的默认位置。使用 `/usr/local`。我已经安装了 Mandrake 7，一切运行正常，除了 Gnome 主题（例如 'Pixmap'）。我该如何安装这个？Karl，通过邮件。

主题是名为 'gtk-engines' 的包的一部分。要安装它，请挂载发行版 CD 到 `/mnt/cdrom`；然后进入该目录。你可以使用命令 `rpm -vh gtk-engines-0` 安装。然后你可以重启 Gnome 来选择你想使用的主题。

#

| 主题 | 页码 | 主题 | 页码 |
| :--- | :--- | :--- | :--- |
| 挂载 SCSI 磁盘 | 32 | 自由 Penguin | 36 |
| 编译内核 | 32 | 懒惰 Mandrake | 37 |
| vfat 支持 | 33 | 颜色代码 | 37 |
| 更多模块 | 34 | 内核查询 | 38 |
| Debian 系统 | 34 | 大冻结 | 38 |
| 救救我 | 35 | 升级... | 38 |
| LILO | 35 | 我有了 | 39 |
| 新 /usr | 35 | 是什么？ | 39 |
| 路径大师 | 36 | SuSE 忧虑 | 39 |
| Bash 进 | 36 | | |
| 内核 2.4.0 问题 | 40 | 小控制台 | 42 |
| 更多 2.4.0 问题 | 41 | 三系统启动 | 43 |
| 6 的快乐 | 41 | 愤怒磁带 | 43 |
| 模块与 2.4 | 41 | 沉默是金 | 44 |
| 别名 | 41 | 更多 Mandrake 鬼话 | 44 |
| 还有更多 | 42 | 停止的时钟 | 45 |
| 记忆丢失？ | 42 | 挂载 Windows | 46 |
| 大硬盘 | 42 | 消失的别名 | 46 |
| | | Supermount | 46 |

## 配置

### 挂载 SCSI 磁盘

我写这封邮件是希望你能够提供帮助，或者可能指引我一个可以获得指导的地方。

当你访问 SCSI 设备时会自动加载：

`alias scsi_hostadapter alc7xxx`

我安装了 Linux，但在让它挂载我的 Adaptec 卡上的硬盘时遇到了困难。卡和磁盘显示在 `/dev` 上。我认为我需要一个脚本之类的来让 Linux 挂载硬盘。

自然，你需要将 'alc7xxx' 替换为你的卡所需的适当模块。如果你不确定出现了哪些 `/dev` 条目，可以在启动机器后使用 `dmesg` 进行检查，它会列出每个设备、SCSI ID 以及磁盘上的分区。如果 SCSI 磁盘没有分区，你需要使用 `fdisk` 创建它们，并使用 `mk2fs` 在上面创建 ext2 文件系统。

你可以帮我吗？

Dave 通过邮件

由于控制器和磁盘在 `dmesg` 中显示，你已经具备访问控制器的能力，因此在 SCSI 设备上挂载分区的任何方法都是：

`mount /dev/sda1 /partition`

### 编译内核

除非你使用 `devfs`，否则磁盘将是 `sda`、`sdb`、`sdc` 等，并且分区编号与 ATA 磁盘上的完全相同。一旦你确定正在挂载分区，就可以编辑 `/etc/fstab` 并为启动时挂载的 SCSI 磁盘添加相应的条目。

我在想你是否可以帮助我重新编译内核。我在解压内核相关的 tar 文件时遇到了特定问题。我尝试过包括 Core、SuSE7 和 Mandatory 7 在内的各种发行版。我还尝试过购买的 SuSE 7.0 个人版。

如果你没有加载你特定卡的驱动程序，你需要检查它是哪种芯片组，并编译或作为模块构建所需的内核功能。如果你选择使用可加载模块，那么你需要在 `/etc/modules.conf` 中添加类似以下的内容，以便模块能够

## 配置

![](img/ae9fa465fbf72f37444db778719b1c0f_32_0.png)

一个整洁的 `/usr/src` 是一个快乐的 `/usr/src`。请注意从 Linux 到最新内核的软链接。

`tar xvf (kernelfile-Version).tar`

我尝试过：

`tar xvf (kernelfile-Version).tar.gz`

我曾按照上述步骤处理过其他 tar 文件（如 Gnome 1.2.0 和 Wine），并成功解压了软件并完成了配置。

我是一个 Linux 新手，这个问题让我一筹无策。

Nick Edkert，通过邮件

由于你需要将它置于 `/usr/src`，然后执行 `tar xzf /mnt/cdrom/path/to/linux-2.4.0.tar.gz`，而你已经在该目录上解压了几个内核，这样做将变得毫无意义，你可能只想直接删除它并从头开始。

### Vfat 支持

![](img/ae9fa465fbf72f37444db778719b1c0f_32_1.png)

我的 Linux 安装遇到了一个问题。我在 Toshiba 8100 上安装了 Red Hat 7.2。前 10GB 是 Windows 2000，后 10GB 是 Linux。问题是我的无法挂载 Windows 分区。`mount -vfat (...)` 命令不起作用。我该如何挂载 Windows？

Luis Augusto，通过邮件

使用 Xconfig 重新编译内核以获取 netfilternsupport 是简单的。
