

# 使用 TCP 包装器控制访问权限

`inetd.conf` 文件中的另一项增强功能是 `tcp_wrappers` 程序，它有助于 Linux 保持对端口的控制并更好地监控启动的服务。`tcp_wrappers` 允许对网络守护程序进行更好的访问控制和日志记录。与其不加犹豫地直接启动守护程序，`tcp_wrappers` 采用了一套检查系统，以确保这些程序有权授予所请求的守护程序执行其任务所需的权限。免费提供的 `tcp_wrappers` 程序（有时被称为单数形式的 `tcp_wrapper`）增强了网络功能到 syslog 文件的日志记录。Syslog 是 Red Hat Linux 记录敏感程序尝试执行的位置。此日志文件及其他日志文件存储在 `/var/log` 目录中。关于系统安全的更全面分析，请参阅第 19 章“Linux 安全”。

与许多守护进程和进程一样，inetd 依赖配置 `/etc/inetd.conf` 文件来确定哪些进程可以或不应被生成。此文件及其他许多配置文件的位置在 `/etc` 目录中。然而，Linux 通过设置文件权限，使得只有 root 用户可以更改文件，从而保护了许多敏感文件（如 `inetd.conf`）。你可以手动更改这些文件的权限，但应谨慎，以免允许他人更改此类敏感文件。

> **提示**
>
> Linux 经常使用配置文件来设置某些进程。这些文件通常可以通过 `.conf` 扩展名轻松识别。

其他 UNIX 系统采取了更多的预防措施，将 `inetd.conf` 文件放置在距离 `/etc` 目录更进一步的目录中。例如，Solaris 是一个专有 UNIX 系统，它将 `inetd.conf` 文件放置在 `/etc/inet/` 目录中，并在 `/etc` 目录中创建一个指向该实际文件的符号链接。这并不能确保没有人会意外地修改该文件，但确实提高了安全性。归根结底，还是取决于文件权限。Linux 通过设置权限，使得只有 root 可以做出更改，来保护敏感文件。更改此文件的权限，使得除 root 外的其他用户可以读取和写入这些文件，将破坏系统安全，并允许这些其他用户启动他们自己的守护进程。

`Tcp_wrappers` 使用 `tcpd` 守护程序，该程序将自己置于 inetd 守护程序和其他子守护程序之间。安装 `tcp_wrappers` 涉及构建 `tcpd` 可执行文件，然后配置 `inetd.conf` 文件。Red Hat Linux 在最新版本中默认安装 `tcp_wrappers`，因此无需手动调整文件即可获得最佳使用效果。`tcpd` 用其自身的守护程序替换标准守护程序，该守护程序在特定端口上充当过滤器，直到发出适当的调用。`tcpd` 查看请求来源的地址以及其想要使用的内容。然后，它查阅配置文件并决定是否允许该请求。

`Tcp_wrappers` 默认安装在几乎所有 Linux 系统上。然而，如果你使用的是其他基于 UNIX 的发行版，如 Solaris 或 AIX，你需要手动安装 `tcpd`。另一方面，Red Hat Linux 在初始安装过程中默认编辑 `inetd.conf` 文件，并且可以轻松使用 RPM 包进行更新。除非你希望进一步收紧安全，否则你可能不需要编辑此配置文件。然而，了解它控制哪些选项以及这些选项如何影响系统是很重要的。关于 `tcp_wrappers` 的解释在第 19 章中。

# 使用 inetd.conf 文件配置守护程序

理解 `inetd.conf` 文件可以帮助你理解系统如何启动某些功能。列表 2.2 是一个标准的 Red Hat Linux 安装中获取的典型 `inetd.conf` 文件示例。第一个示例展示了在未安装 `tcp_wrappers` 时 `inetd.conf` 文件的样子，而第二个示例（列表 2.3）用 `tcpd` 程序替换了配置。以井号（pound sign）开头的行是被注释掉的，其服务已被禁用，出于安全目的或因为它们不被需要。

## 列表 2.2 典型的 inetd.conf 文件部分（未安装 tcp_wrappers）

```
# These are standard services.

ftpd stream tcp nowait root /usr/sbin/ftpd in.ftpd -l -a
telnet stream tcp nowait root /usr/sbin/telnetd in.telnetd

# Shell, login, exec and talk are BSD protocols.
shell stream tcp nowait root /usr/sbin/rshd in.rshd
login stream tcp nowait root /usr/sbin/rlogind in.rlogind

# Pop and imap mail services et al
#pop-2 stream tcp nowait root /usr/sbin/ipop2d ipop2d
pop-3 stream tcp nowait root /usr/sbin/ipop3d ipop3d
imap stream tcp nowait root /usr/sbin/imapd imapd
```

列表 2.3 展示了实现了 tcp wrappers 的相同文件。请注意倒数第二个字段是如何被 `tcpd` 或 tcp 守护程序替换的。

## 列表 2.3 默认 Red Hat Linux 安装 tcp_wrappers 后的 inetd.conf 文件

```
# These are standard services.

ftp stream tcp nowait root /usr/sbin/tcpd in.ftp -l -a
telnet stream tcp nowait root /usr/sbin/tcpd in.telnetd

# Shell, login, exec, and talk are BSD protocols.
shell stream tcp nowait root /usr/sbin/tcpd in.rshd
login stream tcp nowait root /usr/sbin/tcpd in.rlogind

# Pop and imap mail services et al
#pop-2 stream tcp nowait root /usr/sbin/tcpd ipop2d
pop-3 stream tcp nowait root /usr/sbin/tcpd ipop3d
imap stream tcp nowait root /usr/sbin/tcpd imapd
```

以下是 `inetd.conf` 文件中每个字段的详细解释：

-   第一列包含服务名称。这些服务名称链接到特定的端口号，其对应的服务可以在 `/etc/services` 文件中找到（用于 TCP 和 UDP 服务）。
-   第二列决定为该特定服务使用哪种类型的套接字。有三种不同类型的套接字：stream（流式）、dgram（数据报）和 raw（原始）。原始套接字很少使用。流式套接字通常用于 TCP 服务，正变得最为流行。Dgram 在 UDP 服务中实现。
-   第三列识别守护程序使用的协议类型。可用的类型列在 protocols 文件中，该文件位于与服务文件相同的目录中或 /etc 目录中。协议几乎总是 TCP 或 UDP。然而，Linux 保持极大的动态性，允许许多其他协议。
-   第四列通常设置为变量 `nowait`。这意味着 inetd 守护程序可以创建相同守护程序的新副本。它不必等待守护程序重新生成自身，而是可以分叉以生成新版本。然而，如果问题中的守护程序可以处理多个请求，则此变量应设置为 `wait`，以免分叉相同守护程序的多个副本。在 Red Hat Linux 下，`nowait` 是一个可接受的选项。
-   第五列是具有运行守护程序权限的用户名称。可以设置为任何用户，但通常服务需要 root 才能绑定到 1024 以下的端口。因此，许多守护程序只能以 root 身份运行。然而，如果 sendmail 守护程序以非 root 用户身份运行，则此变量应设置为该特定用户。另一个例子是 finger 守护程序，有时以 guest 身份运行，顾名思义，guest 是一个只有有限权限的用户。在此列中指定用户 guest。
-   第六列列出了传递给守护程序可执行文件的参数。在这种情况下，它要么是守护程序本身，要么是 `tcpd` 守护程序。`tcpd` 将要在安全检查通过时运行的程序作为参数。
-   最后一列是用于生成守护程序的参数，以及运行该进程所需的任何标志或额外选项。请注意 `in.ftpd` 守护程序命令。该命令指定了若干选项以正确运行或优化其使用。

`Tcp_wrappers` 随每个 Red Hat Linux 发行版提供。你不必在安装过程中安装它，但建议授予系统更高的安全性。`Tcp_wrappers` 可以稍后安装。由于它

