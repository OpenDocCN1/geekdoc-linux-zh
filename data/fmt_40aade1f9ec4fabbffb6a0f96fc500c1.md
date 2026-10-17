
```
From root@Athena.UniversalExport.ca  Mon Mar 14 06:28:52 2005
Return-Path: <root@Athena.UniversalExport.ca>
X-Original-To: root
Delivered-To: root@Athena.UniversalExport.ca
Received: from ws1.UniversalExport.ca (localhost [10.20.4.1])
    by Athena.UniversalExport.ca (Postfix) with ESMTP id 9C71D25D72
    for <root>; Mon, 14 Mar 2005 06:28:19 -0500 (EST)
To: root@Athena.UniversalExport.ca
    tasha@Athena.UniversalExport.ca
From: root@Athena.UniversalExport.ca
    tasha@Athena.UniversalExport.ca
SUBJECT: Test mail via telnet
Message-Id: <20050314112819.9C71D25D72@Athena.
    UniversalExport.ca>
Date: Mon, 14 Mar 2005 06:28:19 -0500 (EST)
Status: RO

This is a test mail sent via telnet.
```

电子邮件是软件病毒传播最常见的途径之一。SLES 9 随带 AMaViS（A Mail Virus Scanner，http://amavis.sourceforge.net）和 AMaViGate（http://www.nbedv.com）以帮助保护系统。SLES 介质上的包名分别为 `amavisd-new` 和 `amavigate`，安装 Postfix 时自动安装。注意 AMaViS 要求已安装病毒扫描程序，详情见 `/usr/share/doc/packages/amavisd-new`。

以下为可能满足需求的商业反病毒解决方案示例：

- BitDefender for Postfix (http://www.bitdefender.com)
- Sophos Anti-Virus for Linux (http://www.sophos.com)
- Kaspersky Anti-Virus Business Optimal (http://www.kaspersky.com)
- F-Prot Antivirus for Linux (http://www.f-prot.com)

### 文件传输服务

文件传输协议（FTP）是 Internet 上在服务器间复制文件最常见的方式。大多数基于 Web 的下载站点使用浏览器的内置 FTP 功能，因此大多数服务器操作系统通常将 FTP 服务器应用作为软件套件的一部分。Linux 也不例外。有大量商业和免费的 Linux/Unix FTP 服务器可供选择，例如：

- NcFTP Server (http://www.ncftp.com/ncftpd)；商业
- ProFTPD (http://www.proftpd.org)；免费，GPL 许可
- Pure-FTPd (http://www.pureftpd.org)；免费，BSD 许可
- glFTPd (http://www.glftpd.com)；免费
- vsftpd (http://vsftpd.beasts.org)；免费，GPL 许可
- wu-ftpd (http://www.wu-ftpd.org)；免费

Trivial File Transfer Protocol（TFTP）也常用于在网络上提供启动映像以实现无盘工作站的远程启动。TFTP 服务器还用于为网络设备（如路由器和交换机）提供固件更新映像。您也可以将设备配置数据保存到 TFTP 服务器。与 FTP 服务器类似，有许多 TFTP 服务器，例如 Jean-Pierre Lefebvre 编写的 `atftp` (`ftp://ftp.mamalinux.com/pub/atftp`) 和 `tftp-hpa` (`http://www.kernel.org/pub/software/network/tftp`)，可用于各种 Linux/Unix 发行版。

本节介绍如何使用 SLES 9 中包含的 Very Secure FTP Daemon (`vsftpd`) 和 Pure-FTPd (`pure-ftpd`) 软件包设置 FTP 服务器。此外，我们还介绍如何使用随 SLES 9 提供的标准 TFTP 服务器 `in.tftpd` 设置 TFTP 服务器；`atftp` 也包含在 SLES 9 中，但本文不讨论。

### 使用 Pure-FTPd

Pure-FTPd 基本上是一个命令行驱动的应用程序。所有选项都需要在命令行中指定。你可以从其 man 手册 (`man pure-ftpd`) 获取完整列表，或在终端提示符下输入以下命令：

```
pure-ftpd --help
```

你会发现 Pure-FTPd 使用全部 26 个字母（大小写均可）以及一些数字作为开关。以下列表简要解释了一些常用的选项：

- `-A` 将对除 root 之外的所有用户进行 chroot。
- `-b` 指示 `pure-ftpd` 忽略一些标准以处理 Internet Explorer 等有问题的客户端。
- `-B` 在后台启动独立服务器（即“守护进程化”模式），这等同于运行 `./pure-ftpd &`。
- `-c #` 将最大客户端数量限制为 #；默认值为 50。
- `-C #` 将同一 IP 地址的并发连接数限制为 #；默认值为 50（或最大客户端数）。
- `-e` 仅允许匿名用户。此选项与 `-E` 互斥。
- `-E` 仅允许已认证用户（即禁用匿名 FTP 访问）。
- `-H` 阻止将客户端 IP 地址解析为 DNS 名称（因此会记录 10.58.2.5 而不是 `ws2.UniversalExports.ca`）。这可以显著加快连接速度，并有助于减少繁忙服务器（尤其是在公共 FTP 服务器上）的（反向 DNS）带宽使用。
- `-j` 如果不存在则创建用户的主目录。这允许按需创建主目录。此选项在使用 Unix 以外的认证方式（如 LDAP（见下文 -l 选项））时尤其有用。只需在数据库中插入新条目，账户即可使用。无需为该用户创建任何目录：它将在用户首次登录时自动创建。
- `-l authentication_method: filename` 启用新的认证方法并指定包含认证数据的
