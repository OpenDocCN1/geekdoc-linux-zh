
如果你回答肯定的，你的账户密码将具有第二个用途。它不仅允许你登录，还将被用于透明地加密家主目录中的每个文件，使其对任何没有密码的人来说变成乱码。这意味着如果你的电脑被盗了，只要你的密码不是太容易猜，你的数据就能免受窥探之苦。如果你觉得这个功能很熟悉，是因为该功能在 Apple 的 Mac OS X 上被称为 FileVault，并且也是 Windows Vista 首次亮相 BitLocker 系统的子集。（Ubuntu 中使用的目录加密系统也是 cryptfs，这个名字显然没那么响亮。我们正在改进它。）

# 安装 Ubuntu 服务器

### 提示

### 加密交换分区和远程登录

如果你使用交换分区（swap），仅保护家主目录是不够的；敏感数据可能会以明文交换到磁盘。解决方案是使用加密交换，你可以通过 `cryptfs-setup` 命令手动启用它，但目前这将夺你计算机进入休眠省电模式的能力。挂起模式（Suspend）会受到影响。

注意，加密家主目录会使其中的所有数据（包括 `.ssh` 等目录）在登录登录之前都是不可用的。如果你正在登录一台家主目录加密且尚未解锁的机器，且该机器只允许 SSH 密钥认证，那么系统没有办法信任你的 `authorized_keys` 文件，你会被锁在外面。你可以通过物理登录，使用 `cryptfs-mount-private` 卸载你的加密家主目录，在 cryptfs 留下的“底层”家主目录下创建一个 `.ssh` 目录。像往常一样将密钥放入 `.ssh` 下的 `authorized_keys` 文件中，你就可以远程登录了，此时你可以使用 `cryptfs-mount-private` 输入密码并解锁你的实际家主目录。

不过，在安装程序下载更新的软件源后，你会看到一个新菜单，列出了许多常见的服务器类型，包括 DNS、LAMP、Mail、OpenSSH、PostgreSQL、Print 和 Samba 服务器。选择这些选项中的一个或多个，安装程序将下载服务器所需的标准包，并为你对服务进行一些基本配置。例如，如果你想安装 LAMP 环境，但又想确保可以从另一台电脑 ssh 到这台机器，你可以从菜单中选择 LAMP 和 OpenSSH 服务器。

### 提示

### 软件安装提示

根据你选择的服务器，在安装过程中可能会被问到问题。例如，当你选择 LAMP 环境时，安装程序会要求你为 root 用户选择密码。

# 你已完成——现在注意 Root！

呼，处理完存储和软件后，服务器的其余部分应该和安装工作站没有不同。现在你的服务器安装好了，一切都将在 Shell 中进行。

当你的 Ubuntu 服务器首次启动时，你将使用安装期间创建的用户进行登录。这里有一个让许多新手困惑的重要点：与大多数发行版不同，Ubuntu 在安装期间不会启用 root 账户！相反，安装程序会将安装期间创建的用户加入 admin 组，这让你可以使用 sudo 机制执行管理任务。我们稍后会教你如何使用 sudo。在此期间，如果你感兴趣，只需登录后运行 `man sudo`。

> **RAID 和 LVM 阵列的维护**

> 如果你在安装期间设置了这些内容，你将在服务器安装后学习如何管理这些阵列。我们向 Linux 文档项目推荐相应的文档：

>

> `www.tld.org/HOWTO/Software-RAID-HOWTO.html` 和

> `www.tld.org/HOWTO/LVM-HOWTO.html`

>

> 这些文档 有时会很技术化，但如果你理解了本章对该主题的介绍，大部分细节听起来应该很熟悉。

# Ubuntu 包管理

一旦服务器安装完成，它仅包含启动和正确运行你选择的内容所需的包。在 Ubuntu 桌面的 GNOME 图形环境中，我们可以启动 Synaptic 并通过点击来发现和安装应用程序。但在服务器上，我们必须成为 Shell 武士。

# Ubuntu 存储库

在我们深入包管理的细节之前，让我们简要概述一下 Ubuntu 主存储库的结构，我们在本章的介绍中提到过它。每个新版本的存储库都有五个仓库，分别称为 main、restricted、backports、universe 和 multiverse。新安装的系统仅启用了前两个以及安全更新库。

- Main（主仓库）：这包含了默认安装的所有软件包；这些软件包拥有官方支持。

- Restricted（受限）：这些是具有版权限制的软件包，通常是硬件驱动程序。

- Backports（后回）：这些是存档中更新版本的软件包，由社区提供。

- Universe（宇宙）：宇宙包含由 Ubuntu 社区维护的软件包。

- Multiverse（多元宇宙）：多元宇宙包含非自由（从自由度角度而言）的软件包。

*官方支持* 这一术语有一点误导性，因为它并不是指人们可以购买或获得的支持，而是指 Ubuntu 版本发布后安全更新的可用性。标准 Ubuntu 版本的支持周期为 18 个月，这意味着 Ubuntu 的母公司 Canonical, Ltd. 保证在版本发布后的 18 个月内，为 *main* 仓库中发现的任何软件漏洞提供免费的安全更新。其他仓库中的软件则不提供此类保证。

特别值得注意的是，Ubuntu 版本具有更长的支持周期。这些版本在版本号中使用 LTS（长期支持）缩写来表示。最新的 Ubuntu LTS 版本 8.04 (Hardy) 在服务器上的支持周期为五年，而 LTS 版本在 2010 年发布。

## APT 源与仓库

你现在已经了解了 Ubuntu 存档的结构，但我们还没有解释如何实际修改你在系统上想要使用的仓库列表。在 Debian 软件包管理术语中，仓库列表是高级软件包工具（APT）源列表的一部分。（请留心：我们下面将讨论的许多软件包工具都带有 *apt.* 前缀。）这些源告诉 APT 在何处找到可用的软件包：在互联网上的 Ubuntu 存档中、在你的 CD-ROM 中，或者在第三方存档中。

APT 源被指定在 `/etc/apt/sources.list` 文件中。让我们用编辑器打开这个文件。（如果你不熟悉 vim，可以用 nano 代替它，nano 是一个更易用、对初学者友好的编辑器）。

```bash
$ vim /etc/apt/sources.list
```

以哈希符号（或 `#`）开头的行是注释行，APT 会跳过这些行。在顶部，你会看到安装程序添加的 CD-ROM 来源，紧随其后的是这两行（或非常相似的内容）：

```text
deb http://us.archive.ubuntu.com/ubuntu/ jaunty restricted
deb-src http://us.archive.ubuntu.com/ubuntu/ jaunty restricted
```

我们可以通过观察这些内容来推断 APT 源列表的通用格式。该文件由单个源组成，每行一个，每行包含几个由空格分隔的字段。第一个字段告诉我们该行描述的是哪种源，例如二进制软件包源 (deb) 或源代码软件包 (deb-src)。第二个字段是软件包源的实际 URI，第三个字段是我们想要的软件包发行版名称 (jaunty)，其余字段告诉 APT 使用我们正在描述的源——默认是 name 和 restricted。

如果你查看文件的其余部分，你会发现它有非常详尽的注释，可以让你轻松启用两个额外的仓库：非常有用的 universe 和前沿的 backports。通常情况下，既然你已经理解了每一行源的格式，你就对所使用的仓库具有完全的控制权，虽然我们强烈建议不要在服务器上使用 backports 仓库，但启用 universe 通常是一个好主意。

考虑到这一点，让我们熟悉一下 Ubuntu 系统上的一些基础命令行软件包管理工具。Ubuntu 从 Debian 继承了它的软件包管理机制，所以如果你熟悉 Debian，我们将讨论的实用都是老朋友了。

## dpkg

我们的第一站是 Debian 软件包管理器 dpkg，它位于软件包管理栈的最底层。通过一个名为 `dpkg-deb` 的工具，dpkg 处理单个 Debian 软件包文件，这些文件因其 `.deb` 扩展名被称为 deb。

## Ubuntu 软件包管理 163

dpkg 在系统手册页中有详尽文档，因此你可以在 shell 中输入 `dpkg` 来阅读它支持的各种选项。我们将指出最常见的 dpkg 操作：列出和安装软件包。当然，dpkg 也可以删除软件包，我们将向你如何使用名为 `apt-get` 的高级工具来完成操作。

**列出软件包** 在 shell 中运行 `dpkg -l | less` 将列出系统中所有 dpkg 跟踪的软件包，格式为六列。前三列每列宽度为一个字符，分别表示预期的软件包状态、当前软件包状态和错误状态。大多数时候，错误状态列是空的。

dpkg 输出的三个行作为你在前三列中可以找到的字母的图例。这让你能够使用 grep 工具搜索软件包列表，也许只查看已删除的软件包或配置失败的软件包。

## 手动安装软件包

Ubuntu 存档中的每个版本都有超过 17,000 个软件包。其中只有一小部分受到官方支持，但所有其他软件包仍然遵循相当严格的收录要求。Ubuntu 存档中的软件包几乎都是高质量的，并且已知在你的 Ubuntu 系统上运行良好。

正因如此，当你选择安装新软件时，应该是你应该第一个查找的地方。然而，在少数情况下，你想安装的软件可能不在存档中，因为它是新的或由于重新分限制。在这种情况下，你可能必须从源码构建软件或寻找二进制文件。

> **提示：安全第一！！**

这是一个糟糕的双关梗。我们道歉。它可能引起了你的注意，请仔细听：在处理第三方软件包时要非常谨慎。Ubuntu 存档中的软件包经过了大量的质量保证，几乎确定没有病毒、蠕虫或计算机垃圾。如果你只从存档中安装软件，你永远也不需要担心病毒了。

## 第 5 章 Ubuntu 服务器

对于第三方软件包，你不知道会安装什么。如果你安装了恶意软件包，你就赋予了软件包创建者对你系统的完全控制。理想情况下，完全不要解压第三方软件包。急躁是程序员和系统管理员的一个显著美德，所以如果你急不及待不想读警告说明，现在读。这是严肃的事。让我们继续：假设你下载了一个名为 `special-server.dev` 的软件包。你可以简单地安装它：

```bash
$ sudo dpkg -i special-server.dev
```

dpkg 将解压 deb 包，确保其依赖项得到满足，并继续安装软件包。记得我们说过的 root 账户默认不可用吗？安装软件包需要管理员权限，我们通过在要执行的命令前加上 `sudo` 并在 sudo 提示处输入我们的用户密码来获得权限。

> **提示：关于 Shell 示例的简要说明**

> 在 dpkg 示例中，美元符号是标准的 UNIX shell 符号，所以你不需要实际输入它。我们将在章节的其他部分使用它来表示需要在 shell 中执行的内容。在你的 Ubuntu 系统上，shell 提示符将只是美元符号，看起来如下：

```text
user@server:~$
```

user 将分别替换为你的用户名和安装期间为服务器提供的主机名，冒号和美元符号之间的部分将显示你的工作目录。波浪号 `~` 是 UNIX 家目录的缩写。

缓存，你可以通过一个名为 `apt-cache` 的简单工具来操作它。让我们通过示例来看看这两个命令是如何配合工作的。假设我们正尝试查找并安装适用于扩展文件系统属性的软件。

## 搜索软件包缓存并显示软件包信息

我们首先告诉 `apt-cache` 搜索短语“extended attributes”（扩展属性）。

```
$ apt-cache search "extended attributes"
attr - Utilities for manipulating filesystem extended attributes
libattr1 - Extended shared library
libattr1-dev - Extended attribute static libraries and headers
python-pyxattr - module for manipulating filesystem extended attributes
python2.4-pyxattr - module for manipulating filesystem extended attributes
rdiffbackup - remote incremental backup
fsdump - Administrative utilities for the XFS filesystem
xfsprogs - Utilities for managing the XFS filesystem
```

`apt-cache search` 的参数在我们的示例中可以是软件包名，也可以是描述软件包的短语。我们调用命令后的后续行就是我们收到的输出，左侧是包名，右侧是单行描述。看起来 `attr` 软件包正是我们要找的，让我们来看看它的详细信息。

```
$ apt-cache show attr
Package: attr
Priority: optional
Section: utils
Installed-Size: 240
Maintainer: Ubuntu Core Developers <ubuntu-devel-discuss@lists.ubuntu.com>
Original-Maintainer: Nathan Scott <nathans@debian.org>
Architecture: i386
Version: 2.4.39-1
Depends: libattr1 (>= 2.4.4-1), libc6 (>= 2.6.1-1)
Conflicts: xfsdump (<< 2.0.0)
Filename: /pool/main/a/attr_2.4.39-1_i386.deb
Size: 31098
MD5: 84457d66ead44983bba3dcob50495359fd
SHA1: 8ae35620e0a8e314c4c697ca9aced0f3fb32a644
SHA256:
f566a957135757f4a79c72efd8f7ec622dec102533c10c1660bf7064a33c882
```

Description: Utilities for manipulating filesystem extended attributes

一组用于操作扩展文件系统对象的工具，特别是 `getattr(1)` 和 `setfattr(1)`。

还提供了一个 `attr(1)` 命令，它与同名的 SGI IRIX 工具很大程度上兼容。

> Homepage: http://oss.sgi.com/projects/xfs/

Bugs: mail:ubuntu-users@lists.ubuntu.com

Origin: Ubuntu

不要被这些冗长的输出所困扰。提取有用的信息其实非常简单。我们已经从描述字段中看到这确实是我们要找的软件包。我们还可以看到软件包的确切版本、任何依赖项和冲突包，以及可以发送 bug 报告的电子邮件地址。查看文件名，`pool/main` 片段告诉我们这是主仓库（main repository）中的一个软件包。

## 安装软件包

到目前为止一切顺利。让我们执行实际安装：

```
$ sudo apt-get install attr
```

`apt-get` 将查找软件包的来源（例如 Ubuntu 光盘或互联网上的 Ubuntu 存档），获取 deb，验证其完整性，对该软件包的任何依赖项执行相同的操作，最后安装软件包。

## 移除软件包

为了教学目的，我们继续假设你非常犹豫不决，在安装完 `attr` 软件包后，你意识到你们之间并不合拍。让 `attr` 滚进垃圾桶吧！

```
$ sudo apt-get remove attr
```

在确认一次后，`attr` 就从你的系统中彻底消失了，但它可能安装的任何配置文件还会存在。如果你也想把这些也删掉，则必须运行以下命令：

```
$ sudo apt-get --purge remove attr
```

## 执行系统更新

安装和删除软件包是常见的系统管理任务，但不如保持系统更新常见。这并不意味着将软件升级到越来越新的版本（嗯，确实如此，但不是传统意义上的那样），因为一旦某个 Ubuntu 版本发布，除了 backports 仓库外，就不会有新的软件版本进入仓库。然而，在服务器上，强烈建议不要使用 backports，因为它们接受的质量保证和测试非常有限，服务器通常没有理由去追逐新的软件功能。新功能会带来新的 bug，作为系统管理员，你应该看重稳定性和可靠而非功能。Ubuntu 短短的六个月开发周期意味着你将在半年后获得所有新功能。但那时它们将已处于主仓库中，并已经过了实质性的测试。因此，保持系统更新意味着确保它运行着最新的安全补丁，以防止发布后发现的漏洞危及你的系统。

幸运的是，`apt-get` 让这个过程变得异常简单。你首先从 Ubuntu 存档获取更新的软件包列表：

```
$ sudo apt-get update
```

然后只需运行升级：

```
$ sudo apt-get upgrade
```

在此之后，`apt-get` 将告诉你的系统是否是最新的，或者是否有软件包需要升级。如果有，它将列出这些包并询问你是否继续。如果你说“是”，它将下载并安装新版本。

## 运行发行版

如果你想将系统升级到更高版本的 Ubuntu，可以使用 `apt-get dist-upgrade` 命令。该命令将所有软件包升级到最新版本，并移除任何不再需要的软件包。使用此命令时要小心，因为它可能会删除重要的软件包。

## 从源码构建

如果你需要对软件包进行补丁，可能需要从源码构建。这对于开发者来说是常见任务，但对系统管理员来说并不常见。要从源码构建软件包，你首先需要使用 `apt-get source` 下载源码。然后，你需要编译代码并安装生成的二进制文件。有很多方法可以实现，下面的示例展示了最常见的方法。

# 第5章 Ubuntu 服务器
