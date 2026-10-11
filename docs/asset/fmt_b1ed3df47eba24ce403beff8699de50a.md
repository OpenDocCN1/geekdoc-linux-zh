
| `/boot/System.map` | Linux 内核映射（将内核地址映射为函数和变量的名称） |
| `/boot/vmlinuz` | Linux 内核（操作系统的核心） |
| `/etc/apache2/htpd.conf` | Apache Web 服务器的配置文件（Debian 和 MEPIS） |
| `/etc/apt/sources.list` | 列出高级打包工具 (APT) 获取软件包来源的配置文件——FTP 或网站或 CD-ROM——（Debian、MEPIS、Ubuntu 和 Xandros） |
| `/etc/at.allow` | 允许使用 `at` 命令安排稍后执行作业的用户名 |
| `/etc/at.deny` | 禁止使用 `at` 命令的用户名 |
| `/etc/bashrc` | `bash` shell 的系统级函数和别名（Fedora Core） |
| `/etc/bash.bashrc` | `bash` shell 的系统级函数和别名（Debian、MEPIS、SUSE、Ubuntu 和 Xandros） |
| `/etc/cups/cupsd.conf` | 通用 UNIX 打印系统 (CUPS) 调度程序的打印机配置文件 |
| `/etc/fonts` | 包含字体配置文件的目录。（特别是，你可以将本地字体配置设置放在 `/etc/fonts/local.conf` 文件中。） |
| `/etc/fstab` | 可用于挂载的文件系统信息以及每个文件系统的挂载位置 |
| `/etc/group` | 组信息 |
| `/etc/grub.conf` | Fedora Core 和 SUSE 中 GRUB 引导加载程序的配置 |
| `/etc/hosts` | IP 地址及其对应主机名的列表 |
| `/etc/hosts.allow` | 允许访问此系统互联网服务的主机 |
| `/etc/hosts.deny` | 禁止访问此系统互联网服务的主机 |
| `/etc/httpd/conf/httpd.conf` | Apache Web 服务器的配置文件（Fedora Core） |
| `/etc/init.d` | 包含用于启动和停止各种服务器的脚本的目录 |
| `/etc/inittab` | 用于启动所有其他进程的 `init` 进程使用的配置文件 |
| `/etc/issue` | 包含在显示文本模式登录提示之前打印的消息的文件（通常是发行版名称和版本号） |
| `/etc/lilo.conf` | Linux Loader (LILO) 的配置——可从磁盘加载操作系统之一的引导加载程序（仅在使用 LILO 引导加载程序时存在） |
| `/etc/login.defs` | 创建用户账户的默认信息，由 `useradd` 命令使用 |
| `/etc/modprobe.conf` | 可加载内核模块的配置文件，由 `modprobe` 命令使用（Fedora Core 和 SUSE） |
| `/etc/modules.conf` | 可加载模块的配置文件（Debian、MEPIS 和 Xandros） |
| `/etc/mtab` | 当前已挂载文件系统的相关信息 |
| `/etc/passwd` | 所有用户账户的信息。（实际密码存储在 `/etc/shadow` 中。） |
| `/etc/profile` | `bash` shell 的系统级环境和启动文件 |
| `/etc/profile.d` | 包含 `/etc/profile` 脚本执行的脚本文件（以 `.sh` 结尾）的目录 |
| `/etc/init.d/rcS` | Debian、MEPIS、SUSE、Ubuntu 和 Xandros 中的 Linux 初始化脚本 |
| `/etc/rc.d/rc.sysinit` | Fedora Core 中的 Linux 初始化脚本 |
| `/etc/shadow` | 包含所有用户账户加密密码的安全文件（仅 `root` 可读） |
| `/etc/shells` | 用户可在系统上使用的所有 shell 的列表 |
| `/etc/skel` | 存储 `.bash_profile` 等文件初始版本的目录，这些文件会被复制到新用户的主目录中 |
| `/etc/sysconfig` | Linux 配置文件（Fedora Core 和 SUSE） |
| `/etc/sysctl.conf` | 包含在系统启动时由 `sysctl` 读取并设置的内核参数的配置文件 |
| `/etc/termcap` | 终端功能与选项的数据库（Fedora Core 和 SUSE） |
| `/etc/udev` | 包含 `udev` 配置文件的目录——`udev` 是提供动态命名热插拔设备并在 `/dev` 目录中创建设备文件能力的程序 |
| `/etc/X11` | 包含 X 窗口系统 (X11) 以及各种显示管理器（如 `gdm` 和 `xdm`）配置文件的目录 |
| `/etc/X11/XF86Config` 或 `/etc/X11/XF86Config-4` | XFree86 X11 的配置文件（Debian、MEPIS 和 Xandros） |
| `/etc/X11/xorg.xof` | X.org X11——X 窗口系统的配置文件（Fedora Core、Ubuntu 和 SUSE） |
| `/etc/xinetd.conf` | `xinetd` 守护程序的配置，该程序按需启动多个互联网服务 |
| `/etc/yum.conf` | `yum` 软件包更新和安装程序的配置（Fedora Core） |
| `/var/log/apache2` | Web 服务器访问和错误日志（Debian 和 MEPIS） |
| `/var/log/cron` | 包含来自运行计划作业的 `cron` 进程消息的日志文件 |
| `/var/log/boot.msg` | 包含启动消息的文件（SUSE） |
| `/var/log/dmesg` | 包含启动消息的文件（Debian、Fedora Core、MEPIS、Ubuntu 和 Xandros） |
| `/var/log/httpd` | Web 服务器访问和错误日志（Fedora Core） |
| `/var/log/messages` | 系统日志 |

# 监控系统性能

作为系统管理员，您必须密切关注 Linux 系统的运行状况。您可以通过查看以下信息来监控系统的整体性能：

- 中央处理器（CPU）使用率
- 物理内存使用量
- 虚拟内存（交换空间）使用量
- 硬盘使用量

Linux 附带了许多实用工具，您可以使用它们来监控一个或多个这些性能参数。在这里，我将介绍其中一些实用工具，并展示如何理解这些工具所呈现的信息。

## 使用 `top` 实用工具

若要查看占用 CPU 时间最多的前几个进程（即 CPU 使用率最高的进程），您可以使用文本模式的 `top` 实用工具。要在终端窗口（或文本控制台）中启动该实用工具，请输入 `top`。随后，`top` 实用工具会显示一个文本屏幕，其中列出了当前进程，并按照 CPU 使用率排序，同时包含其他各种信息，例如内存和交换空间使用情况。图 1-6 展示了 `top` 实用工具的一个典型输出示例。

`top` 实用工具每五秒刷新一次显示。如果您在窗口中让 `top` 持续运行，您可以持续监控 Linux 系统的状态。若要退出 `top`，请按下 Q 或 Ctrl+C，或者关闭终端窗口。

![](img/792720823146d68f19fd50c99ebfce4b_418_0.png)

输出屏幕的前五行（参见图 1-6）提供了系统的摘要信息。以下是这五行显示的内容：

- 第一行显示当前时间、系统已运行的时长、登录用户的数量，以及三个**负载平均值**——过去 1、5 和 15 分钟内就绪等待运行的平均进程数。
- 第二行列出进程的总数以及这些进程的状态。
- 第三行显示 CPU 使用情况——用户进程占用的 CPU 时间百分比、系统（内核）进程占用的百分比，以及 CPU 空闲的时间百分比。
- 第四行显示物理内存的使用情况——总量、已使用量、可用量，以及分配给缓冲区（例如用于从硬盘读取数据）的量。
- 第五行显示虚拟内存（或交换空间）的使用情况——交换空间总量、已使用量、可用量，以及正在被缓存的量。

摘要信息下方出现的表格（参见图 1-6）列出了当前进程的信息，并按 CPU 时间使用量降序排列。表 1-10 总结了 `top` 显示表格中各列标题的含义。

**表 1-10** `top` 实用工具输出中列标题的含义

| 标题 | 含义 |
| :--- | :--- |
| PID | 进程 ID |
| USER | 进程运行所基于的用户名 |
| PR | 进程的优先级 |
