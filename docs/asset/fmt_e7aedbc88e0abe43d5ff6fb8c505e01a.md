
# Mail 实用程序使用说明

Mail 实用程序从标准输入接收输入。默认情况下，标准输入来自用户在键盘上的输入。然而，通过重定向，你可以使用文件内容作为 Mail 程序的消息。在下一个示例中，文件 `mydata` 被重定向为 Mail 实用程序的输入并发送给 `robert`。

```
$ mail robert < mydata
```

## 发送邮件

你可以通过在命令行 `mail` 命令后列出这些用户的地址作为参数，来同时向多个用户发送消息。在下一个示例中，用户同时向 `chris` 和 `aleina` 发送消息。

```
$ mail chris aleina
```

你可能还想为你保存一份正在发送的消息副本。你可以通过在地址后的命令行指定文件名，将邮件消息复制到你账户中的文件中。文件名必须是相对路径或全路径，且包含斜杠。路径将一个参数识别为文件名，Mail 在其中保存正在发送的消息副本。在示例中，用户将消息副本保存到名为 `birthnote` 的文件中。使用了相对路径，前缀表示当前工作目录：`./birthnote`。

```
$ mail robert ./birthnote
```

## 接收邮件

要接收邮件，只需输入 `mail` 命令并按 ENTER 键。这会启动一个带有自己的提示符和邮件命令的 Mail shell。将显示消息头列表。头部信息根据消息状态和消息头提供的字段排列。消息状态由单个大写字母表示，`N` 表示 *new* 新 或 `U` 表示 *unread* 未读。用于引用消息的消息编号紧随状态字段之后。下一个字段是发送者地址，然后是接收消息的日期时间，以及消息的行数和字符数。最后一个字段是给消息的主题。头部之后，Mail shell 会显示其提示符 `?`。在提示符处，输入对消息进行命令。常用的 Mail 命令如表 17-3 所示。一个 Mail 头部和提示符的示例如下：

```
$ mail

Mail version 8.1 6/6/93. 输入 ? 获取帮助。

"var/spool/mail/larisa": 3 messages unread

1 chris@turtle.mytrek. Jun 7 14:17 22/554 "trip"

U 2 aleina@turtle.mytrek. Jun 7 14:18 22/525 "party"

u 3 dylan@turtle.mytrek. Jun 7 14:18 22/528 "newsletter"

& q
```

示例输入：

```
$ robert

Subject: Birthday

Your present is in the mail

really.

^D

Cc: ENTER
```
