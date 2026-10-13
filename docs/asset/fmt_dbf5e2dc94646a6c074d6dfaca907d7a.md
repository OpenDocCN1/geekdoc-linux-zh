
`define(PRIVACY_FLAGS, `none`)`

```
```

此示例步骤如下：

```bash
[root]# cp /etc/sendmail.cf /etc/sendmail.cf
[root]# cd /usr/lib/sendmail-cf/cf
[root]# echo "PRIVACY_FLAGS, `none`" >>redhat.mc
[root]# m4 redhat >/etc/sendmail.cf
[root]# /etc/rc.d/init.d/sendmail stop
[root]# /etc/rc.d/init.d/sendmail start
```

# 第 4 步
## 安全服务器网络配置

### 步骤 4.4.2. 定义允许转发邮件的主

Sendmail V8.9 有内置停止邮件转发的检查。使用不知情的邮件服务器转发未经请求的邮件是垃圾邮件者的常用做法。组织邮件服务器允许组织内部的转发。转发通过访问数据库控制，在 Red Hat Linux 中位于 `/etc/mail/access`。其他发行版可能通过 `/etc/mail/relay-domains` 控制转发。下面讨论了两种方法。

#### 步骤 4.4.2.1. 检查访问数据库是否激活

为了确保 `sendmail` 能够使用访问数据库，检查 `/etc/sendmail.cf` 中的数据库名称：

```bash
[root]# grep access /etc/sendmail.cf
access -o /etc/mail/access
```

如果没有找到该行，添加此功能的唯一方法是使用 `m4` 宏 `FEATURE('access_db')`。参见步骤 4.4.1 中的示例。

如果你的发行版使用的是 `relay-domains` 文件，请检查 `sendmail` 是否正在使用该文件：

```bash
[root]# grep relay-domains /etc/sendmail.cf
relay-domains -o /etc/mail/relay-domains
```

如果没有找到该行，请编辑 `/etc/sendmail.cf` 并按上述所示方式添加该行，创建 `relay-domains` 文件并重启 `sendmail` 守护进程。

```bash
[root]# touch /etc/mail/relay-domains
[root]# chmod 600 /etc/mail/relay-domains
[root]# /etc/rc.d/init.d/smtp restart
```

#### 步骤 4.4.2.2. 为允许的域名设置访问

访问数据库具有简单的“键值”格式：键是完全限定的主机、子域名、域名或网络；值是操作，`REJECT`、`DISCARD`、`OK`、`RELAY` 或任意消息。只有具有 `RELAY` 操作的主或域名被允许使用邮件服务器作为转发。例如，如果你的域名是 `example.org`，且你的服务器还处理 `128.184.x` 网络上所有主邮件，编辑 `/etc/mail/access` 为：

```
example.org              RELAY
128.184.x               RELAY
```

对于使用 `relay-domains` 的发行版，相反，应向 `/etc/mail/relay-domains` 文件添加内容，仅包含允许通过服务器转发邮件的主机和域名，不再包含其他。记住在修改数据库后重启 `sendmail` 守护进程。

关于转发和反垃圾邮件配置控制的更多信息可以在 `http://www.sendmail.org/m/readme.html` 找到。

### Steps 4.4.3. 设置域名伪装

许多组织倾向于为所有人员设置统一地址，例如 `Joe.Schmo@example.org`。某些客户端可以设置为在所有发送邮件上使用统一地址，但即使是小小组的所有邮件客户端也很麻烦。`sendmail` 可以配置为重写所有发送邮件的头部，使其伪装成中央服务器。要定义伪装地址，编辑 `/etc/sendmail.cf` 并查找 1-2 列的 `DM`：

`DMexample.org`

或者，为了完整，使用 `m` 宏并添加以下内容：

```
MASQUERADE_AS ('example.org')
FEATURE(masquerade_entire_domain)
FEATURE(allmasquerade)
FEATURE(masquerade_envelope)
```

### 步骤 4.4.4. 安装替代 MTA

有多个邮件传输代理（MTA）可以替换 `sendmail`。两个流行的替代方案是 David Bernstein 开发的 Qmail (`www.qmail.org`) 和 Wese Venena 开发的 Postfix (`www.postfix.org`)。这两种 MTA 在设计和编写之初就充分考虑了安全性和性能。获取如何安装和配置这些替代方案的详细信息已超出本指南的范围；互联网上有大量丰富的信息。

### 步骤 4.4.5. 加固 POP 和 IMAP 守护进程

对于收集组织所有入邮件的邮件服务器，将邮件交付给客户端的常用方法是让它们使用邮局协议 (`POP`) 或互联网消息访问协议 (`IMAP`) 获取邮件。`POP` 是两个协议中较旧且更简单的，提供了身份验证、检索和从邮件服务器删除邮件消息的基本命令。`IMAP` 则更加灵活，支持创建、删除和重命名邮件文件夹（邮箱）、选择性检索消息属性等。

#### 步骤 4.4.5.1. 获取最新版本的 POP 和 IMAP 守护进程

许多 POP 和 IMAP 守护进程实现一直受到漏洞的困扰，这些漏洞会导致许多平台上的服务器被 root 攻破。目前有几个已知的利用程序可以破解有漏洞的 Linux POP 和 IMAP 守护进程。希望大多数问题已经被发现并修复，在服务器上拥有最新版本的守护进程程序是非常重要的。

#### 步骤 4.4.5.2. 使用 TCP wrappers 控制对 POP 和 IMAP 的访问

`POP/IMAP` 传统运行在 `inetd` 中，因此通过 `TCP wrappers` 进行访问控制既简单又重要。将访问限制为仅对该服务有合法需求的主机。一个持有整个 `example.org` 域和 `128.184` 网络邮件、并通过 `POP 3` 或 `IMAP` 向客户端交付邮件的邮件枢纽，请在 `/etc/hosts.allow` 中写入此内容（回想步骤 3.21，而 `/etc/hosts.deny` 仅包含 `"ALL: ALL"` 以默认拒绝所有服务）：

```
ipop3d   .example.org 128.184.
imimapd   .example.org 128.184.
```
