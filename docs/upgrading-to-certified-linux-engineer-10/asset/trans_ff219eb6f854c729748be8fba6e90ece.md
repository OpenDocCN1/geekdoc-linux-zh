

| Objective | Summary |
|---|---|
| 2. Activate LDAP Authentication | 如果你使用 LDAP 目录进行用户身份验证，可以通过使用 `ldappasswd` 命令来更改用户的密码。 |
| | 如果你使用 YaST 模块配置 LDAP 客户端，则 PAM 模块 `pam_ldap.so` 会在文件 `/etc/security/pam_unix2.conf` 中为所有类型的身份验证激活。 |
| | 如果你手动配置 LDAP 客户端，则只能为选定的服务激活 LDAP 身份验证。 |
| | 为此，使用 PAM 模块 `pam_ldap.so`（包含在软件包 `pam_ldap` 中）。将对应服务的模块添加到 `/etc/pam.d` 中的 PAM 配置文件。 |

| Objective | Summary |
|---|---|
| 3. Replicate OpenLDAP Servers | 主服务器上的 slapd 可以配置为写入复制日志文件。 |
| | 在主服务器上你还必须指定从服务器的名称。 |
| | 在主服务器上指定一个由主服务器用于访问从服务器的 DN。该 DN 也必须在从服务器上指定，并且必须具有写入数据库的权限。 |
| | **slapcat** 用于根据 slapd 数据库的内容生成 LDIF 输出。 |

## SECTION 12 Configure a Mail Server

SUSE Linux Enterprise Server 10 中的标准邮件服务器是 Postfix。

在本节中你将了解有关 SMTP 协议的一些背景知识。还介绍了用于检测垃圾邮件和病毒的工具。

## Objectives

- 1. Understand SMTP Communication
- 2. Manage Spam
- 3. Use a Virus Scanner for Email

## Objective 1

## Understand SMTP Communication

下面我们想更详细地了解：

- The SMTP Commands
- Command Syntax
- SMTP Reply Codes
- Minimal SMTP Command Implementation
- An Example for Sending Mail with Telnet

## The SMTP Commands

命令如下：

- **HELO (Hello)** 由 SMTP 发送方用来向 SMTP 接收方打开连接（问候）并以其完整主机名进行自我介绍。这个主机名作为参数附加到 **HELO** 命令。

  SMTP 接收方用其完整主机名回答此问候。这完成了 SMTP 发送方和接收方之间通信的初始化。
- **MAIL FROM** 初始化电子邮件消息的传输。在最简单的情况下，**MAIL FROM** 命令以发送者的电子邮件地址（反向路径）作为参数。参数可以可选地扩展为在收件人地址前包含一串主机列表，以便通过这些主机路由回复（源路由中继），例如：
  - @venus.example.com
  - @mars.example.com:Sales@example.com
- **RCPT TO (Recipient)** 设置邮件项目的收件人地址（正向路径）。如果邮件应同时发送给多个收件人，则重复此命令相应次数。
- **VRFY (Verify)** 验证用户 ID。这会导致 SMTP 接收方检查作为参数给出的收件人的有效性。如果 SMTP 读取器知道收件人，则地址会扩展为完整地址（包括域名）。**VRFY** 命令对 **MAIL FROM, RCPT TO,** 和 **DATA** 指令没有影响。
- **EXPN (Expand)** 指示 SMTP 接收方将参数视为邮件列表。结果，列表的成员会被传输给 SMTP 发送方。
- **RSET (Reset )** 重置先前存储的有关 SMTP 接收方的所有信息。正向路径、反向路径和邮件内容都会丢失。
- **HELP** 以任何其他 SMTP 命令作为参数。关于如何使用相应指令的提示页面将被显示。
- **NOOP (No Operation)** 导致 SMTP 接收方以 **OK** 作出回答。除此之外，邮件内容或正向和返回路径不会发生任何更改。
- **QUIT** 结束 SMTP 发送方和接收方之间的连接。

## Command Syntax

SMTP 命令在发送方和接收方之间提供直接通信。以下表格描述了最常用的 SMTP 命令。

## Table 12-1

| Command Syntax | Description of the Arguments |
|---|---|
| HELO hostname | hostname 包含 SMTP 发送方的完整主机名。 |
| MAIL FROM: reverse-path | reverse-path 包含源路由中继的 relay 路径和发送者地址。 |
| RCPT TO: forward-path | forward-path 包含源路由中继的 relay 路径和收件人地址。 |
| DATA data | data 构成邮件的内容（实际消息）。 |
| RSET | /. |
| VRFY string | string 包含用户或邮箱名称。 |
| EXPN string | string 包含邮件列表标识符。 |
| HELP [string] | string 包含任何 SMTP 命令。 |
| NOOP | /. |
| QUIT | /. |

命令可以用小写或大写书写：SMTP 命令不区分大小写。例如，SMTP 接收方会以相同的方式处理以下命令：MAIL FROM, Mail From, mail from, Mail FrOm。

