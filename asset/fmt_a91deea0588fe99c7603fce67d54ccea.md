
> 注意：虽然所有服务都支持此操作，但 `xinetd` 服务允许你在使用服务命令时使用 `reload` 而不是 `restart` 选项。由于 `xinetd` 已经在运行，通过不完全关闭 `xinetd`，执行 `reload` 可以更快完成，且对系统服务的干扰更少。

交叉引用：`xinetd` 超服务器在第 12 章中进行了描述。

# init.d 启动脚本

无法通过 `xinetd` 守护进程提供的网络服务通常由 `/etc/init.d` 目录中的脚本处理。要让 `/etc/init.d` 目录中的脚本激活服务，必须链接到其中一个运行级别目录（`/etc/rc?`）中的文件，且该文件以字母 `S` 开头，后跟两个两位数字。

例如，启动打印服务守护进程的脚本（`/etc/init.d/cups`）链接到 `/etc/rc2.d`、`/etc/rc3.d`、`/etc/rc4.d` 和 `/etc/rc5.d` 目录下的 `S55cups` 文件。这样，当 Fedora 或 RHEL 运行在初始化状态 2、3、4 或 5 时，打印服务就会启动。

交叉引用：有关运行级别和启动脚本的更多详细信息，请参阅第 12 章。

大多数情况下，系统管理员不需要修改这些启动脚本。然而，为了在特定级别开启或关闭服务，请将以 `S`（start，启动）开头的文件名改为以 `K`（kill，杀死）开头的文件。你可以通过 `chkconfig` 命令或服务配置窗口轻松地完成此操作。在以 root 用户登录时，在终端窗口输入 `serviceconf` 即可启动该窗口。

启动脚本通常启动一个或多个代表特定服务的守护进程。要添加选项，你通常不需要直接编辑启动脚本。相反，请在 `/etc/sysconfig` 目录中查找配置文件。例如，DNS (`named`)、Samba (`smbd` 和 `nmbd`) 以及系统日志 (`syslogd`) 服务在 `/etc/sysconfig` 目录中都有选项。

# 选择替代方案

Fedora 和 RHEL 中的某些服务可以使用几个不同的软件包实现。虽然你可以这样做，但你可能不想在同一台计算机上运行多个邮件服务器和打印服务器。至少，你应该设置你想要使用的默认软件。

在 Fedora 和 RHEL 中，替代方案（alternatives）功能被封装在操作系统中。Alternatives 是 Debian GNU/Linux 替代方案功能的实现。本质上，`altern` 将你选择的（或保持默认的）软件链接到实现的服务被启动或提供的通用位置。

交叉引用：请参阅第 10 章的“选择软件替代方案”部分获取有关 alternatives 功能的信息。

在 Fedora 和 RHEL 中，最先通过 alternatives 实现的服务是打印和邮件服务器软件包。然而，当 LPRng 打印服务从 Fedora 和 RHEL 中移除后，邮件成为唯一受 alternatives 功能支持的服务。

假设你有有多个邮件代理。

图 B-1 显示了系统切换窗口的示例。

![](img/c7605e408543e0a1829c1fd0cf2f687d_1057_0.png)

**图 B-1：** 使用 `system-switch-mail` 更改默认邮件传输代理。

# 网络服务的引用

本节包含了与 Fedora 和 RHEL 网络服务相关的快速参考信息。出这些服务的表格（表 B-1）包含以下信息：

- **功能 (Feature):** 它是什么类型的服务？
- **包名 (Package names):** 使用该服务必须安装哪些软件包？
- **启动脚本 (Start-up scripts):** 哪些启动脚本启动该服务？
- **守护进程 (Daemon):** 哪个守护进程正在运行？
- **配置文件 (Configuration files):** 你可以修改哪些配置文件来定制服务？

后续章节提供了有关服务的一些信息。`xinetd` 守护进程被标记为启动脚本。

> `TUX` 服务默认是关闭的。开启它，输入 `chconfig on`，它将在你下次启动计算机时启动。现在启动服务，输入 `service start`。

## Web 服务器

大多数情况下，你使用 Apache 项目 (`httpd`) 在 Fedora 或 RHEL 中创建 Web 服务器。如果安装了 `httpd`，你必须开启服务并启动它。从网络访问你系统的用户默认可以看到 `/var/www/html` 目录的内容。替换 `index.html` 文件并添加自己的内容。如果安装了 `httpd-manual` 包，`/var/www/manual` 将包含手册。

> 交叉引用：有关配置 Apache 服务器，请参阅第 21 章。

可以配合 Apache 使用 Web 服务器是 TUX HTTP 服务器。TUX 是一种在 Linux 内核中运行的高性能协议栈。在 `/etc/sysconfig/tux` 文件中配置 TUX。TUX 服务默认是关闭的。开启它，输入 `chconfig on`，它将在你下次启动计算机时启动。现在启动服务，输入 `service start`。它将提供与……相同的内容。

# 文件服务器

Fedora 和 RHEL 中的文件服务可以使用 FTP 服务器、Samba（Windows）服务器、网络文件系统（NFS）服务器和 NetWare 服务器提供。以下章节将描述这些服务器。

## FTP 服务器

Very Secure FTP 守护进程（`vsftpd`）软件包从零开始设计，具有非常强的扩展性和速度。通过编辑 `/etc/vsftpd/vsftpd.conf` 和 `/etc/vsftpd/user_list` 文件来配置 `vsftpd`。`vsftpd` 软件包共享 `/var/ftp` 目录并在端口 `21` 上监听服务请求。

要开启 FTP 服务，以 root 用户身份输入内容：

```
# service vsftpd start

# chconfig vsftpd on
```
