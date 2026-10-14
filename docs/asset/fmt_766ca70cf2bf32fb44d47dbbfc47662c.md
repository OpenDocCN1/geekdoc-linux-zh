
```
http_access deny all
```

第二行 `http_access` 拒绝所有匹配 `all` ACL 的请求访问。因此，所有请求的访问都被拒绝了。

`http_access` 行从上到下处理。一旦某行及其 `acl` 匹配，就会应用给定的访问规则（`allow` 或 `deny`），并且不再考虑任何后续的 `http_access` 标签。

假设来自 `172.17.0.0/16` 网络的客户端尝试访问示例中的代理服务器。第一行 `http_access` 匹配并允许访问；第二行 `http_access` 完全不会被处理。

当 `172.17.0.0/16` 网络之外的人尝试访问代理时，第一行 `http_access` 行不匹配，处理第二行。该行拒绝所有请求的访问，导致该请求不被允许。

当没有 `http_access` 行匹配请求时，默认访问规则是最后找到的 `http_access` 行的反向。`allow` 变为 `deny`，`deny` 变为 `allow`。

为了避免混淆，你应该在配置的末尾始终有一行匹配每个请求的 `http_access` 行，例如上面的 `http_access deny all`。此行在没有其他 `acl` 匹配时设置默认的（允许/拒绝）。

### 总结

| 目标 | 总结 |
|---|---|
| 配置 Samba 服务器 | 使用 Samba，可以将 Linux 系统配置为用于 Linux、Mac OSX 和 Windows 工作站的文件和打印服务器。从本质上讲，Samba 允许你的 Linux 系统模拟 Windows 服务器。用户可以像在 Windows 服务器上一样访问 Linux 服务器上的共享目录和打印机。Samba 服务在 `/etc/samba/smb.conf` 文件中配置。存储 Samba 用户的选项包括 `/etc/samba/smbspasswd` 和 LDAP。Linux 工作站可以访问 Samba 共享。Samba 客户端工具包括 `nmblookup`、`smbclient` 和 `mount` 命令。 |
| 配置 Web 服务器 | Apache 服务器通过 `/etc/apache2/` 目录下的文件配置。在默认配置中，文档根目录是 `/srv/www/htdocs`，`/var/log/apache2/` 目录包含 Apache 日志文件。虚拟主机允许 从同一个 IP 地址为多个域名提供服务。根据各种标准限制 Web 服务器的访问，包括客户端 IP 地址和用户名。PHP 常用于创建动态内容。通用网接口 `CGI` 也允许使用其他编程语言。 |
| 启用 FTP 服务器 | FTP 是一种广泛使用的文件传输协议。它使用两个连接，一个用于控制，一个用于数据。有多种 FTP 服务器可用。PureFTP 的优点是安全，并且可以通过配置文件进行配置。 |

| 目标 | 总结 |
|---|---|
| 配置电子邮件 | Postfix 是 SLES 11 上安装的默认邮件服务器。Postfix 主守护进程通过 `/etc/postfix/master.cf` 文件配置。文件中的每行都包含一个 Postfix 进程的条目。所有后续配置定义（查找表配置外）都设置在 `/etc/postfix/main.cf` 文件中。Postfix 提供了各种实用程序，例如查看队列的 `mail`、管理邮件队列的 `postqueue` 以及用于更改配置的 `postconf`。 |

| 目标 | 总结 |
|---|---|
| 配置 CUPS 服务器 | 通用 Unix 打印系统 `CUPS` 是 SLES 11 使用的默认打印系统。CUPS 可在本地或远程打印机上打印。使用的协议是 IPP，但也支持其他协议。你可以通过 `http://localhost:631` 或 `http://IP_Address:631/` 进入 CUPS Web 前端。Web 界面允许管理 CUPS 的所有方面，包括管理打印机、查看日志文件或编辑 `/etc/cups/cupd.conf` 文件。打印机使用打印队列进行寻址。CUPS 工具允许你根据以下使用命令：

- Berkeley `LPRng` 风格，例如 `lpr`、`lpq` 和 `lprm`。
- System V 风格，例如 `lp`、`lpstat` 和 `cancel`。

要列出本地队列的当前设置，输入 `lpoptions -p queue -l |` |

| 目标 | 总结 |
|---|---|
| 使用 BIND 配置 DNS 服务器 | DNS 是一种用于将主机名翻译为 IP 地址的分布式数据库。在 SLES 11 中，你可以使用 BIND 软件建立自己的 DNS 服务器。仅缓存 DNS 服务器不负责某个域名；它只是将请求转发到其他名称服务器并缓存结果供后续请求。主服务器负责某个域名。它提供有关该域的权威信息。BIND 配置存储在 `/etc/named.conf` 文件中。DNS 服务器信息存储在区域文件中，这些文件通常位于 `/var/lib/named/master` 目录。 |

在网络中的所有计算机上实现统一时间，所有计算机必须访问至少一个时间服务器。`ntp` 包包含 `ntpd` 时间服务器，它可以从另一个时间服务器获取时间，并通过 NTP 为网络上的其他机器提供时间。

| 目标 | 摘要 |
| --- | --- |
| 启用 xinetd | 扩展互联网守护进程 `xinetd` 用于在建立相应端口连接时启动 FTP 或 POP3 等各种网络服务。状态配置包含在 `/etc/xinetd.conf` 文件以及 `/etc/xinetd.d/` 目录中针对各种服务的单独文件中。可以使用 YaST 网络服务模块、编辑器，以及在某种程度上通过 `chkconfig` 命令进行配置。 |
| 配置代理服务器 | Squid 是最常用的 HTTP 协议应用层网关。它可以执行缓存、日志和过滤等任务。浏览器需要配置使用 Squid。Squid 的配置包含在 `/etc/squid/squid.conf` 文件中。配置文件包含变量，这些变量也称为 `tags`（标签）。`acl` 和 `http_access` 标签用于访问控制管理。 |

### 关键术语

- - (root domain) — DNS 的根域名。
- `.htaccess` — 一个包含针对 Apache Web 服务器的特定目录限制的文件。
- `/etc/aliases` — 包含用户账户的邮件别名。
- `/etc/apache2/default-server.conf` — 如果在其他 Apache 配置文件中未覆盖相同参数，则该文件包含默认 Apache 配置。
- `/etc/apache2/httpd.conf` — Apache 的主配置文件。
- `/etc/cups/cupsd.conf` — 存储 root 用户设置的系统级打印选项的主文件。
- `/etc/cups/lppoptions` — 存储用于特定打印机的活动 PPD 文件的目录。
- `/etc/cups/ppd` — 包含打印机定义的目录。
- `/etc/cups/printers.conf` — 包含 CUPS 打印机定义。
- `/etc/hosts.allow` — `tcpd` 使用的文本文件，列出了允许连接到网络守护进程的主机。
- `/etc/hosts.deny` — `tcpd` 使用的文本文件，列出了不允许允许连接到网络守护进程的主机。
- `/etc/inetd.conf` — `inetd` 的主配置文件。
- `/etc/localtime` — 存储时间和区域信息的文件。
- `/etc/mail/generic.stable` — Sendmail 配置文件，用于修改发送邮件的发送者地址。
- `/etc/mail/mailertransfer` — Sendmail 配置文件，定义了发送邮件的路由方式。
- `/etc/named.conf` — 列出 DNS 服务器上托管的区域类型以及区域文件位置的文件。
- `/etc/ntp.conf` — NTP 服务器和客户端的主配置文件。
- `/etc/postfix/master.conf` — Postfix 主守护进程的配置文件。
- `/etc/printcap` — 在客户端文件中存储打印队列列表的对文件。
- `/etc/pure-ftpd/pure-ftpd.conf` — PureFTPD 的主配置文件。
- `/etc/samba/smb.conf` — Samba 的主配置文件。
- `/etc/sendmail.conf` — Sendmail 的主配置文件。
- `/etc/squid/squid.conf` — Squid 的主配置文件。
- `/etc/sysconfig/clock` — 用于配置 Linux 内核如何获取信息的文件。
- `/etc/sysconfig/ntp` — 在启动和停止 NTP 守护进程时存储变量的文件。
- `/etc/xinetd.conf` — `xinetd` 的主配置文件。它从 `/etc/xinetd.d` 目录加载配置文件。
- `/etc/xinetd.d` — 存储大多数 `xinetd` 配置的目录。
