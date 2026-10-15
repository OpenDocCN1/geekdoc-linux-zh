
```
alias_database = hash:/etc/mail/aliases
alias_maps = hash:/etc/mail/aliases
```

## 第 20 章 电子邮件

所有 DB 类表（`dbm`, `sdbm`, `hash` 和 `btree`）都基于一个文本文件，该文件被被编译为可高效搜索的二进制格式。这些文本文件的语法在注释和续行行方面与配置文件相似。条目以空白字符分隔的简单键/值对形式指定，别名除外，别名在键后使用冒号以保持与 `sendmail` 的兼容性。例如，以下行适用于别名表：

```
postmaster: david, tobias
webmaster: evi
```

另一个示例，这里是一个用于从任何以 `cs.colorado.edu` 结尾的主机名的转发邮件的访问表：

```
.cs.colorado.edu OK
```

文本文件通过 `postmap` 命令将普通表编译为二进制格式，通过 `postalias` 命令将别名表编译为二进制格式。表规范（包括类型）必须作为第一个参数给出。例如：

```
$ sudo postmap hash:/etc/postfix/access
$ postmap 可以查询查找表中的值（不匹配 = 无输出）:
$ postmap -q bablabla hash:/etc/postfix/access
$ postmap -q cs.colorado.edu hash:/etc/postfix/access
OK
```

## 本地投递

`local` 程序将邮件投递给本地收件者。它还处理本地别名。例如，如果目标设置为 `cs.colorado.edu` 且邮件发送到 `evi@cs.colorado.edu`，`local` 会首先查询 `alias_maps` 表，然后递归地匹配任何条目。

如果没有任何别名，`local` 在用户 `evi` 的家目录下查找转发文件（`forward file`），如果该文件存在，则遵循该文件中的指令。（语法与别名映射的右侧相同）。最后，如果没有找到转发文件，邮件将投递到 `evi` 的本地邮箱中。

默认情况下，`local` 使用 `/var/mail` 写入标准的 `mbox` 格式文件。你可以使用表 20.22 所示参数更改该行为。

### 表 20.22 本地邮箱投递的参数（在 `main.cf` 中设置）

| 参数 | 说明 |
| --- | --- |
| `mail_spool_directory` | 将邮件投递到为所有用户服务的中央目录 |
| `home_mailbox` | 将邮件投递到指定相对路径下的 —user |
| `mailbox_command` | 使用外部程序（通常是 `procmail`）投递邮件 |
| `mailbox_transport` | 通过 `master.cf`* 中定义的服务投递邮件 |
| `recipient_delimiter` | 允许扩展用户名（见下文描述） |

- a. 此选项与 `Cyrus imap` 等邮箱服务器进行接口交互。

## 虚拟别名网域

`mail_spool_directory` 和 `home_mailbox` 参数通常生成 `mbox` 格式的邮箱，但它们也可以产生 `Maildir` 格式的邮箱。要请求此行为，请在路径末尾添加一个斜杠。

如果 `recipient_delimiter` 为 `+`，则发送到 `evi+whatever@cs.colorado.edu` 的邮件会被 `evi` 账户接受。通过此功能，用户可以创建特殊用途的地址并根据目标地址发送邮件。`Postfix` 首先查找完整地址，只有在查找失败时，才会扩展组件并回退到基础地址。`Postfix` 还会查找 `forward+whatever` 的对应转发以进行更深层次的别名处理。

## 虚拟域名

要在你的 `Postfix` 邮件服务器上托管邮件域名，你有三个选择：

- 在 `mydestination` 中列出域名。按照描述的方式进行投递：扩展别名并将邮件投递到相应的账户。
- 在 `virtual_alias_domains` 参数中列出域名。此选项为域名提供了独立的地址命名空间，独立于系统用户账户。域名内的所有地址必须能够解析（通过映射）到外部真实地址。
- 在 `virtual_mailbox_domains` 参数中列出域名。与 `virtual_alias_domains` 一样，域名有自己的命名空间。所有邮箱必须位于指定的目录。

在上述三个位置之一列出域名。请仔细选择，因为许多配置元素取决于该选择。我们已经审查了 `mydestination` 方法的处理。其他选项将在下文中讨论。

## 虚拟别名网域

如果域名被列为 `virtual_alias_domains` 参数的值，`Postfix` 将接受发往该网域的邮件，并且必须转发到本地机器或其他处的实际收件者。

虚拟域名中地址的转发必须在 `virtual_alias_maps` 参数包含的查找表中定义。表中的条目左侧是虚拟域名中的地址，右侧是实际目标地址。

右侧的未限定名称被解释为本地用户名。

考虑 `main.cf` 中的以下示例：

```
myorigin = cs.colorado.edu
mydestination = cs.colorado.edu
virtual_alias_domains = admin.com
virtual_alias_maps = hash:/etc/mail/admin.com/virtual
```

在 `/etc/mail/admin.com/virtual` 中我们可以有以下行：

```
postmaster@admin.com evi, david@admin.com
david@admin.com david@schweikert.ch
evi@admin.com
```

发往 `evi@admin.com` 的邮件将重定向到 `evi@cs.colorado.edu`（追加了 `myorigin`），并最终投递到 `evi` 的邮箱，因为 `cs.colorado.edu` 包含在 `mydestination` 中。

定义可以是递归的：右侧可以包含在左侧进一步定义的地址。注意，右侧只能是地址列表。如果你需要执行外部程序或包含文件，则你需要将邮件重定向到别名，然后对该别名进行处理。为了将所有配置元素保持在一个文件中，可以将 `virtual_alias_domains` 设置为与 `virtual_alias_maps` 相同的表，以标记其网域。在 `main.cf` 中：

```
smtpd_recipient_restrictions = $virtual_alias_maps
virtual_alias_maps = hash:/etc/mail/admin.com/virtual
```

在 `/etc/mail/admin.com/virtual` 中：

```
smtpd_recipient_restrictions = notused
postmaster@admin.com evi, david@admin.com
```

## 虚拟域名

在 `virtual_mailbox_domains` 下列出的域名与本地域名类似，但 `virtual_mailbox_maps` 映射对于识别为虚拟网域的地址是足够的。

`virtual_mailbox_maps` 指向一个列出所有网域的表，格式如下：

```
user@domain /path/to/mailbox
```

如果路径以斜杠结尾，则以 `Maildir` 格式存储。`virtual_mailbox_base` 的值是前缀。

你通常希望对虚拟网域的某些地址设置别名。这里有一个完整的示例。在 `main.cf` 中：

```
virtual_mailbox_domains = admin.com
virtual_mailbox_base = /var/mail
virtual_mailbox_maps = hash:/etc/mail/admin.com/vmail
virtual_alias_maps = hash:/etc/mail/admin.com/variases
```

## 访问控制

`/etc/mail/vmail` 可能包含以下条目：

```
evi@admin.com nemeth/
```

`/etc/mail/variases` 可能包含：

```
postmaster@admin.com evi@admin.com
```

你可以在非虚拟别域上使用虚拟别名映射。由于邮箱只能放在别名映射的右侧，使用这种机制是设置网域的唯一方法。

## 表 20.24 常见的 Postfix 访问限制

| 限制 | 功能 |
| --- | --- |
| `check_client_access` | 使用查找表检查客户端主机地址 |
| `check_recipient_access` | 使用查找表检查收件人邮件地址 |
| `permit_mynetworks` | 允许 `mynetworks` 中列出的地址访问 |
| `reject_unauth_destination` | 拒绝针对非本地收件人的邮件；仅执行拒绝 |
