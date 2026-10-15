

将该用户的权限映射到 FTP 目录。默认情况下，FTP 服务器还要求用户使用有效的 shell。它会检查 /etc/shells 文件中的有效 shell 列表。大多数守护进程都有选项可以关闭此功能。

## 可用服务器

在 Red Hat 系统上可以使用多个 FTP 服务器（见表 21-1）。Red Hat 附带了非常安全的 FTP 服务器 vsftpd。你可以从其 FTP 站点（如 ftp.redhat.com）下载特定发行版的 RPM 包更新。软件包包含术语 ftpd。非常安全的 FTP 服务器提供了比 WU-FTPD 简单且更安全的替代方案，尽管它缺乏 ProFTPD 的安全选项和可配置性。

ProFTPD 是一个基于 Apache Web 服务器设计的流行 FTP 守护进程。它具有简化的配置和对虚拟 FTP 主机的支持。虽然它目前未包含在大多数发行版中，但你可以从发行版站点以及 ProFTPD 站点下载 RPM 包。包名以术语 proftpd 开头。最新版本的压缩归档以及文档可在 ProFTPD 网站 www.proftpd.net 上获得。另一个 FTP 守护进程 NcFTPd 是由制作 NcFTP FTP 客户端的同一程序员生产的商业产品。NcFTPd 可供学术用途免费使用，并为小型网络提供减免费用。有关更多信息，请查看 www.ncftpd.org。

还有多个基于安全性的 FTP 服务器可用，包括 SSLFTP 和 SSH sftpd，以及 gssftpd。SSLFTP 使用 SSL（安全套接字层）来加密和验证传输，并使用 MD5 摘要来检查传输文件的完整性。SSH sftpd 是一个 FTP 服务器，现已成为 Open SSH 包的一部分，使用 SSH 加密和身份验证来建立安全的 FTP 连接。gssftpd 服务器是 Kerberos 5 包的一部分，并为 FTP 操作提供 Kerberos 级别的安全性。

## Red Hat FTP 服务器目录

Red Hat 目前在安装期间安装 vsftpd 服务器包以及匿名 FTP 支持。此时，会创建 ftp 目录以及几个子目录，您可以在其中放置供 FTP 访问的文件。目录已配置为通过远程用户控制访问，仅限制使用 ftp 目录及其任何子目录。ftp 目录由不同发行版放置在不同目录中。在 Red Hat 上，ftp 目录放置在 /var 目录中，即 /var/ftp。将您希望允许访问的文件放在 /var/ftp/pub 目录中。例如，在 Red Hat 上，这将位于 /var/ftp/pub。

您还可以创建子目录并在其中放置文件。一旦连接到网络，远程用户就可以连接到您的系统并下载您放置在 /var/ftp/pub 或其任何子目录中的文件。vsftpd FTP 包为这些目录及其文件实现了默认配置。您可以根据需要更改这些配置。如果您要自行安装 FTP 服务器，则需要了解以下各节中详细说明的安装 FTP 服务器并创建其数据目录的程序。

vsftpd FTP 包不会创建用户可以上传文件到 FTP 站点的目录。这样的目录通常命名为 incoming 目录，位于 ftp/pub/incoming。如果您想要这样的目录，您必须创建它，使其成为 ftp 组的成员，然后设置其权限以允许用户写入访问。

```
chgrp ftp /var/ftp/pub/incoming
chmod g+w /var/ftp/pub/incoming
```

| FTP 服务器 | 站点 |
|---|---|
| 非常安全的 FTP 服务器 (vsftpd) | vsftpd.beasts.org |
| ProFTPD | www.proftpd.net |
| NcFTPd | www.ncftpd.org |
| SSH sftp-server | www.openssh.org |
| 华盛顿大学 Web 服务器 (WU-FTPD) | www.wu-ftpd.org |
| Tux | 具有 FTP 功能的 Web 服务器 |
| gssftpd | Kerberos FTP 服务器 |

## FTP 用户

在 FTP 服务器上拥有账户的普通用户只需登录其账户即可获得完全的 FTP 访问权限。此类用户可以直接从自己的账户或其有权访问的任何目录访问和传输文件。您还可以创建称为访客用户的用户，他们对 FTP 公共可访问目录的访问受到限制。这涉及设置标准用户限制，并将 FTP 公共目录作为其主目录。

## 匿名 FTP：vsftpd

匿名 FTP 站点本质上是系统上的一个特殊用户，其主目录中包含公共可访问的目录和文件。任何人都可以登录此账户并访问其文件。由于任何人都可以登录匿名 FTP 账户，您必须小心将远程 FTP 用户限制为仅匿名 FTP 目录上的文件。通常，用户的文件与系统的整个文件结构相互连接。普通用户具有写入访问权限，可以创建或删除文件和目录。匿名 FTP 文件和目录可以配置为使其隐藏系统的其余文件系统，并且仅向远程用户授予读取访问权限。在 ProFTPD 中，这是通过在其配置文件中放置配置指令来实现的。vsftpd 包实现的一种较旧的方法涉及在 FTP 主目录的子目录中放置某些系统配置、命令和库文件的副本。对这些子目录施加的限制随后控制其他用户的访问。在 FTP 主目录内，您然后有一个公共可访问的目录，其中包含您希望提供给远程用户的文件。该目录通常名为 pub，表示公共。

FTP 站点由 FTP 用户账户、FTP 主目录以及包含所选配置和支持文件的某些系统目录的副本组成。新一代 FTP 守护进程，例如 ProFTPD，不需要系统目录和支持文件。大多数发行版，包括 Red Hat，在您安装系统时已经设置了 FTP 用户账户。

