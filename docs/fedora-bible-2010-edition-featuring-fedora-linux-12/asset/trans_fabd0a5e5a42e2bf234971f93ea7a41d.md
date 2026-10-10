
## Samba 服务是否正在运行？

首先，请尝试从您的 Linux 系统使用 `smbclient` 命令，以检查一切是否正常运行，并且资源是否如预期那样被共享。`smbclient` 命令是一个获取 Samba 服务器信息甚至从 Linux 和 Windows 计算机访问共享目录的强大工具。在以 root 或任何有权限访问您的 Samba 服务器的用户身份登录时，输入以下内容：

```bash
$ smbclient -L localhost
Password: ******
Domain=[ESTREET] OS=[Unix]  Server=[Samba  3.4.2-47.fc12]

Sharename       Type      Comment
---------       ----      -------
homes           Disk      Home Directories
IPC$            IPC       IPC Service (Samba Server)
ADMINS$         Disk      IPC Service (Samba Server)
hp-ns1          Printer

Domain=[ESTREET] OS=[Unix]  Server=[Samba  3.4.2-47.fc12]

Server          Comment
---------       -------
PINE            Samba Server
MAPLE           Windows XP
NS1             Samba Server

Workgroup       Master
---------       -------
ESTREET         PINE
```

这表明 Samba 服务器正在本地计算机上运行。共享目录、打印机以及工作组中的服务器都会显示在此处。如果 Samba 服务器未运行，您将看到连接被拒绝的消息。您需要按照本章前面“启动 Samba 服务”一节中的说明启动 Samba 服务。

## 防火墙或 SELinux 是否限制了访问？

如果 Samba 服务器正在运行，它应该开始在您的局域网（LAN）上广播其可用性。如果您尝试从局域网上的 Windows 或 Linux 客户端访问服务器，但收到连接被拒绝错误，问题可能是您的 Linux Samba 服务器上的防火墙正在拒绝访问 NetBIOS 服务。如果您拥有一个安全的局域网，您可以输入以下内容（作为 root 用户）来临时清除防火墙规则并将默认策略设置为接受：

```bash
# service iptables stop
```

然后，尝试从 Windows 或 Linux 客户端连接到 Samba 服务器。如果您发现可以连接到服务器，请重新打开防火墙：

```bash
# service iptables restart
```

然后，您需要在防火墙中开放 137、138 和 139 端口的访问权限，以便 Samba 服务器能够接受服务连接。（有关修改防火墙的信息，请参阅第 13 章。）

如果您怀疑 SELinux 可能正在阻止对您的 Samba 服务的访问，请输入以下内容：

```bash
# setenforce 0
```

这将把您的 SELinux 服务从强制模式更改为宽容模式。如果您随后能够访问 Samba 服务，请确保所有 Samba 配置文件的文件上下文是正确的，并且所需的 Samba 相关 SELinux 布尔值已启用。然后将 SELinux 设置回强制模式（setenforce 1）。

## 用户密码是否有效？

尝试以特定用户身份（从本地主机或局域网上的其他 Linux 系统）访问共享的 Samba 目录。您可以使用 `smbclient` 命令来执行此操作。以下是一个示例：

```bash
# smbclient //localhost/home/ -U chris
added interface ip=10.0.0.1 bcast=10.0.0.255 nmask=255.255.255.0
Password: ******
Domain=[ESTREET]  OS=[Unix]  Server=[Samba  3.4.2-47.fc12]
smb:\>
```

在此示例中，`smbclient` 作为名为 `chris` 的 Samba 用户连接到名为 `home` 的目录共享。如果密码被接受，您应该看到有关服务器的信息以及 `smb:\>` 提示符。如果您无法从 Windows 客户端访问相同的共享目录，很有可能是客户端传递了不正确的用户名和密码。问题的一部分可能在于 Windows 客户端未提供加密密码。

对于某些 Windows 客户端，使用加密密码需要更改该计算机的 Windows 注册表。更改注册表的一种方法是使用 Windows `regedit` 命令。不同 Windows 系统所需的注册表更改包含在 `/usr/share/doc/samba-*/docs/registry` 目录中。

> **提示：** 此处用于列出服务器信息并测试密码的 `smbclient` 命令，在连接后还可以用于浏览共享目录和复制文件。看到 `smb:\>` 提示符后，输入 `help` 以查看可用命令。该界面类似于命令行 ftp 客户端。

## 总结

通过提供集中式文件服务器，组织可以有效地与组织内部的人员、客户或世界各地任何人共享信息应用程序。Fedora 中可用多种不同的技术，使您的 Linux 计算机能够成为文件服务器。

网络文件系统（NFS）协议是最早可用的文件服务器技术之一。它特别适用于在 Fedora 和其他 Linux/UNIX 系统之间共享文件系统。NFS 使用标准的 `mount` 和 `umount` 命令将文件系统连接到客户端计算机的目录结构。

随 Fedora 提供的 Samba 软件包包含在 Windows、UNIX 和 Linux 操作系统之间共享文件和打印机的协议和实用工具。它使用所有 Microsoft Windows 系统都包含的 SMB 和 CIFS 协议，因此为包含许多 Windows 系统的局域网提供了方便的资源共享方法。

# 第 18 章

## 配置邮件服务器

### 本章内容

- 介绍 SMTP 和 sendmail
- 安装和运行 sendmail
- 配置 sendmail
- 介绍 Postfix
- 使用 SpamAssassin 阻止垃圾邮件
- 从服务器获取邮件
- 配置 SquirrelMail
- 管理 mailman 邮件列表

如今，电子消息传递是各种规模公司通信骨干和信息传播的核心。从收发室到实验室，再到首席执行官办公室，每个人都在使用电子邮件。如果您负责组织的邮件服务器，当它停止工作时，您会不断收到通知。

本章介绍了如何在 Fedora 中设置邮件服务器以发送和接收消息。特别是，它重点介绍如何配置 sendmail 邮件服务器，但也说明了如何配置 Postfix 邮件服务器（它也在 Fedora 发行版中）。一旦配置好邮件服务器，Fedora 为您的邮件服务器用户提供不同的方式来从服务器获取电子邮件，例如将其下载到他们的邮件客户端（使用 IMAP 或 POP），或通过 Web 浏览器阅读（使用 SquirrelMail）。

邮件列表的配置和管理（使用 mailman 软件包）也在本章中讨论，详细说明了邮件列表管理软件如何集成并与邮件服务器进行交互。

> **注意：** 虽然本章讨论了邮件服务器配置的主要方面，但许多配置方面超出了其范围，因此未在此处涉及。由于安全是在连接到互联网时的重要问题，因此在此处给予了相当的重视。

## 介绍 SMTP 和 sendmail

尽管如今电子邮件消息中普遍存在多媒体附件和 HTML 编码，但消息传输背后的技术自 20 世纪 80 年代初以来并未发生重大变化。简单邮件传输协议（SMTP）的框架最初在 1982 年的 RFC 821 中描述。该协议本身在 1993 年（RFC 1425）得到扩展，产生了扩展简单邮件传输协议（ESMTP），提供了更多命令和新的投递模式。

消息传输的三个主要部分是邮件传输代理（MTA）、邮件投递代理（MDA）和邮件用户代理（MUA）。MTA，通常称为邮件服务器（sendmail 和 postfix 是其示例），实际上处理发出邮件的分配并监听来自互联网的传入邮件。MDA 从 MTA 接收消息并将消息复制到用户的邮箱中。Fedora 使用 procmail 作为默认 MDA，如 sendmail 配置文件（`sendmail.cf`）中指定。其他 MDA（也称为本地投递代理或 LDA）包括 `maildrop` 和 `postdrop`。

最终用户，即邮件的最终接收者，使用 MUA 从服务器获取邮件并从桌面阅读。大多数 MUA 支持邮局协议（POP3）和互联网消息访问协议（IMAPv4）功能，以便从服务器获取邮件，从而可以在用户的桌面计算机上阅读和管理。在可能的情况下，您应该使用 POP 和 IMAP 协议更安全的版本（分别是 `pop3s` 和 `imaps`）。

> **交叉引用：** 有关 Fedora 提供的邮件用户代理的详细信息，请参阅第 8 章。

本章侧重于 sendmail MTA，它是互联网上最常见的邮件服务器。互联网上近 70% 的电子邮件消息是由 sendmail 投递的。随着互联网人口的增长，每天发送和接收数十亿条电子邮件消息。作为 sendmail 的替代方案，本章还简要介绍了 postfix。

关于从服务器获取邮件，本章介绍了 dovecot 软件包，它包含 POP3 和 IMAPv4 服务器软件。作为替代方案，本章还介绍了如何配置 SquirrelMail，以便用户可以通过 Web 浏览器阅读和管理电子邮件。

sendmail 已有三个主要版本。最初的 sendmail（sendmail 版本 5）由加利福尼亚大学伯克利分校的学生 Eric Allman 于 1983 年编写。他维护该代码直到 1987 年，当时 Lennart Löfvstrand 增强了该程序并开发了 IDA sendmail。Eric Allman 于 1991 年回到伯克利，开始进行大规模代码修订，并于 1993 年发布 sendmail V8，其中整合了 IDA sendmail 的扩展。当前版本（8.14）基于此“版本 8”代码。

## 安装和运行 sendmail

在 Fedora 中，sendmail 发行版由三个 RPM 软件包组成：`sendmail`、`sendmail-cf` 和 `sendmail-doc`。只有第一个软件包对于在您的机器上发送和接收邮件才是真正必要的。第二个软件包包含配置宏和其他文件，可以帮助您

