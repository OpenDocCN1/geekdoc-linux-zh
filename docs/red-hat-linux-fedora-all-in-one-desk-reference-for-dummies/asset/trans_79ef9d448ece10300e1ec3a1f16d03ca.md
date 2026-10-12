
在 Red Hat Linux 系统中执行的几乎所有任务都涉及一个或多个 GNU 软件包。例如，GNOME 图形用户界面（GUI）和命令解释器（即 Bash shell）都是 GNU 软件程序。顺便说一下，*shell* 是命令解释应用程序，它接受你输入的命令并据此运行程序。如果你重新编译内核或开发软件，你使用的是 GNU C 和 C++ 编译器（它是随 Red Hat Linux 提供的 GNU 软件的一部分）。如果你使用 ed 或 Emacs 编辑器编辑文本文件，你又在使用 GNU 软件包。列表不胜枚举。

![](img/a7eec43a54473e95dc5ea333fecf1bd7_41_0.png)

表 1-1 列出了随 Red Hat Linux 提供的一些知名 GNU 软件包。我只展示此表是为了让你感受一下使用 GNU 软件可以做到的各种不同事情。根据你的兴趣，你可能永远不需要使用其中许多包，但了解它们存在以备不时之需是好的。

| Software Package | Description |
|---|---|
| Autoconf | 生成自动配置源代码包的 shell 脚本 |
| Automake | 生成用于 Autoconf 的 `Makefile.in` 文件 |
| Bash | Red Hat Linux 中的默认 shell——命令解释——程序 |
| Bc | 具有任意精度数字的交互式计算器 |
| Binutils | 一个包含多个用于处理二进制文件的实用程序的包：ar, as, gasp, gprof, ld, nm, objcopy, objdump, ranlib, readelf, size, strings, and strip |
| Coreutils | 一个将名为 Fileutils、Shellutils 和 Textutils 的三个独立包合并并实现诸如：chgrp, chmod, chown, cp, dd, df, dir, dircolors, du, install, ln, ls, mkdir, mknod, mktemp, mv, rm, rmdir, sync, touch, vdir, basename, chroot, date, dirname, echo, env, expr, factor, false, groups, hostname, id, login, logname, nice, nohup, pathchk, printenv, printf, pwd, seq, sleep, stty, su, tee, test, true, tty, uname, uptime, users, who, whoami, yes, cut, join, nl, split, tail, wc, and so on 之类的实用程序的包 |
| Cpio | 将文件归档复制到磁盘或文件系统的另一部分，或从磁盘或文件系统的另一部分复制文件归档。 |
| Diff | 比较文件，以多种不同格式显示逐行更改。 |
| Ed | 行式文本编辑器 |
| Emacs | 可扩展、可定制的全屏文本编辑器和计算环境 |
| Findutils | 一个包含 find、locate 和 xargs 实用程序的包 |
| Finger | 一种实用程序，旨在使 Internet 上的用户能够相互获取信息 |

## What Red Hat Linux Includes

![](img/a7eec43a54473e95dc5ea333fecf1bd7_42_0.png)

| Software Package | Description |
|---|---|
| Gawk | GNU 项目对 AWK 编程语言的实现 |
| GCC | C, C++, Objective C 和其他语言的编译器 |
| Gdb | C, C++ 和 Fortran 的源代码级调试器 |
| Gdbm | 传统 dbm 和 ndbm 数据库库的替代品 |
| Gettext | 一组实用程序，使软件维护人员能够国际化（即使软件的用户消息适用于英语、法语、西班牙语等不同语言）软件包的用户消息 |
| Ghostscript | Postscript 和便携式文档格式（PDF）语言的解释器 |
| Ghostview | 一个 X Window System 应用程序，使 Ghostscript 可从 GUI 访问，使用户能够在窗口中查看 Postscript 或 PDF 文件 |
| The GIMP | GNU 图像处理程序是一个类似 Adobe Photoshop 的图像处理程序 |
| GNOME | 为 Linux 用户可能执行的各种任务提供图形用户界面（GUI） |
| GNU C Library | 用于所有 Linux 程序 |
| Gnuchess | 一个下棋程序 |
| Gnumeric | 一个在 GNOME 中工作的图形电子表格（类似于 Microsoft Excel） |
| grep package | 包含用于查找匹配指定文本模式的行 的 grep、egrep 和 fgrep 命令 |
| Groff | 一个类似于 troff 的文档格式化系统 |
| GTK+ | X Window System 的 GUI 工具包（用于开发 GNOME 应用程序） |
| Gzip | 用于压缩和解压缩文件的 GNU 实用程序 |
| Indent | 通过以几种不同样式缩进格式化 C 源代码 |
| Less | 一个逐页显示程序，类似于 more，但具有额外功能 |
| Libpng | 用于便携式网络图形（PNG）格式图像文件的库 |
| m4 | 传统 UNIX 宏处理器的实现 |
| Make | 一个实用程序，用于确定大型软件包中哪些文件需要重新编译，并发出重新编译它们的命令 |
| Mtools | 一组程序，使用户能够读取、写入和操作 DOS 文件系统（通常是软盘）上的文件 |
| Ncurses | 用于在纯文本终端上显示和更新文本的包 |
| Patch | Larry Wall 程序的 GNU 版本，用于获取 diff 的输出并将这些差异应用到原始文件以生成修改后的版本 |
| RCS | 修订控制系统；用于软件项目中源文件的版本控制和管理 |
| Sed | ed 文本编辑器的流式版本 |
| Sharutils | 一个包含 `shar`（用于将多个文件制作为 shell 归档）和 `unshar`（用于解包这些 shell 归档）的包 |
| Tar | 一个磁带归档程序，包括多卷支持；归档稀疏文件、处理压缩和解压缩以及创建远程归档的能力；以及用于增量和完整备份的其他特殊功能 |
| Texinfo | 一组实用程序，生成印刷手册、纯 ASCII 文本和在线超文本文档（称为 Info），并使用户能够查看和阅读在线 Info 文档 |
| Time | 一个实用程序，报告进程使用的用户时间、系统时间和实际时间 |

## GUIs and applications

说实话 — 在终端上输入晦涩的 Linux 命令很无聊。对于我们这样的普通用户来说，通过 *图形用户界面（GUI，发音为“gooey”）* 使用系统要容易得多，它提供可点击的图片和可打开的窗口（小 *w*）。这就是 X Window System，或 X，发挥作用的地方。

X 有点像 Microsoft Windows，但 X 的底层工作原理与 Windows 完全不同。与 Windows 不同，X 提供了在屏幕上显示窗口的基本功能，但它不提供图形应用程序的特定外观或感觉。这种外观和感觉来自 GNOME 和 KDE 等 GUI，它们使用 X Window System。

Red Hat Linux 以 XFree86 的形式提供 X Window System — 这是为 80x86 系统实现的 X Window System。XFree86 可与当今 PC 上可用的各种视频卡配合使用。

至于 GUI，Red Hat Linux 包含两个强大的 GUI 桌面：KDE（K Desktop Environment）和 GNOME（GNU Object Model Environment）。如果在 PC 上同时安装了 GNOME 和 KDE，你可以选择默认的桌面 — 或在两者之间切换。KDE 和 GNOME 提供了类似于 Microsoft Windows 和 Macintosh OS 的桌面。GNOME 还附带 Nautilus 图形 shell，可轻松查找文件、运行应用程序并配置你的 Red Hat Linux 系统。有了 GNOME 或 KDE，你就可以开始使用 Red Hat Linux 工作站，而无需学习晦涩的 Linux 命令。然而，如果你确实需要直接使用这些命令，只需打开一个终端窗口并在提示符下输入即可。

## What Red Hat Linux Includes

Red Hat Linux 还附带许多图形应用程序。最值得注意的程序是 GIMP（GNU Image Manipulation Program，也称为“The Gimp”），一个用于处理照片和其他图像的程序。GIMP 的功能与 Adobe Photoshop 不相上下。

提供常见的生产力软件 — 如文字处理、电子表格和数据库应用程序 — 曾是 Linux 的薄弱环节。这种情况已经改变。Red Hat Linux 附带 OpenOffice.org 办公生产力应用程序。此外，你可能还想查看这些在 Linux 上广受欢迎的商业办公生产力应用程序，它们未包含在随附 DVD 上：

- *Applixware Office — 现在称为 Anyware Desktop for Linux — 是 Linux 生产力软件的一个很好的例子。你可以在 www.vistasource.com 找到它。*
- *来自 Sun Microsystems 的 StarOffice（www.sun.com/staroffice）是另一个广为人知的生产力软件包。*
- *来自 CodeWeavers 的 CrossOver Office（www.codeweavers.com/products/office/）使你能够在 Linux 中安装你的 Microsoft Office 应用程序（仅限 Office 97 或 Office 2000，而不是 Office XP）。*

正如你所见，Linux 上没有缺少与 Microsoft Office 兼容的办公应用程序。

## Networks

Red Hat Linux 附带了使用系统在网络中所需的一切，以便系统可以与其他系统交换数据。在网络中，交换数据的计算机必须遵循明确定义的规则或协议。网络协议是发送方和接收方就如何在网络上交换数据达成一致的方法。这种协议类似于你在聚会上与某人进行礼貌交谈时可能遵循的规则。你通常会先说你好，交换名字，然后轮流说话。网络协议的工作方式也差不多。两台计算机使用协议在网络上传输位和字节。

最知名和流行的网络协议之一是传输控制协议/互联网协议（*TCP/IP*）。TCP/IP 是互联网 — 现在遍及全球的“网络的网络” — 的首选协议。Red Hat Linux 支持 TCP/IP 协议以及使用 TCP/IP 的任何网络应用程序。

## Internet servers

一些流行的网络应用程序专门设计用于从一个系统向另一个系统传递信息。当你发送电子邮件（e-mail
