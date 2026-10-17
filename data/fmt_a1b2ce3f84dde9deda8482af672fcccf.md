
``` 
service ftftp

{
    socket_type     = dgram
    protocol        = udp
    wait            = yes
    user            = root
    server          = /usr/sbin/in.tftpd
    server_args     = -s /ftpasswd
    disable         = yes
    all             = 
    flags           = IPv4
}
```

在此示例中，`ftftp` 代表简单文件传输协议（TFTP）。当服务启用时，`disable` 行被设置为 `no`。当服务禁用时，`disable` 行被设置为 `yes`。

## init.d 启动脚本

网络服务通常由 `/init.d` 中的脚本启动。在大多数情况下，不期望系统管理员修改这些启动脚本。然而，若想在特定的运行级别开启或关闭某个服务，请更改 `/etc/rc?.d` 中的脚本。你可以通过 `service` 命令或“服务配置”窗口轻松实现。

在 Fedora 和 RHEL 中，`alternatives` 下第一个实现的服务是打印和邮件服务器包。这些包链接到 `/etc/rc?.d` 目录，以便它们可以在运行级别下启动。例如，`cups` 服务在 `/etc/rc2.d`、`/etc/rc3.d`、`/etc/rc4.d` 和 `/etc/rc5.d` 中启动。

> 交叉引用：请参见第 12 章关于运行级别的详情。

## 选择替代方案

Fedora 和 RHEL 中的某些服务可以通过几个不同的软件包实现。虽然你可以这样做，但你可能不想在同一台计算机上运行多个邮件和打印服务器。至少，你应该设置你想要默认使用的软件。

在 Fedora 和 RHEL 中，`alternatives` 功能被封装在操作系统中。`Alternatives` 是 Debian GNU/Linux 替代功能的实现。本质上，`alternatives` 将你选择（或保持默认）的软件链接到服务启动或提供的常用位置。

> 交叉引用：请参第 10 章的“选择软件替代方案”章节获取更多关于 `alternatives` 功能的信息。

例如，Samba (`smbd` 和 `nmbd`) 和系统日志 (`syslogd`) 服务在 `/etc/sysconfig` 中拥有选项文件。

假设你有多个 MTA（邮件传输代理），若要从应用程序菜单切换邮件服务，请选择系统工具 -> 邮件传输代理切换器（或在终端窗口中输入 `system-switch-mail`）。出现的窗口允许你于 Sendmail（默认）、Postfix 和 Exim 邮件传输代理之间进行选择。

图 C-1 显示了 `system-switch-mail` 窗口的示例。

![](img/8aa80810fdd3df400bbeeee72b296baad_1060_0.png)

图 C-1：使用 system-switch-mail 更改默认邮件传输代理。

# 引用网络服务

本节包含与 Fedora 和 RHEL 网络服务的快速参考信息。列出这些服务的表格（表 C-1）包含以下信息：

- 特性：它是什么类型的服务？
- 软件包名称：使用该服务必须安装哪些软件包？
- 启动脚本：哪些启动脚本启动该服务？
- 守护进程（Daemon）：哪个守护进程进程正在运行以提供该服务？
- 配置文件：你可以修改哪些配置文件来根据你的特定需求定制服务？

表格后的描述提供了有关该服务的额外信息。这些信息包括该服务是否默认启动，以及你可以在哪里找到有关该服务的更多信息。

> 注意：当 `xinetd` 守护进程被标记为启动脚本时，也会标注将服务移交的哪个守护进程。

后续章节提供了有关表 C-1 中描述服务的额外信息。（你可以在此附录末尾找到该表格。）

### Web 服务器

在大多数情况下，使用 Apache 项目（`httpd` 软件包）在 Fedora 或 RHEL 中创建 Web 服务器。如果安装了 `httpd`，你必须开启该服务，然后启动它以使用该服务（作为 root 用户），输入 `chkconfig httpd on` 然后输入 `service httpd start`。除非为你的 Web 服务器了有效的名称（和 IP 地址），否则启动将失败。要定义服务器名称，请向 `httpd.conf` 文件中添加 `ServerName` 条目并重启服务。

从网络访问你系统的用户默认可以查看 `/var/www/html` 目录的内容。如果安装了 `httpd-manual` 软件包，`/var/www/manual` 包含 apache 手册。

> 交叉引用：有关配置 Apache Web 服务器的信息，请参见第 21 章。

配合 Apache 使用的 Web 服务器是 TUX HTTP 服务器。TUX 是一种高性能 Web 服务器。TUX 的整个协议栈运行在 Linux 内核中。在 `/etc/sysconfig/tux` 文件中配置 TUX。TUX 服务默认关闭。要开启它，输入 `chkconfig tux on`，它将在你下次启动计算机时启动。若现在启动服务，输入 `service tux start`。它将提供与 Apache 相同的内容（来自 `/var/www/html` 目录）。

# 文件服务器

Fedora 和 RHEL 中的文件服务可以使用 FTP 服务器、Samba（Windows）服务器、网络文件系统（NFS）服务器和 NetWare 服务器提供。以下章节描述了这些每种服务：

### FTP 服务器

Very Secure FTP 守护进程 (`vsftpd`) 软件包从头开始设计，具有非常扩展性和速度。它面向需要支持大量并发用户的 FTP 服务器而设计。通过编辑 `/etc/vsftpd.conf` 和 `/etc/vsftpd.user_list` 文件来配置 `vsftpd`。`vsftpd` 软件包共享 `/var/ftp` 目录结构并在端口 21 上监听服务请求。

要开启 FTP 服务，请输入以下命令（作为 root 用户）：

```bash
# service vsftpd start
# chkconfig vsftpd on
```
