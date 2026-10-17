
```
geekoo@da10: ~ telnet da2.digitalairlines.com 25
Trying 10.0.0.2...
Connected to da2.digitalairlines.com.
Escape character is '^'
220 da2.digitalairlines.com SMTP Postfix
HELO da10.digitalairlines.com
250 digitalairlines.com
MAIL FROM:<@da10.digitalairlines.com>
250 OK
RCPT TO:<information@digitalairlines.com>: Recipient
address rejected: User unknown in local recipient table
RCPT TO:<info@digitalairlines.com>
250 OK
DATA
354
Start mail input; end with <CR><LF>.<CR><LF>
Hello,
from today, I will no longer be sending e-mails with Mail,
but only with the program Telnet.
250 OK: queued as
221
Connection closed by foreign host.
geekoo@da10: ~
```

# 三种邮件代理

处理电子邮件消息的程序被称为代理。三种按特定顺序交互的代理：

- 邮件传输代理 `MTA`
- 邮件投递代理 `MDA`
- 邮件用户代理 `MUA`

# 邮件传输代理

电子邮件由电子邮件软件传递给邮件传输代理 `MTA`。`MTA` 将它们发送给接收者，接收者确定目标是否存在。如果，接收者 `MTA` 将邮件传递给投递代理 `MDA`。如果地址本地不存在，接收者 `MTA` 将会将消息发回发送者 `MTA`，或者将消息发送到另一个 `MTA`，由后者将其传递给另一个 `MDA`。著名的 `MTA` 有：

- `Postfix`（默认邮件服务器）
- `Sendmail`
- `Exim`
- `Qmail`

# 邮件投递代理

`MTA` 为本地用户指定邮件意图，并将其传递给投递代理 `MDA`，由 `MDA` 存储在适当的位置。一个著名的 `MDA` 是 `Dove`。

# 邮件用户代理

邮件用户代理 `MUA` 是电子邮件用户用于读写内邮的程序。它显示由 `MDA` 存储的消息，并将新消息传递给 `MTA`。`MUA` 可以通过三种方式访问存储的消息：

- 通过邮件协议（如 `IMAP` 或 `POP3`）
- 远程
- 通过本地访问

在电子邮件早期，消息编码仅限于 7 位 ASCII，因此提供了基础选项。从那时起，电子邮件扩展到包含特殊字符，如重音符号、HTML 文本和附件。`MIME` 格式（在 `RFC 2045` 中定义）规定了邮件类型的交换。`SMTP` 客户端也知道如何显示某些格式。例如，通过电子邮件发送的 HTML 文本可以在浏览器中显示，`PNG` 文件也可以。

# 邮件循环

下图显示了邮件循环以及不同类型的邮件代理如何交互：

# 图 7-11 邮件循环![](img/1402b35af63db8544c13e1f8067)

当 `MTA` 接收到电子邮件时，它首先检查邮件接收者是否为本地用户。如果邮件不是本地用户，`MTA` 将其发送到另一个 `MTA`（即负责目标域名的中继主机）。如果邮件是本地用户，接收者 `MTA` 将其交给 `MDA`，由其存储在用户的邮箱箱中。从那里，可以使用 `POP3` 或 `IMAP` 协议检索电子邮件。如果使用 `POP3`，电子邮件将传输到客户端。根据客户端的设置，可以保留在服务器上或将其删除。如果使用 `IMAP`，所有电子邮件都保留在服务器上，`MUA` 仅在服务器上检查电子邮件。在发送电子邮件时，`MTA` 可以要求 `MUA` 进行身份验证。这可以用于通过 `MTA` 防止垃圾邮件。每个接收者 `MTA` 都会在发送的邮件头中留下一条“received”记录，最新的记录位于顶部。这些记录允许你在某种程度上追溯邮件的来源：

# 第 7 部分 配置应用程序与服务

```
Fri, 26 Jun 2009 11:21:11 +0200
X-Size: CMU CMU 2.3
Received: from examplehost.provider.com ([172.17.228.76]) by
mail.subd.smtp.com
with id 1MK7CK-0DWfQQ0; Fri, 26 Jun 2009 11:21:08
Received: from examplehost.provider.com (local) [127.0.0.1]
by examplehost.provider.com (Postfix) with ESMTP id 55E9B4E7E70
for <geeko@digital airlines.com>; Fri, 26 Jun 2009 11:21:06 +0200
(CEST)
X-Greylist: delayed 971 seconds by postgrey-1.27 at examplehost, Fri;
26 Jun 2009 11:21:05 CEST
Received: from mta.example.net (mta.example.net
[10.11.12.13]) by examplehost.provider.com (Postfix) with SMTP id 1AE6A47E1D
for <geeko@digitalairlines.com>; Fri, 26 Jun 2009 11:21:04 +0200
(CEST)
```

## Postfix

`SLES 11` 中的标准邮件服务器是 `Postfix`。`Postfix` 的编写是作为广为人知的 `MTA` `Sendmail` 的替代方案。

`Postfix` 的作者 `Wiete Venema` 在开发 `Postfix` 时有多个目标，其中最重要的是 `Postfix` 应该是快速的、易于管理且安全的，并且在行为上尽可能与 `Sendmail` 兼容。

其结果是一个模块化的邮件服务器软件，它附带了人类可读的、注释良好的的配置文件，这使得邮件服务器的配置变得相对简单。要理解 `Postfix` 并能够执行基本的邮件服务器管理任务，你需要熟悉以下内容：

- `Postfix` 程序包的组件
- `Postfix` 主守护进程 `Master Daemon`
- 主配置
- 查找表 `Lookup Tables`
- `Postfix` 工具

## Postfix 程序包的组件

在安装 `Postfix` 期间，文件会被保存到 `SLES 11` 系统的各个位置。这些位置可以根据以下标准进行分组：

- `etc/aliases`。这是 `/etc/` 中唯一的 `Postfix` 配置文件。它的格式与 `MTA` `Sendmail` 的 `aliases` 文件相同，包含了本地地址别名。
- `etc/postfix/`。所有定义 `Postfix` 邮件处理的配置文件（`/etc/aliases` 除外）都在此目录下。通常，只有 `Postfix` 管理员可以修改这些文件。
- `/usr/lib/postfix/`。此目录包含 `Postfix` 直接需要的所有程序。更准确地说，这些是 `Postfix` 的二进制执行文件。系统管理员不会直接访问这些程序。
- `/usr/bin/`。此目录包含用于手动控制 `Postfix` 的管理程序。管理员在维护工作会使用这些程序。
- `/usr/bin/`。此目录包含名为 `mailq` 和 `newaliases` 的符号链接。这两个链接都指向 `/usr/bin/sendmail` 程序，该程序为 `Postfix` 提供了一个与 `Sendmail` 兼容的管理接口。
- `/var/spool/postfix/`。此目录包含 `Postfix` 的队列目录，以及在 `chroot` 环境中运行的 `Postfix` 进程的 `etc` 和 `lib/` 目录。如果 `/etc/sysconfig/postfix` 中的变量 `POSTFIX CHROOT` 和 `POSTFIX UPDATE_CHROOT_JAIL` 设置为，则这两个目录将通过以下命令建立：

```
SuSEconfig --module postfix
```

- `/usr/share/man/man[1|8]/`。这些目录包含 `Postfix` 二进制文件、配置文件和管理程序的帮助页。
- `/usr/share/doc/packages/postfix-doc/`。在安装 `postfix-doc` 包后，这里包含关于 `Postfix` 的文档。`html/` 子目录包含关于 `Postfix` 的详细描述以及一个非常有用的 HTML 格式 FAQ。

## Postfix 主守护进程

`Postfix` 主守护进程 `/usr/lib/postfix/master` 在系统启动时由 `Postfix` 直接启动，仅在系统关闭或 `Postfix` 停止时才会终止。

主守护进程通常在邮件系统设置时配置一次，并且通常不会更改。

主守护进程监控整个邮件系统：

- 它控制并监控单个 `Postfix` 进程。
- 它遵循在 `master.cf` 文件中定义的配置资源限制。
- 它重启 `Postfix` 进程。
