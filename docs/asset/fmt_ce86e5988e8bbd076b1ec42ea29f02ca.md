
## 读取特定消息

读取邮件消息是任何邮件程序最基本的功能。以下说明了如何使用 `mailx` 程序显示所有新邮件消息的头并查看 2 号消息：

```
$ mailx

mailx version 5.0 Thu Aug 5 10:36:57 PDT 1999 type ? for help.

/var/mail/user2: 2 messages new

>N 1 user3 Mon May 14 14:4416/334 About lunch!

>N 2 user4 Mon May 14 14:5314/326 Your lunch

?
```

```
- 2

mailx  5.0 Thu Aug 5 10:36:57 PDT 1999

From: 4@jupiter

Date: Mon, 2 1999 14:53

To: user2@venus

Subject: Your lunch

Hi user2

heard you are going to lunch.

Mind if I join you?

?
```

## 邮件头

`mailx` 命令的输出称为邮件头。邮件头显示内容：

- 程序的版本
- 询问 (`?`) 获取帮助
- 信箱的位置（例如，`/var/mail/username`）邮件保存处
- 信箱的状态
- 消息总数
- 接收的顺序
- 发件者（用户和主机名）
- 发送的时间和日期
- 消息的大小（行数和字符数）
- 邮件主题

当收到新邮件或旧未读消息时，表 E-1 所示的字符出现在消息旁边。

### 附录 E mailx

| 字符 | 消息 |
|---|---|
| N | 表示新邮件 |
| U | 表示早在退出 `mailx` 程序前未读的消息 |
| R | 表示在当前调用 `mailx` 期间读取的新消息 |
| O | 表示之前读过并保存在当前的消息 |
| > | 表示当前消息 |
| ? | 表示编号，或者如果用户输入，显示选项列表 |

以下代码是两条新邮件的邮件头，如第一列的 `N` 字符所示。

```
$ mailx

mailx version 5.0 Thu Aug 5 10:36:57 PDT 1999 type ? for help.

/var/mail/user2: 2 messages new

>N 1 user3 Mon May 14 14:4416/334 About lunch!

>N 2 user4 Mon May 14 14:5314/326 Your lunch

?
```

要读取第一封邮件，在邮件提示符 (`?`) 处按回车。当前消息将显示在你的屏幕上。

按回车读取任何后续消息。

## 发送邮件

要发送邮件，请遵循以下步骤：

- 步骤 1：将 `username@hostname` 作为 `mailx` 命令的参数。
- 步骤 2：输入邮件的主题并按回车。
- 步骤 3：输入邮件正文，并在单独的一行按 `.`（句号）键或 `Ctrl-D`（传输消息）以指示消息的结束。

例如：

```
$ mailx user3@cisco

Subject: lunch!

Hi there!

Do you have any plans for lunch today?

如果没有的话，你愿意加入我吗？

user2

(输入点 [.] 并按回车)

EOT
```

> **NOTE**
> `EOT` 是 “end of transmission.” 的缩写。

## 使用邮件发送文件

使用 `mail` 命令和标准输入重定向向他人发送文件——例如：

```
$ mailx user3@saturn < dante
```

在使用上述命令时配合 `-s` 选项，可以包含主题行：

```
$ mailx -s "myfile" user3@saturn < dante
```

## 创建邮件别名

邮件别名（mail alias）是单个文件中的一组用户名（登录 ID）。当你想要向一组用户发送相同的消息时，请使用邮件别名。邮件别名也称为分发列表（distribution list）。

```
mailx alias
```

使用编辑器将别名添加到 `.mailrc` 文件中，该文件位于你的主（或登录）目录下。`.mailrc` 文件用于存储私有的邮件别名和与邮件程序相关的变量。系统管理员可以设置公共别名，供系统上的任何用户使用，或者通过 `/etc/mailrc` 文件设置。

你可以使用任何编辑器创建或向 `.mailrc` 文件中添加别名。每行创建一个别名，然后保存更改——例如：

```
$ cd

$ vi .mailrc

alias class user3@saturn user4@jupiter user5@earth
```

```
".mailrc" [newfile]

:wq
```

```
$ mailx class

Subject: test!

这是我新创建的别名的测试

user2
.
EOT
```

## 取消邮件消息

按 `Ctrl-C` 取消邮件消息：

```
$ mailx user3@saturn

Subject: lunch!

Do you have any plans . . . (press Ctrl-C)

-C

(Interrupt -- one more to kill letter)
```

> **注意**
> 在编写邮件消息时，记住在每行的末尾按回车键（Return）。`mail` 不支持自动换行。

> **注意**
> 一封电子邮件不是单一文件。电子邮件由多个页面组成，每个页面按文件追加。所有邮件消息的存储区域为 `/var/mail/username`。

## 附录 E mailx

510

> **注意**
> 你消息中的每行文本最多可达 256 个字符。当你超过此限制时，屏幕会冻结。如果发生这种情况，请按 `Ctrl-C` 终止你的消息。

```
$ C "/home/user2/dead.letter" 3/29
```

如果你取消了消息，它将保存在你的主目录下的 `dead.letter` 中。删除此文件或将文本另存以备日后传输。

## 删除和恢复邮件消息

在 `mailx` 中使用 `d` (delete) 命令删除邮件消息：

```
d [ number...range ]
```

表 E-2 列出了逐个删除或一次性删除多条消息的若干示例。

| 执行操作 | 使用此命令 |
|---|---|
| 删除当前消息 | `? d` |
| 删除非当前消息 | `? d number` |
| 一次性删除几条消息 | `? d 135` |
| 删除范围范围的消息 | `? d 1-5` |
| 恢复邮件消息 | `? u number`<br>`? u number...`<br>`? u number-number` |

表 E-2 删除/恢复消息的示例

> **注意**
> 你可以一直恢复消息，直到你退出 `mailx` 为止。

## 回复邮件消息

在 `mailx` 中使用 `r` 命令回复当前消息——例如：

```
$ mailx

mail version 5.0 Thu Aug 5 10:36:57 PDT 1999 Type? for help.

*/var/mail/user2: 2 messages 2 new

-N 1 user3 Mon Aug 14 14:44 16/33 About lunch!

-N 2 user4 Mon Aug 24 14:53 14/326 Your lunch

? 1

Message 1:

From:user@saturn Mon Aug 24 14:44 PST 199

Date: 2 Aug 1999 14:45:31 PST

From:user2@saturn

To:user3@venus

Subject: About lunch!

我没有午餐计划，我很乐意加入你们。

user3

? r

To: user3@saturn

Subject: Re: About lunch!

# 退出邮件

太棒了！我们课后在大厅见。

user2

EOT
?
```

要回复非当前消息，输入以下内容：

- `? r number`

你的回复将发送给消息的发送者。

要回复发送者以及所有接收当前消息的人，输入此：

- `? R`

要回复发送者以及所有接收非当前消息的人，输入此：

- `? R number`

## 打印邮件消息

使用带有管道 (`|`) 符号的 `lp` 命令在 `mailx` 中打印邮件消息：

- `? Number 1lp`

以下邮件消息将打印到默认打印机。然而，你可以通过 `lp -d printername` 选项指定目标打印机。

以下是在阅读后将 1 号消息发送到默认打印机的方法：

```
? 1

Message 1:

From user3@saturn Mon Aug 2 14:44:53 PST 1999

Date: Mon, 2 Aug 1999 14:45:31 PST

From:user2@saturn

To:user3@venus

Subject: About lunch!

我没有午餐计划，我很乐意加入你们。

user3

? r

To: user3@saturn

Subject: Re: About lunch!

# 退出邮件

太棒了！我们课后在大厅见。

user2

EOT
?
```

要回复非当前消息，输入以下内容：

- `? r number`

你的回复将发送给消息的发送者。

要回复发送者以及所有接收当前消息的人，输入此：

- `? R`

要回复发送者以及所有接收非当前消息的人，输入此：

- `? R number`

## 使用波浪号命令

在编写邮件时，你可以使用波浪号 (`~`) 执行各种功能：

表 E-3 列出了一些常用的波浪号命令。

> **注意**
> 如果你想在信中包含一个字面的波浪号字符，请输入两个波浪号。

### 表 E-3 波浪号命令和功能

| 命令 | 功能 |
|---|---|
| `~s string` | 将主题行更改字符串。 |
| `~t name` | 将指定的名称添加到收件人列表。 |
| `~m number` | 将指定文件的文本插入到当前信中。这仅在阅读时发送消息时有效。 |

以下代码演示了使用某些波浪号命令来更改主题行 (`-s`) 并刷新和打印到屏幕上的消息 (`-p`)：

```
$ mailx all_staff_alias

Subject: Meeting Today

今天下午 3:00 将举行一次员工会议

-s Staff Meeting 3:00 p.m. Today

在大房间里举行。

请准时参加。

-p

----------------

消息包含：

To: all_staff alias

Subject: Staff Meeting 3:00 p.m. Today

今天下午 3:00 将举行一次员工会议

在大房间里举行。

请准时参加。

(继续)

EOT
```

## 总结

UNIX 运行环境提供了一个名为 `mailx` 的程序，用于发送和接收电子邮件。`mailx` 程序提供了从命令行读取、写入、发送、接收、保存和删除消息的功能。

`mailx` 命令是一个功能全的 UNIX 工具，允许用户在以下条件下访问邮件：

- 当使用命令行 shell 时
- 当使用终端时
