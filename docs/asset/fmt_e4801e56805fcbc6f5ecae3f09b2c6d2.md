
- 空格继续行。

- 制表符继续行。

## 216 第 5 章

- C 类宏。

- D 宏。

- F 来自文件的类宏。

- H 头部。

- K 键映射项（v8）。

- M 邮件投递代理。

- O 定义和选项。

- P 传递属性。

- R 转换规则。

- S 规则集开始。

- T 声明信任用户。

- V 配置文件的版本。

**管理员注意**：你可能在 `sendmail.cf` 文件中看到许多重写规则。这是正常的。始终备份 `sendmail.cf` 文件，以防以后可能需要。

### sendmail.cw

`sendmail.cw` 存储所有的别名并显示虚拟域条目。`domain.com`、`server1.domain.com` 和 `mail.domain.com` 文件位于 `/etc` 目录，其目的是读取系统上的本地主机名。`sendmail.cw` 要求为你的机器包含别名。在 `sendmail.cw` 文件中添加内容的示例：

```
FEATURE ('use_cw_file')
```

此命令可以将 uucp 转换为数据库：

```
FEATURE ('nucpdomain')
```

## 别名

1. 系统邮件别名

2. 用户邮件别名

别名文件位于 `/etc` 目录。系统会创建一个位于 `/usr/lib` 的 sendmail 文件。许多管理员使用该命令更新 sendmail 数据库。最常见的别名有 `postmaster`、`root`、`ftp`、`news` 和 `Mail-Daemon`。别名不是指向单一地址，而是多个地址。系统必须发送到有效的电子邮件账户。

```
postmaster: root
Mail-daemon: root
news: root
systems: bill, bob
assist: root, bill, joe
```

系统的其他已知别名是 `listserv`。在 listserv 中，你通过在邮件正文中内容订阅特定的列表。系统运行的 listserv 是 `listserv@list.xxx`。用户别名是你在系统上拥有的虚名或伪名。有些人将别名设置为一个组，而不仅仅是一个电子邮件账户。

如果 Susie 在为公司检查邮件，你需要设置一个别名。以下是几个别名的示例：

```
cc: suzie, bill, joe
linux: matt, henry
help: root, joe
```

如你所示，大多数别名指向一组特定的人来接收邮件。当员工入职或离职时，邮件别名的缺点变得显而易见。系统管理员必须记住向别文件中添加新员工，并移除离职员工。你不能将 `.forward` 文件与别名名称关联；`.forward` 文件必须使用有效的电子邮件账户。转发邮件是别名的一种形式。`.forward` 重定向每封邮件并将其发送另一个有效的电子邮件账户。这里是使用编辑器 `pico` 或 `vi` 创建 `.forward` 文件的示例：

```
pico .forward joesuser@nobody.mail.com
vi .forward joesuser@nobody.mail.com
```

## 218 第 5 章

按下 `i` 键进入插入模式，输入地址，按下 `Esc`，最后输入 `w` 并按下回车键。写入文件后，你将拥有有效的转发文件。然而，此文件不会转发任何内容。

## 假期文件 (Vacation File)

假期文件设计用于对传入的消息进行自动回复，通知用户不在办公室。调用 vacation 文件的命令是 `vacation`。停止执行 vacation 文件的命令是 `rm .vacation`。可以修改 `.vacation.msg` 文件以实现用户想要的效果。你发送邮件的人列表位于 `.vacation.db` 中，供以后参考。拥有 vacation 文件的账户将接收邮件，这样邮件就不会被退回。通过输入 `ls -l` 列出目录看不到 `.vacation.msg` 文件，因此你需要输入 `ls -la` 显示所有文件。使用 `vi` 编辑器修改此文件。

### .vacation.msg 文件

```
Subject: 我不在办公室，因此暂时不会查看邮件。关于 $$SUBJECT* 的邮件将在回来后处理。
```

## sendmail.mc

`sendmail` 配置过程从创建一个宏语句开始，创建 `/etc/sendmail.cf`。`sendmail.mc` 由宏创建。在创建 `sendmail.mc` 文件后，你必须具备的最低要求是 Oyster 和 Mailer。同时也推荐 Domain 和 Feature。Oyster 读取操作系统。接下来，Mailer 应该读取你所有的邮件投递代理，包括 local、mail、pop、smtp、uucp 和 fact。domain 应显示你正在托管。此功能非常广泛，但在显示关键词方面是必要的。关键词示例包括 `allmasquerade`、`always_add_domain` 和 `redirect`。`sendmail.mc` 文件包含各种宏，其中一些通过注释某些行（`dnl`）包含在防止垃圾邮件中。`sendmail` 宏文件如下：`m4 /etc/sendmail.mc > /etc/sendmail.cf`。此文件正在发生的是 `m4` 处理器正在运行，并将输出重定向到 `/etc/sendmail.cf`。

## /etc/mail/ xxx.db

在 `/etc/mail` 目录下有很多数据库，它们包含在 Makefile 脚本中。

# 应用 219

`makefile` 可以根据你的需要大而或小，但对于系统管理员来说，它通常很大。`makefile` 的设计用于指定 db 的实际位置，但它可以位于任何其他位置。db 有时位于 `/usr/local`。

## smail

Linux 上最受欢迎的邮件传输程序是 `smail` 和 `sendmail`。它们被称为邮件传输代理 (`MTA`)，并且都支持 UUCP。从历史角度来看，`sendmail` 更加悠久、配置更复杂，且功能更强大。它在 Unix 环境中已经使用了很久。相比之下，`smail` 的安装和配置更简单，并且在内存资源有限的系统中运行得更好。它在 Linux 用户中非常受欢迎，广泛应用于各种 Linux 发行版。除了程序本身，还安装了许多示例。`smail` **不应**与 `sendmail` 一起使用。

默认情况下，`smail` 会立即处理并投送所有入站邮件。如果流量较高，用户可能要求 `smail` 将所有消息收集在队列中，并定期间隔进行处理。如果选择了队列，`smail` 将将所有内容存储在邮件目录 `/var/spool/smail` 中。在收到明确指令之前，它不会进行处理。例如，要每 10 分钟处理一次邮件，用户应在命令行上添加选项 `-q10m`。

查看队列，请使用命令：`$ smail -v`。

`smail` 可以配置为在局域网环境或 UUCP 模式工作。

## 配置 smail

配置文件名为 `config`，位于 `/usr/lib/smail`。

在某些发行版中，它可能位于 `/etc/smail`。有一个示例配置文件可以指导用户如何配置 `smail`。不同版本的 `smail` 将二进制文件安装在不同的位置 `/usr/bin`、`/usr/lib` 或 `/usr/sbin`。对于文件系统目录，位置应该是 `/usr/sbin/sendmail`。

## 局域网配置

通常，局域网内的主机通过 TCP/IP 使用 SMTP 交换邮件，而一台机器专门处理来自外部的 UUCP 连接。最好将所有邮箱保留在单个文件系统中，该系统通过 NFS 挂载到所有其他主机；这样，无论用户当前登录到哪台机器，都可以访问自己的邮件。发送者地址应独立于编写邮件的机器。通常，发送者地址中应该是域名而不是主机地址。

将所有邮箱保留在中央主机上的另一种方法是使用 POP（邮局协议）或 IMAP（交互式邮件访问协议）。

## UUCP 配置

配置文件非常简单：

```
# domain names
visible_domain=
#
# name on outgoing mails
visible_name=
#
# uucp name
uucp_name=
#
# smarthost=
```

第一行告知 `smail` 关于我们站点所属的域名。

`visible_name` 包含一个用于出站邮件的单一完全限定域名 (`FQDN`)。当在生成所有出站邮件的发送者地址时会使用此名称。

`uucp-name` 的值应与 `visible_name` 相同。

最后一行指定了用于智能主机路由的路径。`smail` 将任何发往远程地址的邮件转发到智能主机。`smart_path` 属性中指定的路径将作为通往智能主机的路由。

## 运行 smail

你可以将 `smail` 作为独立的守护进程，或者使用 `inetd` 处理 SMTP 端口并调用 `smail`。在 TCP/IP 网络中，`smail` 最常作为独立的守护进程使用。在启动时，`rc.inet2` 脚本启动它，并在后台等待 SMTP 端口上的 TCP 连接。

要与 `inetd` 配合工作，配置文件中包含如下的一行：

```
smtp stream root /usr/sbin/smtpd smtpd
```
