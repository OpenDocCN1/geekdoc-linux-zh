
上述输出显示了 telnet 守护进程的完整路径 (`/usr/sbin/in.telnetd`)。此外，`/etc/xinetd.d/telnet` 文件中的 `disable = yes` 行表示 telnet 守护进程已禁用。

> 用户数据报协议/网协议 (`UDP/IP`) 是一个比 `TCP/IP` 更快但因此可靠性较低的版本。

> 守护进程配置和日志文件的位置在不同的 Linux 发行版之间可能不同。本文讨论的位置适用于 Red Hat Fedora 2。

## 配置常见网络服务

要在 Linux 系统上配置大多数网络服务，必须首先识别网络服务的特征，包括其用途、配置文件、端口以及该服务是独立运行还是由互联网超级守护进程管理。表 15-2 列出了参与网络环境的 Linux 计算机上常见的网络服务的名称和特征。

### 表 15-2 常见网络服务

| 网络服务 | 类型 | 端口 | 描述 |
| :--- | :--- | :--- | :--- |
| Apache Web 服务器 (`httpd`) | 独立运行 | 80/443 | 为网络上带有 Web 浏览器的计算机提供 Web 服务。配置文件:`/etc/httpd/conf` |
| BIND / DNS 服务器 (`named`) | 独立运行 | 53 | 将互联网特定命名空间的完全限定域名解析为 IP 地址。配置文件:`/etc/named.conf` |
| DHCP 服务器 (`dhcp`) | 独立运行 | NA | 为网络上的计算机提供 IP 配置 |
| FTP 服务器 (`in.ftptpd`) | `xinetd` | 20/21 | 与网络上有 FTP 工具的计算机传输文件。配置文件:`/etc/ftpaccess` 拒绝访问的主机:`/etc/ftphosts` 拒绝访问的用户:`/etc/ftpusers` |
| IMAP 服务器 (`imapd`) | `xinetd` 或独立运行 | 143 | 允许带有电子邮件阅读器（邮件用户代理）的用户使用互联网邮件访问协议从服务器获取电子邮件。 |
| 互联网络新闻服务器 (`innd`) | 独立运行 | 119 | 接受并管理新闻组发布并将其传输到其他新闻服务器。配置文件:`/etc/news/inn.conf` |

# 第 15 章 配置网络服务与安全

### 表 15-2 常见网络服务（续）

| 网络服务 | 类型 | 端口 | 描述 |
|---|---|---|---|
| NFS 服务器 (`rpc.nfsd`) | 独立运行 | 2049 | 向网络上具有 NFS 客户端工具的计算机共享文件。配置文件：`/etc/nfs` |
| NIS 服务器 (`ypserv` & `ypbind`) | 独立运行 | 111 | 向属于 NIS 域的 NIS 客户端共享配置信息。配置文件：`/etc/ypserv.conf` |
| POP3 服务器 (`ipop3d`) | `xinetd` 或独立运行 | 110 | 允许使用电子邮件阅读器（邮件用户代理）的用户使用 Post 协议版本 3 从服务器获取电子邮件 |
| `rlogin` 守护进程 (`in.rlogind`) | `xinetd` | 513 | 允许使用 login 和 rpc 工具的用户通过信任访问在网络其他计算机上复制文件并获取 shell |
| `rsh` 守护进程 (`in.rshd`) | `xinetd` | 514 | 允许使用 `rsh` 工具的用户通过信任访问在网络其他计算机上运行命令 |
| Samba 服务器 (`smbd` & `nmbd`) | 独立运行 | 137 138 139 | 允许 Windows 查看 Linux 服务器上的共享文件和打印机。配置文件：`/etc/samba/smbd.conf` |
| 安全 Shell 守护进程 (`sshd`) | 独立运行 | 22 | 通过加密通信为 telnet、login 和 rsh 工具提供安全替代方案。配置文件：`/etc/ssh/sshd_config` |
| Sendmail 电子邮件服务器 (`sendmail`) | 独立运行 | 25 | 使用简单邮件传输协议 (`SMTP`) 向互联网用户或其他电子邮件服务器接收和发送电子邮件。配置文件：`/etc/sendmail.cf` |

### 表 15-2 常见网络服务（续）

| 网络服务 | 类型 | 端口 | 描述 |
|---|---|---|---|
| Squid 代理服务器 (`squid`) | 独立运行 | 3128 | 允许网络计算机共享一个互联网连接。也称为代理服务器。配置文件：`/etc/squid/squid.conf` |
| telnet 守护进程 (`in.telnetd`) | `xinetd` | 23 | 允许拥有 telnet 工具的用户从跨网络登录系统并获取 shell。 |
| 高安全 FTP 服务器 (`vsftpd`) | 独立运行 | 20 21 | 使用 FTP 工具向网络上的其他计算机传输文件并接收其文件。配置文件：`/etc/vsftpd/vsftpd.conf` 拒绝 ftp 访问的用户列表：`/etc/vsftpd.ftusers/vsftpd.user_list` |
| X 服务器 | 独立运行 | 0 | 使用 X 上的 `DISPLAY` 变量在网络具有 X 客户端的计算机上生成图形 |

> 注意：默认情况下，由于 `/etc/secure` 文件中的条目，会被阻止以 root 用户身份登录 telnet 等某些网络服务并获取 shell。该文件列出了允许 root 用户访问的项。删除或重命名此文件将允许 root 用户跨网络登录并接收 shell。

表 15-2 中的某些网络服务已成为当今许多网络的重要组成部分；这些包括 DNS、DHCP、Apache、Samba、NFS、FTP、NIS 和安全守护进程。

## 配置 DNS

回想一下 DNS 是一个层次命名空间，用于识别互联网等大型 TCP/IP 网络上的计算机。此命名空间的每个部分称为一个“区域”(`zone`)，DNS 服务器包含该区域的所有主机名信息。DNS 服务器通常将 FQDN 解析为 IP 地址（称为正向查找），但也可以将 IP 地址解析为 FQDN（称为反向查找）。

`img/8fe037bf1ed016ccb79db1a27184f2_676_png`

当使用 Web浏览器访问互联网上的 Web 服务器时，浏览器会对 FQDN 进行正向查找，以便连接到 Web 服务器的 IP 地址。正向查找和反向查找如图所示。

`img/8fe037bf1ed016ccb79db1a27184f2_676_png`

使用 DNS 解析主机名的过程如下：

- 客户端向本地 DNS 服务器发送查询。
- 如果本地 DNS 服务器没有该信息，它会将查询转发到另一个 DNS 服务器。
- 该过程一直持续，直到找到该区域的权威 DNS 服务器。
- 权威 DNS 服务器将 IP 地址返回给客户端。
- 客户端随后使用 IP 地址连接到 Web 服务器。

DNS 解析过程涉及多个步骤：

1. 客户端向本地 DNS 服务器发送查询。
2. 递归解析器查询根 DNS 服务器。
3. 根 DNS 服务器返回 TLD DNS 服务器的地址。
4. 递归解析器查询 TLD DNS 服务器。
5. 权威 DNS 服务器将 IP 地址返回给递归解析器。
6. 递归解析器将 IP 地址返回给客户端。
7. 客户端使用 IP 地址进行连接。

根据前述输出的说明，DHCP 服务器为客户端租用了从 `192.168.1.1` 到 `192.168.1.100` 之间的 IP 地址，有效期为 `36000` 秒。此外，DHCP 服务器还为客户端配置了默认网关 `192.168.1.254` 和 DNS 服务器 `192.168.1.200`。

在 `/etc/dhcpd.conf` 文件中配置了适当的信息后，你可以使用命令 `/etc/rc.init/dhcpd start` 启动 DHCP 守护进程，并通过检查 `/var/lib/dhcp/dhcpd.leases` 文件查看当前的 DHCP 租用情况。与名称守护进程（name daemon）类似，如果你更改了 `/etc/dhcpd.conf` 配置文件，必须重启 DHCP 守护进程。

## 配置 Apache

Apache 是世界上最常用的 Web 服务器。Web 服务器使用目录树中特定目录下的超文本传输协议 (`HTTP`)）来处理 HTML 文件和其他 Web 内容。该目录被称为文档根目录，包含了服务器上的默认 Web 网站。Red Hat Fedora Core 2 默认文档根目录是 `/var/www/html/`，该目录下提供的默认文档是 `index.html`。Apache 的所有配置选项都设置在一个大的配置文件中；默认情况下，该配置文件为 `/etc/httpd/conf/httpd.conf`。`httpd.conf` 文件中的每一行都是一个指令。表 15-4 列出了一些常用指令。

### 表 15-4 常见的 httpd.conf 指令

| 指令 |  |
| --- | --- |
| `Listen 80` | 指定 Apache 守护进程将在 80 端口上监听 HTTP 请求 |
| `ServerName server1.class.com` | 指定 Web 服务器的名称为 `server1.class.com` |
| `DocumentRoot "/var/www/html"` | 指定本地计算机上的文档根目录为 `/var/www/html` |
| `DirectoryIndex index.html` | 指定向请求 HTML 文档的客户端发送根目录下的 `index.html` 文件 |
| `ErrorLog /var/log/httpd/error_log` | 指定所有 Apache 守护进程消息都写入 `/var/log/httpd/error_log` 文件 |
| `MaxClients 150` | 将最大并发请求数设置为 150 |
| `User apache` | 指定 Apache 守护进程以 "apache" 本地用户账户运行 |
| `Group apache` | 指定 Apache 守护进程以 "apache" 本地组账户运行 |

| 表 15-4 常见的 httpd.conf 指令（续） | |
| 指令 | 描述 |
| :--- | :--- |
| `<Directory /var/www/html> Order allow,deny All from 192.168.1.51</Directory>` | 指定允许所有主机访问 `/var/www/html/` 中的 HTML 文件和其他 Web 内容，但 IP 为 `192.168.1.51` 的计算机除外 |

`httpd.conf` 文件中的默认设置适用于大多数简单的 Web 服务器；因此，你只需要将相应的 HTML 文件复制到 `/var/www/html/` 目录（包括 `index.html` 文件），并启动 Apache Web 服务器守护进程 (`/etc/rc.d/init.httpd`) 来在你的网络上托管 Web 内容。如果你更改了文档目录内的 HTML 内容，则不需要重启守护进程。但是，如果你更改了 `httpd.conf` 的内容，则重启 Apache 守护进程以激活这些更改。

# 第 15 章 配置网络服务与安全

## 配置 Samba

如今网络中最常见的客户端计算机操作系统是 Windows。回想上一章，Windows 使用服务器消息块 (`SMB`) 使用 TCP/IP 数据。因此，为了向 Windows 客户端共享信息，你可以使用模拟 SMB 协议的 Samba 守护进程。此外，Windows 使用 NetBIOS 协议发布其计算机名称；因此，你可以使用 NetBIOS 守护进程来创建并发布 NetBIOS 名称，让 Windows 能够连接到你的 Linux 服务器。

当 Windows 客户端使用 SMB 访问共享目录时，用户名和密码会随共享目录访问请求一同传输，仅限特定用户。因此，你应该为每个 Windows 用户创建 Linux 用户账户，并使用 `smbpasswd` 命令为他们创建一个 Samba 密码，使其与他们在 Windows 上使用的密码匹配，如下所示：
