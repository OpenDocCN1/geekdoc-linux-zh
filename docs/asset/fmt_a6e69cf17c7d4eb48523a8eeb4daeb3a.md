
然后，尝试从 Windows 或 Linux 客户端连接 Samba 服务器。如果你发现可以连接到服务器，请重新开启防火墙：

```bash
# service iptables restart
```

## 第18章：设置文件服务器

随后，你需要在防火墙中开放 137、138 和 139 端口，以便 Samba 服务器能够接受相关服务的连接。（有关修改防火墙的信息请参阅第 14 章。）

### 用户密码是否有效？

尝试以特定用户（从本地主机或局域网内的其他 Linux 系统）访问共享 Samba 目录。你可以使用 `smclient` 命令来执行操作。这是一个示例：

```bash
# smclient //localhost/home/chris/files -U chris

added interface ip=10.0.0.1 bcast=10.0.0.255 mask=255.255.255.0

Password: ********

Domain=[ESTREE] Server=[Samba 3.2.4]

smb:\>
```

在此示例中，`smclient` 以 Samba 用户 `chris` 的身份连接名为 `tmp` 的目录。如果密码通过，你应该能看到服务器的信息和 `smb:\>` 提示符。如果你无法从 Windows 客户端访问共享目录，可能是客户端使用了不正确的用户名和密码。部分原因可能是 Windows 客户端未提供加密密码。

对于 Windows 客户端，使用加密密码需要更改机器的 Windows 注册表。更改注册表的一种方法是使用 `Windowsedit` 命令。不同系统所需的注册表更改包含 `/usr/share/doc/samba-*/docs/registry` 目录下。

> 提示：`smclient` 命令用于列出服务器信息和测试密码，连接后还可以用于浏览共享目录和复制文件。在看到 `smb:\>` 提示符后，输入 `help` 查看可用命令。该接口与任何 `ftp` 客户端（如 `sftp`）类似。

#### 总结

通过提供集化的文件服务，组织可以与组织内部人员、客户或全球任何人高效地共享信息和应用程序。Fedora 和 RHEL 提供了多种技术，让你能够构建自己的 Linux 文件服务器。

网络文件系统（NFS）协议是最早的文件服务器技术之一。它特别适用于在 Fedora、RHEL 和 UNIX 系统之间共享文件系统。NFS 使用标准的 `mount` 和 `umount` 命令将文件系统连接到客户端计算机的目录结构。

Fedora 和 RHEL 自带的 Samba 软件包包含了在 Windows 和 OS/2 操作系统之间共享文件和打印机的协议和实用。它使用了 Microsoft Windows 系统自带的 SMB 协议，因此为包含许多 Windows 系统的局域网提供了方便的方法。

## 第19章：设置邮件服务器

**本章内容**

- *介绍 SMTP 和 sendmail*
- *安装并运行 sendmail*
- *配置 sendmail*
- *介绍 Postfix*
- *使用 SpamAssassin 阻止垃圾邮件*
- *从服务器获取邮件（IMAPv4 和 POP3）*
- *配置 SquirrelMail*
- *管理邮件列表*

今天，电子消息是通信骨干的一部分，是各种规模公司内部信息传递的核心。每个人都使用电子邮件，从邮箱到实验室再到办公室。如果你负责一个组织的邮件服务器，当它停止工作时，你将收到（没完没了的）通知。

本章解释了如何在 Fedora 中设置邮件服务器以发送和接收消息。特别是，它侧重于配置 `sendmail` 邮件服务器，但也介绍了如何配置 `Postfix` 邮件服务器（它同样位于 Fedora 发行版中）。一旦配置好邮件服务器，Fedora 为你的邮件服务器提供了获取电子邮件的不同方式。

> 注意：尽管讨论了邮件服务器的许多方面，但当你连接到互联网时，安全性是一个至关的问题。

### 第四部分：Fedora RHEL 网络与服务器设置

#### 介绍 SMTP 和 sendmail

随着今天电子邮件中多媒体附件和 HTML 编码的流行，消息背后的技术自 20 世纪 80 年代以来并没有改变。简单邮件传输协议（SMTP）的框架最初在 1982 年的 RFC 821 中描述。该协议本身在 1993 年进行了扩展（RFC 1425），产生了扩展邮件传输协议（ESMTP）。

传输消息的三个部分是：邮件传输代理（MTA）、邮件投递代理（MDA）和邮件用户代理（MUA）。MTA 通常称为服务器（`postfix` 就是示例），它实际上处理发出的邮件并监听来自互联网的传入邮件。MTA 接收消息并将其复制到用户的邮箱中。其他 MDA（也称为 LDA）包括 `Maildrop`。

最终用户是邮件的目标对象，他们使用 MUA 从服务器获取邮件并在桌面上读取。大多数 MUA 支持互联网邮件访问协议（IMAP4），用于从服务器获取邮件以便在桌面上进行读取和管理。在可能的情况下，你应该使用安全的 POP 和 IMAP 协议（分别为 `pops` 和 `imaps`）。

> 交叉引用：请参阅第9 章详细了解 Fedora 可用的邮件用户代理。

本章重点关注 `sendmail` MTA，它是互联网上常用的服务器。互联网上近 70% 的电子邮件通过 `sendmail` 投递。随着互联网人口的增长，每天都会发送和接收数十亿封电子邮件。作为 `sendmail` 的替代方案，本章还包含了对 `postfix` 的简要描述。

从服务器获取邮件，本章描述了 `dovecot` 软件包，它包含了 POP 和 IMAPv4 服务器。作为替代方案，允许用户从网页浏览器读取和管理电子邮件，本章介绍了如何配置 `SquirrelMail`。

原始版本（版本5）是由加州大学伯克分校的学生 Eric Allison 在1983年编写的。他维护了代码直到 1987 年，当时 Lennart Lövstrand 增强了程序并开发了 IDA 守护进程。Eric Allison 于 1991 年返回伯州并开始进行大的代码修订，于 1993 年发布了 `sendmail` V8，它整合了 IDA `sendmail` 的扩展。

#### 安装并运行 sendmail

在 Fedora 中，`sendmail` 分发由三个 RPM 软件包组成：`sendmail`、`sendmail-cf` 和 `sendmail-doc`。只有第一个软件包对于在机器上发送和接收邮件是真正必要的。第二个软件包包含了配置宏和其他文件，可以帮助你

如果默认设置不足，请重新配置您网站的 `sendmail` 安装。第三个软件包包含了文档文件，有助于解释当前版本的某些内容。

邮件二进制包包含在 Fedora 发行版中。`sendmail`、`sendmail-cf` 和 `sendmail-doc` 软件包位于附的 Fedora DVD 中。从 DVD 上的 Fedora RPMS 目录，可以使用以下命令安装这些软件包：

```bash
# rpm -Uv sendmail*
```

由于 `sendmail` 是入侵者的常见目标，建议在继续操作之前，立即应用任何可用的 `sendmail` 更新。你可以使用 `yum` 命令或 PackageKit 工具来实现此点。使用 `yum` 更新 `sendmail`，请输入：

```bash
# yum update sendmail*
```
