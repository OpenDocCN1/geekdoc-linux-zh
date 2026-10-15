
在这个例子中，`tftp` 配置文件代表简单文件传输协议（TFTP）服务。默认情况下，该服务是关闭的。当服务开启时，来自网络的向 `xinetd` 服务器守护程序发起的 tftp 服务请求会被交给 `/usr/sbin/in.tftpd` 守护进程。然后，`in.tftpd` 守护进程处理远程用户对该充当 TFTP 服务器的 Linux 系统的文件传输服务的请求。该文件中的其他条目包含与 TFTP 守护进程链接的选项。

要在 `/etc/xinetd.d` 文件中启用服务，请以 root 用户使用任何文本编辑器编辑该文件。开启服务很简单，只需将 `disable` 选项从 `yes` 更改为 `no` 并重启 `xinetd` 守护进程即可。例如，你可以更改 `/etc/xinetd.d/tftp` 中的行，使其看起来如下所示：

```
disable = no
```

然后你可以重启 `xinetd` 守护进程（而不关闭守护程序本身）：

```bash
service xinetd restart
```

> **注意：** 尽管并非所有服务都支持此功能，但 `xinetd` 服务允许你在上述 `service` 命令中使用 `reload` 选项代替 `restart` 选项。在 `xinetd` 已经运行的情况下，通过完全不完全关闭 `xinetd`，重载可以更快地发生，并且对系统服务的干扰更小。

在这种情况下，你可以查看 `/etc/services` 文件，你会发现 tftp 服务（默认情况下）在 TCP/IP 和 UDP 网络上通过端口号 69 接收。因此，进入计算机的针对端口 69 的任何请求首先会被转发给 `xinetd` 守护进程，然后由 `tftpd` 守护进程处理。如果身份验证正确，则可以进行请求的文件传输。

> **交叉引用：** `xinetd` 超级服务器在第 12 章中进行了描述。

## init.d 启动脚本

通常，那些无法通过 `xinetd` 守护进程可用的网络服务是由 `/etc/init.d` 目录中的脚本处理的。对于 `/etc/init.d` 目录中的脚本要激活某个服务，它必须链接到一个运行级别目录（`/etc/rc?.d`）中以字母 `S` 开头后跟两位数字的文件。

例如，用于启动打印服务守护进程（`/etc/init.d/cups`）的脚本被链接到 `/etc/rc2.d`、`/etc/rc3.d`、`/etc/rc4.d` 和 `/etc/rc5.d` 目录中的文件 `S55cups`。这样，当 Fedora Linux 在初始化状态 2、3、4 或 5 下运行时，打印服务会被启动。

> **交叉引用：** 有关运行级别和启动脚本的更多详细信息，请参见第 12 章。

在大多数情况下，系统管理员不需要修改这些启动脚本。但是，为了在特定的运行级别开启或关闭服务，请将脚本的文件名从以 `S`（启动）改为以 `K`（终止）开头。你可以使用 `chkconfig` 命令或服务配置窗口轻松完成此操作。要从终端窗口输入 `serviceconf` 来启动该窗口，此时你必须以 root 用户身份登录。

启动脚本通常会启动代表特定服务的一个或多个守护进程。要为特定服务添加选项，通常不需要直接编辑启动脚本。相反，请查找 `/etc/sysconfig` 目录中的配置文件。例如，代表 DNS（named）、Samba（smbd 和 nmbd）和系统日志记录（syslogd）服务的守护进程选项在 `/etc/sysconfig` 目录中有选项文件。

## 选择替代方案

Fedora Linux 中的某些服务可以通过几个不同的软件包来实现。虽然你可以这样做，但你可能不想在同一台计算机上运行多个邮件和打印服务器。至少，你应该设置你希望默认使用的软件。

在 Fedora Linux 中，“alternatives”（替代方案）功能被打包进了操作系统。Alternatives 是 Debian GNU/Linux alternatives 功能的实现。本质上，alternatives 将你选择的软件（或保留的默认软件）链接到实现该服务时被启动或使其可用的常见位置。

> **交叉引用：** 有关 alternatives 功能的更多信息，请参见第 10 章中的“选择软件替代方案”部分。

在 Fedora Linux 中，首批在 alternatives 下实现的服务是打印和邮件服务器软件包。然而，当 LPDNg 打印服务从 Fedora 中移除后，它使得邮件成为由 alternatives 功能支持的唯一服务。

假设你安装了多个邮件 MTA（邮件传输代理），要从主 Red Hat 菜单切换邮件服务，请选择“系统工具” → “Mail Transport Agent Switcher”（邮件传输代理切换器）（或在终端窗口中键入 `system-switch-mail`）。出现的窗口允许你在 Sendmail（默认）、Postfix 和 Exim 邮件传输代理之间进行选择。

图 C-1 显示了 system-switch-mail 窗口的示例。

![](img/b22364e57409c2481ba806e4e6b9309c_1042_0.png)

## 引用网络服务

本节包含与 Fedora Linux 网络服务相关的快速参考信息。列出这些服务的表格（表 C-1）包含以下信息：

-   **功能：** 这是什么类型的服务？
-   **软件包名称：** 使用服务需要安装哪些软件包？
-   **启动脚本：** 哪些启动脚本启动服务？
-   **守护进程：** 正在运行的什么守护进程提供该服务？
-   **配置文件：** 你可以修改哪些配置文件来将服务定制到你的特定需求？

表格后的描述提供了关于该服务的额外信息。这些信息包括服务是否默认启动以及在哪里可以找到关于该服务的更多信息。

> **注意：** 当 `xinetd` 守护进程被标注为启动脚本时，服务交接的守护进程也会被标注出来。

以下部分提供了关于表 C-1 中描述的服务的额外信息。（你可以在本章末尾找到该表格。）

### Web 服务器

在大多数情况下，你在 Fedora Linux 中使用 `apache` 软件包来创建 Web 服务器。如果安装了 `apache`，你必须打开该服务才能使用它（作为 root 用户，键入 `chkconfig httpd on`）。除非你的 Web 服务器有一个有效的名称（和 IP 地址），否则启动将会失败。要定义服务器名称，请在 `httpd.conf` 文件中添加 `ServerName` 条目并重启服务。

可以从网络访问你系统的用户将能够查看 `/var/www/html/` 目录的内容。替换 `index.html` 文件并添加你自己的内容。如果安装了 `httpd-manual` 软件包，`/var/www/manual/` 包含 apache 手册。

> **交叉引用：** 有关配置 apache Web 服务器的信息，请参见第 21 章。

`apache` 的一种替代方案是 TUX HTTP 服务器。TUX 是一个高性能的 Web 服务器。TUX 的整个协议栈都在 Linux 内核中运行。在 `/etc/sysconfig/tux` 文件中配置 TUX。TUX 服务默认是关闭的。要打开它，键入 `chkconfig tux on`，它将在下次启动计算机时启动。它将提供与 `apache` 相同的内容（来自 `/var/www/html` 目录）。

### 文件服务器

Fedora Linux 中的文件服务可以使用 FTP 服务器、Samba（Windows）服务器、网络文件系统（NFS）服务器和 NetWare 服务器提供。以下部分描述了其中每一种。

#### FTP 服务器

Very Secure FTP 守护进程（`vsftpd`）软件包是从头开始设计的，旨在非常具有可扩展性和快速。它面向需要支持大量同时用户的 FTP 站点。通过编辑 `/etc/vsftpd.conf` 和 `/etc/vsftpd.user_list` 文件来配置 `vsftpd`。`vsftpd` 软件包共享 `/var/ftp` 目录结构，并在端口 21 监听服务请求。

要打开 FTP 服务，请键入以下内容（作为 root 用户）：

```bash
service vsftpd start
chkconfig vsftpd on
```

**交叉引用：** 有关如何配置 `vsftpd` FTP 服务器的信息，请参见第 20 章。

> **注意：** Fedora Linux 还包含支持 Kerberos 5 的 FTP 服务器。`krb5-workstation` 软件包包含包含 Kerberos 5 支持的 `sftp` 守护进程。`wu-ftp` FTP 服务器软件不再包含在 Fedora Linux 发行版中。

#### Samba 服务器

Samba 服务器软件支持服务器消息块（SMB）文件和打印机共享协议。SMB 最常用于共享由运行 Microsoft Windows 的计算机组成的本地网络上的资源。通常不会通过公共网络（如互联网）共享 SMB 文件和打印机。
