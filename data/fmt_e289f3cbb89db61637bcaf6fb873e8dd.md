
```
anon_mkdir_write_enable=YES
```

默认情况下，ftp 用户是匿名用户上传的所有文件的所有者。如果您希望指定匿名上传的文件由其他用户（您自选的用户）拥有，可以使用 `chown_uploads` 和 `chown_username` 选项。例如，如果您有一个名为 `mynewuser` 的用户账户，您可以如下设置这些选项：

```
chown_uploads=YES
chown_username=mynewuser
```

当然，您可以创建并使用任何您想要的用户名。但是，出于安全原因，您不应使用 `root` 登录或其他管理登录来执行此操作。

### 添加消息文件

尽管 vsFTpd 不支持像 WU-FTP 等 FTP 服务器所支持的 README 和欢迎文件布局，但您可以向 vsFTpd 服务器上任何可访问的目录添加 `.message` 文件。然后，如果您如下使用 `dir_message_enable` 选项，当用户进入该目录时，`.message` 文件中的文本将会显示：

```
dir_message_enable=YES
```

您可能至少希望为匿名用户的 FTP 服务器根目录添加一个 `.message` 文件。默认情况下，该位置是 `/var/ftp/.message`。如果您想使用除 `.message` 文件以外的文件，可以设置 `message_file` 选项。例如，要在进入目录时显示 `.my_message` 文件中的文本，您可以添加以下行：

```
message_file=.my_message
```

您还可以设置一条在登录提示之前显示的单行消息。您可以通过输入以下行来执行此操作，并将文本替换为您想要说的任何内容：

```
ftpd_banner=Welcome to my FTP service.
```

### 记录 vsFTpd 活动

在 vsFTpd 中默认启用日志记录，您的 vsFTpd 站点的活动会写入 `/var/log/xferlog` 文件。以下选项启用日志记录并将日志文件更改为 `/var/log/vsftpd.log`：

```
xferlog_enable=YES
xferlog_file=/var/log/vsftpd.log
```

如果您愿意，可以通过将 YES 改为 NO 来关闭日志记录。（但是请注意，日志记录允许您监控潜在的安全入侵，因此不建议关闭它。）或者，您可以通过更改 `xferlog_file` 选项的值来更改日志文件的位置。

```
xferlog_std_format=YES
```

### 设置超时

以下超时设置在 vsFTpd 中默认设置（这些值是内置的，因此您不需要对 `/etc/vsftpd/vsftpd.conf` 文件进行任何修改即可使它们生效）：

```
accept_timeout=60
connect_timeout=60
idle_session_timeout=600
data_connection_timeout=120
```

`accept_timeout=60` 和 `connect_timeout=60` 值分别确定客户端在连接超时需要建立 PASV 或 PORT 风格连接的时间。两者都设置为 60 秒。（请注意，这两行不会自动包含在配置文件中；如果您想更改它们的值，可以手动添加。）`idle_session_timeout=600` 选项会在用户不活动超过 10 分钟（600 秒）时终止 FTP 会话。`data_connection_timeout` 值设置服务器在数据连接没有进展时等待的时间量，然后断开连接（此处的默认值为 120 秒）。

### 导航 vsFTpd 站点

vsFTpd 支持用户可能期望使用的大多数 shell 通配符字符，例如问号和方括号。有一个特别有用的通配符字符可以与 `ls` 命令一起使用，并且还有一个您可以开启的选项。星号（`*`）通配符可以与 `ls` 命令一起使用。同一行中支持多个星号。您可以添加对 `ls` 的 `-R` 选项的支持，以便用户可以递归列出当前目录和所有子目录的内容。要开启此功能（默认情况下是关闭的），您可以将以下行添加到 `vsftpd.conf` 文件：

```
ls_recursion_enable=YES
```

### 获取更多关于 FTP 服务器的信息

有很多资源可以用来获取有关 FTP 服务器的更多信息。以下是您的一些选择：

- **FAQ** — 要查看 vsFTpd 常见问题解答，请转到 `/usr/share/doc/vsftpd*/FAQ`。

- **RFCs** — 请求评论（Requests For Comments）是定义互联网使用标准协议的文档。FTP 的主要 RFC 是 RFC059。您可以从互联网上的各种位置获取 RFC，包括互联网 RFC/FYI/STD/BCP 档案：`www.faqs.org/rfcs`。

- **CERT** — 该组织提供了有关设置 FTP 服务器的有用文档。*匿名 FTP 滥用* 描述了如何应对和恢复 FTP 服务器滥用。它还告诉如何处理软件盗版问题。*匿名 FTP 配置指南* 提供设置 FTP 区域的一般指导，以及设置可写 FTP 区域的具体挑战。这两份文档都可以从 CERT 技术提示页面获取（`www.cert.org/tech_tips`）。

> **提示：** 我强烈建议阅读来自 CERT 的 FTP 文档。这些文档中的提示将有助于保持您的 FTP 服务器安全，同时让您能够提供您希望共享的服务。

### 摘要

FTP 服务是通过互联网向用户提供文档和软件文件归档的主要方法。Fedora 提供的唯一 FTP 服务器包是 Very Secure FTP (vsFTPd) 服务器。vsFTpd 服务器依赖标准的 Linux 文件和用户权限，在 Fedora 中提供一个简单但安全的 FTP 运行环境。

# 第 21 章

# 设置 Web 服务器

## 本章内容

- Web 服务器简介
- 快速启动 Apache Web 服务器
- 配置 Apache Web 服务器
- 启动和停止服务器
- 监控服务器活动

万维网是互联网增长最快的部分。根据 Netcraft (`www.netcraft.com`) 的数据，2004 年 9 月，互联网上有超过 5400 万个网站。电子商务为那些试图保持在技术前沿的企业提供了新的虚拟店面。

Web 也是寻求低成本发布和分发信息的组织的一大福音。随着计算能力的增加、价格的下降、像 Linux 这样的免费操作系统以及像 Apache 和 TUX 这样的免费 Web 服务器，任何人都更容易在 Web 上建立存在。

本章将向您展示如何安装和配置 Apache Web 服务器。服务器每个配置文件的描述和解释都很详细。您将了解启动和停止服务器的各种选项，以及如何监控 Web 服务器的活动。相关的安全关注事项和实践将在本章的描述和示例中加以解决。

> **注意：** 当前版本的 Fedora Linux 附带 Apache 版本 2.0。Apache 2.0 包括对新的 Apache 应用程序编程接口、UNIX 线程（用于多处理）、互联网协议版本 6 (IPv6) 以及多种协议的支持。还添加了一些新模块。在 2.0 版本中，包名称 `apache` 和 `apache-manual` 更改为 `httpd` 和 `httpd-manual`。

### Web 服务器简介

如今所知的万维网始于欧洲粒子物理中心（CERN）的 Tim Berners-Lee 的项目。最初的目标是为地理分散的研究人员和科学家提供一致的用户界面，他们需要访问各种格式的信息。从这个想法中，出现了使用单个客户端（Web 浏览器）访问来自多种类型服务器（HTTP、FTP、SMTP、Gopher、NNTP、WAIS、Finger 和流媒体服务器）的数据（文本、图像、声音、视频和二进制文件）的概念。

Web 服务器通常具有更简单的工作：接受超文本传输协议 (HTTP) 请求并向客户端发送响应。然而，这项工作可能会变得更加复杂（因为服务器还可以执行以下功能，例如：

- 基于文件权限、用户名/密码对以及主机名/IP 地址限制执行访问控制。
- 在将文档发送给客户端之前解析文档（将文档内任何条件字段的适当值替换进去）。
- 生成通用网关接口 (CGI) 脚本或自定义应用程序编程接口 (API) 程序，以评估提交的表单内容、呈现动态创建的文档或访问数据库。
- 向客户端发送 Java 小程序。
- 记录任何成功访问、失败和错误。

#### Apache Web 服务器

Apache Web 服务器最初基于 HTTPd，这是国家超级计算应用中心（NCSA）的一个免费服务器。当时，HTTPd 是互联网上第一个也是唯一的 Web 服务器。不幸的是，服务器开发未能跟上网站管理员的需求，并且已经发现了一些安全问题。许多网站管理员独立地向 NCSA 源代码应用自己的功能和修复。1995 年初，这些开发人员的一个小组汇集他们的努力，创建了一个“拼凑的服务器”，最初只是 HTTPd 代码的一组补丁。从此，Apache 小组大幅重写了代码，并创建了一个稳定的、多平台 Web 服务器守护进程。
