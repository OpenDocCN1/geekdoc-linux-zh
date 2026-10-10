
`etc/xinetd.d` 包含 xinetd 文件

`etc/init.d` 包含启动脚本

这些方法将在后续章节中描述：

## xinetd 超服务器

xinetd 守护进程被称为超服务器。与其为每个服务运行独立的守护进程，只需运行 xinetd 守护进程。要查看由 xinetd 处理的服务是否开启，进入 `/etc/xinetd.d` 目录并使用文本编辑器打开代表该服务的文件。顶部的默认行指示。`disable` 行设置了服务当前是否被禁用。以下示例是 `/etc/xinetd.d/amanda` 文件的片段：

```
service amanda
(
socket_type = dgram
protocol    = udp
wait        = yes
user        = amanda
server      = /usr/lib/amanda/amandad
disable     = yes
)
```

在此示例中，amanda 配置表示从 amanda 客户端检索备份索引。默认情况下，该服务是关闭的。当服务开启时，网络向 xinetd 守护进程提出的 amanda 请求将交给 amandad 守护进程。

启用 `/etc/xinetd.d` 文件中的服务，请以 root 用户身份使用任何文本编辑器编辑文件。开启服务只需将 `disable` 选项从 `yes` 改为 `no` 并重启 xinetd 守护进程。例如，你可以更改 `/etc/xinetd.d/amanda` 文件，使其显示如下：

```
disable      = no
```

然后你可以重启 xinetd 守护进程（而不关闭守护进程本身）：

```
# service xinetd restart
```

> 注意：虽然并非所有服务都支持此操作，但 xinetd 服务允许你使用上述 `service` 命令的 `reload` 选项而不是 `restart` 选项。由于 xinetd 已经在运行，由于不完全关闭 xinetd，`reload` 的速度更快且对系统服务的干扰更小。

# 附录 B：运行网络服务 1019

## init.d 启动脚本

无法通过 xinetd 守护进程使用的的服务通常由 `/etc/init.d` 目录下的脚本处理。要让 `/etc/init.d` 目录中的脚本激活服务，它必须被链接到运行级别目录（`/etc/rc.?`）中的其中一个文件，且文件名以字母 S 开头，后跟两个数字。

例如，启动打印服务守护进程脚本（`/etc/init.d/cups`）链接到 `/etc/rc2.d`、`/etc/rc3.d`、`/etc/rc4.d` 和 `/etc/rc5.d` 目录下的 `S55cups` 文件。这样，当 Fedora 或 RHEL 运行在初始化状态 2、3、4 或 5 时，该服务就会启动。

**引用**：请参阅第 12 章以获取更多运行级别和启动脚本。

通常情况下，系统管理员不需要修改这些启动脚本。然而，若要在特定的运行级别下开启或关闭服务，请将以 S（启动）开头的脚本名更改为以 K（终止）开头的名称。你可以使用 `chkconfig` 命令或服务配置（Service Configuration）窗口来实现。要启动该窗口，请以 root 用户身份登录，在终端窗口中输入 `serviceconf`。

启动脚本通常启动一个或多个代表服务的守护进程（daemon）。若要添加选项，你不需要直接编辑启动脚本。相反，请使用 `/etc/sysconfig` 目录下的配置文件。例如，DNS (`named`)、Samba (`smbd` 和 `nmbd`) 以及系统日志 (`syslogd`) 服务在 `/etc/sysconfig` 目录下都有选项文件。

## 选择替代方案

Fedora 和 RHEL 中的某些服务可以通过多个不同的软件包来实现。虽然你可以这样做这样做，但你可能不想在同一台计算机上运行多个邮件服务器和打印服务器。至少，你应该设置你想要默认使用的服务。

在 Fedora 和 RHEL 中，替代（alternatives）功能被封装在操作系统。Alternatives 是 Debian GNU/Linux 替代功能的实现。从本质上说，Alternatives 将你选择（或保持默认）的软件链接到启动或提供服务的常用位置。

**引用**：请参阅第 10 章中的“选择软件替代方案”部分以获取有关替代功能的更多信息。

在 Fedora 和 RHEL 中，首次通过替代实现的服务是打印和邮件服务器包。然而，当 LPRng 打印服务从 Fedora 和 RHEL 中移除后，邮件就成了唯一受替代功能支持的服务。

假设你有多个邮件代理，可以使用 `system-switch-mail` 在这些服务之间切换。图 B-1 显示了 `system-switch-mail` 窗口的示例。

## 引用网络服务

本节包含与 Fedora 和 RHEL 网络服务的快速参考信息。列出这些服务的表格（表 B-1）包含以下信息：

- **特性 (Feature)** — 它是什么类型的服务？
- **包名 (Package names)** — 使用该服务必须安装哪些软件软件包？
- **启动脚本 (Start-up scripts)** — 哪些启动脚本启动该服务？
- **守护进程 (Daemon)** — 运行哪个守护进程来提供服务？
- **配置文件 (Configuration files)** — 你可以修改哪些配置文件来根据特定需求定制服务？

表格后的描述提供了有关服务的额外信息，包括该服务是否默认启动，以及你可以在哪里找到有关该服务的更多信息。

> 注意：当 xinetd 守护进程被标记为启动脚本时，交付给服务的守护进程也会被标记。

接下来的章节提供了有关表 B-1 中描述服务的额外信息。（你可以在本附录末尾找到该表。）

## Web 服务器

在大多数情况下，你使用 Apache 项目（`httpd` 包）在 Fedora 或 RHEL 中创建 Web 服务器。如果安装了 `httpd`，你必须开启该服务，然后启动它以使用服务（作为 root 用户，输入 `chkconfig httpd on` 然后输入 `service httpd start`）。否则启动将失败，除非

![](img/74f214fbb2938b570bec5f957507ac66_1053_0.png)

图 B-1：使用 `system-switch-mail` 更改你的默认邮件传输代理。

（注）你已经为你的 Web 服务器定义了一个有效的名称（和 IP 地址）。要定义服务器名称，请在 `http.conf` 文件中添加 `ServerName` 条目并重启服务。

默认情况下，能够从网络访问你系统的用户将能够查看 `/var/www/html` 目录的内容。替换 `index.html` 文件并添加自己的内容。如果安装了 `http-manual` 包，`/var/www/manual` 包含 apache 手册。

**引用**：请参阅第 21 章获取有关配置 Apache Web 服务器的信息。

一种可以与 TUX HTTP 服务器配合使用的 Web 服务器。TUX 是一个高性能的 Web 服务器。TUX 的整个协议栈运行在 Linux 内核中。在 `/etc/sysconfig/tux` 文件中配置 TUX。TUX 服务器默认是关闭的。要开启它，请输入 `chkconfig tux on`，它将在下次启动计算机时启动。要现在启动该服务，输入 `service start`。它将启动。

## 文件服务器

Fedora 和 RHEL 中的文件服务由 FTP 服务器、网络文件系统 (NFS) 服务器和 NetWare 服务器提供。接下来的章节将描述每一项。

安全 FTP 守护进程 (`vsftpd`) 设计得具有良好的扩展性和快速快。`vsftpd` 包监听 21 端口。要开启 FTP，请输入以下命令（作为 root）：

```
# service vsftpd start
# chkconfig vsftpd on
```

**引用**：请参阅第 20 章获取 vsftpd 的信息。

> 注意：Fedora 和 RHEL 还包含支持 Kerberos 的 FTP 服务器。`wu-ftp` 服务已不再。

## Samba 服务器

Samba 服务器支持服务器消息块 (SMB) 协议。SMB 通常用于运行 Windows 计算机的本地网络。你通常不会在公共网络（如互联网）上共享 SMB。

Samba 服务在 Fedora 和 RHEL 中默认关闭。要让 Samba 在启动时自动运行，只需输入 `chkconfig smb on`。要现在启动服务，输入 `service samba`。

为了让 Samba 应用，编辑配置文件 `/etc/samba/smb.conf`。配置此文件的简单方法是使用 Samba 配置窗口（见 18）。

**引用**：有关 Samba 的更多信息，请查看第 17 和 18 章。

## Netatalk 服务器
