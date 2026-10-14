
`/etc/sysconfig/sendmail` 文件是 SUSE 特有的，在其他发行版中不一定。

## /etc/sendmail.cf 文件

`/etc/sendmail.cf` 由宏定义和规则集组成，并分类。

例如，本地主机由 C 类中的 C 宏定义。因此，`localhost da10.digitalairlines.com` 定义了 Sendmail 的主机名。

规则集提供了在投递之前处理邮件的方法（例如更改头部或检查垃圾邮件地址）。

以下是定义规则集的示例：

```
# 检查发送者地址：user@address, user0, address
R$< $ + <$ > $; $: $<1> = = <3 > $: {F:$3}:<U:<20>}:H:$3>
R$< $ + <$ | $<1> | $<2> | $<1> | $<2> | $SearchList<From> | $<3>
R$0 <+$ | $<$ |$> | $<33>: reverse result
```

此规则集定义了如何处理邮件头中的不完整地址。

通常情况下，不要直接编辑 `/etc/sendmail.cf`。

在 SLES 系统上，你使用 YaST 配置 sendmail，或者编辑 `/etc/sysconfig/mail` 和 `/etc/sysconfig/sendmail` 然后运行 SuSEconfig 脚本。

在其他系统上，你编辑一个 `sendmail.mc` 文件，该文件由 M4 宏组成，通过 `m4` 命令转换为实际的 `sendmail.cf` 文件。

## /etc/mail/access 配置文件

`/etc/mail/access` 文件定义了通过此服务器中继邮件的主机、网络和域名。该文件的每一行都包含一条邮件转发的规则。

第一列包含一个电子邮件地址、域名名或网络地址。第二列与第一列之间用制表符分隔，包含一个关键字或 SMTP 回复代码，用于定义该行执行的操作。

如果使用 SMTP 回复代码，可以提供一个额外的可选消息文本，当该规则激活时，它将发送给邮件发送者。

电子邮件地址、域名名或网络地址，结合以下关键词之一或 SMTP 代码，定义了所有与第一列条目匹配的邮件的操作：

- `OK`. 接受邮件，即使存在拒绝规则也是如此。
- `REJECT`. 拒绝邮件。发送者将接收到错误消息。
- `RELAY`. 如果没有其他拒绝规则，则转发邮件。
- `DISCARD`. 丢弃邮件。不通知发送者。
- `ERROR:Reply-Code text-message`. 如果发生特定的回复代码，则会将定义的文本发回给邮件发送者。

`/etc/mail/access` 配置文件需要转换为哈希表，然后由邮件服务器进行评估。

要将文件转换为哈希表，请（以 root 用户身份）输入

```
makemap hash -f /etc/mail/access.db < /etc/mail/access
```

## /etc/mail/genericstable 配置文件

`/etc/mail/genericstable` 修改发送邮件的发送者地址。这通常在本地网络与 Internet 之间的邮件网关处需要，因为本地电子邮件地址与官方 Internet 电子邮件地址不同。

该文件的每一行都包含一条电子邮件地址的规则。第一列的值定义了原始发送者地址，第二列的值是预期在发送邮件中显示的地址。列之间用制表符分隔。

更改 `/etc/mail/genericstable` 文件后，输入以下内容（单行）以创建所需的哈希表：

```
makemap hash -f /etc/mail/genericstable.db < /etc/mail/genericstable
```

## /etc/mail/virtertable 配置文件

`/etc/mail/virtertable` 允许更改传入邮件的接收者地址。该文件的每一行都包含一条邮件接收者地址的转换规则。

第一列包含完整的电子邮件地址（`user@domain`）或仅接收者域名。第二列包含应替换相应接收者地址的值。

`/etc/mail/virtertable` 使 Sendmail 能够在不同的域名托管相同的电子邮件地址，因为它会将邮件重定向到不同的本地或远程电子邮件地址。

更改 `/etc/mail/virtertable` 后，输入以下内容（单行）以创建所需的哈希表：

```
makemap hash -f /etc/mail/virtertable.db < /etc/mail/virtertable
```

## /etc/mail/mailertable 配置文件

`/etc/mail/mailertable` 定义了发送邮件消息的路由。每一行包含一个地址范围的路由定义。

第一列包含目标主机或目标域名。所有落在此范围内的邮件都将通过第二列定义的路由发送。路由可以通过 UUCP、SMTP 或本地投递定义。列之间用制表符分隔。

更改 `/etc/mail/mailertable` 后，输入以下内容（单行）以创建所需的哈希表：

```
makemap hash -f /etc/mail/mailertable.db < /etc/mail/mailertable
```

## /etc/aliases 配置文件

`/etc/aliases` 文件（别名数据库）允许定义别名。这是一个纯文本文件，每行一个别名。该文件有两列：

- 第一列包含别名，后跟冒号（如 `mail:`）。
- 第二列与第一列之间用一个或多个制表符分隔，包含用逗号分隔的真实地址列表。

你可以编辑 `/etc/aliases`。要将其转换为哈希表，请 root 用户运行 `newaliases`。

## qmail Exim

除了 postfix 和 sendmail，你还需要熟悉 qmail 和 Exim MTA，如下所示：

- `qmail`
- `Exim`

### qmail

`qmail` 经常作为 sendmail 的替代品。有些人认为它是比 sendmail 更安全的邮件服务器。`qmail` 在 2007 年进入公共领域，但根据所使用的指南，它是非免费的。

`qmail` 使用由互不相关的组件组成的模块化架构。例如，SMTP 队列器的凭据与 SMTP 监听器不同。

许多管理员认为 `qmail` 更容易使用。例如，`qmail` 使用 `maildir` 格式来避免锁定问题。`qmail` 还将邮件拆分成单独的文件。

### Exim

另一个 MTA 是 `Exim`。`Exim` 与 sendmail 类似但具有不同的功能。`Exim` 每天能够处理百万条消息。`Exim` 的当前版本为 4.71，可以在多个网站下载。

## mail 命令

某些程序向 root 用户发送状态邮件。根据服务器的配置，你可能没有安装图形化邮件客户端来读取它们。在这种情况下，了解如何使用 `mail` 命令读取邮件非常有帮助。

如果你登录虚拟终端，如果有你的邮件，你会收到通知，如下：

```
dal login: root
Password:
You have new mail in /var/mail/root.
Last login: Mon Jun 29 07:58:21 2009 from da-host.digitalairlines.com
dal$: 
```

要读取这些消息，你可以使用 `mail` 命令，如下：

```
dal$: # mail
Heirloom mailx version 12.2 01/07/07. 输入 ? 获取帮助。
"/var/mail/root": 2 messages 2 new
>N 1 geeko@da-host.digi Mon Jun 29 08:03 20/858 Testmail
>N 2 geeko@da-host.digi Mon Jun 29 08:08 20/858 Testmail
?
```

`mail` 的提示符是 `"?"`。在提示符处，使用以下命令：

### 表格 7-6 Mail 命令

| 命令 | 目的 |
| --- | --- |
| `message_list` | 输入（显示）消息。 |
| `n` | 显示下一条消息。 |
| `message_list` | 编辑消息。 |
| `message_list` | 显示消息标题。 |
| `message_list` | 删除消息。 |
| `message_list` | 回复消息发送者。 |
| `message_list` | 回复消息发送者及所有接收者。 |
| `user_list` | 向特定用户发送邮件。 |
| `q` | 退出并保存 mbox 中的已读、已删除消息。 |
| `x` | 退出但不移除系统邮箱。 |

`mail_list` 由空格分隔的整数、整数范围或用户名组成。如果省略，`mail` 将使用最后输入的消息。`user_list` 由空格分隔的用户名或别名组成。别名定义在主目录下的 `.mailrc` 文件中。

你也可以在命令行上使用 `mail` 程序发送电子邮件。使用 `mail` 的最简单形式是：

```
mail mail_address
```

你可以在 `mail_address` 处输入本地机器上某人的用户名。（如果需要向本地用户以外的用户发送消息，你需要在本地主机上配置邮件服务器）
