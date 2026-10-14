

## 示例 D-1：mailx 详细模式（续）

```
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

- 1. 已设置 verbose 变量。
- 2. 不带参数执行 alias 命令以显示别名内容。
- 3. 然后发送一条消息，收件人为别名 tg。
- 4. 发送消息时显示别名的展开。
- 5. 执行 q 命令以结束 mailx 会话。

## 在 mailx 会话中使用转义命令

有一组特殊的命令，称为**转义命令**或**转义**，它们可以在你撰写消息的过程中执行功能。

使用转义命令的方法是：单独在一行中输入该命令，并以波浪号（~）作为第一个字符。波浪号之所以被称为转义字符，是因为它通知 mailx 跳出当前编辑环境，去执行后面的命令。你可以通过设置 escape 邮件变量来更改转义字符。如果你想在消息中某一行的行首输入真正的波浪号，则必须输入两个波浪号。

表 E-1 描述了这些转义命令。

**表 E-1：mailx 中的转义命令**

| 命令 | 描述 |
|---|---|
| ~~ | 在邮件正文中输入波浪号（~）字符。 |
| ~! command | 执行你输入的 shell 命令。 |
| ~? | 打印转义命令的简要摘要。 |
| ~: command<br>~_command | 执行指定的 mail 命令。这对于执行内务处理任务（如重新显示消息）很有用。<br>例如，输入 ~:10 会选择并显示消息 10，就像你在 mailx 提示符下输入其编号一样。 |
| ~a | 将 sign 中设置的字符串插入到邮件消息中。 |
| ~A | 将 Sign 中设置的字符串插入到邮件消息中。 |
| ~baddress_list | 将 address_list 中指定的姓名插入到 Bcc：（密件抄送）列表中。 |
| ~caddress_list | 将指定姓名添加到 Cc（抄送）列表中。 |
| ~C | 转储核心。 |

### 表 E-1：mailx 中的转义命令（续）

| 命令 | 描述 |
|---|---|
| ~a | 将主目录中名为 `dead.letter` 的文件包含到消息中。可以使用 DEAD 邮件变量指向另一个文件。 |
| ~e | 调用由 EDITOR 邮件变量指定的编辑器来编辑消息。 |
| ~f [msg_list] | 将当前消息或指定消息读入你的消息中。 |
| ~F[msg_list] | 与 ~f 类似，区别在于无论任何 discard、ignore 或 retain 命令，都会包含所有邮件头。 |
| ~h | 编辑消息头字段。此命令一次显示一个字段，你可以通过在末尾添加文本、使用 Delete 键或按 Ctrl/U 擦除整个字段然后重新输入来更改它们。请谨慎使用此命令。 |
| ~i string | 将指定变量的值插入到邮件消息中。<br>例如：命令 ~a 等价于命令 ~i sign，用于将你的签名插入到消息中。 |
| ~m[msg_list] | 将当前消息或指定消息包含进来，并向右缩进一个制表位。如果设置了 indentprefix 邮件变量，则该值会插入到制表位之前。这对于将你要转发的消息作为新消息的一部分隔开很有用。 |
| ~M[msg_list] | 与 ~m 类似，区别在于无论任何 discard、ignore 或 retain 命令，都会包含所有邮件头。 |
| ~p | 在终端上显示你正在撰写的消息。这有助于查看消息是否符合预期，以及是否包含正确的主题标题和收件人列表。 |
| ~q | 中止当前消息，就像你按了两次 Ctrl/C 中断一样。 |

