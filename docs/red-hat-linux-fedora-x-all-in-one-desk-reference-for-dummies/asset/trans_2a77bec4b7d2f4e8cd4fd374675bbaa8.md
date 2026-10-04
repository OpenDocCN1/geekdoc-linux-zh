

# 运行独立服务器 613

| 服务名称 |or |
| --- | --- |
| rpcsvcgss | 管理 NFS 版本 4 服务器安全性的服务器，为 NFS 等基于 RPC 的协议提供安全性。 |
| rsync | 支持文件远程复制的服务。你必须启用 xinetd 运行此服务。 |
| saslauth | 支持使用 Cyrus-SASL（简单身份验证与安全层）软件进行认证。 |
| sendmail | 将消息从一台机器移动到另一台机器。如果你想从 Fedora Core 发送邮件，请启动此服务。如果你不计划将 Fedora Core 作为服务器，请不要启动 sendmail 服务器，因为它会降低启动速度并消耗不必要的资源。 |
| services | 列出由 xinetd 管理的活动服务。此服务器需要 xinetd 运行。 |
| sgi_fam | 实现文件更改监控器 (FAM)，用于在文件更改时获取报告。 |
| smartd | 监控许多 ATA、IDE 和 SCSI-3 硬盘内置的自我监控、分析和报告技术 (SMART) 系统。该守护进程可以监控硬盘的可靠性并预测故障，还可以对硬盘执行各种自检。 |
| smb | 启动和停止 Fedora Core 系统上支持 LAN Manager 服务的 Samba smbd 和 nmbd 服务。 |
| snmpd | 用于网络管理的简单网络管理协议 (SNMP) 服务。 |
| snmptrap | 接收并记录名为 TRAP 和 INFORM 的 SNMP 消息。 |
| squid | 互联网对象的缓存服务器——任何可以通过 HTTP 和 FTP 访问的内容。 |
| ssh | 用于 OpenSSH（安全外）安全登录的服务器。 |
| syslog | 许多其他程序（包括其他服务）用于在日志文件中记录错误和状态消息（通常是 /var/log/messages 文件）。始终运行此服务。 |
| telnet | 支持 TELNET 远程登录会话的服务器。你必须启用 xinetd 运行此服务。 |
| tux | 基于内核的 HTTP 服务器。 |
| udev | 管理设备节点。你可以通过编辑配置文件 /etc/udev/udev.conf 来管理 /dev 目录下的设备文件。 |

# 614 运行独立服务器

### 表格 1-1（续）

| 服务名称 | 描述 |
| --- | --- |
| vncserver | 通过运行或停止 X VNC 服务器 (Xnc) 来启动和停止虚拟网络计算 (VNC)桌面。通过运行 VNC 服务器，你可以从网络上的任何其他计算机远程控制 Fedora Core 计算机（你需要在访问 Fedora Core 系统 X 显示的计算机上准备一个 VNC 查看器）。 |
| vsftpd | 用于通过文件传输协议 (FTP) 进行文件传输的安全 FTP 守护进程。 |
| winbind | 启动和停止 Samba winbind 服务器，该服务器提供类似于 /etc/nwitch.conf 文件提供的名称切换功能。 |
| xfs | 启动和停止 X 字体服务器的服务。 |
| xinetd | 互联网服务器，旧版 inetd 的替代品。每当需要时，它会启动 TELNET 和 FTP 等互联网服务。 |
| ybind | 运行在网络信息系统 (NIS) 客户端上的服务，并将客户端绑定到 NIS 域。除非你正在使用 NIS，否则不需要绑定。 |
| ypasswdd | 网络信息系统 (NIS) 修改密码所需的的服务。除非你正在使用 NIS，否则不需要启动 ypasswdd。 |
| ypserv | 网络信息系统 (NIS) 的服务器。除非你正在使用 NIS，否则不需要启动 ypserv。 |
| ypfrrd | 帮助 ypserv 的服务器。仅在你使用网络信息系统 (NIS) 时启动此服务。 |
| yum | 每日运行 Yum 以更新系统上安装的软件包。Yum 是一个程序更新器，类似于 Up2date。 |

## 第 2 章：运行 Apache Web 服务器

**本章内容**

- 探索 HTTP
- 安装 Apache Web 服务器
- 配置 Apache Web 服务器
- 使用 Apache Web 服务器支持虚拟主机

世界维网（WWW 或 Web）将互联网推向主流，因为 Web 浏览器让用户能够浏览存储在各种互联网主机上的文档。无论你是经营小企业，还是为大公司管理计算机系统和网络，都有可能需要设置和维护 Web 服务器。由于 Fedora Core PC 内置了网络支持，它可以成为廉价的 Web 服务器。本章介绍了如何在 Fedora Core PC 上配置 Web 服务器。

## 探索 HTTP

Web 服务器使用 HTTP 提供信息。Web 服务器也称为 HTTP 守护进程（因为持续运行的服务器进程在 UNIX 中被称为守护进程）或简称为 HTTPD。Web 服务器程序（如 Fedora Core 自带的 Apache Web）通常命名为 httpd。

HTTP 代表超文本传输协议（HyperText Transfer Protocol）。超文本是指 Web 页面包含超链接。传输协议是指将 Web 页面跨网络从一台计算机传输到另一台计算机的标准。虽然设置 Web 服务器或使用 Web 浏览器并不真的需要理解 HTTP，但了解它的工作原理有助于你理解 Web 是如何工作的。

你可以使用 TELNET 程序连接到 Web 服务器监听的端口来直观体验 HTTP。在大多数系统中，Web 服务器监听 80 端口并响应发送到该端口的任何 HTTP 请求。因此，你可以使用 TELNET 程序连接到系统的 80 端口（如果该系统有 Web 服务器）并尝试一些 HTTP 命令。

# 616 探索 HTTP

## HTTP 是互联网标准吗？

尽管 HTTP 自 1990 年以来在 Web 中被广泛，但直到最近才成为互联网标准。所有的互联网标准都首先作为征求意见（RFC）发布。第一个与 HTTP 相关的 RFC 是 RFC 1945，“超文本传输协议——HTTP/1.0”（T. Berners-Lee, R. Fielding, and H. Frystyk, 1996）。RFC 1945 被认为是一个信息文档，而不是标准。

Frystyk, L. Masinter, P. Leech, T. Berners-Lee, June 1999 是 HTTP 的草案互联网标准。

要读取这些 RFC，请使用 Web 浏览器访问 www://apps.ietf.org/rfc/ 或 www.faqs.org/rfcs/。

要了解更多关于 HTTP/1.1 及相关标准，请按照以下步骤操作：

1. 确保连接已建立。
2. 输入以下命令：
```
telnet www.gao.gov
```
3. 看到 Connected 消息后，输入以下命令：
```
GET / HTTP/1.0
```
作为对此 HTTP 命令的响应，Web 服务器返回一些信息，随后是默认文件的内容（通常是 index.html）。

```
Trying 161.203.16...
Connected to www.gao.gov.
Escape character is '^'
HTTP/1.1 200 OK
Date: Sat, 13 Mar 2004 21:14:42 GMT
Server: Apache
Connection: close
Content-type: text/html

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.0 Transitional//EN"
http://www.w3.org/TR/html40/loose.dtd">

<HTML>
<HEAD>
<TITLE>The United States Accounting Office</TITLE>
.... (lines deleted)
</HEAD>
.... (lines deleted)

<BODY>
  ... The rest of the document goes here
</BODY>
</HTML>
```

当你用 TELNET 尝试此示例时，你会看到 Web 服务器发送给浏览器的内容。前几行是给浏览器的管理信息。服务器返回这些信息：

- 显示服务器使用 HTTP 协议 1.1且状态码 200 表示成功的：
  HTTP/1.1 200 OK
- 当前日期和时间。示例日期和时间字符串如下：
  Date: Sat, 13 Mar 2004 21:14:42 GMT
- Web 服务器软件名称。例如，对于运行 Apache Web 服务器的站点，服务器返回以下字符串：
  Server: Apache
- 服务器隐藏了版本号和其他细节，这样黑客无法利用 Apache Web 服务器特定版本的已知安全漏洞。
- Web 服务器返回的文档类型。对于 HTML 文档，内容类型报告如下：
  Content-type: text/html

文档本身位于管理信息之后。一个 HTML 文档具有以下通用布局：

```
<title>Document's title goes here</title>
<html>
<body optional attributes go here
  ... The rest of the document goes here
</body>
</html>
```

