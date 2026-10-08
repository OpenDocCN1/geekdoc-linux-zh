

会弹出 tus 窗口，显示正在从 x 目录（**xmenu2.bmp**）复制的文件名称。

![](img/75f39fc91296b889c0653851accdfd46_1232_0.png)

在运行 FTP 时，你可以选择多种选项。请注意图 16-17 中的“传输类型：”为二进制。这是我在发起传输之前选择的选项之一。

虽然这种功能不如 NFS 的文件共享功能那么全面，但它被广泛用于在系统之间复制文件，因此可以在 Windows 和 UNIX 互操作性中发挥作用。

在这个例子中，我使用图标来指定要复制的信息。你也可以使用 FTP 命令。以下是 FTP 的概述，包括从命令行运行它的示例和命令摘要。

| 文件传输协议 (FTP) | 将一个或多个文件从一个系统传输到另一个系统，例如从 Windows 到 UNIX。以下示例显示了将文件 /tmp/krsort.c 从 system2（远程主机）复制到 system1（本地主机）的本地目录。 |
| :--- | :--- |

```
$ ftp system2
Connected to system2.
system2 FTP server (Version 16.2) ready.
Name (system2:root): root
Password required for root.
Password:
User root logged in.
Remote system type is UNIX.
Using binary mode to transfer files.
ftp> cd /tmp
CWD command successful
ftp> get krsort.c
PORT command successful
Opening BINARY mode data connection for krsort.c
Transfer complete.
2896 bytes received in 0.08 seconds
```

-   注释
    -   发出 ftp 命令
    -   登录到 system2
    -   输入密码
    -   在 system2 上 cd 到 /tmp
    -   获取 krsort.c 文件
    -   ftp> bye | 退出 ftp
    -   再见。
    -   $

在这个示例中，两个系统都运行 UNIX；但是，你通过 **FTP** 发出的命令是与操作系统无关的。上面用于改变目录的 `cd` 和 `get` 命令适用于运行 **FTP** 的任何操作系统。如果你对几个 **FTP** 命令变得熟悉，你可能会发现在异构网络环境中传输信息并不难。

由于 **FTP** 被如此广泛地使用，我将描述一些更常用的 **FTP** 命令。

**ftp** - 用于通过网络复制文件的文件传输协议。

以下列表包含一些常用的 `ftp` 命令。此列表并不完整。

-   `ascii` 将传输的文件类型设置为 ASCII。这意味着你将从一个系统向另一个系统传输 ASCII 文件。这是默认设置，因此你不必设置它。
    -   示例：`ascii`

-   `binary` 将传输的文件类型设置为二进制。这意味着你将从一个系统向另一个系统传输二进制文件。例如，如果你想在 UNIX 系统上有一个目录来存放你要复制到非 UNIX 系统的应用程序，那么你就需要使用二进制传输。
    -   示例：**binary**

-   `cd` 更改到远程主机上的指定目录。
    -   示例：**cd /tmp**

-   `dir` 将远程系统上目录的内容列出显示在屏幕上，或者如果你指定了本地文件名，则列出到本地系统上的文件中。

-   `get` 将指定的远程文件复制到指定的本地文件。如果你没有指定本地文件名，则使用远程文件名。

-   `lcd` 更改到本地主机上的指定目录。
    -   示例：**lcd /tmp**

-   `ls` 将远程系统上目录的内容列出显示在屏幕上，或者如果你指定了本地文件名，则列出到本地系统上的文件中。

-   `mget` 从远程主机复制多个文件到本地主机。
    -   示例：**mget *.c**

-   `put` 将指定的本地文件复制到指定的远程文件。如果你没有指定远程文件名，则使用本地文件名。
    -   示例：put test.c

-   `mput` 从本地主机复制多个文件到远程主机。
    -   示例：mput *.c

-   `system` 显示远程主机上运行的操作系统类型。
    -   示例：**system**

-   `bye/quit` 关闭与远程主机的连接。
    -   示例：**bye**

除了这里涵盖的内容外，还存在 **FTP** 命令。

# 其他连接主题

还有其他方法可以将你连接到 UNIX 系统。连接其他系统的两种流行技术是刚刚讨论过的 FTP 和 TELNET。NFS Maestro 提供了这两种功能。我可以在 Windows 系统上使用 TELNET，并在 UNIX 系统上打开一个窗口来发出命令。

图 16-18 显示了用于指定你的 TELNET 会话特征的 *HostExplorer* 窗口。

![](img/75f39fc91296b889c0653851accdfd46_1237_0.png)

我在 HostExplorer 窗口中选择了 VT，并成功登录到 UNIX 系统，如图 16-19 所示。

![](img/75f39fc91296b889c0653851accdfd46_1238_0.png)

图 16-19 telnet 窗口

在这个窗口中，我们可以发出 UNIX 命令，就像我们坐在直接连接到 UNIX 系统的终端前一样。此窗口显示 /home/hp，包括之前复制的 nfs 目录，以及所有文件和目录的权限、所有者和组。

telnet 在异构环境中被广泛使用。有了 X Windows，你得到的图形功能不是 telnet 的一部分。

在 UNIX 系统上运行的协议被分配给端口。我们可以使用 UNIX 系统上的 rpcinfo 命令查看这些端口、协议和相关联的信息，如图 16-20 所示。

![](img/75f39fc91296b889c0653851accdfd46_1239_0.png)

图 16-20 UNIX 上的 rpcinfo 命令

这个窗口中有大量与我们感兴趣的 NFS 相关的信息。然而，我们不必建立与 UNIX 系统的 telnet 会话并发出 rpcinfo 才能看到这些信息。Maestro 下的 Rpcinfo 菜单选择将查询 UNIX 主机并列出其正在运行的服务。图 16-21 显示了此窗口。

![](img/75f39fc91296b889c0653851accdfd46_1240_0.png)

*图 16-21* *Windows 上的 Rpcinfo 窗口*

RPC 代表远程过程调用。有各种程序具有与 RPC 相关的信息。需要几个程序来实现 Windows 和 UNIX 的互操作性。

显示的第一个数字是程序号。对于各种程序，有广泛接受的 RPC 编号。对于 NFS，程序号是 10003。下一个数字是协议的版本。在这种情况下，NFS 是版本 2。下一个数字是端口。端口号用于客户端（在我们的例子中是 Windows 系统）和服务器（在我们的例子中是 UNIX 系统）之间使用 NFS 进行通信。下一个字段是使用的协议，通常是 UDP 或 TCP。最后一个字段是程序名称。

对于 NFS，我必须确保在我的 UNIX 系统上运行 NFS、portmapper、mountd 和 pcnfds，然后我才能使用 NFS Maestro NFS 产品。

*Rpcinfo* 是一个有用的工具，用于查看你的 Windows 系统将连接到的主机上的所有信息。

## 第 17 章

### Advanced Server for UNIX

#### UNIX 上的 Windows 功能

到目前为止，我们一直在讨论将 UNIX 功能（如 X Windows 和 NFS）移植到 Windows 上以实现互操作性。为什么不反过来做呢？在某些情况下，在 UNIX 上拥有一些 Windows 功能肯定会很有帮助。这样就可以将打印机和磁盘等 UNIX 资源与网络上的多个 Windows 系统共享。

Advanced Server for UNIX® 是 AT&T 的产品，它是许多将 Windows 功能引入 UNIX 的产品的基础。Advanced Server for UNIX Systems 是 AT&T 和 Microsoft 公司联合开发协议的结果。它提供了促进 Windows 和 UNIX 互操作性的 Windows 功能。使用 Advanced Server for UNIX，UNIX 系统可以作为主域控制器或备份域控制器、文件服务器、打印服务器或其他的 Windows 功能组件。大多数主要的 UNIX 供应商都有基于 Advanced Server for UNIX 的产品。本章将使用称为 Advanced Server/9000 的 HP-UX 版本的 Advanced Server for UNIX。其他 Advanced Server for UNIX 的实现是相似的，因此你可以使用

