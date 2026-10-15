
```
apt-cache search games | grep kde
```

当你找到要安装的软件包后，像往常一样通过 apt-get install 运行它们即可。如果你想先了解该软件包的更多信息，可以使用 apt-cache showpkg，如下所示：

```
apt-cache showpkg mysql-server-5.0
```

这会显示“反向依赖”（哪些软件包需要、推荐或建议 mysql-server-5.0）、“依赖关系”（哪些软件包是安装 mysql-server-5.0 所必需、推荐或建议的）以及“提供”（此软件包为你提供哪些功能）方面的信息。“provides”列表非常强大，因为它允许多个不同的软件包提供同一个资源。例如，基于 MySQL 数据库的程序要求安装 MySQL，但并不关心你安装的是 MySQL 4.1 还是 MySQL 5.0。在这种情况下，MySQL 4.1 和 MySQL 5.0 的 Debian 软件包都会在 provides 列表中包含“mysql-server-4.1”，这意味着它们提供了 MySQL 4.1 所具备的功能。因此，你可以安装任一版本来满足基于 MySQL 的应用程序的需求。

## 从源代码编译软件

从源代码编译应用程序并不难。大多数源代码以压缩的源代码 tarball 形式提供——也就是使用 gzip 或 bzip 压缩的 tar 文件。这些压缩文件通常会解压到一个包含多个文件的目录中。最好始终以普通用户身份编译源代码，以限制损坏或恶意代码可能造成的损害，因此请在你的主目录中创建一个名为 source 的目录。

无论你将源代码 tarball 下载到哪里，都可以使用 tar 的 -C 选项将其解压缩到 ~/source 目录：

```
tar zxvf packagename.tgz -C ~/source
```

```
tar zxvf packagename.tar.gz -C ~/source
```

以下是关于如何编译和安装软件的说明。通常，编译源代码的流程如下：

```
./configure
```

此命令会运行一个脚本，检查所有依赖项是否满足以及构建环境是否正确。如果缺少依赖项，configure 脚本通常会明确告诉你它需要哪些。如果你在 Synaptic 中启用了 Universe 和 Multiverse 软件源，你很可能会在其中找到缺失的软件（通常是库）。

当 configure 脚本成功执行后，运行

```
make
```

来编译软件。最后，运行

```
sudo make install.
```

如果编译失败，请检查错误消息以查找原因，然后运行

```
make clean
```

在重新开始之前。你也可以运行

```
sudo make uninstall
```

如果不喜欢该软件，可以用它来卸载。

## 相关的 Ubuntu 和 Linux 命令

在管理 Ubuntu 系统资源和软件包时，你会用到以下命令：

- apt-get——默认的命令行软件包管理工具（更多关于 APT 的内容请参阅第 30 章）
- gnome-app-install——Ubuntu 图形界面软件包管理器
- synaptic——用于软件操作和软件源编辑的高级工具
- update-manager——Ubuntu 软件包更新的主要来源

## 参考资料

- http://www.debian.org/doc/manuals/project-history/ch-detailed.en.html——Debian Linux 软件包系统的历史。
- http://www.nongnu.org/synaptic/——Synaptic 软件包管理器的主页。
- http://www.ubuntu.com/usn——Ubuntu 安全公告的官方列表。

# 第32章

# 内核与模块管理

内核是一个复杂的软件，负责管理操作系统中发生的进程及进程交互。作为用户，你很少（如果曾经有过的话）直接与它交互。相反，你使用的是内核管理的应用程序。

Linux 内核就是 Linux。它是世界各地众多人士多年合作（有时也充满争议）的成果。只有一个公共内核源代码树，但每个主要的 Linux 发行版都会对其版本稍作调整和修补，以增加功能、提升性能或提供更多选项。包括 Ubuntu 在内的每个 Linux 发行版都附带自己的预编译内核以及内核源代码，让你对 Linux 操作系统拥有绝对的控制权。在本章中，我们将研究内核，了解它为我们和操作系统做了些什么。

在本章中，你还将学习如何获取内核源代码，以及如何、何时为内核打补丁。本章将带你以专家的视角浏览内核架构，并教你内核配置中的几个关键步骤、如何构建和安装模块，以及如何在 Ubuntu 中编译驱动程序。本章还将教你使用 GRUB（Ubuntu 默认引导加载程序）的重要方面。最后，本章的故障排除信息将帮助你了解 Linux 内核安装或编译过程出现问题时该怎么做。尽管这些问题看起来令人不安，但本章将向你展示许多内核问题的简单修复方法。

大多数用户发现预编译的 Ubuntu 内核已经满足他们的需求。在某些时候，你可能需要重新编译

### 本章内容

- Linux 内核
- 管理模块
- 何时重新编译
- 内核版本
- 获取内核源代码
- 为内核打补丁
- 编译内核
- 出现问题时的处理
- 参考资料

