
Domain=[ESTREET] OS=[Unix] Server={Samba 3.0.14a-2}

| 共享名称 | 类型 | 注释 |
| :--- | :--- | :--- |
| homes | Disk | 用户主目录 (Samba 服务器) |
| IPC | | IPC 服务 (Samba 服务器) |
| ADMIN$ | Disk | IPC 服务 (Samba 服务器) |
| hp-nsl | Printer | |
| Domain=[ESTREET] OS=[Unix] Server={Samba 3.0.14a-2} |

# 第四部分：Fedora 和 RHEL 网络与服务器设置

| 服务器 | 注释 |
| :--- | :--- |
| PINE | Samba 服务器 |
| MAPLE | Windows XP |
| NS1 | Samba 服务器 |
| Workgroup | Master |

这显示 Samba 服务器正在本地计算机上运行。共享目录、打印机以及工作组中的内容也会显示在这里。如果 Samba 服务器未运行，你将看到“拒绝连接”的消息。你需要按照本章早期“启动 Samba 服务”部分的描述启动 Samba 服务。

# 防火墙已打开？

如果 Samba 服务器正在运行，它应该开始在你的局域网上广播其可用性。如果你尝试从局域网上的 Windows 或 Linux 客户端访问服务器，但得到“拒绝连接”错误，问题可能是你的 Linux 服务器上的防火墙拒绝了访问。如果发现可以连接服务器，请清除防火墙规则：

```
$ iptables -F
```

然后，从 Windows 客户端连接服务器。重新开启防火墙：

```
$ service iptables restart
```

# 用户密码正常？

尝试作为特定用户（从本地主机）访问共享目录。你可以使用 `smclient` 来实现。这是一个示例：

```
$ smclient //localhost/tmp -U chris

added interface=10.0.0.1 bcast=10.0.0.255 nmask=255.255.255.0

Password: *********

Domain=[ESTREET] OS=[Unix] Samba=2.2.7

smb\> tmp
```

在此示例中，`smclient` 以用户 `chris` 的身份连接到 `tmp` 目录。如果密码通过，你应该看到关于服务器的信息和 `smb\>` 提示符。如果你无法从 Windows 客户端访问同一个共享目录，很可能是客户端传递了错误的用户名和密码。部分可能是 Windows 客户端没有提供加密密码。

对于某些 Windows 客户端，使用加密密码需要更改 Windows 注册表。更改注册表的方法是使用 Windows `regedit` 命令。不同 Windows 系统所需的注册表更改位于 `/usr/share/doc/samba-*/docs/registry` 目录。

### 总结

通过提供集中文件服务器，组织可以与内部、客户或全球任何人高效地共享信息和应用程序。Fedora 和 RHEL 提供了多种技术，让你将 Linux 计算机变为文件服务器。

网络文件系统（NFS）协议是最早可用的文件服务器技术之一。它特别适用于在 Fedora、RHEL 和其他 UNIX 系统之间共享文件系统。NFS 使用标准的 `mount` 和 `ummount` 命令将文件系统挂载到客户端的目录结构中。

Fedora 和 RHEL 自带的 Samba 软件包包含了用于 Windows 和 OS/2 操作系统之间共享文件和打印机的协议和实用。它使用了所有 Microsoft Windows 系统的 SMB 协议，因此为包含许多 Windows 系统的局域网提供了一种方便的资源共享方法。

## 第 19 章

## 设置邮件服务器

### 本章内容

- 介绍 SMTP 和 `sendmail`
- 安装并运行 `sendmail`
- 配置 `sendmail`
- 介绍 Postfix
- 使用 SpamAssassin 阻止垃圾邮件
- 从服务器获取邮件 (IMAP 和 POP3)
- 配置 SquirrelMail
- 管理 `mailman` 邮件列表

在今天，电子消息已成为通信骨干的一部分，是各种规模公司内部信息传播的核心。从邮件收发室到实验室，再到首席执行官办公室，每个人都在使用电子邮件。如果你负责一个组织的邮件服务器，当它停止工作时，你将会收到（没完没了的）通知。

本章解释了如何在 Fedora 中设置邮件服务器以发送和接收消息。特别是，本章重点关注了配置 Sendmail 邮件服务器，但也介绍了如何配置 Postfix 邮件服务器（该服务器也包含在 Fedora Linux 发行版中）。一旦配置好邮件服务器，Fedora 为你的邮件服务器用户提供了多种从服务器获取电子邮件的方法，例如将其下载到邮件客户端（使用 IMAP 或 POP3），或通过 Web 浏览器阅读（使用 SquirrelMail）。

本章还讨论了邮件列表配置和管理（使用 `mailman` 软件包），并详细说明了邮件列表管理软件如何与邮件服务器集成和进行交互。

> 注意：尽管本章讨论了邮件服务器配置的主要方面，但许多配置方面超出了本章的范畴，因此未予讨论。由于在连接到互联网时安全性是一个非常关注的问题，因此在这里给予了大量的关注。

## 介绍 SMTP 和 sendmail

随着今天电子邮件中附件和 HTML 编码的普及，消息传输背后的技术自 20 世纪 80 年代以来并没有显著变化。简单邮件传输协议 (SMTP) 的框架最初在 1982 年的 RFC 821 中引入。该协议在 1993 年进行了扩展 (RFC 1425)，产生了扩展邮件传输协议 (ESMTP)，它提供了更多的命令和新的交付模式。

消息传输的三部分是邮件传输代理 (MTA)、邮件投递代理 (MDA) 和邮件用户代理 (MUA)。通常（邮件服务器，`sendmail` 和 `postfix` 就是其示例）实际上处理邮件邮件并监听来自互联网的传入邮件。MDA 接收 MTA 的消息并将其复制到邮箱箱中。正如 `sendmail` 配置文件 (`sendmail.conf`) 中指定的，，管理员使用 `postfix` 作为默认 MDA。邮件的最终目标是终端用户使用 MUA 从服务器获取邮件并在他们的桌面上读取。MUA 使用邮局传输协议 (POP3) 和互联网消息访问协议 (IMAP) 特性从服务器获取邮件，以便在用户的桌面级计算机上对其进行读取和管理。

> **交叉引用：** 请参阅第 9 章了解有关 Fedora 可用邮件用户代理的详情。

本章重点关注 `sendmail` MTA，它是互联网上常用的邮件服务器。互联网上近 70% 的电子邮件都是通过 `sendmail` 交付的。随着互联网人口的增长，每天有数十亿封电子邮件发送和接收。作为 `sendmail` 的替代方案，本章还包含了 `postfix` 的描述。

为了从服务器获取邮件，本章涵盖了 `dovec` 软件包，它包含 POP3 和 IMAP 服务器软件。作为替代方案，为了允许用户从 Web 浏览器读取和管理电子邮件，本章描述了如何配置 SquirrelMail。

`sendmail` 经历过三次大发布。原始的 `sendmail`（`sendmail` 版本 5）于 1987 年由加州大学伯克利分校的学生 Eric Allman 编写。Lennart 维护了代码直到 1987 年，当时 Lennart Holm 增强了程序并开发了 IDA `sendmail`。Eric Allman 于 1993 年回到伯克利并开始了一次重大修订，发布了 `sendmail` V8，该版本整合了 IDA `sendmail` 的扩展。当前版本 (8.13.3) 基于此“版本 8”代码。

## 安装和运行 sendmail

在 Fedora 中，`sendmail` 分发由三个 RPM 包组成：`sendmail`、`sendmail-cf` 和 `sendmail-doc`。只有第一个包对于从你的机器发送和接收邮件是必要的。第二个包包含了配置宏和其他文件，如果默认设置不足，这些文件可以帮助你重新配置站点的 `sendmail` 安装。第三个包包含文档文件，有助于解释当前版本的某些细节。

`sendmail` 二进制包包含在 Fedora 发行版。`sendmail`、`sendmail-cf` 和 `sendmail-doc` 包包含在随书提供的 Fedora Core 4 DVD 中。从 DVD 上的 Fedora RPM 目录，可以使用以下命令安装这些包：

```
# rpm -Uhv sendmail
```

由于 `sendmail` 是入侵者的特别目标，因此在继续之前，立即获取任何可用的 `sendmail` 更新是一个好主意。你可以使用 `yum` 命令或 `update2` 功能来实现。要使用 `yum` 更新 `sendmail`，输入：

```
# yum update sendmail
```
