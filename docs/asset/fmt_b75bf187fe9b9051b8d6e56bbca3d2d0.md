
随着`AOL/Netscape`与`Sun`之间联盟的出现，对`FastTrack`的兴趣重新复燃。它现在是`iPlanet` Web 和应用程序服务器家族的一部分。`FastTrack`现在是基于 Java 的`iPlanet` Web 服务器免费版。该服务器的企业版本是一个商业产品。

`FastTrack`是一个易于管理的Web服务器。所有配置和管理都通过基于Web的表单完成。这些表单允许管理员完成从创建用户到控制目录级文件访问的所有操作。

`FastTrack`提供对服务器端包含（SSI）、CGI 以及`Netscape`用于开发的 API 支持。此外，`FastTrack`还可以支持`Netscape`的服务器端 JavaScript 开发环境`LiveWire`。

该服务器还可以通过`SSL`技术作为安全服务器使用。

# AOLserver

`AOLserver`拥有有趣的历史，从 1995 年的商业产品变成了目前可用功能最全的免费服务器之一。

`AOLserver`起于`NaviPress`，这是最早的商业服务器之一。1995 年底，`AOL`收购了生产`NaviPress`的公司并开始在内部使用该服务器。1997 年初，`AOL`将该服务器作为免费产品在互联网上发布。

编写期间，`AOLserver`的最新版本（`3.3`）包含以下功能：

- 内置全文索引，用于为网站提供搜索功能
- 可从 C 和 `Tcl`（`v.7.6`）脚本语言访问的内置 API
- 全 CGI（可选）和服务器端包含支持
- 类似于`Microsoft Active Server Pages`的服务器端动态页面功能
- 数据库连接，用于在没有第三方 Web-数据库集成工具的情况下构建数据库驱动的动态应用程序

截至编写，尽管`AOL/Netscape`与`Sun`的联盟在`iPlanet`系列服务器上付出了努力，但`AOLserver`仍受到支持。你可以在`AOLserver`网站`www.aolserver.com`下载`AOLserver`。

# Java Web Server

来自`Sun` Java 部门的`Java Web Server`是此列表中一个独特的 Web 服务器。像`Jigsaw`一样，`Java Web Server`理论上可以运行在任何带有 Java 虚拟机的平台上。

`Java Web Server`提供了许多使其具有竞争力的功能，包括对 CGI 的支持以及对`SSL`的完全支持，以便该服务器用于在线商店等安全应用程序。

为了提高性能，可以生成包含 HTML 和程序代码的编译页面。为了统计目的，可以使用内置的跟踪机制跟踪用户会话。

遗憾的是，随着`AOL/Netscape`与`Sun`联盟的扩大，他们有三个 Web 服务器需要支持。截至编写，已决定在 2001 年初停止该产品的开发。尽管如此，这仍然是一个热门的选择。如果你需要管理或支持`Java Web Server`，可以在主页`www.javasoft.com`查看其完整规范。

# Zeus

本调查讨论的最后一个 Web 服务器是`Zeus`服务器。`Zeus`是适用于`Unix/Linux`和`Windows NT`的 Web 服务器。它提供了内置的集群支持，这显然使其定位为高流量网站的潜在选择。通过集群，可以从多个 Web 服务器提供单个 Web 地址，并允许将请求负载分布到一组服务器上，这意味着可以处理更多的并发访问。

这种功能帮助`Zeus`成为一些访问量网站（包括`eBay`和英国电信）的首选 Web 服务器。在最近的一篇文章中，`IBM` Linux 技术中心发现`Linux 2.4`内核服务器上的`Zeus`性能几乎是`Linux 2.2`内核服务器的两倍。

此外，`Zeus`还支持微软`Internet Information Server`的 API —— `ISAPI`，并在`Unix`以及`Windows NT/2000`上都提供这种支持。`Zeus`还支持像`Java Web Server`中那样的 Java servlet，并使用`JDBC`标准提供集成数据库连接。

可能最有趣的是，`Zeus`全范围内提供`SSL`，并提供全 128 位加密。由于美国政府限制 128 位加密技术的出口，美国公司出口的大多数安全产品仅提供缩水的 56 位加密。大多数报道的破解`Netscape`等产品加密的事件都涉及产品的 56 位加密版本。`Zeus`的信息可以在`www.zeus.uk`获取。

# 安装 Apache

本章的其余部分将详细介绍`Apache` Web 服务器，原因如下：

1. `Apache`服务器是大多数 Linux 发行版自带的默认 Web 服务器（包括随本书附带的光盘中的`Red Hat Linux 7`）。
2. `Apache`是目前互联网上最流行的 Web 服务器，它很可能是你想要使用的 Web 服务器。

如果你在设置 Linux 系统时执行了相当完全的安装，那么很有可能你已经安装了`Apache`。有几种方法可以检查这一点。例如，你可以使用`rpm`命令：

```bash
$ rpm -q apache
```

如果你已经安装了`Apache`，你将得到类似所示的结果：

```
apache-1.3.12-25
```

如果你收到`Apache`已安装的指示，可以直接跳到“配置 Apache”章节。

# 从 Red Hat 光盘安装 Apache

安装`Apache`最简单的方法是使用随本书附带的`Red Hat`光盘。要实现这一点，只需挂载光盘（通常在`/mnt/cdrom`），然后使用`cd /mnt/cdrom/RedHat/RPMS`命令。如果你将光盘挂载到`/mnt/cdrom`以外的路径，你需要根据挂载点更改相应的目录。该目录包含了完整`Red Hat Linux`发行版的所有`RPM`文件。在这里，你只需使用`rpm`安装包即可：

```bash
$ rpm -i apache-1.3.12-25.i386.rpm
```

# 下载最新版本的 Apache

如果你计划运行关键任务或高流量的 Web 服务器，你可能想从`www.apache.org`下载最新版本的`Apache`（见图 32.1）。通过使用最新版本，你可以确保小 Bug 不会影响普通网站，且不会困扰你更复杂或使用更频繁的网站。

# 图 32.1：Apache 网站

![](img/bc3027047bbbcc0b55a71a4b67c60968_750_0.png)

## 注意

所有关于`Apache`配置和管理的讨论均假设你正在使用本书附带的`Red Hat`光盘上的`Apache`版本。通常，`Apache`的新版本是向后兼容的。也就是说，你在本章中看到的配置文件应该适用于较新版本的`Apache`。

从`Apache`网站下载`Apache`时，你有权下载原始源代码或适用于 Linux 的预编译二进制文件。虽然使用源代码版本有充分的理由，特别是当你计划使用`Apache` API 开发程序时，或者你想向服务器中构建模块时，但你应该下载预编译的二进制文件来设置具有基础`Apache`功能集的网站。本书将不会讨论编译你自己的`Apache`，因为这需要对 Web 服务器进行更深入的讨论，单个章节无法提供的。

如果你想从`Apache`获取最新的二进制分发版，请将浏览器指向`Apache`网站（`http://apache.org`）并点击那里的`Download`链接。这将进入一个文件目录。有时可以在此目录找到最新发布版本。如果没有，请遵循`httpd`和`binaries`链接，然后选择你的操作系统（在本例中为 Linux）。在这里你将找到可用文件列表。

在编写时，此列表包含以下内容：

```
apache_1.3.9-sparc-whatever-linux.README
apache_1.3.9-sparc-whatever-linux.tar.gz
apache_1.3.9-sparc-whatever-linux.tar.gz.asc
apache_1.3.6-armv41-whatever-linux2.README
apache_1.3.6-armv41-whatever-linux2.tar.gz
apache_1.3.9-i586-whatever-linux2.README
apache_1.3.9-i586-whatever-linux2.tar.gz
apache_1.3.9-i586-whatever-linux2.tar.gz.asc
apache_1.3.14-i686-whatever-linux2.README
apache_1.3.14-i686-whatever-linux2.tar.gz
apache_1.3.14-i686-whatever-linux2.tar.gz.asc
apache_1.3.9-sparc-whatever-linux.tar.gz
apache_1.3.9-i586-whatever-linux2.tar.gz
apache_1.3.14-i686-whatever-linux2.tar.gz
```

# 配置 Apache
