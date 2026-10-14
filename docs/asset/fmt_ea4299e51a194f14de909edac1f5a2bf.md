
#### 表 D-1：自定义 `mailx` 会话的变量

| Variable | Type | Description |
|---|---|---|
| `keep` | Binary | 允许 `mailx` 在系统邮箱为空时截断它，而不是删除它。如果你出于安全原因对系统邮箱设置了特殊权限，这会很有用。如果未设置 `keep`，系统邮箱在为空时会被删除；下次创建时，你必须重新建立所需的权限。 |
| `keepsave` | Binary | 防止在退出 `mail` 时删除已保存的消息。通常，`mailx` 程序在你将消息保存到其他文件或文件夹时对它们做标记，然后在你离开 `mailx` 时从你的系统邮箱中删除它们。设置 `keepsave` 会让 `mailx` 将这些消息保留在你的系统邮箱中。 |
| `lang` | String | 允许用户指定用于显示邮件消息的区域设置。 |
| `LISTER` | String | 允许用户指定 `folders` 命令使用的命令。 |
| `MBOX` | String | 允许用户指定 `mbox` 文件夹的位置。`mbox` 文件夹通常位于 `$HOME/mbox`。 |
| `metoo` | Binary | 当你向自己是其成员的别名发送邮件时，将你包含在收件人列表中。如果未设置 `metoo`，你将不会收到发送给自己是其成员的别名的消息的副本。 |
| `noheader` | Binary | 禁止在调用 `mailx` 时显示头信息和版本标识。 |
| `nosave` | Binary | 防止 `mailx` 将中止的消息保存为你主目录中的 `dead.letter`。 |
| `onehop` | Binary | 当回复包含其他收件人的消息时，有时收件人的地址相对于发件人的地址。`onehop` 选项强制投递不沿着消息到达的路径进行，而是直接投递，从而提高性能。 |
| `outfolder` | Binary | 导致 `mailx` 将传出邮件消息保存到 `folder` 指定的目录中。 |
| `page` | Binary | 在由 `pipe` (`\|`) 命令处理的消息之间插入换页符。 |
| `PAGER` | String | 允许用户指定在显示消息时使用的分页程序。<br>例如：<br>`PAGER=/usr/bin/more`<br>或<br>`PAGER=/usr/bin/pg` |
| `prompt` | String | 允许用户更改调用 `mailx` 时的 `mailx` 提示符。例如：`prompt=>>>` |
| `quiet` | Binary | 在首次调用时抑制打印版本，并在使用 `type` 命令时抑制打印消息编号。 |
| `record` | String | 指定 `mailx` 将保存所有传出消息副本的文件名。 |
| `Replayall` | Binary | 反转 `reply` 和 `Reply` 命令的功能。 |
| `save` | Binary | 允许用户将邮件消息保存到 `dead.letter`。 |
| `sendwait` | Binary | 导致 `mailx` 等待邮件已被邮件程序处理。从用户角度看，此选项可能会导致性能下降，因为用户必须等待消息被投递。 |
| `SHELL` | String | 允许用户指定在调用 `-` 或 `!` 命令时使用的 shell。 |
| `screen` | Numeric | 指定在输入 `headers` 命令时一次显示的消息数。 |
| `sendmail` | String | 指定用于发送邮件消息的程序的路径名。如果未指定此变量，`mailx` 使用默认投递系统。请咨询系统管理员以获取有关替代投递系统的信息。 |
| `showto` | Binary | 在消息头中显示收件人姓名而不是作者姓名。 |
| `sign` | String | 允许用户指定在使用 `-a` 命令时插入到邮件消息中的字符串。 |
| `Sign` | String | 允许用户指定在使用 `-A` 命令时插入到邮件消息中的字符串。 |
| `toplines` | Numeric | 指定 `top` 命令打印的行数；默认值为 5。 |
| `verbose` | Binary | 以详细模式调用 `mailx`。消息的实际投递将在终端上显示。这与在命令行上使用 `-v` 标志相同。此变量主要用于调试目的。示例 D-1 显示了 `verbose` 变量的使用。 |
| `VISUAL` | String | 指定在使用 `visual` 命令或 `-v` 转义时将使用的屏幕编辑器的路径名。<br>例如：<br>`set VISUAL=/usr/ucb/vi`<br><br>如果你的唯一终端是 CRT，你也可以为 `EDITOR` 变量指定一个屏幕编辑器；那么 `edit` (`-e`) 或 `visual` (`-v`) 将调用相同的编辑器。 |

以下示例显示了上一表中讨论的 `verbose` 变量的使用，该变量导致 `mailx` 在发送消息时显示别名的展开：

#### 示例 D-1：`mailx` 详细模式

```
? set verbose
? alias
smith csug@solo.my.company.com smith@my.company.com smith
? mailx tg
Subject: Conference Room
Starting tomorrow, our weekly meeting will be
moved to Meeting Room 4.
.
EOT
csug@solo.my.company.com... Connecting to (local)...
about to exec
csug@solo.my.company.com... Sent
smith, smith@my.company.com... Connecting to
your.company.com (smtp)...
220 your.company.com ESMTP Sendmail 8.7.6/UNIX 1.7
(1.1.10.5/28Jun99-0151PM) Tue, 25 Nov 1999
09:52:10 -0500 (EST)
>>> HELO solo.my.company.com
250 your.company.com Hello solo.my.company.com
[255.255.255.0],
pleased to meet you
>>> MAIL From:250 ... Sender ok
>>> RCPT To:250 Recipient ok
>>> RCPT To:250 Recipient ok
>>> DATA
354 Enter mail, end with "." on a line by itself
>>> .
250 JAA0000022475 Message accepted for delivery
>>> QUIT
221 your.company.com closing connection
smith@my.company.com,smith... Sent
? q
```

以下列表项对应示例中的数字。

- 1. 已设置 `verbose` 变量。
- 2. 不带参数执行 `alias` 命令以显示别名内容。
- 3. 然后发送一条消息，收件人为别名 tg。
- 4. 发送消息时显示别名的展开。
- 5. 执行 `q` 命令以结束 `mailx` 会话。

## 在 `mailx` 会话中使用转义命令

有一组特殊的命令，称为**转义命令**或**转义**，它们可以在你撰写消息的过程中执行功能。

使用转义命令的方法是：单独在一行中输入该命令，并以波浪号（~）作为第一个字符。波浪号之所以被称为转义字符，是因为它通知 `mailx` 跳出当前编辑环境，去执行后面的命令。你可以通过设置 `escape` 邮件变量来更改转义字符。如果你想在消息中某一行的行首输入真正的波浪号，则必须输入两个波浪号。

表 E-1 描述了这些转义命令。

**表 E-1：`mailx` 中的转义命令**

| 命令 | 描述 |
|---|---|
| `~~` | 在邮件正文中输入波浪号（~）字符。 |
| `~! command` | 执行你输入的 shell 命令。 |
| `~?` | 打印转义命令的简要摘要。 |
| `~: command`<br>`~_command` | 执行指定的 `mail` 命令。这对于执行内务处理任务（如重新显示消息）很有用。<br>例如，输入 `~:10` 会选择并显示消息 10，就像你在 `mailx` 提示符下输入其编号一样。 |
| `~a` | 将 `sign` 中设置的字符串插入到邮件消息中。 |
| `~A` | 将 `Sign` 中设置的字符串插入到邮件消息中。 |
| `~baddress_list` | 将 `address_list` 中指定的姓名插入到 Bcc：（密件抄送）列表中。 |
| `~caddress_list` | 将指定姓名添加到 Cc（抄送）列表中。 |
