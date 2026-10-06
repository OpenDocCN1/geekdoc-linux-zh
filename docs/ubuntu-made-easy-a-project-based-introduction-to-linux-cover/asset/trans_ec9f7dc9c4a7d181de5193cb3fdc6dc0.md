

# 安装类型

| sda1 (linux-swap) | sda2 (ext4) |
| :--- | :--- |
| 4.2 GB | 103.2 GB |
| 设备 | 类型 | 挂载点 | 格式？ | 大小 | 使用 |
| /dev/sda | | | | | |
| /dev/sda swap | | | | 4198 MB | 未知 |
| /dev/sda2 ext4 | | | | 103173 MB | 未知 |

新建分区表... 添加... 更改... 删除... 还原

引导程序安装设备：
/dev/sda ATA VBOX HARDDISK (107.4 GB)

**图 C-5：仅适用于 Ubuntu 的简单分区布局**

# 安装类型

| sda1 (linux-swap) | sda5 (ext4) | sda6 (ext4) |
| :--- | :--- | :--- |
| 4.0 GB | 12.0 GB | 91.4 GB |
| 设备 | 类型 | 挂载点 | 格式？ | 大小 | 使用 |
| /dev/sda | | | | | |
| /dev/sda swap | | | | 3999 MB | 未知 |
| /dev/sda5 ext4 | | | | 11998 MB | 未知 |
| /dev/sda6 ext4 /home | | | | 91371 MB | 未知 |

新建分区表... 添加... 更改... 删除... 还原

引导程序安装设备：
/dev/sda ATA VBOX HARDDISK (107.4 GB)

**图 C-6：带有独立 home 分区的 Ubuntu 分区布局**

# 带有共享分区的 Ubuntu 和 Windows

Ubuntu 将与 Windows XP 并排安装，我想要共享分区，以便在两个操作系统之间拷贝文件（见图 C-7）。我现有的 Windows 安装使用了磁盘上 6.7 GB 的空间，上面安装了文件和程序。我将 Windows 安装分区调整为 15GB，留下了 8.3GB 的空空间以供以后扩展。请注意，Windows 分区不会被格式化，因此 Windows 以及该分区上的所有文件都将保持完好。我创建了一个 40GB 的 Ubuntu 根分区和一个 4.2GB 的交换分区，然后在剩余的 40GB 磁盘空间中创建了一个共享 FAT32 分区。

![](img/d35fa962e6f9664d66dc83916f426418_455_0.png)

# 完成

如果你已完成，请点击**现在安装**以完成您的更改。如果你正在删除或格式化任何分区，更改将写入磁盘。这是一个不可逆的更改，因此请务确保您已备份受影响分区上的任何宝贵数据！

图 C-7：Ubuntu、Windows 和共享分区

# 资源

![](img/d35fa962e6f9664d66dc83916f426418_456_0.png)

由于 Linux 的增长和发展很大程度上归功于互联网，因此在网上找到关于 Linux 各种发行版（包括 Ubuntu）的丰富信息并不令人意外。除了常见的新闻、教程和下载网站外，你还会发现各种教程、论坛、博客和其他有用信息源——当你在使用并更多地学习系统时，都可以参考这些资源。

# 论坛

当你寻求建议、尝试解决某个特定问题或只是在寻找一些通用技巧时，在线论坛是首选。坦率地说，Ubuntu 有它自己的论坛，而且由于 Ubuntu 主要是一个以桌面为导向的 Linux发行版，你可能在在那里发现很多新手和对新手友好的帖子（而不是你在某些其他网站上可能会看到的硬核极客）。当然，还有其他对新手友好的论坛，虽然它们不是针对 Ubuntu 的，但应该也能为你提供很多有用信息。

无论你在哪个论坛发帖，无论你使用的是哪个版本（如果你忘记了，是 Precise Pangolin），也无论你是 Linux 新手，当得到一个你不理解的答案时，始终记住寻求说明。同一个发帖者通常会回来为你重新解答。你应该会在这些大多数网站上感到如归家，尽管你可能会比其他网站多去一两个。

- http://ubuntu.org/ 这是官方的 Ubuntu 社区论坛，在第 21 章中进行了详细介绍。当你遇到困难、有疑问或只是想了解发生了什么时，这一直是一个很好的起点。
- http://www.ubuntu.org/forum/ 如果你觉得 UbuntuForums 内容太多读不完，你可能会发现这个较小的 Ubuntu 专用论坛是一个很好的去处。
- http://askubuntu.com/ 这是一个真正以解决问题和教程为导向的论坛，所以当你有问题、疑问或怀疑时，它是另一个很好的去处。
- http://www.ubuntuforums.net/ 该论坛专门用于 Ubuntu，是一个基于 KDE 桌面环境的官方 Ubuntu 版本。
- http://www.justlinux.com/ 和 http://www.linuxquestions.com/ 如果你在此上述论坛中找不到你想要的，可以尝试这些处理通用 Linux 问题的论坛。你肯定能在上面找到很多 Ubuntu 用户。

# Linux 参考

你可以在这些网站学习更多关于 Ubuntu 或通用 Linux 的知识，其中许多针对新手的：

- http://www.ubuntu.com/ubuntu/ Ubuntu 及其功能的概述。
- http://ubuntuguide.org/wiki/ubuntu:precise 非官方的 Ubuntu 启动指南。
- http://help.ubuntu.com/ Ubuntu 当前发布版本的官方文档。
- http://www.tukuxfiles.org/ 针对 Linux 新手的大量教程和信息。
- http://www.linuxcommand.org/ 你可以在这里学习如何使用 Linux 命令。
- http://www.linux.org/ 新闻、书评、下载和各种其他内容——都是关于 Linux 的。
- http://www.libreoffice.org/get-help/ 为 Ubuntu LibreOffice 套件用户提供的若干帮助资源。

# 博客

你也可以在博客中找到很多很好的信息。在这些博客中，你可以发现其他用户在尝试新事物时的发现、分享的技巧以及对问题的解决方案：

- http://www.ubuntu.org/blog/ 一个主要面向 Ubuntu 的新闻博客。
- http://www.ubuntugeek.com/ 尽管名字里有“geek”（极客）一词，但这是一组非常易于获取的、实用的 Ubuntu 系统和软件调优。
- http://www.omubuntu.com/ 一个非常有趣的博客，像杂志一样，涵盖了但但不限于 Ubuntu 和其他发行版。
- http://webup.org/ 关于 Ubuntu 的博客。

# 硬件兼容性

如果你想知道你的硬件是否与 Linux 兼容，或者只是想了解硬件兼容性问题，可以查看以下网站：

- http://www.ubuntu.com/certification/ 包含 Ubuntu 兼容性信息。
- http://wiki.ubuntu.com/HardwareSupport/ 也提供 Ubuntu 兼容性信息。
- http://www.linuxcompatible.org/ 按发行版排列的众多兼容列表。
- http://www.linuxfoundation.org/ 关于打印机兼容问题的良好场所。
- http://www.linuxmodems.org/ 查看你的调制解调器支持。
- http://www.sane-project.org/ 查看你的扫描仪是否兼容。
- http://www.linux-laptop.net/ 有笔记本，想要 Linux 吗？看看这里。
- http://www.tuxobi.net/ 提供适用于非桌面设备的 Linux（笔记本、PDA、手机等）。

# 无线连接

如果你使用无线卡连接互联网并遇到困难，或者只是想知道哪里有免费热点，以下网站可以帮到你：

- https://help.ubuntu.com/community/WifiDocs/
- http://www.linuxux.org/
- http://www.hpl.com/personal/Jean_Tourril/
- http://www.ezgoal.com/hotspots/wireless/

# 免费下载

如果你发现自己在寻找更多好玩的东西，你应该能在这些网站之一找到大量可下载的免费资源。你可以从 Ubuntu 应用程序目录开始。

# 与其他软件包

- https://apps.ubuntu.com/cat/
- http://www.getdeb.net/
- http://sourceforge.net/
- http://www.freecode.com/
- http://www.gnomefiles.org/

# 免费字体

- http://www.fontfreak.com/
- http://www.fontparadise.com/
- http://fonts.tom.com/

# 新闻与信息

这些网站主要是提供信息的，让你了解整个 Linux 世界的最新情况（我在第 21 章中介绍了一些针对 Ubuntu 的网站）。DistroWatch 关注各种发行版，而 Linux Today、LinuxPlanet 和 Phoronix 则更符合在线杂志/报纸类型。

- http://www.distrowatch.com/
- http://www.linuxtoday.com/
- http://www.linuxplanet.com/
- http://www.phoronix.com/

