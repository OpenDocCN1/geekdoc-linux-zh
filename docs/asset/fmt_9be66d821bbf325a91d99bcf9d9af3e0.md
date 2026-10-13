
请记住，通常 `sendmail` 以 `root` 身份运行，并访问许多不同的文件。为了实现适当的安全，那些配置文件（以及通往它们的所有目录）必须具有正确的权限和所有权。`/etc/sendmail.cf` 必须具有正确的权限和所有权以确保适当的安全。如果 `/etc/sendmail.cf` 权限正确，那么 `sendmail` 即使以 `root` 运行也是安全的。

确保你的 Sendmail 版本不支持 `debug`、`wiz` 或 `kill` 命令。可以通过连接到你的 Sendmail 并发送这些命令进行测试：

```
telnet mail.pentacorp.com smtp
220-mail.pent.orp.mail 8.9.3/8.8.7 ready at 6 Sep 2000 22:20
220 ESMTP spoken here
wiz
500 Command unrecognized
debug
500 Command unrecognized
kill
500 Command unrecognized
quit
221 mail.pentacorp.com closing connection
Connection closed by foreign host.
```

在这个示例中，Sendmail 不支持这些命令，因此对于这些威胁是安全的。如果你收到任何非 `500 Command unrecognized` 的响应，你需要升级你的 Sendmail 版本。

对于旧版本的 Sendmail 安装，在 `/etc/sendmail.cf` 文件中搜索以 `OW` 开头的行

`OW` 命令表示启用 `W` 选项。如果启用了 `W` 选项，魔法密码将被接受；许多黑客都知道它。以下命令可以执行此操作：

```
grep '^OW' /etc/sendmail.cf
```

这将会是魔法密码。如果它看起来不像下面这一行，则应该被修改为看起来像那样的。这将禁用魔法密码。不这样做将为任何知道魔法密码的人提供 shell 访问。

`OW*`

检查 `/etc/aliases` 文件，并分析任何输出到程序或文件而不是邮箱的别名。删除 `decode` 别名（如果存在），它会引发漏洞；它看起来像这样：

```
decode: "|/usr/bin/udecode
```

比删除 `decode` 别名更好的方法是将其发送到 `root` 以提醒你注意可能的攻击，条目如下：

```
decode: root
```

邮件可能会积存在 `/etc/passwd` 中任何账户的邮箱箱中。其中一些账户不是供人类使用的。发送到这些账户的邮件应该路由到系统管理员读取的邮箱中（或丢弃），以避免随时间推移积累数兆的数据。确保提供 `abuse`、`Postmaster` 和 `MAILER-DAEMON` 邮箱，因为这些都是网络礼仪所要求的。许多站点还提供销售和支持。以下将是典型的。

root: sysadm

sales: jtfasttalker

support: nopatience

sysadm: spock

abuse: root

Postmaster: root

MAILER-DAEMON: Postmaster

bin: root

daemon: root

adm: root

lp: root

sync: root

shutdown: root

halt: root

mail: root

news: root

uucp: root

operator: root

games: root

copher: root

ftp: root

nobody: root

xfs: root

gdm: root

在对 `/etc/aliases` 文件进行任何更改后，请执行命令

`newaliases`

以将 `/etc/aliases` 文件编译为 Sendmail 实际使用的 `/etc/aliases.db` 数据库。如果 `/etc/sendmail.mc` 文件中存在以下行

`+ O AutoRebuildAliases`

则不需要执行 `newaliases` 命令。在这种情况下，该行

`-O5`

会导致 `/etc/aliases` 文件在更改后五分钟内被编译到 `/etc/aliases.db`。（旧版本的 Sendmail 使用 `-ODTrue` 替它。）

## 4.2.3 Sendmail 安全选项

### 危险等级
