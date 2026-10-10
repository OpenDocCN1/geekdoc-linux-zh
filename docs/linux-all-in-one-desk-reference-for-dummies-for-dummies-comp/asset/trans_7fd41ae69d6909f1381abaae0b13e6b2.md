

# 18 Linux 发行版包含的内容

表 1-2（续）

| 软件包 | 描述 |
| :--- | :--- |
| Coreutils | 一个组合了名为 Fileutils、Shellutils 和 Textutils 的三个独立软件包的软件包，实现了诸如 chgrp、chmod、chown、cp、dd、df、dir、dircolors、du、install、ln、ls、mkdir、mkfifo、mknod、mv、rm、rmdir、sync、touch、vdir、basename、chroot、date、dirname、echo、env、expr、factor、false、groups、hostname、id、logname、nice、nohup、pathchk、printenv、printf、pwd、seq、sleep、stty、su、tee、test、true、tty、uname、uptime、users、who、whoami、yes、cut、join、nl、split、tail、wc 等实用工具 |
| GNUchess | 一款国际象棋游戏 |
| GNU C 库 | 供所有 Linux 程序使用 |
| cpio | 将文件归档复制到磁盘或文件系统的另一部分，或从磁盘/文件系统复制 |
| diff | 比较文件，以几种不同的格式逐行显示更改 |
| ed | 一个面向行的文本编辑器 |
| emacs | 一个可扩展、可定制的全屏文本编辑器及计算环境 |
| Findutils | 一个包含 find、locate 和 xargs 实用工具的软件包 |
| finger | 一个旨在让互联网用户获取彼此信息设计的实用程序 |
| gawk | GNU 项目对 awk 编程语言的实现 |
| gcc | C、C++、Objective C 及其他语言的编译器 |
| gdb | C、C++ 和 Fortran 的源代码级调试器 |
| gdbm | 传统 cfm 和 ndbm 数据库库的替代品 |
| gettext | 一组实用工具，使软件维护人员能够使其软件包的用户消息国际化（即让软件支持英语、法语、西班牙语等不同语言） |
| ghostscript | PostScript 和便携式文档格式（PDF）语言的解释器 |
| ghostview | 一个 X Window 系统应用程序，通过图形用户界面（GUI）使 ghostscript 可被访问，从而让用户能在窗口中查看 PostScript 或 PDF 文件 |
| The GIMP | （GNU 图像操纵程序）：类似于 Adobe Photoshop 的图像处理程序 |
| GNOME | 为 Linux 用户可能执行的广泛任务提供图形用户界面（GUI） |
| gnumeric | 一个在 GNOME 中工作的图形化电子表格（类似于 Microsoft Excel） |
| grep 软件包 | 包含用于查找匹配指定文本模式的行的 grep、egrep 和 fgrep 命令 |
| groff | 类似于 troff 的文档格式化系统 |
| gtk+ | X Window 系统的图形用户界面工具包（用于开发 GNOME 应用程序） |
| gzip | 一个用于压缩和解压文件的 GNU 实用工具 |
| indent | 通过以几种不同风格之一缩进来格式化 C 源代码 |
| less | 一个类似于 more 的逐页显示程序，但具备更多功能 |
| libpng | 用于便携式网络图形（PNG）格式图像文件的库 |
| m4 | 传统 UNIX 宏处理器的实现 |
| make | 一个确定大型软件包中哪些文件需要重新编译，并发出重新编译命令的实用工具 |
| mtools | 一组允许用户读取、写入和操作 DOS 文件系统（通常是软盘）上文件的程序 |
| ncurses | 一个用于在纯文本终端上显示和更新文本的软件包 |
| patch | Larry Wall 程序的 GNU 版本，用于获取 diff 的输出并将这些差异应用于原始文件以生成修改后的版本 |
| rcs | （修订控制系统）：用于软件项目中源文件的版本控制和管理 |
| sed | ed 文本编辑器的面向流的版本 |
| Sharutils | 一个包含 shar（用于将许多文件制作成 shell 归档）和 unshar（用于解压这些 shell 归档）的软件包 |
| tar | 一个磁带归档程序，包含多卷支持；能够归档稀疏文件（包含大量全零数据块的文件）、处理压缩和解压以及创建远程归档；以及其他用于增量和完全备份的特殊功能 |
| texinfo | 一组生成打印手册、纯 ASCII 文本和在线超文本文档（称为 info）的实用工具，并允许用户查看和阅读在线 info 文档 |
| time | 一个报告进程使用的用户时间、系统时间和实际时间的实用工具 |

## 图形用户界面和应用程序

面对现实吧——在终端上输入晦涩难懂的 Linux 命令很无聊。对于普通用户来说，通过图形用户界面（GUI，读作 GOO-ee）使用系统——即提供可点击的图片和小写 w 开始的窗口（windows）来打开的界面——要容易得多。这时，X Window 系统，或简称 X，就派上了用场。

X 有点像 Microsoft Windows，但 X 的工作底层细节与 Windows 完全不同。X 提供了在屏幕上显示窗口的基本功能，但（与 Microsoft Windows 不同）它并不附带任何特定的图形应用程序外观或感觉。那种外观和感觉来自图形用户界面，例如利用 X Window 系统的 GNOME 和 KDE。

大多数 Linux 发行版都包含 X Window 系统，形式为 XFree86 或 X.Org X11 —— 这是针对 80x86 系统的 X Window 系统实现。XFree86 和 X.Org X11 可与当今个人电脑上可用的各种视频卡协同工作。

![](img/11709a8f88c8cd03868a929dc94c0e2b_45_0.png)

直到 2004 年初，XFree86 项目（<http://www.xfree86.org>）的 XFree86 是 x86 系统中最常用的 X Window 系统实现。然而，大约在 4.4 版本时，XFree86 许可条款的一些变更引起了许多 Linux 和 UNIX 供应商的担忧——他们认为许可条款不再与 GNU 通用公共许可证（GPL）兼容。2004 年 1 月，几家供应商成立了 X.Org 基金会（<http://www.x.org>），以促进开源 X Window 系统和图形桌面的持续开发。X.Org X11 的第一个版本使用的是 XFree86 4.4 所使用的相同代码，直到 XFree86 许可变更导致 X.Org 基金会成立的时刻。

至于图形用户界面，Linux 发行版包含两个强大的图形用户界面桌面中的一个或两者：KDE（K 桌面环境）和 GNOME（GNU 对象模型环境）。如果 PC 上同时安装了 GNOME 和 KDE，你可以选择哪个桌面作为默认——或者在两者之间切换。KDE 和 GNOME 提供类似于 Microsoft Windows 和 Mac OS 的桌面。GNOME 还附带 Nautilus 图形外壳，使查找文件、运行应用程序和配置你的 Linux 系统变得容易。使用 GNOME 或 KDE，你无需了解晦涩难懂的 Linux 命令就可以开始使用你的 Linux 工作站。但是，如果你需要直接使用这些命令，你只需打开一个终端窗口并在提示符处输入它们即可。

Linux 还附带许多图形应用程序。最值得注意的程序是 The GIMP（GNU 图像操纵程序），一个用于处理照片和其他图像的程序。The GIMP 的能力与 Adobe Photoshop 不相上下。

提供常见的生产力软件——如文字处理、电子表格和数据库应用程序——曾经是 Linux 缺乏的一个领域。但这种情况已经改变。Linux 附带 OpenOffice.org 办公生产力应用程序。此外，你可能想看看这些未在本书配套 DVD-ROM 中提供的著名商业 Linux 办公生产力应用程序：

-   **Applixware**：此办公套装包是 Linux 生产力软件的一个良好示例。你可以在 `www.vistasource.com` 找到它。
-   **StarOffice**：来自 Sun Microsystems（`www.sun.com/staroffice`），StarOffice 是另一个著名的生产力软件包。
-   **CrossOver Office**：来自 CodeWeavers（`www.codeweavers.com/products/cxoffice`），你可以使用 CrossOver Office 在 Linux 中安装你的 Microsoft Office 应用程序（Office 97、Office 2000 和 Office XP）以及几个其他 Windows 应用程序。

如你所见，兼容 Microsoft Office 的 Linux 办公应用程序并不缺乏。

## 网络

Linux 附带了你所需的一切，以便在网络上使用该系统，使系统能够与其他系统交换数据。在网络中，交换数据的计算机必须遵循定义明确的规则，或**协议**。**网络协议**是发送方和接收方同意的通过网络交换数据的方法。这样的协议类似于你在聚会上与人礼貌交谈时可能遵循的规则。你通常从说你好、交换名字开始，然后轮流说话。网络协议的工作方式大致相同。两台计算机使用相同的协议在网络上相互发送位和字节。

最著名和流行的网络协议之一是传输控制协议/互联网协议（*TCP/IP*）。TCP/IP 是互联网上首选的协议——如今覆盖全球的“网络的网络”。Linux 支持 TCP/IP 协议以及任何利用 TCP/IP 的网络应用程序。

## 互联网服务器

一些流行的网络应用程序专门设计用于将一个系统上的信息传送到另一个系统。当你使用电子邮件（e-mail）发送电子邮件或使用 Web 浏览器访问网站时，你正在使用这些网络应用程序（也称为*互联网服务*）。以下是一些常见的互联网服务：

-   **电子邮件**（e-mail），你使用它通过类似 `joe@someplace.com` 的地址向互联网上的任何其他人员发送消息
-   **万维网**（或简称为 Web），你使用 Web 浏览器浏览它
-   **新闻服务**，你可以阅读新闻组并向名为 `comp.os.linux.networking` 或 `comp.os.linux.setup` 等新闻组发布新闻条目

