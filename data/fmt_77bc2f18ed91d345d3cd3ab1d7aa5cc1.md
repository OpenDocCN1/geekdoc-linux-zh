
GPG 会提示你输入密码短。如果你输入了正确的密码短，GPG 将解密文件并将输出（在本例中）保存到名为 `myfile` 的文件中。

# 监控系统安全

即使你加固了系统，也必须定期检查日志文件，以发现入侵迹象。你可能想要使用 Tripwire 软件（一种用于检测系统文件任何更改的工具），这样你就可以监控关键系统文件和目录的完整性。你的 Linux 系统可能没有附带 Tripwire 软件包。要使用 Tripwire，你必须从 www.tripwire.com 购买。购买并安装 Tripwire 后，你需要配置它来监控系统中系统文件和目录的任何更改。

定期检查 `/var/log` 目录及其子目录下的日志文件。许多 Linux 应用（包括某些服务器）通过 syslog 或 syslogd 的日志功能来记录信息。在 Linux 系统上，由 syslog 和 syslogd 写入的日志位于 `/var/log` 目录。确保只有 root 用户可以读写这些文件。

syslog 配置文件为 `/etc/syslog.conf`，而 syslog 配置文件（存在于许多新系统中）为 `/etc/rsyslog.conf`。syslog 的默认配置会生成必要的日志文件；但如果你想检查并理解配置文件，请输入 `man syslog.conf` 获取更多信息。

# 安全互联网服务

对于连接到互联网的 Linux 系统（甚至是连接到 TCP/IP 局域网但未连接互联网的系统），一个重大威胁是有人可以使用许多互联网服务之一来访问你的系统。每种服务——例如邮件、Web 或 FTP——都需要一个运行的服务器程序，用于响应通过 TCP/IP 网络到达的客户端请求。其中某些服务器程序存在漏洞，允许外部人员登录你的系统——可能还具有 root 权限。幸运的是，Linux 有一些功能可以利用来使服务更加安全。

潜在的入侵者可以使用端口扫描工具——一种尝试在某个端口上建立 TCP/IP 连接并寻找响应的程序——来检查你的系统上是否运行着互联网服务器。为了访问你的系统，入侵者可能会利用一个或多个服务的任何已知漏洞。

# 运行独立服务

为了提供互联网服务（如 Web、电子邮件和 FTP），你的 Linux 系统必须运行监听入站 TCP/IP 网络请求的服务器程序。其中某些服务器在系统启动时启动，并且一直直运行。某些服务器是独立服务器。Web 服务器和邮件服务器就是独立服务的示例。

另一个服务器 `xinetd` 会启动其他配置为由 `xinetd` 运行的服务器。某些 Linux 系统使用 `inetd` 服务器而不是 `xinetd` 来启动其他服务。

某些服务器可以配置为独立运行，也可以在像 `xinetd` 这样的超级服务器下运行。例如，`vsftpd` FTP 服务器可以配置为独立运行，或在 `xinetd` 的控制下运行。

在 Debian、MEPIX、Ubuntu 和 Xandros 中，使用 `update-rc.d` 命令关闭独立服务器，并使用 `invoke-rc.d` 命令交互式地启动或停止服务器。要获取可用服务的线索，输入 `/etc/init.d` 并查看所有要启动或关闭的配置文件。当你想要开启或关闭服务时，必须输入这些文件名。例如，要关闭 Samba，输入 `update-rc.d -f samba remove`。如果服务已经在运行，输入 `invoke-rc.d samba stop` 来停止该服务。你可以以类似的方式使用 `invoke-rc.d` 命令停止任何服务。

在 Fedora 和 SUSE 中，你可以使用 `chconfig` 命令开启或关闭独立服务器。你可以通过输入 `/etc/init.d` 获取服务脚本的名称。然后你可以通过输入 `chconfig -del smb` 来关闭某个服务（例如 Samba）。如果服务已经在运行，输入 `/etc/init.d/samba stop` 来停止该服务。你可以运行 `/etc/init.d` 目录下的脚本并使用 `stop` 参数，以类似的方式停止任何服务。

# 安全互联网服务 415

# 配置互联网超级服务器

除了像 Web 服务器或邮件服务器等独立服务器外，还有其他服务器——`xinetd`——需要你单独配置。在 Debian、MEPIX、Ubuntu 和 Xandros 中，使用 `update-rc.d` 命令关闭独立服务器，并使用 `invoke-rc.d` 命令交互式地启动或停止服务器。要获取可用服务的线索，输入 `/etc/init.d` 并查看所有要启动或关闭的配置文件。当你想要开启或关闭服务时，必须输入这些文件名。例如，要关闭 Samba，输入 `update-rc.d -f samba remove`。如果服务已经在运行，输入 `invoke-rc.d samba stop` 来停止该服务。你可以以类似的方式使用 `invoke-rc.d` 命令停止任何服务。

在 Fedora 和 SUSE 中，你可以使用 `chconfig` 命令开启或关闭独立服务器。你可以通过输入 `/etc/init.d` 获取服务脚本的名称。然后你可以通过输入 `chconfig -del smb` 来关闭某个服务（例如 Samba）。如果服务已经在运行，输入 `/etc/init.d/samba stop` 来停止该服务。你可以运行 `/etc/init.d` 目录下的脚本并使用 `stop` 参数，以类似的方式停止任何服务。

# 配置 TCP wrapper

`inetd` 和 `xinetd` 的一个安全特性是它们使用了 TCP wrapper。TCP wrapper 是一种为服务提供访问控制策略的代码。在启动服务之前，它会查询 `/hosts.allow` 文件查看是否允许该主机。如果 `/hosts.allow` 为空，TCP wrapper 将检查 `/hosts.deny` 文件查看是否拒绝该主机。如果两个文件都是空的，TCP wrapper 将提供访问。

# 416 使用安全 Shell (SSH) 进行远程登录

以下是加固服务访问的遵循步骤：

- 使用文本编辑器编辑 `/hosts.deny` 文件，在文件中添加以下行：
```
ALL:ALL
```
这拒绝了所有主机的访问。

- 编辑 `/hosts.allow` 文件并向其添加可以访问服务的名称。例如，要允许来自 192.168.1.0 网络以及本地主机（IP 地址 127.0.0.1）访问系统服务，请在 `/hosts.allow` 中放置以下行：
```
ALL:192.168.1.0/255.255.250 127.0.0.1
```

- 如果你想从特定的远程主机访问特定的互联网服务，可以使用 `/hosts.allow` 中的以下语法：
```
server_program_name: hosts
```
