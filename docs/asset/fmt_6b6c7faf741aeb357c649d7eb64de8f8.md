
我们应该设置的另一个参数是`mydestination`，它指定本地的邮件域。如果消息的收件人地址的邮件域为`mydestination`，则消息将通过本地程序投递给相应的用户（假设未找到相关的别名或`.forward`文件）。如果`mydestination`中包含多个邮件域，则这些域都被视为同一域的别名。

对于空客户端，我们不希望有本地投递，因此此参数应为空：

```
mydestination =
```

最后，`relayhost`参数告诉 Postfix 将所有非本地消息发送到指定的主机，而不是直接发送到其明显的目的地：

```
relayhost = [mail.cs.colorado.edu]
```

方括号告诉 Postfix 将指定的字符串视为主机名（DNS A 记录），而不是邮件域名（DNS MX 记录）。

由于空客户端不应从其他系统接收邮件，空客户端配置中要做的最后一件事是在`master.cf`文件中注释掉`smtpd`行。此更改可防止 Postfix 完全运行`smtpd`。仅凭这几行，我们就定义了一个功能齐全的空客户端！

对于“真正的”邮件服务器，您还需要一些更多配置选项以及一些映射表。我们在接下来的几节中介绍这些。

### 使用 postconf

`postconf`是一个方便的工具，可帮助您配置 Postfix。无参数运行时，它会打印所有参数的当前配置。如果将特定参数作为参数命名，`postconf`会打印该参数的值。`-d`选项使`postconf`打印默认值而不是当前配置的值。例如：

```
$ postconf mydestination
mydestination =
$ postconf -d mydestination
mydestination = $myhostname, localhost.$mydomain, localhost
```

另一个有用的选项是`-n`，它使`postconf`仅打印与默认值不同的参数。如果您在 Postfix 邮件列表上寻求帮助，那就是您应该放在电子邮件中的配置信息。

### 查找表

Postfix 的许多行为都是通过使用查找表来塑造的，查找表可以将键映射到值或实现简单的列表。例如，`alias_maps`表的默认设置是

```
alias_maps = dbm:/etc/mail/aliases, nis:mail.aliases
```

数据源使用`type:path`记法指定。请注意，此特定表实际上同时使用了两个不同的信息源：`dbm`数据库和 NIS 映射。多个值可以用逗号、空格或两者分隔。表 20.21 列出了可用的数据源；`postconf -m`也会显示此信息。

#### 表 20.21 Postfix 查找表的信息源

| Type | Description |
|------|-------------|
| `dbm/sdbm` | 传统 `dbm` 或 `gdbm` 数据库文件 |
| `cidr` | CIDR 形式的网络地址 |
| `hash/btree` | Berkeley DB 哈希表或 B-tree 文件（取代 `dbm`） |
| `ldap` | LDAP 目录服务 |
| `mysql` | MySQL 数据库 |
| `nis` | NIS 目录服务 |
| `pcre` | Perl 兼容正则表达式 |
| `pgsql` | PostgreSQL 数据库 |
| `proxy` | 通过 `proxymap` 访问，例如以逃避 `chroot` |
| `regexp` | POSIX 正则表达式 |
| `static` | 无论键如何，都返回作为路径指定的值 |
| `unix` | `/etc/passwd` 和 `/etc/group` 文件；使用 NIS 语法* |

a. `unix:passwd.byname` 是 `passwd` 文件，`unix:group.byname` 是 `group` 文件。

仅为与传统 `sendmail` 别名表兼容而使用 `dbm` 和 `sdbm` 类型。Berkeley DB（`hash`）是更现代的实现；它更安全、更快。如果兼容性不是问题，请使用

```
alias_database = hash:/etc/mail/aliases
alias_maps = hash:/etc/mail/aliases
```

`alias_database`指定由`newaliases`重建的表，应与您在`alias_maps`中指定的表相对应。之所以有两个参数，是因为`alias_maps`可能包含`mysql`或`nis`等非 DB 源，这些源无需重建。

所有 DB 类表（`dbm`、`sdbm`、`hash`和`btree`）都基于一个文本文件，该文件被编译为高效可搜索的二进制格式。这些文本文件的语法在注释和续行方面与配置文件类似。条目指定为由空白分隔的简单键/值对，除了别名表，后者使用键后的冒号以保持与 `sendmail` 的兼容性。例如，以下行适用于别名表：

```
postmaster:  david, tobias
webmaster:   evi
```

另一个例子，这里是一个用于中继来自主机名以 `cs.colorado.edu` 结尾的任何客户端邮件的访问表。

```
.cs.colorado.edu  OK
```

文本文件通过`postmap`命令编译为其二进制格式，用于普通表，以及`postalias`命令用于别名表。表规范（包括类型）必须作为第一个参数给出。例如：

```
$ sudo postmap hash:/etc/postfix/access
```

`postmap`也可以查询查找表中的值（无匹配 = 无输出）：

```
$ postmap -q blabla hash:/etc/postfix/access
$ postmap -q .cs.colorado.edu hash:/etc/postfix/access
OK
```

### 本地投递

`local`程序将邮件投递给本地收件人。它也处理本地别名。例如，如果`mydestination`设置为`cs.colorado.edu`且邮件到达`evi@cs.colorado.edu`，`local`首先查询`alias_maps`表，然后递归地替换任何匹配的条目。

如果没有别名匹配，`local`会在用户 `evi` 的主目录中查找`.forward`文件，如果存在则遵循该文件中的说明。（语法与别名映射的右侧相同。）最后，如果找不到`.forward`文件，邮件将被投递到 `evi` 的本地邮箱。

默认情况下，`local`将以标准 `mbox` 格式的文件写入`/var/mail`下。您可以使用表 20.22 中显示的参数更改该行为。

#### 表 20.22 本地邮箱投递的参数（在 `main.cf` 中设置）

| 参数 | 描述 |
|---|---|
| `mail_spool_directory` | 将邮件投递到为所有用户服务的中央目录 |
| `home_mailbox` | 将邮件投递到 `~user` 下的指定相对路径 |
| `mailbox_command` | 使用外部程序，通常是 `procmail` 投递邮件 |
| `mailbox_transport` | 通过 `master.cf` 中定义的一项服务投递邮件* |
| `recipient_delimiter` | 允许扩展用户名（见下文描述） |

a. 此选项与诸如 `Cyrus imapd` 之类的邮箱服务器接口。

`mail_spool_directory` 和 `home_mailbox` 选项通常生成 **mbox-format** 邮箱，但它们也可以生成 **Maildir** 邮箱。要请求此行为，请在路径名末尾添加斜杠。

如果 `recipient_delimiter` 为 `+`，则发往 `evi+whatever@cs.colorado.edu` 的邮件将被接受并投递到 `evi` 账户。通过此功能，用户可以创建专用地址并按目标地址对邮件进行分类。Postfix 首先尝试对完整地址进行查找，只有在失败时才剥离扩展组件并回退到基本地址。Postfix 还会查找相应的文件 `forward+whatever` 以进行进一步的别名处理。

### 虚拟域

要在您的 Postfix 邮件服务器上托管邮件域，您有三种选择：

- 在 `mydestination` 中列出该域。投递按上述描述执行：别名会被展开，邮件被投递到相应的账户。
- 在 `virtual_alias_domains` 参数中列出该域。此选项为该域提供独立于系统用户账户的寻址命名空间。域内的所有地址都必须可解析（通过映射）到其外部的真实地址。
- 在 `virtual_mailbox_domains` 参数中列出该域。与 `virtual_alias_domains` 选项一样，该域拥有自己的命名空间。所有邮箱必须位于指定的目录下。

仅在一个地方列出该域。谨慎选择，因为许多配置元素都依赖于该选择。我们已经回顾了 `mydestination` 方法的处理方式。其他选项将在下面讨论。

### 虚拟别名域

如果一个域被列为 `virtual_alias_domains` 参数的值，则发往该域的邮件将被 Postfix 接受，并且必须转发到本地机器或别处的实际收件人。
