
```
ftp> cd pub
250-请阅读 README 文件
250- 最后修改时间为 2001 年 9 月 2 日星期日 19:25:47 - 1 天前
250 CWD 命令成功。
ftp> ls
200 正在打开目录列表的 ASCII 模式数据连接。
total 552
-rw-r--r-- 1 root 50 100 Sep 2 19:25:47 README
-rw-r--r-- 1 root 50 8 Sep 3 07:03:33 configuration
-rw-r--r-- 1 root 50 8 Sep 3 07:03:33 temp.txt
-rw-r--r-- 1 root 50 15798 Sep 3 10:29:18 tftp-0.17-14.i386.rpm
-rw-r--r-- 1 root 50 26011 Sep 3 10:30 tftp-server-0.17-14.i386.rpm
-rw-r--r-- 1 root 50 219332 Sep 3 10:29:00 wu-ftpd-2.6.1-18.i386.rpm222 传输完成。
```

要将所有 `.rpm` 文件传输到本地机器，请执行 `mget *.rpm` 命令。

```
ftp> mget *.rpm
local: tftp-0.17-14.i386.rpm remote: tftp-0.17-14.i386.rpm
200 PORT 命令成功。
150 正在打开 tftp-0.17-14.i386.rpm 的 ASCII 模式数据连接。
(15798 字节).###########
```

```
226 传输完成。
0.974 秒内接收了 15798 字节 (16 Kbytes/sec)
local: tftp-0.17-14.i386.rpm remote: tftp-0.17-14.i386.rpm
200 PORT 命令成功。
150 正在打开 tftp-0.17-14.i386.rpm 的 ASCII 模式数据连接 (26011 字节).################
226 传输完成。
2.5 秒内接收了 26011 字节 (10 Kbytes/sec)
local: wu-ftpd-2.6.1-18.i386.rpm remote: wu-ftpd-2.6.1-18.i386.rpm
200 PORT 命令成功。
150 正在打开 wu-ftpd-2.6.1-18.i386.rpm 的 BINARY 模式数据连接 (219332 字节)################################################
226 传输完成。
50.3 秒内接收了 219332 字节 (4.3 Kbytes/sec)
```

如上所述，`mget` 命令将所有带有 `.rpm` 扩展的文件传输到本地机器。FTP 客户端每传输到我们机器的 1024 字节就会打印一个 `#`。这在慢连接上传输时非常有用，可以确保连接不会中断。

# 第 18 章 安全文件传输协议 (FTP) 服务

![](img/446debe023486a07fde575245cf7a3ff_659_0.png)

图 18.2 一个典型的 gFTP 会话。

在所有文件都完成上传或下载后，你必须关闭会话。通过点击应用程序窗口右上角的红色按钮来发送退出命令。gFTP 在应用程序底部的日志面板中显示会话摘要信息。

尽管使用了图形化界面，但你仍然需要理解 FTP 的基本功能才能使用 gFTP。如果不知道需要设置的文件类型，可能会导致以 ASCII 格式下载二进制文件，从而导致文件无法使用。gFTP 默认使用二进制文件类型，但在传输过程中检测文件类型。gFTP 是一个健壮的应用程序，它以美观、易于使用的格式提供了 FTP 会话中典型的所有必要操作。

## 配置 GNOME 的 galleon 浏览器

GNOME 的 galleon Web 浏览器能够处理多种网络和文件协议，包括 FTP。第一次启动此浏览器时，系统会要求你配置各种设置，例如工具栏的外观，或者你想让 galleon 处理的协议（参见图 18.3）。

启用 gFTP 并启动客户端后，你可以使用 `ftp://` URL 格式访问远程服务器。设置保存在主目录下名为 `.galeon` 的目录中。

![](img/446debe023486a07fde575245cf7a3ff_660_0.png)

图 18.3 在初始设置期间检查 FTP 协议以启用 galeon 使用 FTP。

### 在 GNOME 和 KDE 中使用 ftp:// URL

K 桌面环境 `KDE` 和 GNU 网络对象模型环境 `GNOME` 图形客户端已在窗口管理中集成了 FTP 功能。你也可以配合 Nautilus 或 konqueror 文件浏览器使用 FTP。使用 `ftp://` URL 后后跟服务器名称或 IP 地址来启动匿名 FTP 会话。

KDE 和 GNOME 窗口器的拖放功能允许用户选择远程文件并将其拖到桌面。图 18.4 显示了如何使用 Nautilus 匿名登录远程 FTP 服务器。此类功能可以保护用户无需了解 FTP 工作原理的细节，也不需要记忆各种命令。

![](img/446debe023486a07fde575245cf7a3ff_660_1.png)

图 18.4 使用 Nautilus 文件管理器的 FTP 会话。

## 相关的 Red Hat 和 Linux 命令

你将使用这些命令在 Red Hat Linux 中安装、配置和管理 FTP 服务：

- `ftp`—一种基于文本的交互式 FTP 命令
- `ftcopy`—从 FTP 服务器复制目录和文件
- `ftpcp`—从 FTP 服务器检索远程数据，但不覆盖现有的本地文件
- `ftpd`—FTP 服务器守护进程
- `gftp`—用于 GNOME 的图形化 FTP 客户端
- `wuftpd`—一个 KDE 工具，用于编辑 wu-ftp ftppass 文件
- `l1ftp`—一种高级的基于文本的 FTP 程序
- `cftftp`—一种复杂的基于文本的 FTP 程序
- `redhat-config-services`—Red Hat 的服务 GUI 管理工具
- `sftp`—安全文件传输程序
- `simpleftp`—用 Perl 编写的 FTP 客户端
- `smbclient`—Samba FTP 客户端，用于访问服务器上的 SMB/CIFS 资源
- `vsftpd`—非常安全的 FTP 守护进程
- `webcam`—包含在 xawt 中的网络摄像头型 FTP 客户端

### 参考

- http://www.wu-ftp.org/—WU-FTP 官方网站
- http://www.redhat.com/—Red Hat 官方网站
- http://www.redhat.com/support/docs/tips/FTP-Setup/—来自 Red Hat 的 FTP 设置提示文档
- http://www.openssh.com/—OpenSSH 主页及其最新版本的组件源码（如 `sftp`）
- http://www.cert.org/tech_tips/anonymous_ftp_config.html—CERT 匿名 FTP 配置指南
- http://vsftpd.beasts.org/—vsftpd FTP 服务器主页
- ftp://ferret.lmh.ox.ac.uk/pub/linux/vsftpd—vsftpd 下载站点

# 第 19 章 处理邮件

## 19.1 术语简介绍

本章涵盖了一些与电子邮件相关的常用缩写。

- `RFC`—请求征稿，这是最接近规则书的内容。
- `SMTP`—简单邮件传输协议，用于从一个网络发送邮件到另一个网络。
- `IMAP`—互联网消息访问协议，用于 MUA 从远程站点接收邮件。
- `POP`—邮局协议，用于 MUA 从远程站点接收邮件。
- `MTA`—邮件传输代理，在后台发送和接收电子邮件。
- `MUA`—邮件用户代理，用于读取和编写电子邮件的应用程序。
- `MDA`—邮件投递代理处理本地投递。
- `MIME`—多用途互联网邮件扩展解决了邮件格式问题，使其包含非 ASCII 文本、编码二进制图像和多媒体内容。

## 19.2 电子邮件如何发送和接收

电子邮件通过 `SMTP` 以纯文本形式跨网络发送。`SMTP` 用于从一个网络发送邮件到另一个网络。该协议的扩展为基础协议增加了认证和错误消息。邮件传输代理 `MTA` 在计算机之间后台发送并接收电子邮件。

图 19.1 显示了在两个服务器之间传输邮件的示例。图中的编号标记对应随后的解释。

### 电子邮件的发送与接收

smtp.lion.org  smtp.cheetah.org

![](img/446debe023486a07fde575245cf7a3ff_664_0.png)

**图 19.1** 电子邮件如何成功处理并发送到目的地的简单示例。

- 1. user1@lion.org 编写并向 user2@cheetah.org 发送了一封电子邮件。
- 2. lion.org 的 `MTA` 接收了 user1 的电子邮件，并将其放入队列，排在其他等待发送的消息之后。
