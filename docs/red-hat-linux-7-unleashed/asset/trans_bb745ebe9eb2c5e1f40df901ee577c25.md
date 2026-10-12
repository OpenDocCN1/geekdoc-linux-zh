
# 初始化流程与启动脚本

根据 Red Hat 团队的说法，这种方法正在成为 Linux 世界的标准，因为它“更容易使用，并且更强大、更灵活”。基于发行版销售数据的最新估算表明，近 60% 的 Linux 用户正在使用 Red Hat 或基于 Red Hat 的 Linux 系统。事实上，其他发行版，如 Caldera 的 OpenLinux，也使用了类似的初始化方案（尽管脚本的命名约定有所不同）。

当你在本章稍后的“`linuxconf` 与管理系统服务”部分了解到 `linuxconf` 客户端时，你也会明白为什么对于 Red Hat Linux 用户来说，启动配置甚至更加容易。

本节描述了 Linux 的启动方式，并详细说明了用于准备系统以供使用的启动脚本的功能。一个需要注意的重要概念是各种运行级别（runlevels）或 Linux 系统状态的使用。

系统状态源于根据对系统进行维护的形式来分离系统运行方式的需要。这类似于在较旧的 PC 上执行软件或硬件升级，通常这需要重启或关闭并重新启动计算机。然而，如今，通过新的软件和硬件技术，这种做法在一定程度上已被避免。*可热插拔* 的硬件和软件意味着你可以即时更改硬盘、PC 卡或相关软件——在系统运行过程中（例如，使用 `insmod` 和 `rmmod` 命令加载或卸载 Linux 内核模块）。

你可以在 `/etc/inittab` 文件或系统初始化表中找到各种运行级别的描述。虽然 Linux 在几个级别上与其他版本的 UNIX 有所不同，但 Red Hat Intel/Linux 主要使用以下级别（如 `/etc/inittab` 中所列出的）：

```text
# The runlevels used by RHS are:
# 0 - halt (Do NOT set initdefault to this)
# 1 - Single user mode
# 2 - Multiuser, without NFS (The same as 3, if you do not have networking)
# 3 - Full multiuser mode
# 4 - unused
# 5 - X11
# 6 - reboot (Do NOT set initdefault to this)
```

在旧版本的 Red Hat Linux 中，你在这个列表下方会发现一行看起来像这样的内容：

```text
id:3:initdefault:
```

这一行指定了运行级别 3 并使用了 initdefault 关键字，它告诉 Linux 在加载内核后进入运行级别 3（完全多用户模式）（有关其他关键字，请参阅 inittab 的手册页）。然而，在较新版本的 Red Hat Linux 中，如果在安装过程中配置了 X11，现在最有可能启动到运行级别 5，其 /etc/inittab 条目如下所示：

```text
id:5:initdefault:
```

这意味着，如果你配置了 X11，Red Hat Linux 现在将直接启动到 X 窗口系统，前提是你选择启动到图形登录（使用 gdm 客户端，即 GNOME 显示管理器）。详情请参阅第 5 章“窗口管理器”。

下一节描述了这些运行级别，包括初始化表中的第一个启动脚本 /etc/rc.d/rc.sysinit，或系统初始化脚本，该脚本在启动时由 init 命令运行一次。它还涵盖了 /etc/rc.d 目录结构以及这些脚本中的一些功能。

## init 和 /etc/inittab

init 手册页指出：“init 是所有进程之父。”它的主要角色是从存储在 /etc/inittab 中的脚本创建进程。Linux 在加载内核后启动其进程的方式很多来自另一个 UNIX 系统，即 System V。事实上，Linux 的 init 命令与 System V init 命令兼容，并且启动脚本模仿了这种方法。虽然 init 作为“内核启动的最后一步”开始，但它初始化并配置系统以供使用的第一个命令。

你可以通过在控制台或 X11 终端窗口的命令行上使用 pstree 命令来查看这一过程的证据。在命令行中输入

```text
# pstree
```

按下 Enter 后，你将看到一个进程树列表，看起来大致如下（特别是如果你使用的是笔记本电脑，因为有高级电源管理和 cardmgr PCMCIA 管理器守护进程）：

```text
init+-appd
    |-atd
    |-2*[automount]
    |-battery_applet
    |-cardmgr
    |-cron
    |-deskguide_applet
    |-gdm+-X
    |   `---gnome-session
    |-gmc
    |-gnome-name-serv
    |-gnome-smpfox
    ...
```

尽管此处未显示 *pstree* 的完整输出，但你可以看到 *init* 作为第一个进程启动系统，并作为所有后续进程的父进程。*init* 通过解析 */etc/inittab* 并根据默认或所需的运行级别运行 */etc/rc.d* 中的脚本来工作。每个脚本都可以启动或停止服务，例如网络、邮件、新闻或 Web 服务。

以下是 */etc/rc.d* 目录的列表：

- init.d/
- rc*
- rc.local*
- rc.sysinit*
- rc0.d/
- rc1.d/
- rc2.d/
- rc3.d/
- rc4.d/
- rc5.d/
- rc6.d/

在 *init.d* 目录下，你可以找到许多用于启动和停止服务的脚本。这里没有给出每个脚本的详细信息，但你应该能够通过它们的名称和简短描述来猜测其中一些脚本的功能，如表 9.1 所示。请注意，你拥有的脚本数量可能比所示的多或少，因为一些脚本是服务包的一部分，将在安装软件时安装。

**表 9.1 Red Hat Linux 系统初始化脚本**

| 名称 | 描述 |
| :--- | :--- |
| amd | 控制自动挂载守护进程 |
| anacron | 调度控制 |
| apmd | 目录包含 *apmd.init*，用于电源管理和日志记录控制 |
| arpwatch | 跟踪以太网和互联网协议地址配对 |
| atd | 控制 *at*（个人调度）守护进程 |
| autofs | 控制 *autofs* 文件系统守护进程 |
| bootparamd | 可用于网络启动旧的 Sun 工作站 |
| crond | 控制 *cron* 系统调度守护进程 |
| dhcpd | 控制动态主机配置协议守护进程 |
| functions | 用于 *init* 脚本的 Shell 脚本函数 |
| gated | 控制路由网关守护进程 |
| gpm | 控制控制台鼠标服务器（控制台剪切和粘贴实用程序） |
| halt | 控制如何处理关闭和重启 |
| httpd | 控制 Apache Web 服务器和 HTTP 服务 |
| identd | 控制用户标识服务器 |
| innd | 控制 InterNet 新闻系统 |
| irda | 启动/停止 IrDA 守护进程 |
| isdn | 控制 ISDN 服务 |
| kdcrotate | Kerberos 配置脚本 |
| keytable | 控制键盘映射加载 |
| killall | 用于 amd、crond、inet、kernel、mars-nwe 和 nfs 初始化脚本终止进程的实用脚本 |
| krbs5server | 启动/停止 Kerberos 服务器 |
| kudzu | 硬件探测/配置控制 |
| ldap | 控制目录访问协议守护进程 |
| linuxconf | Red Hat linuxconf 工具的实用脚本 |
| lpd | 控制打印后台作业服务 |
| mars-nwe | 控制与 Netware 兼容的系统服务 |
| mcserv | 控制 Midnight Commander 远程服务 |
| named | 控制域名服务的启动和停止 |
| netfs | 控制 NFS、SMB、NCP 挂载 |
| network | 控制系统网络的启动和停止 |
| nfs | 控制网络文件系统服务 |
| nfslock | 控制 NFS 文件锁定 |
| nfsfs | 控制 NFS 文件系统的挂载 |
| nscd | 控制名称切换缓存守护进程 |
| pcmcia | 控制笔记本电脑的卡服务 |
| phntpd | 控制 HTTP 加速器 |
| portmap | 控制远程过程调用服务 |
| postgresql | 控制 PostgreSQL 数据库守护进程 |
| ppoe | 启动或停止 ADSL 会话 |
| pulse | 控制集群监视器 |
| pxe | 控制远程启动服务器 |
| random | 控制随机数生成 |
| rarpd | 控制 RARP 守护进程 |
| reconfig | 管理 anaconda 的 reconfig 操作 |
| routed | 控制网络路由表守护进程 |
| rstated | 控制 rpc.stated 网络内核统计守护进程 |
| rusersd | 控制 rpc.rusersd 网络服务 |
| rwalld | 控制 rpc.rwalld 网络墙服务 |
| rwhod | 控制 rwhod 守护进程网络 rwho 服务 |
| sendmail | 控制邮件传输服务 |
| single | 当 Linux 启动到运行级别 1 或单用户管理模式下由 init 使用 |
| smb | 控制 Samba smbd 和 nmbd 守护进程 |
| snmpd | 控制简单网络管理协议守护进程 |
| sound | 保存和恢复混音器信息和级别 |
| squid | 控制 httpd 对象缓存服务 |
| sshd | 控制 OpenSSH 服务器 |
| syslog | 启动和停止系统日志服务 |
| xdm | 控制是否为运行级别 5 启动或停止 X 显示管理器、K 显示管理器或 GNOME 显示管理器 |
| xfs | 启动和停止 X11 字体服务器 |
| xinetd | 启动和停止 xinetd 守护进程 |
| xntpd | 启动和停止用于时间同步的网络时间协议（NTPv3）守护进程 |
| ypbind | 控制 NIS 绑定服务 |
| yppasswd | 控制 YP 密码服务器 |
| ypserv | 控制网络信息服务 |

通常，表 9.1 中列出的每个脚本都设计为响应以下形式的命令：

```text
script {start|stop|status|restart}
```

这意味着，取决于使用的语法，特定的服务可以由其他程序控制。

> **注意**
> 并非所有脚本都会响应重启或状态调用。
