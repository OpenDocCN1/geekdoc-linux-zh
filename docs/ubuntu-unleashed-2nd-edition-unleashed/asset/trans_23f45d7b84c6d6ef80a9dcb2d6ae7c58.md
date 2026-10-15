

## NOTE

许多 Linux 用户现在使用 OpenSSH 及其客户端套件，例如 sftp 命令，以在传输文件时获得更安全的解决方案。OpenSSH 套件提供 sshd 守护进程并启用加密远程登录（有关更多信息，请参阅第 19 章）。

## Choosing an Authenticated or Anonymous Server

在准备设置 FTP 服务器时，您必须首先决定安装经过身份验证的服务还是匿名服务。经过身份验证的服务需要输入有效的用户名和密码才能访问。如前所述，匿名服务允许使用用户名 anonymous 和电子邮件地址作为密码进行访问。

经过身份验证的 FTP 服务器用于为远程用户提供一定程度的安全数据传输，但由于使用用户名和密码，因此需要维护用户账户。匿名 FTP 服务器在不需要或不必要用户身份验证时使用，可以在为客户支持或公开分发文档、软件或其他数据提供易于访问的平台方面有所帮助。

如果您在家庭或企业 Linux 系统中使用匿名 FTP 服务器，那么正确安装和配置它以保持相对安全的环境至关重要。通常，托管匿名 FTP 服务器的站点会将其放置在防火墙外部的专用机器上。专用机器仅包含 FTP 服务器，并且不应包含无法快速恢复的数据。这种专用机器设置可以防止恶意用户在入侵服务器后获取关键或敏感数据。作为额外的，但绝不是更安全的设置，文件系统的 FTP 部分可以从单独的硬盘分区或卷以只读方式挂载，或从只读介质（如 CD-ROM、DVD 或其他光学存储）挂载。

## Ubuntu FTP Server Packages

非常安全的 vsftpd 服务器，与本章中也讨论的 wu-ftpd 一样，采用 GNU GPL 许可。该服务器可用于个人或商业用途。wu-ftpd 和 vsftpd 服务器将在本章的其余部分介绍；只需启用 Universe 仓库即可查看可供您使用的完整 FTP 服务器列表。

## Other FTP Servers

一种替代服务器是 NcFTPd，可从 http://www.ncftp.com 获得。该服务器独立于 inetd 运行（通常用于启用和启动 wu-ftpd 服务器），并提供自己的优化守护进程。此外，NcFTPd 能够将 FTP 服务器的目录列表缓存到内存中，从而提高用户获取可用文件和目录列表的速度。虽然 NcFTPd 相对于 wu-ftpd 具有许多优势，但 NcFTPd 并非 GPL 许可软件，其许可费用根据最大同时服务器连接数而变化（51 个或以上并发用户为 $199，最高 50 个并发用户为 $129，但对具有合规域名教育机构免费）。

## NOTE

请勿将 ncftp 客户端与 ncftpd 混淆。Ubuntu 中包含的 ncftp-3.1 软件包是客户端软件，是 ftp-0.17 的替代品，并包含 ncftpget 和 ncftpput 命令，用于通过命令行或使用远程文件统一资源定位符（URL）地址传输文件。ncftpd 是 FTP 服务器，可从 www.ncftpd.com 下载。

Linux 的另一个 FTP 服务器软件包是 ProFTPD，采用 GNU GPL 许可。该服务器与大多数 Linux 发行版配合良好，已被许多 Linux 站点使用，包括 ftp.kernel.org 和 ftp.sourceforge.net。ProFTPD 积极维护并更新以修复错误和安全增强。其开发人员建议您使用最新版本（截至本文撰写时为 1.2.10），以避免暴露于利用和漏洞。浏览至 http://www.proftpd.org 下载副本。

又一个 FTP 服务器软件包是 Bsdftpd-ssl，它基于 BSD ftpd（并在 BSD 许可下分发）。Bsdftpd-ssl 提供使用安全扩展的同时标准和安全访问；安全访问需要特殊客户端。有关更多详细信息，请浏览至 http://bsdftpd-ssl.sc.ru。

最后，另一个替代方案是使用 Apache（和 HTTP 协议）来提供文件。使用 Web 服务器提供数据下载可以减少在服务器上监控和维护单独软件服务（或目录）的需求。这种提供文件的方法还可以减少系统资源需求，并为远程用户在下载时提供更多灵活性（例如，使其能够一次下载多个文件）。有关使用 Apache 的更多信息，请参阅第 20 章“Apache Web Server Management”。

## Installing FTP Software

作为标准安装的一部分，FTP 客户端软件已经安装。您可以通过使用 dpkg、grep 和 sort 命令进行此查询来验证 FTP 相关软件是否已安装在您的系统上：

```
$ dpkg --get-selections | grep ftp | sort
```

示例结果可能有所不同，具体取决于安装了哪些软件包。在您的 Ubuntu 文件系统中，您会发现文件 /usr/bin/pftp 符号链接到 /usr/bin/netkit-ftp，以及 /usr/sbin 目录下的 vsftpd 服务器。其他已安装的软件包包括额外的基于文本和图形的 FTP 客户端。

如果未安装 vsftpd，您可以通过 Synaptic 安装它。

