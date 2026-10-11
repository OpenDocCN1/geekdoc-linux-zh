
`/opt` 目录包含可选程序——通常是大型程序。如果你下载了新版本的 Netscape，它可能会安装在这里。K 桌面环境默认安装在 `/opt` 目录。

# /proc 目录

`/proc` 目录并不包含实际的文件；它是由 Linux 动态生成的。它包含了关于运行进程和硬件状态的信息。你可以通过对这些文件使用 `cat` 命令获取硬件设备或运行进程的信息。例如，你可以通过以下命令获取内核支持的文件系统信息：

```
/proc/filesystems
```

或者，你可以运行此命令获取硬件设备使用的中断：

```
/proc/interrupts
```

通常，`/proc` 目录是高级用户的区域，但偶尔你可能需要从中获取信息。

# /root 目录

`/root` 目录是 root 用户的家目录。当你登录时，执行 `cd` 命令会进入此目录。它与其他家目录分开，以便 root 用户维护系统。

# /sbin 目录

`/sbin` 目录包含更多的二进制文件。该目录的作用与 `/bin` 类似，但 `/sbin` 包含了系统相关的二进制文件。通常你必须是 root 用户才能使用这些文件。

# /tmp 目录

`/tmp` 目录包含临时文件。对于计划删除的文件，这里是一个很好的存放处。许多程序会自动在 `/tmp` 中创建临时文件。

# /usr 目录

`/usr` 目录及其子目录 `/usr/local` 通常位于独立的分区上。`/usr` 目录是较大的目录之一，因为它包含了系统中大部分软件：X11 目录、开发工具、库文件和游戏。

`/usr/local` 内的目录布局模仿了 `/usr`。

# /var 目录

`/var` 目录包含变量文件，主要是系统日志。根据一般原则，除非你想监控 Linux 的健康状况，否则 `/var` 下的文件并不感兴趣。

结论 这篇 Linux 入门指南应该让你对如何在 Linux CLI 中操作有一个良好的了解。大多数用户都是 Linux 新手，只想把 Linux 当作工作站使用。桌面操作系统可能不需要成为 Shell 提示符大师，但如果需要，了解如何操作 Shell 永远无坏处。你甚至可能会发现，很多情况下使用 CLI 更好。Linux 的棒之处在于，你不需要在 GUI 和 CLI 之间做出选择；你可以启动 KDE（或任何你喜欢的窗口管理器/桌面环境），打开多个控制窗口，尽情发挥吧！

# 附录 B：在线资源

![](img/dd467368d25ae4aa349c6d8be90f7ffb_394_0.png)

在本书中，你已经学习了许多 Linux 配置技巧。随着越来越多的网站致力于照顾和喂养这头如今已被驯服的猛兽，Linux 知识每天都在增长。

本附录按类别列出了获取更多 Linux 信息和知识的互联网 URL。

## 通用 Linux 信息

- 红帽 Linux | http://www.redhat.com
- Linux | http://www.linux.org
- Linux 内内核 | ftp://ftp/ftp.kernel.org
- X Window | http://www.x.org
- Prima Linux | http://www.primalux.com
- Linux Planet | http://www.linuxplanet.com
- Freshmeat | http://freshmeat.net

## 窗口管理器和桌面环境

- GNOME | http://www.gnome.org
- KDE | http://www.kde.org
- Sawfish | http://sawmill.sourceforge.net
- 桌面主题 | http://www.themes.org

### 编辑器

- emacs | http://www.gnu.org/software/emacs
- jed | http://space.mit.edu/~davis/jed.html
- joe | ftp://ftp.std.com/src/editors/
- Vim | http://www.vim.org

### 图形

| Electric Eyes | http://www.labs.redhat.com/ee.shtml |
| GIMP | http://www.gimp.org |
| xfig | http://epb1.lbl.gov/homepages/Brian_Smith/xfig/ |

## 互联网

- elm | http://www.instinct.org/elm
- fwhois | http://www.oxygene.500mhz.net/software.html |
- gftp | http://gftp.seul.org
- Lynx | http://lynx.browser.org
- mutt | http://www.mutt.org
- ncftp | http://www.ncftp.com
- Netscape | http://www.netscape.com
- pine | http://www.Washington.edu/pine/
- slrn | http://space.mit.edu/~davis/slrn.html
- tin | http://www.tin.org
- trn | http://www.clari.net/~-wayne
- ytalk | http://www.iagora.com/~espel/ytalk/ytalk.html |

## 游戏

- Linux 游戏 | http://www.linuxgames.com

# 附录 C：硬件兼容性日志

垂直同步率 ______________________________________________________

## 硬盘

| 制造商 | 型号 | 大小 | 类型 |
| :--- | :--- | :--- | :--- |
| SCSI | | | |
| IDE | | | |

## 网卡

| 制造商 | 型号 |
| :--- | :--- |
| | |

## CD-ROM 驱动器

| 制造商 | 型号 | 大小 |
| :--- | :--- | :--- |
| | | |

## 软盘驱动器

| 制造商 | 型号 | 大小 |
| :--- | :--- | :--- |
| | | |

## 调制解调器

| 制造商 | 型号 | 传输速度 |
| :--- | :--- | :--- |
| | | |

## 打印机

| 制造商 | 型号 |
| :--- | :--- |
| | |

### 鼠标

| 制造商 | 型号 | 类型 |
| :--- | :--- | :--- |
| PS/2 | | |
| 串口 | | |

### 键盘

| 制造商 | 型号 | 键键数 | 语言 |
| :--- | :--- | :--- | :--- |
| | | | |

## SCSI 卡及设备

| 制造商 | 型号 | 控制的设备类型 |
| :--- | :--- | :--- |
| | | |

## IDE 适配器

| 制造商 | 型号 | 控制的设备类型 |
| :--- | :--- | :--- |
| | | |

## ZIP/JAZ 驱动器

| 制造商 | 型号 | 大小 |
| :--- | :--- | :--- |
| | | |

## 磁带驱动器

| 制造商 | 型号 | 大小 |
| :--- | :--- | :--- |
| | | |

## 声卡

| 制造商 | 型号 |
| :--- | :--- |
| | |

## 扫描仪

| 制造商 | 型号 |
| :--- | :--- |
| | |

## 红外设备

| 制造商 | 型号 | 控制的设备类型 |
| :--- | :--- | :--- |
| | | |

## 摇杆

| 制造商 | 型号 |
| :--- | :--- |
| | |

## 串口设备

| 制造商 | 型号 | 控制的设备类型 |
| :--- | :--- | :--- |
| | | |

## 并行设备

| 制造商 | 型号 | 控制的设备类型 |
| :--- | :--- | :--- |
| | | |

## PCMCIA

| 制造商 | 型号 | 卡片类型 |
| :--- | :--- | :--- |
| | | |

## BIOS 设置

网络设置

# 附录 D：高级配置参考

文件系统配置文件 (/etc/fstab)

磁盘几何结构

容量限制

LILO

查看文件系统信息

文件系统结构：概览

在本附录中，介绍了几个主题。每个主题都属于高级级内容，所以不要觉得你一开始就必须攻克它们。随着你对 Linux 的越来越了解，你可以参考本附录来帮助解决你可能会遇到的一些更棘手的配置问题。

## 文件系统配置文件 (/etc/fstab)

作为 Linux 系统一个重要的配置文件，`/etc/fstab` 包含了挂载设备所需的所有信息。该文件共有六字段：

- `fs_spec`. 描述要挂载的设备。
- `fs_file`. 描述文件系统的挂载点。交换分区在此字段中应为空或 `swap`。
