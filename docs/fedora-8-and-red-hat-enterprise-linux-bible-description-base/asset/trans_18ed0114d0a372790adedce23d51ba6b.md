
## 第 19 章
### 设置邮件服务器

### 本章导读

- 介绍 SMTP 和 sendmail
- 安装并运行 sendmail
- 配置 sendmail
- 介绍 Postfix
- 使用 SpamAssassin 拦截垃圾邮件
- 从服务器获取邮件（IMAP 和 POP3）
- 配置 SquirrelMail
- 管理 mailman 邮件列表

如今，电子邮件是通信主干的一部分，也是各类规模公司内部信息传播的核心。从收发室到实验室，再到首席执行官办公室，每个人都在使用电子邮件。如果你负责管理一个组织的邮件服务器，当它停止工作时（不可避免地），你会收到通知。

本章讲解如何在 Fedora 中设置邮件服务器以发送和接收消息。特别是，它侧重于配置 sendmail 邮件服务器，同时也介绍了如何配置 Postfix 邮件服务器（它也在 Fedora 发行版中）。一旦邮件服务器配置完成，Fedora 为邮件服务器的用户提供多种从服务器获取电子邮件的方式，例如通过 IMAP 或 POP3 下载到他们的邮件客户端，或者使用 SquirrelMail 通过 Web 浏览器阅读。

本章还讨论了使用 mailman 软件包进行邮件列表的配置和管理，详细介绍了邮件列表管理软件如何与邮件服务器集成和交互。

> **注意：** 虽然本章讨论了邮件服务器配置的主要方面，但许多配置细节超出了其范围，因此未予涉及。由于安全是在连接到互联网时的重要关注点，这里对此给予了相当多的关注。

## 介绍 SMTP 和 sendmail

尽管如今电子邮件消息中普遍存在多媒体附件和 HTML 编码，但自 20 世纪 80 年代初以来，消息传输背后的技术没有发生显著变化。简单邮件传输协议（SMTP）的框架最初在 1982 年的 RFC 821 中描述。该协议本身在 1993 年得到了扩展（RFC 1425），产生了扩展简单邮件传输协议（ESMTP），提供了更多的命令和新的投递模式。

消息传输由三部分组成：邮件传输代理（MTA）、邮件投递代理（MDA）和邮件用户代理（MUA）。MTA 通常被称为邮件服务器（sendmail 和 postfix 是其中的例子），它实际上负责分发出站邮件并监听来自互联网的入站邮件。MDA 从 MTA 接受消息并将消息复制到用户的邮箱中。Fedora 使用 procmail 作为默认的 MDA，如 sendmail 配置文件（sendmail.cf）中所述。

最终面向终端用户（邮件的最终接收者），他们使用 MUA 从服务器获取邮件并在其桌面上阅读。大多数 MUA 支持邮局协议（POP3）和互联网消息访问协议（IMAP）功能，以便从服务器获取邮件，从而可以在用户的台式计算机上进行阅读和管理。

> **交叉参考**：有关 Fedora 中可用的邮件用户代理的详细信息，请参见*第 9 章*。

本章重点关注 sendmail MTA，这是互联网上最常见的邮件服务器。互联网上近 70% 的所有电子邮件消息都是由 sendmail 投递的。随着互联网用户数量的增长，每天有数十亿条电子邮件被发送和接收。作为 sendmail 的替代方案，本章还包括对 postfix 的简短描述。

关于从服务器获取邮件，本章描述了 dovecot 软件包，其中包含 POP3 和 IMAP 服务器软件。作为替代方案，关于允许用户通过 Web 浏览器阅读和管理电子邮件，本章描述了如何配置 SquirrelMail。

sendmail 已有三个主要版本。最初的 sendmail（sendmail 版本 5）由加州大学伯克利分校的学生 Eric Allman 于 1983 年编写。他维护该代码直到 1987 年，当时 Lennart Lövström 增强了该程序并开发了 IDA sendmail。Eric Allman 于 1991 年回到伯克利，并着手进行大规模代码修订，于 1993 年发布了 sendmail V8，其中纳入了 IDA sendmail 的扩展功能。当前版本（8.14）基于此“版本 8”代码。

## 安装和运行 sendmail

在 Fedora 中，sendmail 发行版由三个 RPM 包组成：sendmail、sendmail-cf 和 sendmail-doc。只有第一个包是真正必要的，用于在机器上发送和接收邮件。第二个包包含配置宏和其他文件，如果默认设置不足，可以帮助你重新配置你站点的 sendmail 安装。第三个包包含文档文件，有助于解释当前版本的一些细节。

sendmail 二进制包包含在 Fedora 发行版中。sendmail、sendmail-cf 和 sendmail-doc 包位于随本书附带的 Fedora DVD 上。从 DVD 上的 Fedora RPMs 目录，以下命令安装这些包：

```
# rpm -Uhv sendmail*
```

由于 sendmail 是入侵者的常见目标，在继续之前，最好立即获取 sendmail 可用的任何更新。你可以使用 `yum` 命令或软件包更新器窗口来完成此操作。若要使用 `yum` 更新 sendmail，请输入：

```
# yum update sendmail*
```

## 启动 sendmail

安装后，sendmail 服务默认开启。若要立即启动 sendmail，你可以重新启动机器，或者只需运行 `service sendmail start` 来启动服务器。启动和停止 sendmail 的过程与其他服务器进程类似。

## Fedora 或 Red Hat Linux 的其他邮件服务器

sendmail 的开源版本并非 Fedora 和 Red Hat Enterprise Linux 系统中唯一的邮件服务器，但它肯定是最常见的。以下列表描述了其他服务器，并提供了更多信息的 URL：

- **Postfix** — 与 sendmail 一样，Postfix MTA 也包含在 Fedora 中。由 Wietse Venema（以 `tcp_wrappers` 而闻名）编写，这款免费邮件服务器在设计时考虑了安全性，并在受限的 chroot 环境中以非特权用户身份执行大多数功能。该服务器包含十多个小型程序（每个执行简单、不同的任务）和几个专用队列。你可以在 www.postfix.org 找到更多信息和源代码。
- **Exim** — Exim MTA 是一个免费的邮件服务器（基于 GPL），运行在 Linux 和其他 UNIX 系统上。Exim 包含在 Fedora 发行版中。此 MTA 包含用于检查和路由邮件的灵活功能。你可以从 Exim 主页（www.exim.org）了解有关 Exim 的更多信息。
- **Qmail** — 同样以安全为高优先级进行构思，这款邮件服务器（由 Daniel J. Bernstein 编写）提供安全可靠的消息传输、邮箱配额、虚拟域和反垃圾邮件功能。更多信息可在 www.qmail.org/tcp.html 上找到。
- **Sendmail（商业版）** — Sendmail, Inc.（www.sendmail.com）提供基于与开源 sendmail 相同源代码的产品，旨在用于企业电子邮件安装。产品包括 Mailstream Manager（包括支持企业范围、高容量邮件服务的反垃圾邮件和防病毒功能）、MailCenter（提供 IMAP/POP3、Webmail 和智能收件箱）以及 Workforce Mail（可扩展的、基于策略的企业电子邮件服务）。
- **Smail** — Smail 提供与 sendmail 相同的许多功能，但配置相对简单，所需的内存更少。Smail 最适合小型到中型邮件服务器。Smail 项目页面可在 www.weird.com/~woods/projects/smail.html 上找到。源代码可从 ftp://ftp.plixix.com/pub/smail/ 下载。

默认情况下，sendmail 接收的传入消息会被处理并存储在 /var/spool/mail 目录中。此目录中的每个文件代表本地机器上的一个有效用户名。该文件在第一次向用户发送邮件时自动创建（或者如果它不存在则会被创建）。拥有登录账户的人使用此目录及其用户名作为其传入邮箱（例如，/var/spool/mail/johnq）。

传出消息在 /var/spool/mqueue 目录中等待发送。此目录中的文件名遵循一致的命名方案。前两个字符指示文件中存储的数据类型（见表 19-1）。后续字符形成基于处理该消息的 sendmail 进程 PID 的唯一随机标识符。

### 表 19-1：/var/spool/mqueue 中的文件前缀

| **文件名前缀** | **存储的数据类型** |
| :--- | :--- |
| d$f | 构成电子邮件消息正文的数据。 |
| q$f | 包含消息头和其他管理细节的队列控制文件。 |
| t$f | 如果发生投递错误，则创建的 q$f 文件的临时副本。 |
| x$f | 在尝试发送消息期间生成的任何错误消息。 |

### 其他程序

发行版中包含几个其他可执行程序。这些在表 19-2 中描述。

### 表 19-2：其他相关 sendmail 程序

| **程序** | **描述** |
| :--- | :--- |
| mailq | 显示等待在邮件队列中处理的消息摘要（该命令等同于 sendmail -bp）。 |
| mailstats | 显示消息数量和字节计数统计信息。 |
| makemap | 将文本文件（/etc/mail/virtuser 表）转换为哈希化的 Berkeley 数据库（/etc/mail/virtuser 表.db）。此命令在每次 sendmail 脚本启动时运行。 |
