
检查 `cupsd` 正在监听哪些地址。为了让远程系统能够打印，`cupsd` 进程必须在 `localhost` 之外监听。按照如下方式（作为 `root` 用户）使用 `netstat` 命令进行此检查。第一个示例显示 `cupsd` 仅监听在本地主机（`127.0.0.1:631`）；第二个示例显示 `cupsd` 监听在所有网络接口（`0.0.0.0:631`）；

```
# netstat -tupl | grep 631
tcp       0 127.0.0.1:631         0.0.0.0:*      LISTEN
6492/cupsd
# netstat -tupl | grep 631
tcp       0 0.0.0.0:631             0.0.0.0:*      LISTEN
6492/cupsd
```

对共享打印机的更改可以在 `/etc/cups/` 目录下的 `cupsd.conf` 和 `printers.conf` 文件中进行。

# 配置共享 Samba 打印机

你的 Linux 打印机可以配置为 SMB 打印机，以便在 Windows 系统上显示可用。要像 Samba (SMB) 打印机一样共享你的打印机，只需按照第 19 章“配置 Windows 文件共享服务器”中的描述配置基本的 Samba 服务器设置。你所有的打印机默认都应该在本地网络上共享。下一节将展示生成的设置外观，以及你可能想要更改它们。

## 理解用于打印的 sm.conf

当你配置 Samba 时，系统会构建 `/etc/smb.conf` 文件以启用你所有配置的打印机进行共享。以下是 `smb.conf` 文件中与打印机共享相关的几行：

```
[global]
..
load printers = yes
cups options = raw
printcap name = /etc/printcap
printing = cups
...
```

```
[printers]
comment = All Printers
path = /var/spool/samba
browseable = yes
writeable = no
printable = yes
```

你可以阅读注释行来了解更多关于文件内容的信息。以分号 (`;`) 开头的行表示该选项在注释行上的默认设置。删除分号即可更改设置。

所选行显示了来自 `/etc/printcap` 的打印机已加载，并且正在使用 CUPS 服务。当 `cups` 设置为 `raw` 时，Samba 假设打印文件在到达你的打印机之前已经过格式化。这允许 Linux 或 Windows 客户端提供它们自己的打印机。

最后几行是打印机的实际定义。通过将 `browseable` 选项从 `no` 改为 `yes`，你赋予了用户打印所有打印机（`printable = yes`）的能力。你还可以为 Samba 服务器存储 Windows 打印驱动程序。当 Windows 客户端使用你的打印机时，驱动会自动可用。你不需要从供应商网站下载驱动程序。要启用打印机程序，请添加如下 Samba 共享 `print$`：

```
comment = Printer Drivers
path = /var/lib/samba/drivers
browse = yes
guest ok = no
read only = yes
write list = chris, dduffey
```

在共享可用后，你可以开始将 Windows 打印驱动程序拷贝到 `/var/lib/samba/drivers` 目录。

# 设置 SMB 客户端

如果你在 Linux 计算机上配置 Samba 打印机，很有可能你想要将其与 Windows 客户端共享。如果 Samba 在你的电脑上配置正确，且客户端计算机可以通过网络访问你，用户在使用你的打印机时应该不会遇到问题。

对于许多 Windows 10 系统，点击开始 -> 打印机和扫描仪并从列表中选择打印机进行配置。

在 Windows Vista 中，你打开网络图标。你的主机计算机名称（NetBIOS 名称）将显示在这里。下一节将展示生成的设置外观，以及你可能想要更改它们。提示：如果你在 Windows 操作系统上要配置 SMB 打印机，请前往开始 -> 打印机。共享打印机。在打印机窗口中，点击你的打印机。CUPS 服务 (`cupsd` 进程) 窗口显示了你的打印机。

# 第 17 章

# 配置 Web 服务器

## 本章内容

- 安装 Apache Web 服务器
- 配置 Apache
- 使用 `iptables` 和 `SELinux` 安全加固 Apache
- 创建虚拟主机
- 构建一个安全的 (HTTPS) 网站
- 检查 Apache 错误

Web 服务器 负责提供你每天在互联网上查看到的内容。到目前为止，最流行的 Web 服务器是 Apache (`HTTPD`) Web 服务器，它由 Apache 软件基金会（http://apache.org）赞助。由于 Apache 是一个开源项目，它包含在每个主要的 Linux 发行版中，包括 Fedora、RHEL 和 Ubuntu。

你只需要几分钟时间就可以在 Linux 中配置一个运行的基础性 Web 服务器。但是，你也可以配置你的 Apache Web 服务器，使其为多个域名提供内容（虚拟主机）、提供加密通信（HTTPS），并使用不同类型的身份验证来确保网站部分或全部的安全性。

本章将带你逐步完成安装和配置 Apache Web 服务器的步骤。这些步骤包括保护服务器的程序，以及使用各种模块，以便你可以将不同的身份验证方法和脚本语言整合到你的 Web 服务器中。然后，我将描述如何生成证书以创建一个 HTTPS 套接层 (SSL) 网站。

## 理解 Apache Web 服务器

Apache `HTTPD`（也称为 Apache HTTP 服务器）提供了客户端 Web 浏览器与之通信的服务。守护进程 (`httpd`) 在你的服务器后台运行并等待来自 Web 客户端的请求。Web 浏览器为 HTTP 守护进程提供这些连接并发送请求，守护进程解释这些请求，并返回适当的数据（如网页或其他内容）。

Apache `HTTPD` 包含一个接口，允许模块挂载到进程中处理请求的特定部分。除其他外，模块还用于处理 Web 文档中脚本语言（如 Perl 或 PHP）的解析，并为客户端与服务器之间的连接添加加密。

Apache 起于伊利诺伊大学厄巴纳-香槟槟分校（UIUC）国家级超级计算机应用中心（NCSA）对 HTTP 守护进程提供的一系列补丁和改进集合。NCSA HTTP 守护进程是当时最流行的 HTTP 服务器，但在其作者 Rob McCool 于 1994 年中旬离开 NCSA 后，它开始显示出年代痕迹。

> 另一个来自 NCSA 的项目是 Mosaic。大多数现代 Web 浏览器的起源都可以追溯到 Mosaic。

1995 年，一组开发者组成了 Apache Group，并开始对 NCSA HTTPD 代码库进行大量的修改。Apache 取代了 NCSA HTTPD 成为最流行的 Web 服务器，这一地位一直保持至今。

Apache 组组成了 Apache 软件基金会 (ASF)，以促进 Apache 和其他自由软件的发展。随着 ASF 新项目的启动，Apache 服务器被称为 Apache HTTPD，尽管这两个术语仍被交替使用。目前，ASF 拥有超过 350 个开源计划，包括 Tomcat（包含源自 Java Servlet 和 JavaServer Pages 技术）、Hadoop（一个提供高可用分布式计算的项目）和 SpamAssassin（一个电子邮件过滤程序）。

## 获取并安装你的 Web 服务器

Apache 在每个主要的 Linux 发行版中都可用，它通常以不同的方式打包。在大多数情况下，启动一个简单的 Apache Web 服务器只需要包含 Apache 本身（`/usr/bin/httpd`）及其相关文件的包。在 Fedora、RHEL 等其他发行中，apache Web 服务器位于 `http` 软件包中。

## 理解 httpd 包

在 Fedora 或 RHEL 中安装之前检查 `httpd` 包，请使用 `yumdownloader` 下载包并运行几个 `rpm` 命令来查看其内容：

```
# yumdownloader httpd
# rpm -qi httpd-rpm
Name : httpd
Version : 2.4.41
Release : 1.fc30
Architecture: x86_64
Install Date: (not installed)
```

Group : Unspecified

Size : 5070831

License : ASL 2.0

Signature : RSA/SHA256, Mon 19 Aug 2019 06:06:09 AM EDT, Key ID ef3c1llcfc65bab

Source RPM : httpd-2.4.41-1.fc30.src.rpm

Build Date : Thu 15 Aug 2019 06:07:29 PM EDT
