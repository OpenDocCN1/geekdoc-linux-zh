

其他运行级别反映了你希望系统如何使用。运行级别 2 是一个部分多用户状态，允许多个用户访问，但不提供 NFS 或 xinetd（eXtended InterNET services daemon）等网络服务。此级别适用于不属于网络的系统。运行级别 3 和运行级别 5 都运行一个完全可操作的 Linux 系统，具有多用户支持和远程文件共享访问。它们在使用的界面方面有所不同。运行级别 3 启动系统时使用命令行界面（也称为文本模式界面）。运行级别 5 启动系统时使用 X 会话，运行 X Window System 服务器并调用图形登录，使用显示管理器，如 gdm 或 xdm。如果你选择在安装期间使用图形登录，运行级别 5 将是你的默认运行级别。Linux 提供了两个键盘序列，让你在登录会话期间在这两者之间切换：CTRL-ALT-F1 从图形界面（运行级别 5）切换到命令行界面（运行级别 3），CTRL-ALT-F7 从命令行界面切换到图形界面。运行级别在表 27-3 中列出。

更改运行级别在特定运行级别出现问题时可能很有帮助。例如，如果你的视频卡未正确安装，那么任何尝试在运行级别 5 启动都可能会失败，因为该级别会立即启动你的图形界面。相反，你应该使用命令行界面，运行级别 3，来修复你的视频卡安装。

> Tip 你可以使用单用户运行级别（1）作为恢复模式状态，允许你在不运行 DNS 等服务的启动脚本的情况下启动系统。这在你尝试启动此类服务时系统挂起时很有帮助。网络被禁用，以及任何多用户访问。你也可以在启动提示符下使用 linux -s 进入运行级别 1。如果你想进入单用户状态并同时运行启动脚本，可以使用特殊的 s 或 S 运行级别。

| State | Description |
| --- | --- |
| System Runlevels (states) |  |
| 0 | Halt (do not set the default to this level); shuts down the system completely. |
| 1 | Administrative single-user mode; denies other users access to the system, but allows root access to the entire multiuser file system. Startup scripts are not run. (Use s or S to enter single-user mode and have startup scripts run.) |
| 2 | Multiuser, without network services like NFS, xinetd, and NIS (the same as 3, but you do not have networking). |
| 3 | Full multiuser mode with login to command-line interface; allows remote file sharing with other systems on your network. Also referred to as the text mode state. |
| 4 | Unused. |
| 5 | Full multiuser mode that starts up in an X session, initiating a graphical login; allows remote file sharing with other systems on your network (same as 3, but with graphical login). |
| 6 | Reboots; shuts down and restarts the system (do not set the default to this). |

TABLE 27-3 System Runlevels (States)

## initab Runlevels

当你的系统启动时，它使用 /etc/inittab 文件中 default init 条目指定的默认运行级别。例如，如果你的默认 init 运行级别是 5（图形登录），则 /etc/inittab 文件中的默认 init 条目将为

```
id:5:initdefault:
```

你可以通过编辑 /etc/inittab 文件并更改 init default 条目来更改默认运行级别。编辑 /etc/inittab 文件可能很危险。你应该非常小心地进行操作。作为示例，如果默认运行级别是 3（命令行），则 /etc/inittab 文件中默认运行级别的条目应如下所示：

```
id:3:initdefault:
```

你可以将 3 改为 5，以将默认运行级别从命令行界面（3）更改为图形登录（5）。仅更改此数字，不要更改其他内容。

```
id:5:initdefault:
```

> Tip 如果你的 /etc/inittab 文件损坏，你可以重新启动并在启动提示符下输入 linux single 启动系统，从而绕过 inittab 文件。然后你可以编辑该文件来修复它。

## Changing Runlevels with telinit

无论你从哪个运行级别启动，你都可以使用 telinit 命令从一个运行级别更改到另一个运行级别。如果你的默认运行级别是 3，你在运行级别 3 启动，但你可以使用 telinit 5 更改为运行级别 5。命令 telinit 0 关闭你的系统。在下一个示例中，telinit 命令更改为运行级别 1，即管理状态：

```
# telinit 1
```

telinit 实际上是 init 命令的符号链接（命令的另一个名称）。init 命令执行实际的启动操作，并在系统启动时自动调用。虽然你可以使用 init 更改运行级别，但最好使用 telinit。当作为 telinit 调用时，init 仅更改运行级别。

## runlevel Command

使用 runlevel 命令查看你当前运行的状态。它列出先前的状态，然后是当前状态。如果你没有更改状态，先前的状态将列为 N，表示没有先前的状态。这就是你启动时的状态。在下一个示例中，系统正在状态 3 运行，没有先前的状态更改。

```
# runlevel
N 3
```

## Shutdown

虽然你可以使用 telinit 命令和 0 状态关闭系统，但你也可以使用 shutdown 命令。shutdown 命令有一个时间参数

