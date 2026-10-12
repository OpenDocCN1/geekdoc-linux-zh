
为了实现这一点，破解者首先向中间节点的 FTP 目录写入一个文件，其中包含连接到目标并在那里检索某些文件的命令。当中间节点连接到目标时，该连接来自它自身的地址（而不是破解者的地址）。目标主机接受连接请求并转发指定的文件。

从历史上看，FTP 弹射攻击一直不是高优先级问题，主要因为它们不涉及渗透尝试。大多数弹射攻击源于海外。美国对许多计算机安全产品有出口限制。外国破解者有时使用弹射攻击来规避美国 FTP 站的限制。然而，这种情况正变得稀少，因为许多黑客、破解者甚至普通用户已经在海外或非受保护服务器上发布了受限软件，任何人都可以从那里获取它们。这种攻击的许多变体已经层出不穷。一种有趣的方法是攻击者误用 `PORT` 命令。在正常的 FTP 会话中，客户端通过 21 端口连接服务器，进行握手，然后客户端发送自己的高位端口（在客户端上）以执行传输。

然而，攻击者也可以指定第三台机器上的端口。这开启了各种可能性。例如，在某些情况下，攻击者可以使用一个受害者来扫描位于另一个受害者防火墙后的服务。在这种情况下，端口扫描似乎源自第一个受害者，而不是攻击者的机器。

Kit Knox 编写了一个很棒的利用程序来自动化这一过程，使你能够绕过或“跳跃”防火墙。可以在 `http://www.hobie.net/security/exploits/hacking/ftp-scan.c` 查看。

> 注意
>
> 如果你有一台旧系统并想尝试弹射攻击，可以在 `http://hackerlink.or.id/files/exploits/apps/ftp/ftpBounceAttack.txt` 获取 FTP 弹射攻击代码。这种攻击允许攻击者执行各种不当行为，包括使用你的服务器发布虚假邮件、假用户名、IRC 轰炸等。

总来说，解决方案是防止你的 FTP 服务器向任意机器建立第三方连接。然而，这并不总是可能的。要全面了解这种攻击以及各种补救方法，请查看 `http://www.fm-muenchen.de/docs/security/FTP_PORT_attacks` 中的“FTP PORT 命令的问题”。

## 错误的权限

过去，攻击者通过利用目标机器上错误的文件和目录权限获得了便利或 root 访问。如果你正在运行匿名 FTP，请对照表 11.1 检查你的 FTP 权限以关闭这里的任何漏洞。

### 表 11.1 FTP 目录与权限

| 目录 | 权限 |
| :--- | :--- |
| `[ftp-home]ftp` | 将 `ftp/home` 设置为 `555` 并所有权归 `root`，如果尚未这样设置。这限制了用户只能读取和执行。 |
| `[ftp-home]ftp/bin` | 将 `ftp/bin` 设置为 `555` 并所有归 `root`，如果尚未这样设置。同样，这限制了用户只能读取和执行。 |
| `[ftp-home]ftp/bin/ls` | 将 `ftp/ls` 设置为 `555` 并所有归 `root`，如果尚未这样设置。 |
| `[ftp-home]ftp/etc` | 将 `ftp/etc` 设置为 `555` 并所有归 `root`，如果尚未这样设置。 |
| `[ftp-home]ftp/passwd` | 将 `ftp/passwd` 设置为 `555` 并所有归 `root`，如果尚未这样设置。 |

## SITE EXEC Bug

过去，攻击者通过利用目标机器上错误的文件和目录权限获得了便利或 root 访问。如果你正在运行匿名 FTP，请对照表 11.1 检查你的 FTP 权限以关闭这里的任何漏洞。

早期 FTP 版本允许远程执行。你需要文档是“FTP 安全扩展”。该文档由 M. Horowitz (Cygnus Solutions) 和 S. Lunt (Bellcore) 编写。这份互联网草案（IDraft）编写于 1996 年 11 月，摘要部分如下：

本文定义了对 1985 年 RFC 959 “文件协议”规范的扩展。这些扩展通过引入新的可选命令、回复和文件传输编码，在控制通道和数据通道上提供了强身份验证、完整性和机密性。

（FTP 安全扩展位于 `[URL]`）。

通用 FTP 安全是一个最好通过研究 FTP 技术来处理的话题。FTP 技术自引入以来发生了很大变化。然而，尽管有了进步，你真的不应该使用标准 FTP。在本章后面的部分，我将提供一种安全的替代方案。现在，让我们快速浏览 FTP 提供的一些功能。

# FTP 的默认安全功能

`ftpd` 提供有限的安全功能，包括基于主机和用户的网络访问控制。你使用三个文件来实现这些功能：

- `/etc/ftpusers`
- `/etc/ftphosts`
- `/etc/ftpaccess`

让我们检查每个文件的作用。

## `/etc/ftpusers`: 受限用户访问文件

`/etc/ftpusers` 是受限用户访问文件。出现在此中的任何用户都被拒绝 FTP 登录访问。

你的 `/etc/ftpusers` 文件可能如下：

```
[root@linux8 /etc]# more ftpusers
root
```

`bin/daemon`

`adm`

`lp`

`sync`

`shutdown`

`halt`

`mail`

`news`

`uucp`

`operator`

`games`

`nody`

默认情况下，所有系统登录都应该被禁用。

> 注意
>
> 如果你的 `/etc/ftpusers` 是空的（或几乎为空），请将其与 `/etc/passwd` 进行比较，并添加缺失的系统用户名。
>
> 要完全拒绝某个用户的 FTP 访问，请在 `/etc/ftpusers` 中单独占一行插入该用户的用户名。

## `fthosts`

`fthosts` 是 `ftpd` 的针对单个用户/主机访问的文件。正如手册页中解释的：

`fthosts` 文件用于允许或拒绝来自各种主机对某些账户的访问。

你的 `/etc/fthosts` 文件可能是空的，或者看起来如下所示：

```
[root@linux8 /etc]# more fthosts
# 示例主机访问文件
# ' - ' 之后的所有内容都被视为注释，
# 空行会被忽略
```

要指定规则以允许或拒绝特定用户从特定主机访问，请使用以下语法：

```
allow [username] [host or host pattern] [host or host pattern]
deny [username] [host or host pattern] [host or host pattern]
```

例如，假设你想拒绝用户 `mwagner` 从 `theircompany.com` 访问，但允许用户 `jsprat` 从 `ourcompany.net` 访问。你将实施以下策略：

## FTP 安全

### 第 11 章

`#` 之后的所有内容都被视为注释，

空行会被忽略

`deny mwagner theircompany.com`

`allow jsprat ourcompany.net`

在这种情况下，由于两个用户来自不同的网络，你不需要担心允许/拒绝的顺序。`ftppd` 会顺序处理 `deny` 和 `allow` 指令，并且发现它们之间没有冲突。

然而，假设你想拒绝来自 `accounting.ourcompany.net` 之外的所有对 `ourcompany.net` 用户 `jsprat` 的访问。那么，你就必须注意允许/拒绝的顺序。例如，假设你定义了以下策略：

- `deny jsprat *.ourcompany.net`
- `allow jsprat accounting.ourcompany.net`

此时，`jsprat` 将完全无法登录，因为 `ftppd` 会先处理并执行 `deny` 指令（其优先级高于 `allow` 指令）。因此，为了让配置生效，你必须反转允许/拒绝的顺序：

- `allow jsprat accounting.ourcompany.net`
- `deny jsprat *.ourcompany.net`

在这里，`ftppd` 会先处理 `allow` 指令，因此用户 `jsprat` 可以从 `accounting` 登录。

> 注意
>
> 如果你未在 `/etc/ftusers` 或 `/etc/fthosts` 中定义某个用户，`ftppd` 将以常规方式处理他们并允许其访问。

`[host or host pattern]` 参数可以是主机名、IP 地址或二者的部分掩码（支持通配符）。例如，以下所有条目都是有效的：

- `development.mycompany.net`
- `*.mycompany.net`
- `207.171.0.*`

此外，你可以通过空格将主机和主机模式堆叠在一起。因此，以下所有条目也是有效的：

- `development.mycompany.net accounting.mycompany.net`
- `*.mycompany.net *.theircompany.net`
- `207.171.0.* *.some.othercompany.net`

## `/etc/ftppass`: ftppd 配置文件

`/etc/ftppass` 是 `ftppd` 的核心配置文件。通过此文件中的指令，你可以控制 `ftppd` 的运行方式。

以下是 `ftppass` 的示例：
