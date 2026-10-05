

# 在 SuSE Linux 上打印
第 24 章

图 24.15
为你的远程打印机配置 apsfilter 软件。

![](img/cbac72550c7126a22162e94d91a0c360_766_0.png)

滚动对话框并为打印机（Printer）、纸张（Paper）和颜色（Color）部分添加设置。完成后，选择 ADD 选项保存你的设置。

> 注意
> 你应该能够 ping 通远程主机！不要忘记在 /etc/hosts 文件中为远程主机添加条目，或者确保你可以通过网络访问远程主机。

有关远程打印机条目的详细信息，请参阅 printcap man 页面并查找 rp 属性。

要设置打印到 SMB 打印机，你必须启用 Server Message Block 服务（通过作为 Samba 软件包一部分的 `smbd` 守护进程）。你还必须在 `/usr/bin` 目录下安装 `smbclient`，并且必须连接到 Windows 网络，并在 Windows 下启用打印机共享。

例如，在 Windows 95 下，导航到控制面板中的网络设备（通过开始菜单中的设置菜单）。点击“文件和打印共享”按钮，选择“我允许其他人在我的打印机上打印”，并点击 OK 按钮。点击网络窗口顶部的“标识”选项卡，记下你的计算机名称并关闭窗口。

# 24
在 SuSE Linux 上打印

重启后，打开“打印机”文件夹，右键点击你想要共享的打印机，选择“共享”菜单项。选择“共享为”（Shared As），输入共享名称和密码，并点击 OK 按钮。在运行 YaST 时你需要这些名称和密码信息。

# SUSE 系统管理
第三部分

要创建一个通过 Samba 打印到远程打印机的本地打印机条目，启动 YaST，选择系统管理，然后选择网络配置。滚动到“通过 YaST 连接打印机”菜单并按回车。你将看到图 24.16 所示的对话框。

图 24.16
通过 Samba 服务设置打印到远程打印机需要几个重要的配置参数。

![](img/cbac72550c7126a22162e94d91a0c360_767_0.png)

此对话框用于为远程打印机配置 `/etc/printcap` 条目。你需要指定远程服务器颜色使用、打印机类型、打印机名称、纸张格式、分辨率、打印服务名称，以及远程打印机的用户名和密码。

这些信息在对话框中输入。完成后，点击 Install 按钮创建条目。

> 注意
> 请查看第 16 章“Samba”，获取有关通过 Server Message Block (SMB) Windows 网络设置其他服务的信息。需要更多关于从 Linux 打印到 Windows 95/98/NT 系统上的打印机，或从 Windows 5 打印到 Linux 打印机的更详细说明吗？访问：http://sdb.suse.de/sdb/en/html/fehr_druck_1.html 获取有关在 SuSE Linux 上配置和排查打印故障的信息。你还可以在 http://samba.anu.edu.au/samba 获取有关 Samba 的最新信息。

在打印到你的 SMB 打印机之前，你应该有一个活跃的网络连接。你可以使用 `smbprint` 命令（Arthur Tridgill 在 Samba 软件包中程序集的一部分）打印到局域网打印机。`smbprint` 命令是一个 shell脚本，位于 `/usr/doc/packages/samba/examples/printing` 目录下，使用 `smclient` 命令将文件发送到共享打印机。如果你想使用它打印到远程打印机，你需要配置并安装此脚本。有关 `smclient` 的详细信息，请参阅其 man页面。

# 在 SUSE Linux 上打印
第 24 章

# Linux 打印命令

当然，你不一定需要使用 yast 命令来设置打印机。你可以直接编辑 `/etc/printcap`，但你应该清楚自己在做什么，并理解 `printcap` 的格式。此文件是系统本地和网络打印机的 ASCII 数据库，详细描述了每个打印机的功能。有关完整细节，请参阅用于命令的 printcap man 页面和用于文件布局的 termcap man 页面。

事实上，你可以为每个打印机创建多个条目，这对于你想打印不同尺寸的纸张、打印彩色或黑白文档或更改打印机托盘将非常有帮助。

SUSE Linux 使用 4.3BSD 行打印机池系统。这个经过时间考验的系统从 Berkeley 软件发行版的 UNIX 移植而来，具有许多功能和相关程序，支持后台打印、多个本地和网络打印机，以及对打印机和队列文档的控制。

Linux 打印溢存系统中使用的主要文件如下：

- /etc/printcap
- /usr/sbin/lpd
- /usr/sbin/lpc
- /usr/bin/lpr
- /usr/bin/lrm
- /usr/bin/lpq
- /dev/printer（指向 /var/run/etc/rc.d 的符号链接）

当你首次启动 SUSE Linux 时，shell 脚本 `lpd`（位于 `/etc/rc.d/` 下）启动 `lpd` 守护进程。`lpd` 守护进程是一个打印机服务器。在首次启动时，此类初始化脚本会让守护进程读取 `/etc/printcap` 文件并在后台运行，等待打印请求。打印请求通过 `lpr` 命令启动。例如，以下命令将你的文档打印到 `/var/spool/lpd/` 目录下的文件：

```
# lpr myfile.txt
```

其他的打印溢存命令可以跟踪你的请求。如果你正在打印大文档或多个小文件，可以使用 `lpq` 命令查看运行中的打印任务。例如，要一次打印多个文件，使用此命令：

![](img/cbac72550c7126a22162e94d91a0c360_768_0.png)

```
# lpr .x*
```

跟随该命令：

```
# lpq
```

输出如下：

| 状态 | 所有者 | 任务 | 文件 | 总大小 |
| :--- | :--- | :--- | :--- | :--- |
| active | root | 301 | .xboming | |

在打印到你的 SMB 打印机之前，你应该有一个活跃的网络连接。你可以使用 `smbprint` 命令（Arthur Tridgill Samba 软件包程序集的一部分）打印到局域网打印机。`smbprint` 命令是一个 shell 脚本，位于 `/usr/doc/packages/samba/examples/printing` 目录下，使用 `smclient` 命令将文件发送到共享打印机。如果你想使用它打印到远程打印机，你需要配置并安装此脚本。有关 `smclient` 的详细信息，请参阅其 man页面。

# Linux 打印命令

当然，你不一定需要使用 yast 命令来设置打印机。你可以直接编辑 `/etc/printcap`，但你应该清楚自己在做什么，并理解 `printcap` 的格式。此文件是系统本地和网络打印机的 ASCII 数据库，详细描述了每个打印机的功能。有关完整细节，请参阅用于命令的 printcap man 页面和用于文件布局的 termcap man 页面。

事实上，你可以为每个打印机创建多个条目，这对于你想打印不同尺寸的纸张、打印彩色或黑白文档或更改打印机托盘将非常有帮助。

SUSE Linux 使用 4.3BSD 行打印机池系统。这个经过时间考验的系统从 Berkeley 软件发行版的 UNIX 移植而来，具有许多功能和相关程序，支持后台打印、多个本地和网络打印机，以及对打印机和队列文档的控制。

Linux 打印溢存系统使用的主要文件如下：

- /etc/printcap
- /usr/sbin/lpd
- /usr/sbin/lpc
- /usr/bin/lpr
- /usr/bin/lrm
- /usr/bin/lpq
- /dev/printer（指向 /var/run/etc/rc.d 的符号链接）

当你首次启动 SUSE Linux 时，shell 脚本 `lpd`（位于 `/etc/rc.d/` 下）启动 `lpd` 守护进程。`lpd` 守护进程是一个打印机服务器。在首次启动时，此类初始化脚本会让守护进程读取 `/etc/printcap` 文件并在后台运行，等待打印请求。打印请求通过 `lpr` 命令启动。例如，以下命令将你的文档打印到 `/var/spool/lpd/` 目录下的文件：

```
# lpr myfile.txt
```

其他的打印溢存命令可以跟踪你的请求。如果你正在打印大文档或多个小文件，可以使用 `lpq` 命令查看运行中的打印任务。例如，要一次打印多个文件，使用此命令：

![](img/cbac72550c7126a22162e94d91a0c360_768_0.png)

```
# lpr .x*
```

跟随该命令：

```
# lpq
```

输出如下：

| 状态 | 所有者 | 任务 | 文件 | 总大小 |
| :--- | :--- | :--- | :--- | :--- |
| active | root | 301 | .xboming | |

# 简单格式

当然，你不一定需要使用 yast 命令来设置打印机。你可以直接编辑 `/etc/printcap`，但你应该清楚自己在做什么，并理解 `printcap` 的格式。此文件是系统本地和网络打印机的 ASCII 数据库，详细描述了每个打印机的功能。有关完整细节，请参阅用于命令的 printcap man 页面和用于文件布局的 termcap man 页面。

事实上，你可以为每个打印机创建多个条目，这对于你想打印不同尺寸的纸张、打印彩色或黑白文档或更改打印机托盘将非常有帮助。

SUSE Linux 使用 4.3BSD 行打印机池系统。这个经过时间考验的系统从 Berkeley 软件发行版的 UNIX 移植而来，具有许多功能和相关程序，支持后台打印、多个本地和网络打印机，以及对打印机和队列文档的控制。

Linux 打印溢存系统使用的主要文件如下：

- /etc/printcap
- /usr/sbin/lpd
- /usr/sbin/lpc
- /usr/bin/lpr
- /usr/bin/lrm
- /usr/bin/lpq
- /dev/printer（指向 /var/run/etc/rc.d 的符号链接）

当你首次启动 SUSE Linux 时，shell 脚本 `lpd`（位于 `/etc/rc.d/` 下）启动 `lpd` 守护进程。`lpd` 守护进程是一个打印机服务器。在首次启动时，此类初始化脚本会让守护进程读取 `/etc/printcap` 文件并在后台运行，等待打印请求。打印请求通过 `lpr` 命令启动。例如，以下命令将你的文档打印到 `/var/spool/lpd/` 目录下的文件：

```
# lpr myfile.txt
```

其他的打印溢存命令可以跟踪你的请求。如果你正在打印大文档或多个小文件，可以使用 `lpq` 命令查看运行中的打印任务。例如，要一次打印多个文件，使用此命令：

![](img/cbac72550c7126a22162e94d91a0c360_768_0.png)

```
# lpr .x*
```

跟随该命令：

```
# lpq
```

输出如下：

| 状态 | 所有者 | 任务 | 文件 | 总大小 |
| :--- | :--- | :--- | :--- | :--- |
| active | root | 301 | .xboming | |

# PostScript 打印机

如果你想要一个专为 PostScript 打印机设计的溢存，请尝试 Dave Chappell 的 PPR。PPR 适用于连接到并行、串口以及 AppleTalk (LocalTalk) 端口的打印机，以及其他网络接口。PPR 还像非 PostScript 打印机过滤器一样工作，并将多种图形格式转换为打印格式。你可以在 http://ppr-dist.tricoll.edu/pub/ppr/ 找到 PPR。

# 打印会计

如果你知道你或用户打印了多少，成本是多少，Linux 提供了几种不同的命令来设置会计报告并跟踪打印机使用情况。请查看 `pac` 命令的主页以跟踪使用和成本。你还需要阅读 `printcap` 数据库的主页以了解如何启用打印会计。

# 红外打印机支持

对于那些幸运拥有支持红外的打印机（如佳能 BJC 80 或 BJC 50）和带有红外端口的 Linux 系统的人来说，有一个好消息：你不需要打印线就可以打印！最近的 Linux 设备驱动开发产生了红外打印（和网络）支持，并且最新的 Linux 内核内置了 IrDA 支持。IrDA 支持作为一系列可加载内核模块提供，并支持系统日志、网络、串口仿真和打印等功能。

你需要阅读位于 `/usr/doc/howto/en` 目录下的 Werner Heuser 的 IR-HOWTO。你还需要下载最新的 IrDA 工具程序集

