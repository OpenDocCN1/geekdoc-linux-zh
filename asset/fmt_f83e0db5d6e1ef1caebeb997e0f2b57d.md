
# 在 SUSE Linux 上打印

第 24 章

在打印到你的 SMB 打印机之前，你应该有一个活跃的网络连接。你可以使用 `smbprint` 命令（Arthur Tridgill 在 Samba 软件包中程序集的一部分）打印到局域网打印机。`smbprint` 命令是一个 shell 脚本，位于 `/usr/doc/packages/samba/examples/printing` 目录下，使用 `smclient` 命令将文件发送到共享打印机。如果你想使用它打印到远程打印机，你需要配置并安装此脚本。有关 `smclient` 的详细信息，请参阅其 man 页面。

## Linux 打印命令

当然，你不一定需要使用 `yast` 命令来设置打印机。你可以直接编辑 `/etc/printcap`，但你应该清楚自己在做什么，并理解 `printcap` 的格式。此文件是系统本地和网络打印机的 ASCII 数据库，详细描述了每个打印机的功能。有关完整细节，请参阅用于命令的 `printcap` man 页面和用于文件布局的 `termcap` man 页面。

事实上，你可以为每个打印机创建多个条目，这对于你想打印不同尺寸的纸张、打印彩色或黑白文档或更改打印机托盘将非常有帮助。

SUSE Linux 使用 4.3BSD 行打印机池系统。这个经过时间考验的系统从 Berkeley 软件发行版的 UNIX 移植而来，具有许多功能和相关程序，支持后台打印、多个本地和网络打印机，以及对打印机和队列文档的控制。

Linux 打印溢存系统中使用的主要文件如下：

- `/etc/printcap`
- `/usr/sbin/lpd`
- `/usr/sbin/lpc`
- `/usr/bin/lpr`
- `/usr/bin/lrm`
- `/usr/bin/lpq`
- `/dev/printer`（指向 `/var/run/etc/rc.d` 的符号链接）

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

在打印到你的 SMB 打印机之前，你应该有一个活跃的网络连接。你可以使用 `smbprint` 命令（Arthur Tridgill Samba 软件包程序集的一部分）打印到局域网打印机。`smbprint` 命令是一个 shell 脚本，位于 `/usr/doc/packages/samba/examples/printing` 目录下，使用 `smclient` 命令将文件发送到共享打印机。如果你想使用它打印到远程打印机，你需要配置并安装此脚本。有关 `smclient` 的详细信息，请参阅其 man 页面。

## 简单格式

当然，你不一定需要使用 `yast` 命令来设置打印机。你可以直接编辑 `/etc/printcap`，但你应该清楚自己在做什么，并理解 `printcap` 的格式。此文件是系统本地和网络打印机的 ASCII 数据库，详细描述了每个打印机的功能。有关完整细节，请参阅用于命令的 `printcap` man 页面和用于文件布局的 `termcap` man 页面。

事实上，你可以为每个打印机创建多个条目，这对于你想打印不同尺寸的纸张、打印彩色或黑白文档或更改打印机托盘将非常有帮助。

SUSE Linux 使用 4.3BSD 行打印机池系统。这个经过时间考验的系统从 Berkeley 软件发行版的 UNIX 移植而来，具有许多功能和相关程序，支持后台打印、多个本地和网络打印机，以及对打印机和队列文档的控制。

Linux 打印溢存系统使用的主要文件如下：

- `/etc/printcap`
- `/usr/sbin/lpd`
- `/usr/sbin/lpc`
- `/usr/bin/lpr`
- `/usr/bin/lrm`
- `/usr/bin/lpq`
- `/dev/printer`（指向 `/var/run/etc/rc.d` 的符号链接）

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

## PostScript 打印机

如果你想要一个专为 PostScript 打印机设计的溢存，请尝试 Dave Chappell 的 PPR。PPR 适用于连接到并行、串口以及 AppleTalk (LocalTalk) 端口的打印机，以及其他网络接口。PPR 还像非 PostScript 打印机过滤器一样工作，并将多种图形格式转换为打印格式。你可以在 http://ppr-dist.tricoll.edu/pub/ppr/ 找到 PPR。

## 打印会计
