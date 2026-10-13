
| named | 控制域名解析服务 (DNS) 的启动与停止 |
| network | 控制系统网络服务的启动与停止 |
| nfs | 控制网络文件系统 (NFS) 服务 |
| nfsfs | 控制挂载 NFS 文件系统 |
| nscd | 控制名称切换缓存（Name Switch Cache）守护进程 |
| pcmcia | 控制笔记本电脑的卡服务 |
| portmap | 控制远程过程调用 (RPC) 服务 |
| postgresql | 控制 PostgreSQL 数据库守护进程 |
| random | 控制随机数生成 |
| routed | 控制网络路由表守护进程 |
| rstatd | 控制 rpc.statd 内核统计守护进程 |
| rusersd | 控制 rpc.usersd 网络服务 |
| rwalld | 控制 rpc.rald 网络墙服务 |
| rwhod | 控制 rwh 守护进程 who 服务 |
| sendmail | 控制邮件传输服务 |
| single | init 在 Linux 启动到运行级别 1 或单用户管理模式时使用 |
| smb | 控制 Samba 守护进程和 nbd |
| snmpd | 控制简单网络管理协议 (SNMP) 守护进程 |
| sound | 保存并恢复混合器信息和电平 |
| squid | 控制 http 对象缓存服务 |
| syslog | 启动和停止系统日志服务 |
| xdm | 控制在运行级别 5 下启动或停止 X 显示管理器、K 显示管理器或 GNOME 显示管理器 |
| xfs | 启动并停止 X11 字体服务器 |
| xntpd | 启动并停止用于时间同步的网络时间协议 (NTPv3) 守护进程 |
| ypbind | 控制 NIS 绑定服务 |

# 系统启动与关机

第6 章

| 名称 | 描述 |
|---|---|
| ypasswdd | 控制 YP 密码服务器 |
| ypserv | 控制网络信息服务 |

![](img/fbfff30e42d507bc7531108a281d6cf4_188_0.png)

通常情况下，表 6.1 列出的每个脚本都设计为响应以下格式的命令：

`script {start|stop|status|restart}`

这意味着根据使用的语法，可以从其他程序控制特定的服务。

## 注意

并不是所有脚本都会响应 `restart` 或 `status` 调用。

## /etc/inittab 和系统状态

`/etc/inittab` 中最重要的脚本之一是 `rc.sysinit`，它是系统初始化脚本。当 `init` 解析 `/etc/inittab` 时，`rc.sysinit` 是第一个被找到并执行的脚本。这与其他版本的 UNIX 略有不同，其他版本可能直接将系统初始化命令包含在 `/etc/inittab` 文件中。

然而，与其他版本的 UNIX 一，Red Hat Linux 的 sysinit 脚本执行了以下部分或全部功能：

- 设置一些初始 `PATH` 变量
- 配置网络
- 启动虚拟内存交换分区
- 设置系统主机名
- 检查根文件系统是否存在可能需要修复
- 检查根文件系统配额
- 开启根文件系统的用户和组配额
- 重新挂载根文件系统为读写模式
- 清空挂载的文件表 `/etc/mtab`
- 将根文件系统输入 `mtab`
- 准备系统以加载模块
- 查找模块依赖
- 检查文件系统是否存在可能需要修复
- 挂载所有其他文件系统
- 清理 `/etc` 下的文件：`/etc/mtab`, `/etc/fastboot` 和 `/etc/nlogin`
- 删除 UUCP 锁文件
- 删除过期的子系统文件
- 删除过期的文件
- 设置系统时
- 开启交换分区
- 初始化串口
- 加载模块

对于第一个启动脚本来说，这些工作非常多，但这只是启动系统所需的众多步骤中的第一步。你已经看到 `init` 命令在 Linux 内核加载后运行。在 `init` 运行 `rc.sysinit` 后，它会运行 `rc.local`。如果你查看 Red Linux 的 `rc.local` 脚本，你会发现它获取计算机的操作系统名称和架构，并将其放入名为 `/etc/issue` 的文件中，该文件稍后用于登录提示符显示。

`rc.local` 的目的并不是提供一个用于系统特定初始化的地方（尽管有些人确实这么做）。在 BSD UNIX 中，`rc.local` 通常用于控制网络服务。Linux 并不总是使用相同的初始化脚本或启动方法。你可能会发现不同发行版之间的差异，例如 Red Hat Linux、Caldera、Slackware、SuSE 或其他。对于 Red Hat Linux，请使用图形界面工具（如 `tksys`、`ntsysysv` 或 `linfconf`）来控制你的系统服务。虽然你可以通过复制 `init.d` 目录下的框架脚本并设置正确的符号链接来手动操作，但你会发现合适的 Red Hat 工具可以满足你的大部分需求。

下一个 `init` 任务是运行每个运行级别的脚本。如果你查看 `rc.d` 目录的列表，你会看到各种 `rcXd` 目录，其中 X 是 0 到 6 的数字。如果你查看其中一个目录下的文件，你会发现每个文件都是 `init.d` 下某个脚本的链接，并带有一个特定服务的关联名称。例如，在 `rc3` 目录下你会发现以下内容：

```
lrwxrwxrwx root root 13 Apr 13 04:47 S05 -> ../init.d/xdm
lrwxrwxrwx root root 16 Apr 13 04:46 S08 -> ../init.d/autofs
lrwxrwxrwx root root 20 Apr 13 05:07 S15 -> ../init.d/postgresql
lrwxrwxrwx root root 15 Apr 13 05:00 S15 -> ../init.d/sound
lrwxrwxrwx root root 16 Apr 13 05:00 S20 -> ../init.d/rwalld
lrwxrwxrwx root root 15 Apr 13 05:00 S20 -> ../init.d/rwhod
lrwxrwxrwx root root 15 Apr 13 05:00 S25 -> ../init.d/squid
lrwxrwxrwx root root 13 Apr 13 05:07 S28 -> ../init.d/amd
lrwxrwxrwx root root 16 Apr 13 04:47 S30 -> ../init.d/mcserv
lrwxrwxrwx root root 15 Apr 13 05:00 S39 -> ../init.d/upassd
lrwxrwxrwx root root 15 Apr 13 05:07 S35 -> ../init.d/dhcpd
lrwxrwxrwx root root 15 Apr 13 05:04 S50 -> ../init.d/smpd
lrwxrwxrwx root root 16 Apr 13 05:00 S55 -> ../init.d/routed
lrwxrwxrwx root root 18 Apr 13 04:47 S60 -> ../init.d/mars-nwe
lrwxrwxrwx root root 15 Apr 13 05:49 S75 -> ../init.d/gated
lrwxrwxrwx root root 16 Apr 13 05:06 S80 -> ../init.d/ypserv
lrwxrwxrwx root root 17 Apr 13 05:07 S81 -> ../init.d/kernel
lrwxrwxrwx root root 15 Apr 13 05:07 S10 -> ../init.d/network
lrwxrwxrwx root root 17 Apr 13 05:07 S11 -> ../init.d/portmap
lrwxrwxrwx root root 15 Apr 13 05:07 S15 -> ../init.d/nfsfs
lrwxrwxrwx root root 16 Apr 13 05:20 S20 -> ../init.d/random
lrwxrwxrwx root root 16 Apr 13 05:07 S30 -> ../init.d/syslog
lrwxrwxrwx root root 13 Apr 13 05:07 S40 -> ../init.d/at
lrwxrwxrwx root root 15 Apr 13 05:00 S50 -> ../init.d/crond
lrwxrwxrwx root root 16 Apr 13 05:04 S54 -> ../init.d/pcmcia
lrwxrwxrwx root root 15 Apr 13 05:07 S55 -> ../init.d/inet
```
