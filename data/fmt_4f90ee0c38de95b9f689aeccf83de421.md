
## slurpd 的命令行选项

可以通过 `man 8 slurpd` 访问 `slurpd` 的帮助页。

`slurpd` 的选项有：

- **-d level** 指定调试级别。可能的调试级别有：
  - 4. 强力跟踪调试
  - 64. 配置文件处理
  - 65535. 启用所有调试
  - ?. 列出调试级别并退出 slurpd。

- **-f file** 指定 slapd 配置文件。默认是 `/etc/openldap/slapd.conf`。

- **-r file** 指定 slapd 复制日志文件的名称。

- **-o** 在“单次”模式下运行。通常情况下，`slurpd` 处理 replog 文件并等待更多追加的复制条目。在单次模式下，`slurpd` 处理一个复制日志并退出。

- **-t directory** `slurpd` 在处理复制日志之前将其复制到工作目录。

在 `/etc/init.d/` 中提供有一个启动脚本，你可以通过输入 `rcslurpd start` 来启动 slurpd。

## 传输 LDAP 数据库

在从服务器上启动 `slurpd` 之前，你必须从主服务器传输数据库。

你可以使用 `slapcat` 根据 slapd 数据库的内容生成 LDIF 输出。默认情况下，输出写入 STDOUT。

你可以使用 `slapcat` 过滤数据库。`slapcat` 的帮助页还有其他有趣的选项（例如 -l）。你可以使用 `slurpd` 进行复制。

在本次练习中，你将设置一个 LDAP 用户数据库。

你可以在练习集中找到此练习。

（练习结束）

## 目标 7 复制 OpenLDAP 服务器

如果对 LDAP 服务器的请求很多，你可能需要多一台服务器。其中一台是主服务器（master），其他服务器是从服务器（slave）。主从结构提供了一种增加容量、可用性和可靠性的有效方法。

| 目标 | 总结 |
| --- | --- |
| 1. 理解 LDAP 基础 | 目录服务是包含条目的树形数据库。LDAP 在 SUSE Enterprise 10 中最为流行。 |
| 2. 安装并设置 LDAP 服务器 | 如果在安装期间没有配置 LDAP 服务器，你需要安装以下软件包：\n* openldap2\n* openldap-client\n服务器配置位于 `/etc/openldap/slapd.conf`。\n你可以使用 `ldappasswd` 为条目创建密码。 |
| 3. 向 LDAP 服务器添加条目 | 使用 `ldapadd` 将 LDIF 文件中的数据插入目录。确保 LDIF 文件符合 Unicode 格式。 |
| 4. 从 LDAP 服务器查询信息 | 使用 `ldapsearch` 查询目录中的信息。 |
| 5. 修改和删除 LDAP 服务器条目 | 使用 `ldapmodify` 修改目录中的条目。使用 `ldapdelete` 删除目录条目。 |
| 6. 激活 LDAP 身份验证 | 如果你使用 LDAP 目录进行用户验证，可以使用 `ldappasswd` 更改用户密码。如果你用 YaST 配置 LDAP 客户端，PAM 模块 `pam_ldap.so` 将激活 `/etc/security/pam_unix.conf` 中的所有类型验证。如果你手动配置 LDAP 客户端，可以仅为选的服务激活 LDAP 身份验证。要实现这一点，使用了 PAM 模块 `pam_ldap.so`（包含在 `pam_ldap` 包中）。 |
| 7. 复制 OpenLDAP 服务器 | `slapd` 可以写入复制日志文件。\n在主服务器上你还需要指定从服务器的名称。\n在主服务器上指定一个主服务器访问从服务器的 DN。此 DN 也必须在从服务器上指定，并具有写入数据库的权限。\n**slapcat** 用于根据 slapd 数据库的内容生成 LDIF 输出。默认情况下，输出写入 STDOUT。\n可以使用 `slapcat` 过滤数据库。`slapcat` 的帮助页还有其他有趣的选项（例如 -l）。你可以使用 `slurpd` 进行复制。 |

## 目标

1. 理解三种邮件代理的功能
2. 使用基础的 Linux 邮件命令
3. 理解 Postfix 的架构和组件
4. 启动、停止和重新初始化 Postfix
5. 配置 Postfix
6. 使用 Postfix 工具
7. 通过 IMAP 和 POP3 接收邮件
8. 管理垃圾邮件
9. 使用病毒扫描器处理邮件

## 目标 1
### 理解三种邮件代理的功能

处理互联网消息的程序被称为代理（Agents）。

共有三种类型的代理：

- 邮件传输代理 (MTA)
- 邮件投递代理 (MDA)
- 邮件用户代理 (MUA)

以下还描述了：

- 邮件循环周期 (The Mail Cycle)
- 简单邮件传输协议 (SMTP)

### 邮件传输代理 (MTA)

邮件由邮件软件传递给 MTA。MTA 将其发送到接收方 MTA，接收方检查目标地址是否存在。如果存在，接收方 MTA 将邮件传递给 MDA。

如果地址在本地不存在，接收方 MTA 将消息发回发送方 MTA。

也可以进行链式传输：一个 MTA 可以将消息发送到另一个 MTA，后者再将其传递给其他 MTA。常见的 MTA 有：

- Sendmail
- Postfix
- Exim
- Qmail

### 邮件投递代理 (MDA)

每个接收方 MTA 指定了该消息针对哪个本地用户，并将其传递给 MDA，MDA 将其存储在正确的位置。一个著名的 MDA 程序是 Procmail。

### 邮件用户代理 (MUA)

MUA 读取保存的消息并将新消息传递给 MTA。它是 MDA 和用户之间的接口。MUA 可以通过三种方式接收保存的消息：

- 通过邮件协议（如 IMAP 或 POP）
- 通过文件协议远程访问
- 通过本地访问

当 MUA 通过 IMAP 或 POP 运行时，其功能被分为邮件客户端和位于客户端与存储位置之间的服务器。

#### 邮件循环周期

下图显示了邮件循环（图 4-1）：

当 MTA 接收到邮件时，它首先检查邮件收件者是否为本地机器上的现有用户。如果邮件不是给本地用户的，MTA 将其发送到另一个 MTA（所谓的中继主机或负责目标域的邮件服务器）。

如果邮件是给本地用户的，MTA 将其交给 MDA，MDA 将邮件存储在相应用户的邮箱中。从那里，可以使用 POP 或 IMAP 检索邮件。

如果使用 POP，邮件将传输到客户端计算机；此外，它也可以保留在服务器上。

如果使用 IMAP，所有邮件都保留在服务器上，MUA 仅检查邮件。邮件不会传输到客户端计算机。

在发送邮件时，可以配置 MTA 要求 MUA 对用户进行身份验证。这可以用于禁止发送垃圾邮件。

#### 简单邮件传输协议 (SMTP)

互联网上的邮件发送统一由 SMTP（简单邮件传输协议）控制。SMTP 定义在 RFC 821 中。自 1982 年创建以来，它已经历了许多扩展，例如 MIME (RFC 2045) 和 SMTP 服务扩展 (RFC 1869)。

SMTP 具有以下特征：

- 发送计算机和接收计算机之间存在直接的 TCP 连接 - 涉及相关过程。
- SMTP 的任务只是传输，而不是接收或保存消息。
- 每条消息都会得到确认。
- 消息可以被转发，例如，当地址发生变化时。
- 客户端和服务器通过可读的纯文本命令进行通信。

在接下来，我们将更详细地查看：

- SMTP 命令
- 命令语法
- SMTP 回复代码
- 最小 SMTP 命令实现
- 使用 Telnet 发送邮件的示例

### SMTP 命令

命令如下：

- **HELO** (Hello)：用于 SMTP 发送者打开与 SMTP 接收方的连接（问候），并用其完整主机名介绍自己。
- **MAIL FROM**：初始化邮件传输。SMTP 接收者以其完整主机名回复。参数包含源路由路径和发送者地址。
- **RCPT TO**：设置收件者。如果需要发送到多个收件者，则重复执行此命令。参数可以包含源路由路径（例如：
  - @mars.com
  通过主机列表进行路由：
  - @venus.com
  - @example.com:info@example.com
- **DATA**：告知后续内容为邮件内容。当邮件内容结束时，SMTP 接收者开始处理接收到的信息。这涉及更新可能的返回路径。如果处理结果没有失败，则向发送者发送 OK。否则，发送错误消息。

在 SMTP 接收到邮件时，时间戳插入邮件开头。如果 SMTP 接收者负责邮件的最终交付（例如，收件者的邮箱位于 SMTP 接收者处），时间戳包含发送者的身份以及邮件到达服务器的时间。通过多个 SMTP 中继的邮件包含相应的时间戳。

- **VRFY** 验证用户。导致 SMTP 接收者检查给定地址的有效性。如果 SMTP 接收者知道该地址，则将其扩展为完整地址（包括域名）。VRFY 命令对 MAIL FROM、RCPT TO 和 DATA 指令没有影响。
- **EXPN** 指令 SMTP 接收者将参数视为列表。结果是将列表成员发送给 SMTP 发送者。
- **RSET** 重置。
- **HELP** 接受任何 SMTP 命令作为参数。将显示有关如何使用相应指令的页面。
- **NOOP**（无操作）导致 SMTP 接收者回答 OK。除此之外，不对邮件内容或转发和返回路径进行更改。
- **QUIT** 结束发送者和接收者之间的连接。

#### 命令语法

SMTP 命令提供了发送者和接收者之间的直接通信。最常用的 SMTP 命令在下表所示。

| 命令语法 | 参数描述 |
| --- | --- |
| HELO hostname | `hostname` SMTP 发送者的完整主机名 |
| MAIL FROM: reverse-path | `reverse-path` 包含源路由路径和发送者地址 |
| RCPT TO: forward-path | `forward-path` 包含源路由路径和收件者地址 |
| DATA data | `data` 构成邮件的内容（实际消息）。 |
| RSET | ./ |
| VRFY string | `string` 包含用户或邮箱名 |
| EXPN string | `string` 包含邮件列表标识符 |
| HELP [string] | `string` 包含任何 SMTP 命令 |

| 命令语法 | 参数描述 |
|---|---|
| NOOP | /. |
| QUIT | /. |

命令可以使用小写或大写字母写；SMTP 命令是不区分大小写的。例如，SMTP 接收者将以**相同**的方式处理以下命令：**MAIL FROM, Mail From, mail from, Mail FrOm。**

此相反，*正向路径*（forward-path）和*反向路径*（reverse-path）中的参数可能是区分大小写敏感的。这些参数的解释取决于 SMTP 接收者的操作系统以及用户数据库的结构，其中小写和大写字符可能会被区别对待。

### SMTP 响应码

在 SMTP 发送者和接收者之间的通信过程中，发送者向接收者传输各种命令，并控制整个通信过程。接收者确认消息接收，并用相应的响应码提供命令处理状态。只有当发送者收到上一个命令的收执后，才能开始传输下一个命令。

最常见的 SMTP 响应码列如下表所示：

| 响应码 | 描述 |
|---|---|
| 211 | 系统状态或系统帮助响应 |
| 214 | 输入 HELP 后显示帮助消息。 |
| 220 | SMTP 服务器响应。 |
| 221 | SMTP 服务器已关闭连接。 |
| 250 | 指定命令已执行。 |
| 251 | 用户不是本地的；将转发到正向路径。 |
| 354 | DATA 输入的开始。 |
| 421 | SMTP 服务不可用。 |
| 450 | 请求的操作未执行（邮箱已在使用中）。 |
| 451 | 请求的操作中止。 |
| 452 | 请求的操作未执行；系统存储空间不足。 |
| 500 | 语法错误，命令无法识别。 |
| 501 | 参数或参数语法错误。 |
| 502 | 命令未实现。 |
| 503 | 命令序列错误。 |
| 504 | 该参数未实现该命令。 |
| 550 | 请求的操作未执行；文件不可（例如：未找到邮箱，无访问权限）。 |
| 551 | 邮件服务器上不存在用户；尝试正向路径。 |
| 552 | 请求的邮件操作中止：超出存储配额。 |
| 553 | 请求的操作未执行：不允许的邮箱（例如：邮箱语法错误）。 |
| 554 | 事务失败。 |

### 极简 SMTP 命令实现

并非目前为止引入的所有命令都被每个服务器都实现。某些 SMTP 命令故意未包含在某些服务器实现中，以增加服务器的安全性。其中一个安全至关重要的命令是 HELP。由 Wietse Venema 开发的 Postfix SMTP 服务器尚未完全实现此命令，仅简单对 HELP 命令响应响应码 502（“命令未实现”）。

以下列表显示了 SMTP 服务器为了提供 SMTP 通信而**绝对必须**实现的 SMTP 命令：

- HELO
- MAIL FROM:
- RCPT TO:
- DATA
- RSET
- NOOP
- QUIT

### 使用 Telnet 发送邮件的示例

下面的文本显示了一个典型的日志输出示例，可以使用在 25 端口（标准邮件服务器端口）上的 telnet 会话轻松重构：

```
da53:- # telnet da51.digitalairlines.com 25

Trying 127.0.0.1...

Connected to localhost.

Escape character is '^'.

220 da51.digitalairlines.com ESMTP Postfix

HELO da53.digitalairlines.com

250 da53.digitalairlines.com

MAIL FROM: jgoldman@digitalairlines.com

250 OK

RCPT TO: geeko@digitalairlines.com

250 OK

DATA

354 End data with <CR><LF><CR>

Subject: Lorem ipsum dolor sit amet

Lorem ipsum dolor sit amet, consectetuer adipiscing elit, sed diam nonummy nibh euismod tincidunt ut laoreet dolore magna aliquam erat volutpat. Ut ut wis enim ad minim veniam, quis nostrud exerci ea ullamcorper suscipit lobortis ut aliquip ex ea commodo consequat.

250 OK: queued as 45B516A9D

QUIT

221 Bye

Connection closed by foreign host.

da53:~ #
```

## 目标 2 使用基础 Linux mail 命令

你可以通过两种方式之一使用 `mail` 命令：

- 读取状态邮件
- 使用简单邮件客户端

### 读取状态邮件

某些程序会向 root 用户发送状态邮件消息或备注。如果你登录到虚拟终端，如果有给你的邮件消息，你将收到通知：

```
da51 login: root

Password:

You have new mail in /var/mail/root.

Last login: FRI Jul 18 13:23:51 from 10.0.0.6

da51:~ #
```

要读取这些消息，你可以使用 `mail` 命令：

```
da51:~ # mail

mailx version nail 10.6 11/15/05. Type ? for help.

"/var/mail/root": 3 messages 3 new

> N 1 root@da51.digital Wed 9 15:02 28/894 SuSeConfig:

xntp.caveats

> N 1 root@da51.digital Wed 9 15:02 28/894 SuSeConfig:

xntp.caveats

> N 1 root@da51.digital Wed 9 15:02 28/894 SuSeConfig:

xntp.caveats

> N 1 root@da51.digital  9 15:02 28/894.SeConfig:

p.

:

...
```
