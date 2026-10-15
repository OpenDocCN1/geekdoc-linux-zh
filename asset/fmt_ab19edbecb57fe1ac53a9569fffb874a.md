
| `access-mode` | 用户登录服务器的方式。其值为 `a` 表示匿名访客，`g` 表示访客用户（对应 `/etc/ftppasswd` 中的 `guestgroup` 命令），`r` 表示本地机器上的真实用户。 |
| `username` | 如果以真实用户身份登录，则显示用户名。 |
| `service-name` | 如果访问模式为访客，则显示使用的服务名称，通常为 FTP。 |
| `authentication-method` | 身份验证类型。其值为 `ø` 表示 RFC2331 身份验证（格式正确的电子邮件地址）。 |
| `authenticated-user-id` | 这是根据访问服务器时使用的身份验证方法返回给服务器的用户 ID。当找不到经过验证的用户 ID 时，使用 `*`。 |
| `completion-status` | 单字符字段，用于标识传输状态。其值为 `c` 表示传输完成，`i` 表示传输未完成。 |

该文件的示例见列表 20.5。

## 列表 20.5 `/var/log/xferlog` 文件入站和出站日志

```
Mon Sep 03 07:13:05 2001 1 localhost.localdomain 100
/var/pub/README b o a testing@test.com ftp 0 * c
Mon Sep 03 02:35:35 2001 1 helios 8 /var/pub/configuration a o
a o testing@test.com ftp 0 * c
Mon Sep 03 02:35:35 2001 1 helios 8 /var/pub/temp.txt a o
a testing@test.com ftp 0 * c
Mon Sep 03 02:35:35 2001 1 helios 8 /var/pub/tftp-server-
0.17-14.i386.rpm a o testing@test.com ftp 0 * c
Mon Sep 03 02:35:35 2001 1 helios 8 /var/pub/wu-ftpd-2.6.1-
22.i386.rpm a o testing@test.com ftp 0 * c
```

## 相关的 Fedora 和 Linux 命令

你使用这些命令在 Fedora 中安装、配置和管理 FTP 服务：

- `epiphany`—一个支持 FTP 的 GNOME 图形浏览器
- `ftp`—一个基于文本的交互式 FTP 命令
- `ftpcopy`—从 FTP 服务器复制目录和文件
- `ftpc`—从远程 FTP 服务器检索数据，但不覆盖现有的本地文件
- `gftp`—一个用于 GNOME 的 FTP 客户端
- `konqueror`—KDE 的图形化网络浏览器
- `lftp`—一个高级的基于文本的 FTP 程序
- `nautilus`—红帽的图形化文件管理器和
- `ncftp`—一个复杂的基于文本的 FTP 程序
- `sftp`—安全文件传输程序
- `smclient`—用于访问服务器上 SMB/CIFS 资源的 Samba 客户端
- `system-config-services`—红帽的服务 GUI 管理实用工具
- `vsftpd`—非常安全的 FTP 守护进程
- `webcam`—一个包含在 `xawtv` 中的、面向网络摄像头的 FTP 客户端

## 引用

- http://www.wu-ftpd.org/—wu-ftp 官方网站。
- http://www.cert.org/—计算机应急响应小组。
- http://www.openssh.com/—OpenSSH 主页，以及最新版本 OpenSSH 及其组件客户端（如 `sftp`）的源码。
- http://www.cert.org/tech_tips/anonymous_ftp_config.html—CERT 匿名 FTP 配置指南。
- http://vsftpd.beasts.org/—vsftpd 服务器主页。
- ftp:////vsftpd.beasts.org/users/cevans/—vsftpd 服务器最新版本的下载站点。

# 第 21 章 处理电子邮件

电子邮件仍然是互联网上主的通信形式。它快速、免费且易于使用。然而，其背后的许多工作极其复杂，对于任何了解电子邮件如何处理的人来说，看起来可能非常令畏。Fedora 配备了许多强大的应用程序，帮助你构建从小型邮件服务器到处理成千上万消息的大型服务器等任何内容。

本章将介绍如何配置 Fedora 作为电子邮件服务器。我们将查看 Fedora 中可用的选项以及各自的优缺点。你还将了解 Linux（以及较小程度 Unix）是如何处理邮件的。

## 电子邮件如何发送和接收

电子邮件通过 `SMTP` 协议（简单邮件传输协议）在全球网络范围内以纯文传输。正如名称所示，协议本身非常基础，它已经过扩展以增加进一步的身份验证和错误报告/消息，以满足现代电子邮件日益增长的需求。邮件传输代理（或 `MTA`）在后台运行，将电子邮件从服务器传输到服务器，允许电子邮件发送到全球。你可能遇到过此类 `MTA` 软件，如 `Sendmail`、`Postfix`、`Fetchmail`、`Exim` 或 `Qmail`。

`SMTP` 使通过电子邮件的每台计算机都能将其向正确的方向转发到最终目的地。当你考虑到世界上有数百万台电子邮件服务器时，你会惊讶于它是如此简单。

- 电子邮件如何发送和接收
- Sendmail 配置与操作
- 介绍 Postfix
- 使用 Fetchmail 检索
- 选择邮件投递代理
- 邮件守护进程
- Microsoft Exchange 服务器的替代方案
- 引用

以下是电子邮件成功处理并发送到目的地的简化示例：

1. `andrew@hudson.org` 编写并发送一条邮件到 `paul@hudzilla.org`。
2. `hudson.org` 的 `MTA` 接收到 `andrew` 的邮件，并将其排在其他等待发送的消息队列中。
3. `hudson.org` 的 `MTA` 连接端口 `25` 上的 `hudzilla.org` `MTA`。当 `hudzilla.org` 确认连接后，`hudson.org` 的 `MTA` 发送邮件。当 `hudzilla.org` 接受消息后，
4. `hudzilla.org` 的 `MTA` 接收消息并将其投递到 `paul` 的邮箱中。
