
如果你仔细阅读了列表 29-1，你将看到许多指令与你在 TurboFTP Config 中可以进行的设置相对应。例如，让我们更仔细地查看虚拟主机（`VirtualHost`）部分。

回顾第 25 章“使用 Apache 提供 Web 服务”，我创建了一个名为 `gabriele.home.now` 的基于 IP 的虚拟主机。在这里，我正使用它创建一个虚拟 FTP 主机。当用户使用 FTP 连接到 `gabriele.home.now` 时，ProFTPd 会使用 `VirtualHost` 容器内定义的设置。如果此容器不存在，由于 `DefaultServer` 设置为 `on`，将使用默认设置。用户可以使用有效的用户名和密码连接。他们被放置在 `DefaultRoot` 目录定义的 FTP 根目录 `/home/http/gabriele/ftp` 中。

匿名用户可以使用 `anonymous` 或 `nobody` 等用户别名登录。他们被重定向到由 `<Anonymous>` 标签定义的匿名根目录 `/home/http/gabriele/ftp/pub`。这里存在目录限制。匿名用户不允许上传文件，这通过第一个 `<Limit WRITE>` 容器进行了指示。该规则的例外通过 `<Directory incoming/*>` 容器实现。`incoming` 目录及其后续子目录如 `<Limit STOR>` 容器所示，仅限制上传文件。此外，如 `<Limit WRITE DIRS>` 指令所示，他们不允许通过上传文件来覆盖现有文件。再进一步，他们不能查看 `incoming` 子目录的内容。但是，如果他们知道文件的确切名称，就可以从 `incoming` 下载文件。如果你想关闭此功能，请在以下 Limit 容器中添加 `READ` 操作：

```
<Limit WRITE DIRS READ>
  DenyAll
</Limit>
```

拒绝 `READ` 操作将停止从 `incoming` 目录的下载。

如果你将 ProFTPd 作为 `inetd` 服务运行，则配置会在随后的连接中重新读取。如果你将 ProFTPd 作为独立服务运行，你必须重启它或发送 `SIGHUP` 信号强制其重新读取配置文件。

## 总结

ProFTPd 完成了标准 BSD FTP 服务器的所有工作，并且功能更多。由于它的配置同样简单，它是一个极佳的替代方案。在本章结束时，你应该已经运行起来了基础的用户和匿名 FTP 服务。你可能还对如何在不损害安全性的情况下增强特定用户或目录的 FTP 访问有一些想法。你可以在 `/usr/share/doc/packages/proftpd-1.2/` 中找到实用的文档，以及如何在某些场景下设置 ProFTPd 的教程示例。你可能会发现某些有用功能如带宽限制和备用验证方法。虽然 ProFTPd 的默认配置设置为与 PAM 配合工作，但你可能会发现，在验证特定用户而无需让该用户被系统其他部分感知的情况下非常有有用。ProFTPd 的一本在线书籍开头位于：`http://hamster.wibble.org/proftpd/proftpd_userguide.html`。

# 网络信息服务

# 第 30 章

## 本章内容

- 关于网络信息服务 (`NIS`)
- 安装 `NIS`
- 配置 `NIS`
- 使用 `NIS`

在 TurboLinux 中管理用户、组和密码等系统资源，如果你只负责一两台计算机，这是一个非常简单的任务。然而，如果你负责网络上的许多系统，维护所有机器之间的一性可能会变成一项全职工作。

例如，如果用户 Joe 有权访问局域网上的十台机器，并且他在其中一台机器上更改了密码，那么同一个密码必须传播到所有其他机器。这就是 `NIS` 发挥作用的地方。

## 关于网络信息服务

网络信息服务 (`NIS`) 是一种用于向参与计算机发布系统信息的协议和工具集。它由 SUN Microsystems 开发，被大多数 UNIX 环境使用。

`NIS` 是一种基于客户端的服务器架构。这意味着有负责发布系统信息的机器（称为服务器），以及其他对接收这些信息感兴趣的机器（称为客户端）。

## 安装 NIS

要安装 `NIS`，你必须首先确定你需要安装 `NIS` 软件、客户端软件还是两者都要。如果你的网络上已经有一个 `NIS` 服务器，你可以只需安装 `NIS` 客户端软件。如果你正在为你的网络设置 `NIS`，你必须安装 `NIS` 服务器软件，如果你希望 `NIS` 服务器机器也能使用 `NIS` 服务，则可以选择性安装客户端软件。

客户端和服务器都需要启用 `portmapper` 服务。`portmapper` 将 `NIS` 使用的 RPC 数字映射为 TCP/IP 端口。如果 `portmapper` 未运行，请启动 `TurboService`。

```
/usr/sbin/turboservice
```

滚动到 `portmap` 并确保它已启用且正在运行。

为了使 RPC 更安全，请启用 `inetd` 中的时间服务。编辑 `/etc/inetd.conf` 并确认时间条目未注释。时间条目应该像这样：

```
# 时间服务用于时钟同步
#ntime stream tcp nowait nobody /usr/sbin/tcpd in.timed
time dgram udp wait nobody /usr/sbin/tcpd in.timed
```

接下来，如果系统中尚未安装相应的软件，请进行安装。

最后，你必须确保你的 `NIS` 域名名已设置。要设置域名名，你可以使用命令 `/bin/domain <nis.domain>`，其中 `<nis.domain>` 是你的域名名。例如：

- `/bin/domainname home.now`

要使参数在系统启动之间保持持久，你可以将命令放置在 `/etc/rc.d/rc.local` 文件中，或任何你确定会在 `ypserv` 或 `ybind` 启动之前执行的类似位置。

### Server

如果你安装了 TurboLinux Server 6.0，那么 `NIS` 服务器 `ypserv` 可能已经安装在你的系统中了。它是 TurboLinux Server 标准安装的一部分。你可以通过执行以下命令判断 `ypserv` 是否安装：

```
> rpm -q ypserv
ypserv-1.3.9-1
```

如果尚未安装，你可以从 TurboLinux Server CD-ROM 安装它，并使用类似于下所示命令：

- `rpm -Uhv /misc/cdrom/TurboLinux/RPMS/ypserv-1.3.9-1.i386.rpm`

如果你使用的是 TurboLinux Workstation，它并没有被包含在标准安装中。不过，你可以从随附的 CD-ROM 安装它，或者从 TurboLinux 的 FTP 站点下载。

- `rpm -Uhv /misc/cdrom/TurboContrib/RPMS/ypserv-1.3.9-1.i386.rpm`

TurboLinux 自带的 `ypserv` 版本是 `NIS+` (`NYS`) 版本。`NIS+` 是 `NIS` 的新版本，行为与 `NIS` 类似。

```
> ypserv --version
ypserv - NIS YP Server version 1.3.9 (with tcp wrapper)
```

安装完成后，你可以继续阅读本章的“配置 `NIS`”部分来学习如何设置。如果你还想安装 `NIS` 的客户端部分，请阅读下一节“客户端”。

### Client

要使用 `NIS` 的客户端部分，你必须安装两个 RPM 包：分别是 `yp-tools` 和 `ybind`。`yp-tools` 提供了常用的 `NIS` 客户端工具，例如：

```
/usr/bin/ypcat
/usr/bin/ypchfn
/usr/bin/ypchsh
/usr/bin/ypmatch
```

这些工具允许你查询 `NIS` 服务器的信息，并更改由 `NIS` 管理的信息——例如用户密码、shell 等。`ybind` 连接到 `NIS` 服务器并在本地维护它的关键信息。`yp-tools` 需要 `ybind` 才能工作。

如果你使用的是 TurboLinux Workstation 或服务器，你可能已经安装了 `yp-tools` 和 `ybind`。要查看你安装了哪些 Y 包，你可以使用类似于下面的命令查询 RPM 数据库：

```
rpm -qa | grep ^yp
yp-tools-2.3-2
ybind-3.3-16
```

在上一个例中，你可以看到已经安装了 RPM 包 `yp-tools-2.3-2` 和 `ybind`。如果没有安装，你可以使用以下命令从 TurboLinux CD-ROM 安装它们：

```
> rpm -Uvh /misc/cdrom/TurboLinux/RPMS/yp-tools-2.3-2.i386.rpm
rpm -Uvh /misc/cdrom/TurboLinux/RPMS/ybind-3.3-16.i386.rpm
```

在安装 `ybind` 和 `yp-tools` 后，你可以继续进行下一节。

## Configuring NIS
