
## 总结

在本章中，我们描述了在您的 Linux 系统上设置网络软件的流程：

- 编译支持网络服务的 Linux 内核
- 执行基础配置，包括编辑 `hosts`、`services` 和 `inetd.conf` 文件
- 使用网络命令在您的系统中启动网络，并将这些命令插入相应的 `rc` 文件中，以便在启动 Linux 系统时自动开启网络
- 排除某些基础网络问题以及如何使用监控工具
- 编写脚本建立到互联网服务提供商的 PPP 连接，将您的机器连接到互联网
- 在您的机器上设置自动拨号以自动拨打您的 ISP（互联网服务商）

## 第 4 章

# 使用网络的命令

本章内容

- ftp：传输文件
- telnet
- Usenet 新闻
- 浏览器

在您探索 Linux 网络的**这一阶段**，您的 Linux 机器已经在与互联网上的其他主机进行通信。编译软件和修改配置脚本的工作已经完成；现在是时候享受探索互联网的乐趣了。

为了帮助您探索互联网，Linux 提供了许多实用的应用程序。其中许多应用程序都是经典工具，您可能在其他时间或其他地方遇到过它们。而其他工具对您来说可能是全新的。

在本节中，我们介绍了四种常用的网络应用程序：

- ftp：允许您在远程主机之间传输文件
- telnet：模拟连接到远程主机的终端
- trn：允许您阅读和发布 Usenet 新闻
- lynx 和 Netscape Navigator（网景浏览器）：允许您浏览万维网

这些并不是可以在互联网上运行的全部应用程序，但它们是其中最常见且最实用的。

请注意，存在另一组命令，被称为 r* 命令（每个命令都以字母 r 开头），我们将在第 6 章中介绍这些命令。这些命令几乎总是用于内域网而不是互联网：它们很有用，但存在安全风险，因此仅供本地用户（据推是值得信任的）使用。如果您是通过以太网而不是通过调制解调器将您的 Linux 系统连接到内域网，在读完本章后，您可能想直接跳到第 6 章，并阅读关于 r* 命令的章节。

# ftp：传输文件

ftp 是一个使用 TCP/IP 文件传输协议（FTP）的应用程序，帮助您将文件从一个主机传输到另一个主机。ftp 使用传输控制协议（TCP）来可靠地传输数据。

ftp 是最老的 TCP/IP 应用程序之一，正因如此，它的面向文本的界面相当笨拙。然而，它仍然是执行从一个主机复制文件到另一个主机这一平凡但必要的任务时最有用的工具之一。

在本节中，我们将展示您如何调用 ftp 并使用它登录另一个系统；并向您展示最常用的命令。

## FTP 协议

ftp 实现了 1985 年 10 月份的 RFC 959 中描述的文件传输协议（FTP）。可以从 InterNIC 网站（www.internic.net）下载该 RFC 的副本。

简而言之，FTP 描述了一组 FTP 客户端可以发送给 FTP 服务器的指令，以及服务器回复时发送的消息。FTP 还描述了客户端和服务器之间建立的通道，允许客户端在文件正在上传到服务器或从服务器下载时，仍能向服务器发送命令。

目前没有专门的人详细介绍该协议的细节，但如果您感兴趣，我们敦促您阅读它。与大多数互联网 RFC 一样，RFC 959 写得非常清晰，非深通互联网历史的人士也能读懂。

# 使用 ftp：一个示例

ftp 是一个具有大量子命令和选项的命令。然而，在大多数情况下，您只使用它可选的几个命令和选项；因此，学习如何使用 ftp 最简单最好的方法是走一遍 ftp 会话示例。

在本节中，我们将完成一个简单的任务：从堪萨斯大学的公开存档下载文件。接下来的小节提供了 ftp 命令和选项的概述。

# 调用 ftp 并登录

要调用命令 `ftp`，请输入：

```
ftp hostname
```

其中 `hostname` 是您想要交换文件的主机；或者输入：

```
ftp ipaddress
```

其中 `address` 给出您想要交换文件的主机的 IP 地址。

例如，堪萨斯大学在线提供了许多北欧圣哲的译本。如果您想浏览这些可用文本，请输入：

```
ftp ukanaix.cc.ukans.edu
```

一旦建立连接，您将看到：

```
Connected to raven.cc.ukans.edu
220
220 You have connected from: fred@myipprovider.com
220
220 For assistance call 864 0110 to report network problems
call 864 0200
220
220 Login as 'kufacts' for access to the Campus Wide Information System.
220  'lynx' for access to the World Web using Lynx.
220  'www' for access to the World Web using Lynx.
220  'linemode' for access to the World Wide Web using
220 Line Mode.
220  'history' for history network resources.
220  'ex ussr' for former Soviet Union info.
220
220 raven.cc.ukans.edu FTP server (Digital UNIX 5.6) ready.
ukanaix.cc.ukans.edu:fred):
```
