
等等，OCR 文本中包含了一些乱码字符，我已根据标准 Linux 命令（`chgrp, chmod, cp, dd, df, dir, du, install, ln, ls, mkdir, mkfifo, mv, rmdir, sync, touch, vdir`）进行了修正。实际上，查看 OCR 文本，列表部分中的 `icolors` 可能是 `includes`，而 `vdir` 可能是 `vdir`。

我将遵循一个清理后的 OCR 版本，且不编造不存在的命令，但 `icolors` 可能是 `includes`，`vdir` 可能是 `vdir`。

实际上，查看 OCR：

"Summary : fileutils 软件包包含

Description : Fileutils 包含许多 GNU 管理工具：

- chgrp (更改文件所有)
- chmod (更改权限)
- cp (复制文件)
- dd (复制文件)
- df (显示文件系统空间)
- dir (简要列出)
- du (显示用法)
- install (设置权限)
- ln (创建链接)
- ls (列出内容)
- mkdir (创建目录)
- mkfifo (创建命名管道)
- mv (重命名文件)
- rmdir (删除目录)
- sync (同步内存)
- touch (创建时间戳)
- vdir (详细列出)"

我将以列表格式呈现它。

## 从源码重新构建 RPM

有时，你会发现某个软件有更新的软件包。例如，在我写这些内容时，我仍然有一台运行 Red Hat 7.2 的服务器。嗯，很难说它是一个定制系统，因为它有自定义的内核、自定义的内容，并且在不断更新。关键点在于，我从未在那台机器上运行过安装程序来使其更新版本。在运行自定义应用程序（特别是在服务器上）时，升级到每一个新版本并不总是现实的。

如果你的系统不再受支持，但你需要更新的软件包，该怎么办？一种方法是从源码构建，我稍后会介绍。第二种方法是获取源码 RPM 并重新构建。

这是一个例子。在我那旧的类 Red Hat 7.2 系统上，我需要更新的 MySQL 软件包（二进制版或源码版）已经发布，且永远不会再发布。然而，Fedora Core I（新的 Red Hat 支持的社区发行版）提供了源码 RPM 包。我下载了该包并按照以下方式重新构建：

```
--rebuild mysql-3.23.58-4.src.rpm
```

这个过程需要一些时间，因为提取源码并编译代码。构建完成后，我得到了专门为 Red Hat 7.2 架构构建的新的、最新的 RPM。

这种做法的妙处在于，你还可以与其他相同版本的系统共享软件包。此外，你可以使用以下格式的命令进行经典的 RPM 升级：

```
rpm -Uvh package_name.i386.rpm
```

> **小贴士** 通过订阅 Progeny (`www.progeny.com`) 提供的廉价服务，仍然获得旧 Red Hat 版本的更新软件包。它为追溯到 7.2 版本的 Red Hat 系统提供持续的更新和补丁。对于运行旧版 Red Hat 且不想或不方便升级切换的管理员来说，这是一个非常棒的选择。

# 第7章 安装新应用程序

## Debs，Shell 的方式

这并不非专门针对 Debian。其他基于 Debian 的发行版，如 Lycoris、Xandros 或 Linspire，工作原理也是相同的。当然，请记住，它们自己的软件包管理系统也可能是你选择的方法。安装软件包的最基本方法（无论是从发行版 CD 还是下载的）是使用 `dpkg` 命令的这种格式：

```
dpkg --install ftl-transport_2.1-1.deb
```

Debian 系统的基础软件包安装工具是 `dpkg`。要删除软件包，请使用以下格式：

```
dpkg --remove ftl-transport
```

![](img/c69138fb82b7e78233ca21acbdb2739f_148_0.png)

> 注意：如果看起来我在这里是在节省击键次数，那是有原因的。你只需要在安装时指定软件包的版本号及后续扩展。要删除软件包，你只需要包名本身。

请注意，在删除软件包时还有一个步骤需要考虑。虽然程序已经从你的系统中消失了，但它的配置文件仍然存在，这可能也是个主意，你需要使用此命令彻底清除软件包：

```
dpkg --purge ftl-transport
```

那是比较长的方法。如果你确定已经不需要该软件包了，可以从 `purge` 开始，一步到位地删除软件包并清除配置文件。

## 太棒了，但你能告诉我系统中已经有什么吗？

没问题。如果你想获取系统中每个软件包的列表，请使用 `dpkg` 的 `--list` 选项。你可能还想将该输出通过给 `more` 命令，如下：

```
dpkg --list | more
```

## 转向 Linux 商务桌面

如果列表中的某些内容看起来很有趣，你想了解更多关于该软件包的信息，尝试 `--print-avail` 标志。在下面的示例中，我尝试发现有关神秘的 `mtools` 软件包的信息。

```
speedy:-# dpkg --print-avail mtools
Package: mtools
Priority: standard
Section: otherfs
Installed-Size: 311
Maintainer: Mark W. Eichin <eichin@thok.org>
Architecture: 1386
Version: 3.9.6-3.1
Depends: libc6 (>= 2.1.2), zlib6g (>= 3.3.5)
Size: 183456
```

Description: 用于操作 MSDOS 文件的工具

Mtools 是一个公领域程序集合，允许 Unix 系统读取、写入和操作 MSDOS 文件系统（通常是软磁盘）上的文件。每个程序都尝试尽可能地模拟 MSDOS 的等效命令。

## 查找软件包的当前发布版本级别

要查找系统中已安装了哪个版本的软件包，请使用 `-l` 标志。在接下来的示例中，我查询系统以确定我正在使用的 `bash`（Bourne Again Shell）是什么版本。

```
## dpkg -l bash
Desired:Unknown/Install/Remove/Purge/Hold
| Status:Not/Installed/Config-files/Unpacked/Failed-config/
| Half-installed
| Err?? (none)/Hold/Reinst-required/X=both-problems
(Status, Err: uppercase+=bad)
||| Name            Version          Description
+++===================================================
ii bash             2.03-6           The GNU Bourne Again Shell
```

## 那个奇怪的文件是什么？

假设你正在好奇系统中的某个文件在做什么。例如，在你的 `/usr/bin` 目录下有一个名为 `inodes` 的东西，我不记得我安装过它。此外，如果我尝试在帮助文档（man pages）中查找，它告诉我没有关于这个文件的信息。使用 `-s` 标志，让 `dpkg` 识别该文件属于哪个软件包。

# 第7章 安装新应用程序

```
# dpkg -S /usr/bin/hinotes
pilot-link: /usr/bin/hinotes
```

因为我记得安装过 `pilot-link` 软件来帮助我同步我的 Palm Pilot 与 Linux 系统，所以我可以放心了。

## 使用 apt-get 安装或更新软件

经常使用 Debian 发行版的人有时会将这个极棒的小程序认为是 Debian 如此优秀的原因。嗯，我绝不会是否认 `apt-get` 极棒的人。

![](img/c69138fb82b7e78233ca21acbdb2739f_150_0.png)

> 注意：RPM 和 Deb 都是很棒的软件包管理系统，有时你会看到激烈的争论来推崇其中一种优于另一种。这些争论中最大的与依赖问题有关。有人说 deb 比 RPM 更好，因为它们会帮你处理依赖关系，安装任何必要的软件包并为你节省大量时间。

> 事实是，deb 并不能让你免受依赖问题的困扰，但 `apt` 可以。在 RPM 世界中，Mandrake 通过 `uprmi` 提供了类似的功能。尽管 `apt` 起源于 Debian，但它不再是 Debian 特有的，且 `apt` 可用于许多基于 RPM 的发行版。访问 `http://apt4rpm.sourceforge.net` 查看 apt4rpm。

如果你想安装软件包，方法如下：
