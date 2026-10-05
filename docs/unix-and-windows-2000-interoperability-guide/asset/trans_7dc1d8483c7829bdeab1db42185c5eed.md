

## Telnet

在不在重定向符号上加引号的情况下，有如下示例：

```
C:\rexec hpux1 -l root cat /.profile > \windows\temp\root_profile
Password (hpux1.book.local):
```

在这里，我们在 `C:\windows\temp` 目录下拥有了 HP-UX 文件 `/profile` 的副本，名为 `root_profile`。顺便提一下，文本文件使用这种方法复制看起来完美，没有换行符问题。

## 9.7 Telnet

根据《Microsoft Windows 2000 Server TCP/IP 核心网络指南》第 828 页：“此连接性工具通过远程主机 telnet 服务器服务启动终端仿真。Telnet 提供 DEC VT 100、DEC VT 52 和 ANSI 仿真，使用基于连接的 TCP 服务？”然而，这意味着什么呢？

## 关于终端与仿真的

Telnet 起于 UNIX 世界。UNIX 世界中的第一批终端是电传打字（teletypes），本质上是打字机/打印机，通过串口连接到计算机。随着时间的推移，阴极射线管（CRT）也取代了这些电传打字机，它们也是串口设备，首先仿真电传打字机，然后有了了自己的特性。存在许多版本的终端，每个版本都有自己的功能。

对于你在 UNIX 系统上配置的每个终端，你必须在每个终端端口上运行一个 `get` 进程。该进程设置端口的初始字符并提示进行登录会话。在 HP-UX 系统上，当登录文件 `/etc/getdefs` 时，`get` 进程会设置终端以配置速度和最小设置。`tset` 命令在登录 HP-UX 系统时设置终端。它执行依赖于终端的处理，例如设置删除（erase）和杀死（kill）字符，或重置延迟，以及任何为了正确初始化终端所需的序列。它首先确定涉及的终端类型，然后进行必要的初始设置和模式设置。连接到每个 HP-UX 端口的终端类型在 `/etc/tty` 数据库中指定。终端类型名称可以在 `/usr/share/libterminfo` 目录下的文件中找到。如 `vi` 和文本版本的 SAM 等程序知道你正在使用什么终端，以便正常运行。它们查询由 `tset` 程序在登录时设置的 `TERM` 变量的值来确定你的终端。

所有处理对于登录和使用物理连接的终端都是必要的。Telnet 是一种方法，让你登录并在远程系统上工作，就像你在物理连接的系统上工作一样。它通过一个名为“终端仿真”的过程实现，软件产生一个伪装终端的屏幕。你在发送到远程系统的屏幕上输入命令，这些命令的输出会被传回你的屏幕。广泛仿真的终端类型包括 VT52、VT100 和 ANSI。通过 Telnet，你打开一个终端仿真器并使用它通过网络连接到远程系统。

## 9.7.2 Windows 2000 Telnet 客户端

微软在其可选的 `Services for UNIX` 产品中提供了一个 Telnet 服务器；客户端会自动安装。如果你运行“开始”→“运行...”，然后在“打开”框中输入 `telnet`，你将得到一个运行着 Telnet 客户端的命令提示符，如图 9–9 所示。

![](img/1c1e7552b53cca888836b6c6895bdb48_159_0.png)

图 9–9 Windows 2000 Telnet 客户端。该客户端在命令提示符窗口中运行。

Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

## 9.8 身份验证问题

微软在其可选的 `Services for UNIX` 产品中提供了一个 Telnet 服务器；客户端会自动安装。如果你运行“开始”→“运行...”，然后在“打开”框中输入 `telnet`，你将得到一个运行着 Telnet 客户端的命令提示符，如图 9–9 所示。

Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

The Windows 2000 Telnet 客户端非常基础，提供 VT100、VT52 和 ANSI（基于 VT100）仿真，并仅支持少数几个子命令和选项。Windows 2000 Telnet 的语法是 `telnet [host [port]]`，其中可选的 `host` 参数是目标系统的主机名，可选的 `port` 参数在不使用默认端口 23 的情况下为目标端口。输入 `telnet` 会启动 Telnet 客户端，它会提示你输入子命令。要连接到远程计算机，请在 `Microsoft Telnet>` 处输入 `open` 命令。例如：

```
Microsoft Telnet> open hpux1
```

要查看当前的 Telnet 客户端设置，使用 `display` 命令。例如：
Microsoft Telnet> display
Escape Character is 'CTRL+]'
WILL AUTH (NTLM Authentication)
LOCAL ECHO off
Sending both CR & LF
WILL TERM TYPE
Preferred Term Type is ANSI

NIS（网络信息服务）在 UNIX 世界中被广泛用于网络提供常用信息。Server 将 Windows 2000 变为启用 Active Directory 的 NIS 服务器。Windows 2000 服务器，在独立产品中提供，将在下一节介绍。

## 9.9 结论

我们在本章中查看的基础 TCP/IP 工具适用于 Windows 2000 和 HP-UX。在这些工具中，最广泛使用的无疑是 FTP 和 Telnet。HP-UX 包含了 FTP 服务器和客户端，而在 Windows 2000 上我们只有客户端——除非你安装服务器。我们将在下一节中介绍在独立产品中提供的 Windows 2000 服务器。

