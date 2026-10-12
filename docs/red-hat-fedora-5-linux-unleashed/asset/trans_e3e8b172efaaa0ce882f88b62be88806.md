

## 相关的 FEDORA 和 LINUX 命令

以下程序和内置 shell 命令在命令行操作时常用。这些命令按类别组织，帮助你理解命令的用途。如果你需要查找使用命令的完整信息，可以在该命令的手册页中找到这些信息。

- **管理用户和组**—*finger, chfn, chsh, edquota, gpasswd, groupadd, groupdel, groupmod, groups, mkpasswd, newgrp, newusers, passwd, pwck, useradd, userdel, usermod*
- **管理文件和文件系统**—*stat, md, chattr, chmod, chown, compress, cp, dd, fdisk, find, gzip, ln, mkdir, mksfs, mount, mv, rm, rmdir, rpm, sort, swapon, swapoff, tar, touch, umount, uncompress, uniq, unzip, zip*
- **管理运行中的程序**—*bg, fg, kill, killall, nice, ps, pstree, renice, top, watch*
- **获取信息**—*apropos, cal, cat, cmp, date, diff, df, dir, dmesg, du, env, file, free, grep, head, info, last, less, locate, ls, lsattr, man, more, pinfo, ps, pwd, stat, strings, tac, tail, top, uname, uptime, vdir, vstest, w, wc, Whatis, whereis, which, who, whoami*
- **控制台文本编辑器**—*ed, jed, joe, mc, nano, red, sed, vim*
- **控制台互联网和网络命令**—*cinc, elml, ftp, host, hostname, ifconfig, links, lynx, mail, mutt, ncftp, netcfg, netstat, ping, pump, rdate, route, scp, sftp, ssh, tcpdump, traceroute, whois, wire-test*

## 参考

迁移到新的计算机操作系统对管理人员和用户来说不一定痛苦。提供易于理解的说明、一些背景信息以及已安装系统的预配置，可以帮助完成过渡。

本节列出了一些额外的参考点，包含本章讨论的标准和命令的背景信息。浏览这些链接以进一步了解本章讨论的一些概念，并扩展你对新 Linux 社区的知识。

- http://www.winnmag.com/Articles/Index.cfm?ArticleID=7420—一篇由 Windows NT 用户撰写的文章，该用户在尝试使用 Linux 时，天真地承认因为在 Linux 控制台上不知道如何读取文本文件而重启了系统。
- http://standards.ieee.org/regex/h/posix/—IEEE 的 POSIX 信息页面。
- http://www.itworld.com/Comp/2362/1w-01-government/#sidebar—关于 Linux 和 POSIX 合规性的讨论。
- http://www.pathname.com/fhs/—Linux FHS（Linux 文件系统层次结构标准）的主页。
- http://www.tldp.org/—浏览 HOWTO 部分以查找并阅读 *The Linux Keyboard and Console HOWTO*—Andries Brouwer 编写的一份略显陈旧但极其有用的关于使用 Linux 键盘和控制台的指南。
- http://www.gnu.org/software/emacs/emacs.html—FSF 的 GNU Emacs 编辑环境的主页；你可以在这里找到额外的文档以及最新版本源代码的链接。
- http://www.vim.org/—随 Linux 发行版附带发行的 vim（vi 克隆版）编辑器的主页。在这里查看该编辑器的更新、错误修复和新闻。
- http://www.courtesan.com/sudo/—sudo 命令的主页。在这里查看最新更新、安全功能和错误修复。

![](img/2045828cf45e5632bf056f9ca99d6755_199_0.png)

# 第二部分

## 桌面版 Fedora

### 本部分包含

- 第 6 章 X 窗口系统 167
- 第 7 章 管理软件 193
- 第 8 章 在互联网上：浏览网页、撰写电子邮件和阅读新闻 211
- 第 9 章 生产力应用程序 241
- 第 10 章 多媒体应用程序 263
- 第 11 章 图形处理 287
- 第 12 章 使用 Fedora 打印 301
- 第 13 章 游戏 315

# 第 6 章

# X 窗口系统

X 窗口系统是许多 Linux 发行版上找到的图形网络接口，它为广泛的图形工具和窗口管理器提供了基础。它通常简称为 X，也可被称为 X11R7 和 X11（例如在 Mac OS X 上找到的）。X 来自世界闻名的麻省理工学院，已经过几个版本，每个版本都扩展和增强了该技术。其开源实现由 X.Org 基金会管理，该董事会由开源界的一些关键人物组成。

令人困惑的是，X 有两个不同的版本：X11R6.9 和 X11R7。它们共享相同的源代码基础，但 X11R7 是模块化的，这意味着源代码被分解成较小的模块，使开发人员更容易开展工作。作为最终用户，你使用哪个版本并不重要；它们具有完全相同的功能。Fedora 5 中包含的 X 版本是 X11R7，于 2005 年 12 月发布。

理解 X 工作方式的最佳方法是将其视为客户端/服务器系统。X 服务器为那些旨在最大程度利用服务器下可用图形和网络功能以及受支持库的程序提供服务。X.Org 为许多不同平台提供版本，包括 Linux 和 Mac OS X。最初实现为 XFree86，当围绕即将包含在 XFree86 许可证中的某些限制发生争执时，X.Org 分叉了。通过对在先前版本许可证下获得许可的代码进行快照，X.Org 基于该代码推动了自己的实现。几乎同时，大多数 Linux 发行版背弃了 XFree86，并将他们的开发工作转向 X.Org。

### 本章内容

- 基本 X 概念
- 使用 X11R6
- 启动 X
- 选择和窗口管理器
- GNOME 和 KDE 桌面环境
- 参考

在本章中，你将学习如何处理随 Fedora 附带的 X 版本。我们将查看 X 的基础知识，以及如何使 X 与可能影响它的任何升级协同工作，例如新的图形显卡或你刚刚购买的新平板显示器。

## 红帽和 Fedora 桌面

如果你使用过 Fedora 的先前版本，甚至 Red Hat Linux，你会非常清楚 BlueCurve，这是专门为 Red Hat 开发的自定义桌面外观和感觉。尽管有些人讨厌 Red Hat 的点状外观和感觉，但其他人发现无论是在 KDE 还是 GNOME 中，拥有一个熟悉的环境都是很有用的。

随着 Fedora 4，Fedora 项目团队使其 GNOME 实现更接近上游版本。这导致使用最近添加的 Clearlooks 主题，而不是 BlueCurve。更进一步，Fedora 项目现在拥有独特的身份，与 Red Hat 分开，现在已融入 Fedora 5 的外观和感觉中。

当然，你可以自由使用 Fedora 为 KDE 或 GNOME 提供的任何其他主题。其他窗口管理器，例如 *twin* 和 *xfce*，也可以使用，尽管你可能需要使用 yum 检索和安装它们。

## 基本 X 概念

X11 的底层引擎是 X 协议，它提供了管理本地和远程桌面的显示的系统。该协议使用客户端/服务器模型，允许对客户端窗口和其他装饰的绘制进行本地和网络抽象。X 服务器绘制特定的本地硬件和响应客户端请求的客户端窗口、对话框和按钮。但是，客户端不需要特定于本地硬件。这意味着系统管理员可以设置一个带有大型服务器和客户端的网络，并启用用户在工作站上查看和使用这些客户端，即使它们具有完全不同的 CPU 和图形显示。

## 注意

演示 X 处理远程客户端能力的更好方式是什么，除了使用其能力来生成本章？本章的 OpenOffice.org 文件驻留在 Mac mini（运行 Fedora）上，但实际使用的显示器和键盘是运行 Ubuntu 5.10 的 Acer Ferrari 笔记本电脑的一部分，通过以太网连接。修订是使用运行 Fedora 5 的台式计算机上的 Logitech 键盘和鼠标完成的，再次通过 X 连接到 Mac mini，但这次使用无线连接。

由于 X 为用户提供了一种分布式处理形式，这意味着 Fedora 可以用作连接到强大 X 服务器的非常廉价的桌面平台。X 服务器越强大，可以容纳的基于 X 的客户端数量就越多。如果打算运行许多 X 客户端，快速网络是必不可少的，因为 X 可能会变得带宽消耗很大。

