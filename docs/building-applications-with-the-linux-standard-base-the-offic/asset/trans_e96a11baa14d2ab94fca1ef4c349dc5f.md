

书面规范（Written Specification）并不包含各种数据库共享库，因此必须寻找其他解决方案。幸运的是，Apache 的源代码甚至考虑到了这种情况，通过提供一个有限的数据库引擎来解决，该引擎可以与 Apache 一起构建和发布。在应用程序电池（Application Battery）中构建 Apache 的技巧是说服 configure 脚本使用内部数据库，而不是依赖构建系统上找到的数据库。实现这一点的方法是在运行 configure 时提供 `--without-gdbm` 和 `--without-berkeley-db` 标志。这防止 configure 在构建系统上搜索这些非 LSB 共享库。configure 脚本确定应使用内部共享库。为了满足非 LSB 共享库的要求，Apache 在安装期间随 Apache 应用程序提供数据库库和另外两个实用程序库。

Celestia 的情况与 Apache 类似，因为它试图使用可用的最佳共享库来处理图形信息的显示。通常，当在 Gnome 桌面环境中运行时，应用程序将运行 GTK；当在 KDE 桌面环境中运行时，将运行 Qt。这些图形界面库均未被 LSB 指定，因此必须找到另一种替代方案。将这些接口静态链接到 Celestia 被证明非常困难，因此应用程序电池采取了不同的方向。Celestia 的源代码也包含对使用 libGL 进行图形处理的支持，这是好事，因为 libGL 是一个有效的 LSB 共享库。由于应用程序电池是在大多数可能安装了 GTK、Qt 或两者的系统上构建的，因此 Celestia 的 configure 脚本被调用时使用 `--without-gtk` 和 `--without-kde` 标志。这防止 configure 尝试使用 GTK 或 Qt。相反，Celestia 将被构建为仅支持 libGL，从而允许其符合 LSB 书面规范。

Samba 应用程序是另一种旨在在各种环境中工作并利用受支持功能的应用程序。其中一个特性是使用通用 UNIX 打印系统（CUPS）来提供打印支持。CUPS 接口为应用程序提供了一个可移植性层，将与受支持的任何 UNIX 打印系统（如 lp 或 lpr）一起工作。该接口提供了超出仅仅提交打印作业之外的额外功能，因此 Samba 利用了这些能力。再次，这是创建 LSB 版本 Samba 的问题，因为 CUPS 未在规范中定义。应用程序电池在使用 configure 调用时使用 `--disable-cups` 标志，以告知 Samba 不要尝试使用 CUPS 接口。然后，Samba 将回退到功能较少的 lp 或 lpr 命令，但仍然提供打印支持。

## 14.3.4 更改应用程序安装位置

一旦应用程序电池中的应用程序成功编译，是时候考虑 LSB 合规性的另一个要求了。所有应用程序在应用程序安装到系统上的位置方面必须遵循文件系统层级标准（FHS）。就应用程序电池而言，所有包含的应用程序都被视为第三方应用程序，因为它们并非随 Linux 发行版一起分发。FHS 规定第三方应用程序必须将其组件部分安装在特定目录中。应用程序的任何静态部分，例如主应用程序二进制文件，必须安装在 /opt 目录下。与该应用程序关联的任何配置文件必须安装在 /etc/opt 目录下。在应用程序运行时可以修改的任何文件都应安装在 /var/opt 目录下。LSB 应用程序电池将其所有应用程序安装在 /opt/lsb/appbat、/etc/opt/lsb/appbat 和 /var/opt/lsb/appbat 目录下。

修改应用程序电池应用程序安装位置的方法因应用程序的编写方式而略有不同。一些行为良好的应用程序在安装时使用其 makefile 中的 DESTDIR 变量。这使得将 DESTDIR 设置为 /opt/lsb/appbat 并使用应用程序的常规 makefile 进行安装变得容易。不幸的是，并非所有应用程序在替代安装位置方面都如此体贴。对于这些情况，应用程序电池使用了其他方法，例如修补 makefile 以允许其他安装位置。解决这类问题的一般方案将涉及一个决策树。最好的情况是支持 DESTDIR。如果不支持，则需要检查应用程序安装代码，以确定如何最好地修改它。

## 14.4 下载应用程序电池

要获取 LSB 应用程序电池，请访问 LSB 下载网页。²

表 14.1 展示了可通过万维网访问的信息。

- `lsb-apache-2.0.49` Apache 的 LSB 合规版本，一个功能强大、功能齐全、高效且免费可用的 Web 服务器。它是互联网上最流行的 Web 服务器。Apache 主要被添加到 LSB 应用程序电池中，以演示网络、线程和应用程序提供的共享库。
- `lsb-celestia-1.3.1` Celestia 的 LSB 合规版本，一个免费的实时太空模拟程序，让您在三维空间中体验我们的宇宙。Celestia 主要被添加到 LSB 应用程序电池中，以演示使用 OpenGL 库的 C++ 程序。
- `lsb-expect-5.41.0` **expect** 的 LSB 合规版本，expect 是用于自动化和测试交互式应用程序（如 **telnet**、**ftp**、**passwd**、**fscck**、**login**、**tip** 等）的 Tcl 扩展。该程序主要被添加到 LSB 应用程序电池中，以演示软件包依赖性，因为它依赖于 LSB 合规的 Tcl。它也用于构建 LSB 运行时测试套件。
- `lsb-groff-1.19` **groff** 的 LSB 合规版本，一个文档格式化系统。它主要被添加到 LSB 应用程序电池中，以演示 C++ 程序的使用。
- `lsb-lynx-2.8.5` Lynx 的 LSB 合规版本，一个基于文本的 Web 浏览器。Lynx 主要被添加到 LSB 应用程序电池中，以演示 **ncurses** 库的使用。
- `lsb-python-2.3.4` Python 的 LSB 合规版本，一种解释型、交互式、面向对象的编程语言。它包含模块、类、异常、非常高级的动态数据结构和动态类型。Python 被添加到 LSB 应用程序电池中，因为包含的测试套件练习了许多 LSB 功能，包括套接字、网络、curses 和其他功能。
- `lsb-rsync-2.6.2` `rsync` 的 LSB 合规版本，一个用于非常快速使远程和主机文件同步的程序。它很快，因为它只通过网络发送文件的差异，而不是发送完整的文件。通常，`rsync` 被用作非常强大的镜像过程，或者作为比 `rcp` 命令更强大替代方案。该程序主要被添加到 LSB 应用程序电池中，以演示网络的使用。
- `lsb-samba-3.0.4` Samba 的 LSB 合规版本，一个可用于为 SMB（有时称为 *LAN Manager*）客户端提供网络服务的 SMB 服务器。Samba 使用基于 TCP/IP 的 NetBIOS（NetBT）协议，并且*不需要* NetBEUI（Microsoft 原始 NetBIOS 帧）协议。Samba 主要被添加到 LSB 应用程序电池中，以演示网络和基于 PAM 的身份验证的使用。
- `lsb-tcl-8.4.6` Tcl 的 LSB 合规版本，一种设计为嵌入在其他应用程序中的简单脚本语言。此软件包还包括 *tclsh*，一个简单的 Tcl 应用程序示例。Tcl 主要被添加到 LSB 应用程序电池中，因为包含的测试套件练习了许多 LSB 功能；它还提供了 LSB 合规版本 expect 的依赖项。
- `lsb-xpaint-2.7.0` XPaint 的 LSB 合规版本，一个 X Window 系统颜色图像编辑和绘画程序。它主要被添加到 LSB 应用程序电池中，以演示 X11 库的使用。
- `lsb-xpdf-1.01` *xpdf* 的 LSB 合规版本，一个用于便携式文档格式（PDF）文件的 X Window 系统查看器。这是一个小而高效的程序，使用标准的 X 字体。它主要被添加到 LSB 应用程序电池中，以演示练习 X11 库的 C++ 程序的使用。

表 14.1：应用程序电池下载页面

| 规范版本 | 软件包 | 版本 | 架构 |
|---|---|---|---|
| 2.0 | lsb-apache-2.0.49 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-celestia-1.3.1 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-expect-5.41.0 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-groff-1.19 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-lynx-2.8.5 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-python-2.3.4 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-rsync-2.6.2 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-samba-3.0.4 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-tcl-8.4.6 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-xpaint-2.7.0 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |
| 2.0 | lsb-xpdf-1.01 | 1.2.Lsb20 | IA32, IA64, PPC, PPC64, S390, S390X, x86_64, SRC |

2. http://www.linuxbase.org/download/

