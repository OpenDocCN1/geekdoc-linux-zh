
# shell-command

转义到 shell。注意，在 `shell-command` 有效的地方，并不总是允许参数。建议进行尝试。

- `# comment` 空命令（注释）。在 `mailrc` 文件有用。
- `=` 打印当前消息编号。
- `?` 打印命令摘要。
- `alias alias name...`
- `group alias name...`

为给定的名称声明别名。当你使用 `alias` 作为收件人时，替换这些名称。此命令在 `mailrc` 文件中有用。不带参数时，显示定义的别名列表。另见第 781 页“内部变量”中的 `allnet`。

- `alternates name...`
为你的登录名声明一组备用名称列表。在回复消息时，从回复收件人列表中移除这些名称。不带参数时，打印当前的备用名称列表。

- `cd [directory]` `chdir [directory]`

更改目录。如果未指定目录，则使用 `HOME`。

- `copy [file]`
- `copy [message-list] file`

将消息复制到文件，但不将消息标记为已保存。
否则，等同于 `save` 命令。

- `copy [message-list]`

将指定的消息保存到文件中，文件名源自要保存消息的作者，但不将消息标记为已保存。否则，等同于 `Save` 命令。

- `delete [message-list]`

从信箱删除消息。如果设置了 `autoprint`，则在最后一条消息之后打印下一条（参见第 781 页“内部变量”）。

- `discard [header-field...]`
- `ignore [header-field..]`

在屏幕上显示消息时，抑制指定头部字段的打印。忽略的头部字段示例有 `Status` 和 `Received`。除非设置了 `alwaysignore` 变量，否则保存消息时包含这些字段。`More`、`Page`、`Print` 和 `Type` 命令会覆盖此命令。如果未指定头部，则打印当前正在忽略的头部字段列表。另见 `discard` 和 `unignore` 命令。

- `dp [message-list]`
- `dt [message-list]`

从信箱删除指定的消息并打印下一条消息。

- `echo string...`
回显给字符串。

- `edit [message-list]`

编辑指定的消息。调用名为 `editor` 的程序。

- `exit`
退出 `mailx`。

- `field [message-list]`
显示字段的值。

- `headers [message-list]`
打印头部。

- `help`
打印命令摘要。

- `hold [message-list]`
在信箱中保留指定的消息。

- `preserve [message-list]`
保留指定的消息。

- `ignore [header-field...]`
- `discard [header-field...]`

在屏幕上显示消息时，抑制头部字段的打印。忽略的头部字段示例有 `Status` 和 `Cc`。

- `inc`
包含在你读取系统信箱期间到达的消息。将新消息添加到当前邮件会话中的消息列表中。

- `list`
打印所有可用命令。不提供解释。

- `load [message] file`
用命名文件中的消息替换指定的消息。

- `mail recipient...`
发送给指定收件人的消息。

- `mail recipient...`
发送给指定收件人的邮件消息。

- `mbox [message-list]`
安排给消息在 `mailx` 正常退出时进入标准的 `mbox` 文件。

# mailx, mail, Mail 775

- `more [message-list]`
- `page [message-list]`

打印指定的消息。如果设置了 `crt`，则使用 `PAGER` 变量指定的命令，对超过 `crt` 变量指定行数的消息进行分页。默认命令是 `pg(1)`，如果设置了 `bsdcompat` 变量，默认为 `more(1)`。请参第 785 页的“环境变量”。与 `print` 和 `type` 命令相同。

- `More [message-list]`
- `Page [message-list]`

在屏幕上打印指定的消息，包括所有头字段。覆盖 `ignore` 命令对字段的抑制限制。与 `print` 和 `Type` 命令相同。

- `new [message-list]`
- `unread [message-list]`

将消息列表中的每条消息标记为未读。

- `next [message]`

跳转到匹配 `message` 的下一条消息。如果不提供消息，则找到未删除或未保存的下一个消息。如果指定了 `message-list`，则仅使用列表中的第一个有效消息。此命令用于从特定用户跳转到下一条消息，否则在没有实际命令的情况下，名称将被视为命令。请参见上文对 `message-list` 的讨论以获取可能的消息规范。

- `pipe [message-list] [shell-command]`
- `| [message-list] [shell-command]`

通过给定的 `shell-command` 传递消息。将消息视为已读。如果不指定参数，则通过 `cmd` 变量值指定的命令传递消息。如果设置了 `page` 变量，则在每条消息后插入一个分页符（见第 781 页的“内部变量”）。

- `preserve [message-list]`
- `hold [message-list]`

在邮箱中保留指定的消息。

- `print [message-list]`
- `type [message-list]`

打印指定的消息。如果设置了 `crt`，则使用 `PAGER` 变量指定的命令，对超过 `crt` 变量指定行数的消息进行分页。默认命令是 `pg(1)`，如果设置了 `bsdcompat` 变量，默认为 `more(1)`。请参第 785 页的“环境变量”。与 `print` 和 `page` 命令相同。

```
Print [message-list]

Type [message-list]
```

在屏幕上打印指定的消息，包括所有头字段。
覆盖 `ignore` 命令对字段的抑制限制。与 `More` 和 `Page` 命令相同。

```
put [file]

put [message-list] file
```

将指定的消息保存到给文件中。使用与 `print` 命令相同的约定，即忽略头字段。

```
Put [file]

Put [message-list] file
```

将指定的消息保存到给文件中。覆盖 `ignore` 命令对字段的抑制限制。

- `quit`
退出 `mailx`，将已读消息存入 `bbox`，将未读消息存为邮箱。除非设置了 `keepsave` 变量，否则删除已显式保存到文件的消息。

```
reply [message-list]

respond [message-list]

replysender [message-list]
```

向 `message-list` 中每条消息的作者发送回复。从第一条消息获取主题行。如果 `record` 设置为一个文件，则将回复的副本添加到该文件。如果设置了 `replyall` 变量，则反转 `Reply/Respond` 和 `reply/respond` 的操作。`replysender` 命令不受 `replyall` 变量影响，但仅向每条消息的发送者发送回复。请参第 769 页的“启动邮件”。

```
reply [message]

Respond [message]

replyall [message]
```
