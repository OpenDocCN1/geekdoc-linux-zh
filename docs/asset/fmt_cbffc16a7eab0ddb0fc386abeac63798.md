
对于匿名上传，必须激活全局写入启用。您还必须确保 `/var/ftp` 包含一个或多个对匿名用户开放写入权限的目录。例如，您可能想创建一个 `incoming` 目录并开放其权限（`chmod 777 /var/ftp/incoming`）。

匿名用户上传的文件默认以 600 权限创建（赋予 ftp 用户读/写权限，任何其他用户均无法访问，即使是上传文件的用户也无法删除甚至查看它们）。要允许 644 权限，例如，您可以添加以下行：

```
anon_umask=022
```

匿名用户上传的文件默认以 600 权限创建（赋予 ftp 用户读/写权限，任何其他用户均无法访问，即使是上传文件的用户也无法删除甚至查看它们）。要允许 644 权限，例如，您可以添加以下行：

```
anon_umask=022
```

当您允许匿名用户重命名或删除文件时，通过以下内容来启用（前提是用户对文件具有写入权限）：

```
anon_write_enable=YES
```

如果您也允许匿名用户创建自己的目录，请添加：

```
anon_mkdir_write_enable=YES
```

默认情况下，FTP 服务器拥有匿名上传文件的所有权。如果您希望匿名上传的文件由不同的用户所有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果您有一个名为 `newewuser` 的用户，可以这样设置：

```
chown_uploads=YES
chown_username=newewuser
```

当然，可以使用任何用户。出于安全考虑，不应使用 root 或其他。

## 添加消息文件

作为安全措施，您可以考虑添加一个与您运行的操作系统不同的 banner。这可以降低潜在入侵者识别您运行软件的速度。

您还可以在登录提示符之前设置单行消息。您可以通过输入以下内容来实现，将文本替换为您想说的：

`ftpd_banner=Welcome to My service`

## 第 20 章：设置 FTP 服务器

`message_file=.mymessage`

如果您希望能够使用生成统计信息的工具，可以让 vsFTPD 写入 WU-FTPD 和其他 FTP 服务器使用的标准 xlog 格式。要将传输数据存储在 xlog 格式中，请设置以下选项：

```
xferlog_std_format=YES
```

FTP 启用日志，您的 vsFTPD 活动写入 `/var/log/xlog` 文件。以下选项启用日志并更改日志文件：

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

如果您愿意，可以将 YES 更改为 NO 来关闭日志。（但注意，日志允许您监控潜在的入侵，因此不建议关闭。）或者可以通过更改 `xferlog_file` 的值来更改日志的位置。请记住，在流量很大时，您的 FTP 服务器会产生大量的日志。为了使其有用，您需要经常监控日志。

### 设置超时

超时在 vsFTPd 中默认设置（这些值是内置的，因此无需对 `/etc/vsftpd/vsftpd.conf` 文件进行任何更改即可生效）：

`accept_timeout=60` 和 `connect_timeout=60` 值决定了客户端在超时之前建立 PASV 或 PORT 连接的等待时间。这两个值未自动包含在配置文件中；如果您想更改它们，可以手动添加。`idle_session_timeout=600` 选项会导致用户空闲超过 10 分钟（600 秒）时掉线 FTP 会话。`data_connection_timeout`

## 824 第四部分：Fedora 和 RHEL 网络与服务器设置

`value` 设置了服务器在断开连接之前等待无进展状态的时间（此处的默认值值为 120 秒）。

### 导航至 vsFTpd 站点

用户可能预期使用的绝多数通配符（如问号和括号）都受 vsFTpd 支持。有一个你可以配合 `ls` 命令使用的特别有用的通配符字符，以及一个可以开启的选项。星号 (`*`) 通配符可以与 `ls` 命令配合。支持在同一行中使用多个星号。你可以为 `ls` 添加 `-R` 选项的支持，以便递归列出当前目录及其所有子目录的内容。要开启此功能（默认关闭），你可以在 `vsftpd.conf` 文件中添加以下行：

```
ls_recurse_enable=YES
```

### 在在防火墙后设置 vsFTpd

如果你在防火墙后配置 FTP 服务器，将需要进行一些特殊配置，以允许通信通过防火墙到达你想要访问服务器的用户。为了解决这个问题，可以使用临时端口号（它们在所需的数字范围内提供随机的临时端口号）。关于该问题的描述，请参考 www.ncftpd.com/ncftpd/doc/misc/ftp_firewalls.html 上的 FTP 和防火墙页面。

### 获取更多关于 FTP 服务器的信息

有许多资源可以获取更多关于 FTP 服务器的信息。以下是一些选项：

- FAQ — 要查看 vsFTpd 的常见问题解答，请前往 `/usr/share/doc/vsftpd*/FAQ`。

- RFCs — 征求意见（Requests For Comments）是定义互联网标准协议的文档。FTP 的主要 RFC 是 RFC959。你可以从互联网上的多个位置获取 RFCs，包括互联网 RFC/FYI/STD/BCP 存档（www.faqs.org/rfcs）。

- CERT — 该组织为设置 FTP 服务器提供了实用的文档。《匿名 FTP 滥用》（Anonymous FTP Abuses）描述了如何应对并从 FTP 服务器被滥用中恢复。它还告诉了如何处理软件盗版问题。《匿名 FTP 配置指南》（Anonymous FTP Configuration Guidelines）为设置你的 FTP 区域提供了通用指导，并说明了设置可写 FTP 区域的特定挑战。这两份文档均可在 CERT Tips 页面（www.cert.org/tech_tips）获得。

> 提示：我强烈建议阅读 CERT 的 FTP 文档。这些文档中的技巧将帮助保持你的 FTP 服务器安全，让你能够提供你想要共享的服务。

## 总结

FTP 服务是通过互联网向用户提供文档和软件文件存档的主要方法。Fedora 和 RHEL 附带唯一的 FTP 服务器包是极安全 FTP（vsSFTPd）服务器。vsSFTPd 服务器依赖标准的 Linux 文件和用户权限，在 Fedora 中运行提供一个简单而安全的 FTP 环境。

# 第 21 章

# 设置 Web 服务器

**本章内容包括**

- Web 服务器简介

- 快速启动 Apache Web 服务器

- 配置 Apache Web 服务器

- 启动和停止服务器

- 监控服务器活动

今天约 60% 的 Web 网站由开源的 Apache Web 服务器项目驱动（相比之下，微软 Web 服务器的占比约为 31%）。2007 年年中旬，Netcraft（www.netcraft.com）收到了来自超过 6600 万个运行 Apache 的站点的响应。随着互联网域名的注册以每月超过 100 万个的平均速度持续增长，Apache 正在占据新启动 Web 网站的大份额。

Web 对于寻求廉价手段发布和分发信息的组织来说也是一种福音。使用本书附带的 Fedora Linux 发行版或 RHEL，你可以使用 Apache 项目提供的软件来启动你自己的 Web 网站。将你自己的域名、互联网连接以及 Fedora 或 RHEL 结合，在世界维网上创建你自己的阵地。

本章将向你展示如何安装和配置 Apache Web 服务器。书中将详细描述并解释服务器的每一份配置文件。你将学习到启动和停止服务器的各种选项，以及如何监控 Web 服务器的活动。整个本章的描述中都涉及了相关的安全考虑和实践，并在第 14 章的特殊 Web 服务器安全章节（“使用证书和加密保护 Web 服务器”）中也进行了阐述。

> 注意：当前版本的 Fedora 带有 Apache 2.2 版本。Apache 2.2 支持新的 Apache 应用程序接口、UNIX 线程（用于多处理）、互联网协议版本 6 (IPv6) 以及多种协议。如果你一直在使用 2.0 之前的 Apache 版本，应该包名 `apache` 和 `apache-manual` 已更改为 `httpd` 和 `httpd-manual`。

## Web 服务器简介

现为人知的维网（Wide Web）始于姆·伯纳斯-李（Tim Berners-Lee）在欧洲粒子物理中心（CERN）的一个项目。最初的目标是为地理位置分散的研究人员和科学家提供一个统一的接口，以便他们访问各种格式的信息。这一想法产生了使用一个客户端（Web 浏览器）从多种类型的服务器（HTTP, FTP, SMTP, Gopher, NNTP, WAIS, Finger 和流媒体服务器）访问数据（文本、图像、声音、视频和二进制文件）。

服务器通常的工作更为简单：接受超文本协议（HTTP）请求并向客户端发送响应。然而，这项工作可能会变得复杂得多（因为服务器需要）：

- 接受超文本协议（HTTP）请求并向客户端发送响应。

- 动态处理实时内容。
