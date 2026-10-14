

## 1.104.8 查找系统文件并将文件放置在正确的位置

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应彻底熟悉文件系统层次结构标准，包括典型文件位置和目录分类。本目标包括在 Linux 系统上查找文件和命令的能力。关键文件、术语和实用程序包括：find, locate, slocate, updatedb, whereis, which, /etc/updatedb.conf。 | 第 1 章，“探索文件系统”和“查找命令帮助” |

## Topic 110 The X Window System

## 1.110.1 安装和配置 XFree86

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应能够配置和安装 X 和 X 字体服务器。本目标包括验证视频卡和显示器是否受 X 服务器支持，以及为视频卡和显示器定制和调整 X。它还包括安装 X 字体服务器、安装字体并配置 X 使用字体服务器（可能需要在“Files”部分手动编辑 /etc/X11/XF86Config）。关键文件、术语和实用程序包括：XF86Setup, xf86config, xvidtune, /etc/X11/XF86Config, Xresources。 | 第 2 章，“Linux 图形桌面” |
| | | 第 15 章，“X Window System 高级配置” |

## 1.110.2 设置显示管理器

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够设置和自定义显示管理器。本目标包括打开或关闭显示管理器并更改显示管理器问候语。本目标包括更改显示管理器的默认位图。它还包括为 X 工作站配置显示管理器。本目标涵盖显示管理器 XDM（X Display Manager）、GDM（Gnome Display Manager）和 KDM（KDE Display Manager）。关键文件、术语和实用程序包括：/etc/inittab, /etc/X11/xdm/*, /etc/X11/kdm/*, /etc/X11/gdm/* | 第 2 章，“Linux 图形桌面” |
| | | 第 15 章，“X Window System 高级配置” |

## 1.110.4 安装和自定义窗口管理器环境

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 5 | 考生应能够自定义系统范围的桌面环境和/或窗口管理器，以展示对窗口管理器菜单和/或桌面面板菜单自定义程序的理解。本目标包括选择和配置所需 X 终端（xterm, rxvt, aterm 等），验证和解决 X 应用程序的库依赖问题，并将 X 显示导出到客户端工作站。关键文件、术语和实用程序包括：.xinitrc, .Xdefaults, xhost, DISPLAY 环境变量。 | 第 2 章，“Linux 图形桌面”和“配置 GNOME 和 KDE” 第 15 章，“X Window System 高级配置” |

## OBJECTIVES FOR EXAM 102

## Topic 105 Kernel

## 1.105.1 管理/查询运行时内核和内核模块

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 4 | 考生应能够管理和/或查询内核和内核可加载模块。本目标包括使用命令行实用程序获取有关当前正在运行的内核和内核模块的信息。它还包括根据需要手动加载和卸载模块。它还包括能够确定何时可以卸载模块以及模块接受哪些参数。考生应能够配置系统以使用除其文件名之外的名称加载模块。关键文件、术语和实用程序包括：/lib/modules/kernel-version/modules.dep, /etc/modules.conf & /etc/conf.modules, depmod, insmod, lsmod, rmmod, modinfo, modprobe, uname。 | 第 13 章，“探索内核组件” |

## 1.105.2 重新配置、构建和安装自定义内核和内核模块

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够从源代码自定义、构建和安装内核和内核可加载模块。本目标包括自定义当前内核配置、构建新内核以及根据需要构建内核模块。它还包括安装新内核以及任何模块，并确保引导管理器可以找到新内核和相关文件（通常位于 /boot 下，另见目标 1.102.2 了解有关引导管理器配置的更多详细信息）。关键文件、术语和实用程序包括：/usr/src/linux/*, /usr/src/linux/.config, /lib/modules/kernel-version/*, /boot/*; make, make targets, config, menuconfig, xconfig, oldconfig, modules, install, modules_install, depmod。 | 第 13 章，“配置和升级内核组件” |

## Topic 106 Boot, Initialization, Shutdown, and Run Levels

## 1.106.1 引导系统

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够引导系统通过启动过程。这包括向引导加载程序发出命令并在启动时向内核提供选项，并检查日志文件中的事件。关键文件、术语和实用程序包括：dmesg, /var/log/messages, /etc/conf.modules 或 /etc/modules.conf, LILO, GRUB。 | 第 9 章，“硬件初始化”和“配置引导加载程序” 第 13 章，“探索内核组件” |

## 1.106.2 更改运行级别并关闭或重新启动系统

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够管理系统的运行级别。本目标包括更改为单用户模式、关闭或重新启动系统。考生应能够在切换运行级别前提醒用户，并正确终止进程。本目标还包括设置默认运行级别。关键文件、术语和实用程序包括：shutdown, init, /etc/inittab。 | 第 9 章，“init 及其脚本” |

## Topic 107 Printing

## 1.107.2 管理打印机和打印队列

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够管理打印队列和用户打印作业。本目标包括监控打印服务器和用户打印队列并排除一般打印问题。关键文件、术语和实用程序包括：lpc, lpq, lprm, lpr, /etc/printcap | 第 3 章，“从命令行打印” 第 12 章，“网络打印服务” |

## 1.107.3 打印文件

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够管理打印队列和操作打印作业。本目标包括向配置的打印机队列添加和删除作业以及将文本文件转换为 PostScript 以便打印。关键文件、术语和实用程序包括：lpr, lpq, mpage。 | 第 3 章，“从命令行打印” 第 12 章，“网络打印服务” |

## 1.107.4 安装和配置本地和远程打印机

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够安装打印机守护进程，并安装和配置打印过滤器（例如，apsfilter, magicfilter）。本目标包括使本地和远程打印机可供 Linux 系统访问，包括 PostScript、非 PostScript 和 Samba 打印机。关键文件、术语和实用程序包括：lpd, /etc/printcap, /etc/apsfilter/*, /var/lib/apsfilter/*/, /etc/magicfilter/*/, /var/spool/lpd/*/. | 第 3 章，“从命令行打印” 第 12 章，“网络打印服务” |

## Topic 108 Documentation

## 1.108.1 使用和管理本地系统文档

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 4 | 考生应能够使用和维护 man 设施以及 /usr/share/doc/ 中的材料。本目标包括查找相关 man 页面、搜索 man 页面部分、查找与之相关的命令和 man 页面，以及配置对 man 源和 man 系统的访问。它还包括使用存储在 /usr/share/doc/ 中的系统文档并确定在 /usr/share/doc/ 中保留哪些文档。关键命令和术语：man, apropos, whatis, MANPATH。 | 第 1 章，“查找命令帮助” |

## 1.108.2 在互联网上查找 Linux 文档

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 3 | 考生应能够查找和使用 Linux 文档。本目标包括使用 Linux Documentation Project（LDP）、厂商和第三方网站、新闻组、新闻组存档和邮件列表等来源的 Linux 文档。 | 第 1 章，“查找命令帮助” |

## 1.108.5 通知用户系统相关问题

| Weight | Description of Objective | Location in This Book (Chapter, Heading) |
|---|---|---|
| 1 | 考生应能够通知用户有关系统相关问题的当前情况。本目标包括通过登录消息等自动化通信过程。关键文件、术语和实用程序包括：/etc/issue, /etc/issue.net, /etc/motd。 | 第 11 章，“用户安全问题” |

